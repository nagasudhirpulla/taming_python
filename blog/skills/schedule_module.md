# Schedule python scripts without task scheduler or cron jobs

-   The `schedule` python module can be used to run python script periodically without task scheduler or cron job
-   The python script using schedule module will run in an infinite loop and trigger the required python function as per the configured schedule

```python
from schedule import every, repeat, run_pending
import time

@repeat(every(10).minutes)
def job():
    print("I am a scheduled job")

while True:
    run_pending()
    time.sleep(1)

```

## Installation

-   schedule python module can be installed using `python -m pip install schedule`

## Use cases

### Simple example

The below example runs a python function every 2 minutes

```python
import schedule
import time

def job():
    print("Running the scheduled task...")

# run job every 2 minutes starting from now
schedule.every(2).minutes.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)

```

### Decorator for declaring a function as a job

A decorator can also be used to declare a function as a job. This makes the job schedule declaration more readable.

```python
from schedule import every, repeat, run_pending
import time

@repeat(every(2).minutes)
def job():
    print("Running the scheduled task...")

while True:
    run_pending()
    time.sleep(1)

```

### Run job every x seconds/minutes/hours/days/weeks

```python
import schedule
import time

def job():
    print("Running the scheduled task...")

# run job every 2 seconds starting from now
schedule.every(2).seconds.do(job)

# run job every 2 minutes starting from now
schedule.every(2).minutes.do(job)

# run job every 2 hours starting from now
schedule.every(2).hours.do(job)

# run job every 2 days starting from now
schedule.every(2).days.do(job)

# run job every 2 weeks starting from now
schedule.every(2).weeks.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)

```

### Run at particular time

The `at` function can be called after `every` function, to control the time at which the job will be triggered.

-   For daily jobs -> `HH:MM:SS` or `HH:MM` A job can be triggered every 2 days at 14:30 using `schedule.every(2).days.at("14:30").do(job)`
-   For hourly jobs -> `MM:SS` or `:MM` A job can be triggered every 3 hours at 24th minute using `schedule.every(3).hours.at(":24").do(job)`
-   For minute jobs -> `:SS` A job can be triggered every one minute at 52nd second using `schedule.every(1).minutes.at(":52").do(job)`

### Pass arguments to job function

-   arguments to the job function can be provided in the do function as extra arguments

```python
import schedule
import time
from schedule import repeat, every

def hello(name):
    print(f"Hello {name} !")

# example
schedule.every(3).seconds.do(hello, "John")

# decorator example
@repeat(every(4).seconds, name='Alice')
def hi(name):
    print(f"Hi {name} !")

while True:
    schedule.run_pending()
    time.sleep(1)

```

### Handle errors during job execution

-   If an error occurs while job execution, the scheduler stops since the python code crashes.
-   To avoid stopping of scheduler during errors in job execution, a decorator (`catch_exceptions`) can be used on the job as shown below

```python
import schedule
import time
import functools

def catch_exceptions(cancel_on_failure=False):
    def catch_exceptions_decorator(job_func):
        @functools.wraps(job_func)
        def wrapper(*args, **kwargs):
            try:
                return job_func(*args, **kwargs)
            except:
                import traceback
                print(traceback.format_exc())
                if cancel_on_failure:
                    return schedule.CancelJob
        return wrapper
    return catch_exceptions_decorator

@catch_exceptions(cancel_on_failure=False)
def bad_task():
    return 1 / 0

schedule.every(5).minutes.do(bad_task)

while True:
    schedule.run_pending()
    time.sleep(1)

```

-   To avoid writing the decorator on each job, the scheduler itself can be extended and modified to handle errors as shown below

```python
import logging
from traceback import format_exc
import datetime
import time

from schedule import Scheduler

logger = logging.getLogger('schedule')

class SafeScheduler(Scheduler):
    """
    An implementation of Scheduler that catches jobs that fail, logs their
    exception tracebacks as errors, optionally reschedules the jobs for their
    next run time, and keeps going.
    Use this to run jobs that may or may not crash without worrying about
    whether other jobs will run or if they'll crash the entire script.
    """

    def __init__(self, reschedule_on_failure=True):
        """
        If reschedule_on_failure is True, jobs will be rescheduled for their
        next run as if they had completed successfully. If False, they'll run
        on the next run_pending() tick.
        """
        self.reschedule_on_failure = reschedule_on_failure
        super().__init__()

    def _run_job(self, job):
        try:
            super()._run_job(job)
        except Exception:
            logger.error(format_exc())
            job.last_run = datetime.datetime.now()
            job._schedule_next_run()

def bad_task():
    return 1 / 0

scheduler = SafeScheduler()
scheduler.every(3).seconds.do(bad_task)

while True:
    scheduler.run_pending()
    time.sleep(1)

```

