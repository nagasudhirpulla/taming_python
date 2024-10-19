# Hyper-V for creating VMs in Windows
-   Hyper-V is a type-1 virtualization platform in windows that can be used to create and manage virtual machines (VMs) directly in the Windows operating system without installing any third party hypervisors like virtual box.
-   Hyper-V is a type-1 hypervisor because when it is enabled, it effectively transforms the host operating system into a virtual machine running on top of the Hyper-V hypervisor.
-   Virtual machines of many Windows and Linux based operating systems are supported in Hyper-V

## Check if virtualization is enabled in Task Manager’s performance tab

Virtualization in CPU should be enabled for Hyper-V. It can be checked in Task Manager

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/task_manager_virtualization_check.png?raw=true)

## Add Hyper-V feature for Windows home edition

-   Hyper-V is not present in Windows home edition by default.
-   It can be enabled by running a batch script with the following text

```powershell
rem install_hyperv.bat file

pushd "%~dp0"

dir /b %SystemRoot%\\servicing\\Packages\\*Hyper-V*.mum >hyper-v.txt

for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\\servicing\\Packages\\%%i"

del hyper-v.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL

pause

```

## Enable Hyper-v in windows features

-   For windows desktop OS, Hyper-V feature can be enabled in Windows Features as shown below.

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_windows_feature.png?raw=true)

-   For Windows servers, the Hyper-V role should be enabled to user Hyper-V.

## Hyper-v manager

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_manager_start.png?raw=true)

-   Hyper-V Manager provides a UI to manage the virtual machines
-   Search for Hyper-V manager and run as administrator
-   You can also open it from command line by opening command prompt as administrator and type `virtmgmt.msc`

## Create a VM from ISO file in Hyper-V manager

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/windows_server_iso_download.png?raw=true)

-   Download ISO for the OS. For this example, we are downloading windows server 2022 evaluation edition. The OS is free to use for about 18 days
-   In the right pane, click New → Virtual Machine. Specify the new VM name and also if required specify another folder location for storing VM

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_1.png?raw=true)

-   Specify VM Generation (Generation 2 is preferred)

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_2.png?raw=true)

-   Specify Start-up RAM (generally keep it at least 1024 MB). Dynamic Memory option can also be used to allocate only the required amount of RAM to VM while it is running

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_3.png?raw=true)

-   Configure virtual switch for VM network adapter

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_4.png?raw=true)

-   Configure virtual hard disk size for VM

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_5.png?raw=true)

-   Select ISO file for VM operating system. Create a new VM.

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_6.png?raw=true)

-   Start the new VM from Hyper-V Manager.

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_7.png?raw=true)

-   Connect to VM after VM has started

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_8.png?raw=true)

-   Select the required server setup options for the first time booting

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_9.png?raw=true)

![Untitled](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/hyper_v_vm_setup_10.png?raw=true)

-   Now the VM is setup and can be managed from Hyper-V Manager.

## Stop and start the Hyper-V service

-   Click “Stop Service” in the right pane of Hyper-V Manager to stop Hyper-V service
-   To start the service start the windows service “Hyper-V Virtual Machine Management” in services.msc

### Video
The video for this post can be seen [here](https://youtu.be/0HTD-8_nZD0?si=UDt6BZI0nNSxuRdq)

<iframe width="560" height="315" src="https://www.youtube.com/embed/0HTD-8_nZD0?si=UDt6BZI0nNSxuRdq" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

-   Explanation on why Hper-V is a type 1 hypervisor - [https://superuser.com/a/836123](https://superuser.com/a/836123)
-   Hyper-V official documentation - [https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwMjE4OTcwOCwtMTg5NDcxODg5Myw2Mz
U0ODc5NjhdfQ==
-->