### View scheduler Logs

-   schedule module uses a logger named ‘schedule’ and sends logs at debug level
-   schedule logs can be printed on command line by setting the logging level to debug of the schedule logger as shown below

```python
import schedule
import logging

logging.basicConfig()
logging.getLogger('schedule').setLevel(level=logging.DEBUG)

def job():
    print("running the script...")

schedule.every().second.do(job)

schedule.run_all()

schedule.clear()

```

### Additional logging

-   scheduler can be inherited to add additional logging functionality on all jobs as shown below

```python
import logging
import datetime as dt
import time

from schedule import Scheduler

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger('schedule')

class AppScheduler(Scheduler):
    """
    An implementation of Scheduler that does additional logging
    """

    def __init__(self):
        super().__init__()

    def _run_job(self, job):
        startDt = dt.datetime.now()
        logger.info(f"job {job.job_func.__name__} started at {startDt}")

        super()._run_job(job)

        endDt = dt.datetime.now()
        logger.info(f"job {job.job_func.__name__} ended at {endDt} in {(endDt-startDt).total_seconds()} seconds")

def appScript():
    print("Running the script...")

scheduler = AppScheduler()
scheduler.every(3).seconds.do(appScript)

while True:
    scheduler.run_pending()
    time.sleep(1)

```

-   Instead of inheriting the scheduler class, a decorator approach as shown below can also be used to add additional logging to scheduled jobs. But the decorator needs to be written on each job for logging.

```python
import functools
import time
import schedule
import datetime as dt

# This decorator can be applied to any job function to log the elapsed time of each job
def print_elapsed_time(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start_timestamp = dt.datetime.now()
        print(f'LOG: started job {func.__name__} at {start_timestamp}')
        result = func(*args, **kwargs)
        print(f'LOG: Job {func.__name__} completed in {(dt.datetime.now() - start_timestamp).total_seconds()} seconds at {dt.datetime.now()}')
        return result

    return wrapper

@print_elapsed_time
def appScript():
    print('Hello, Logs')

schedule.every(3).seconds.do(appScript)

while True:
    schedule.run_pending()
    time.sleep(1)

```

## When not to use schedule for jobs

-   Use schedule module only for simple job scheduling. If advanced features like concurrent job execution, sub second precision is required, go for robust and standard options like task scheduler, cron etc.

## Run as windows background service

-   The python script using schedule module will always be open in a command line since infinite loop is being used
-   The script can be run as a windows background service using tools like nssm

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/schedule_python_nssm.png?raw=true)

-   Using nssm, the script can be configured to start on system startup

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/schedule_python_nssm_auto_startup.png?raw=true)

-   Using nssm, the script can be configured to restart if it crashes due to some reason

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/schedule_python_nssm_auto_restart.png?raw=true)
#### Video
The video tutorial for this post can be found [here](https://youtu.be/9dNkPcpO0P0?si=--VP-CsWuIxjDzkP)

<iframe width="560" height="315" src="https://www.youtube.com/embed/9dNkPcpO0P0?si=--VP-CsWuIxjDzkP" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

-  Examples - [https://schedule.readthedocs.io/en/stable/examples.html#](https://schedule.readthedocs.io/en/stable/examples.html#)
-  Exception Handling with decorator - [https://schedule.readthedocs.io/en/stable/exception-handling.html](https://schedule.readthedocs.io/en/stable/exception-handling.html)
-  Exception handling with inherited scheduler - [https://gist.github.com/mplewis/8483f1c24f2d6259aef6](https://gist.github.com/mplewis/8483f1c24f2d6259aef6)
-  Logging - [https://schedule.readthedocs.io/en/stable/logging.html](https://schedule.readthedocs.io/en/stable/logging.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2NDA5MDQ4NCwxMzIxNzQ2OTM1LDIwOD
AzMzAwMDNdfQ==
-->