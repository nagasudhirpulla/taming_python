## Grafana variables

-   Variables in Grafana can be used to use common values in dashboard queries, titles etc.
-   Variables can be used to create input elements like select boxes, text inputs that can change the dashboard based on user input
-   A variable can also be used in another variable (chained variables). This can be used to create hierarchical select boxes for user inputs

## Manage variables in a dashboard

-   As shown below, go to the dashboard settings page and go to the `variables` tab

![grafana%20variables%20screen.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20variables%20screen.png?raw=true)

## Variable types

### Query variable

-   The variable value select list options will be fetched from a datasource using a query

![grafana%20query%20variable%20configuration.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20query%20variable%20configuration.png?raw=true)

![grafana%20query%20variable%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20query%20variable%20demo.png?raw=true)

### Custom variable

-   The variable value select list options will be defined manually

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/c3bb313a-e227-4fb0-9a1f-4e0cc8a910a2/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/cdbba86c-8fd5-4492-abac-b3e65c1ca5d2/image.png)

### Text box variable

-   The variable value can be defined by the user in a textbox

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/9a5f7a65-3324-454d-b0c5-8cb17c2c6b3e/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/fd62b238-84ed-41c8-b42e-06bf647b7966/image.png)

## Using variable in the query of a visualization

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/77cced8d-d5a3-49e0-ac27-6c9a8c08eb9e/image.png)

-   Variable value can be used in a query of the visualization as shown in the above image
-   In the above example, using `$state_name` in the query will use value of the `state_name` variable
-   The above example uses a variable in an infinity datasource query. In a similar way, variables can be used in any datasource queries (like PostgreSQL, JSON, SQL Server etc.)

## Using variable in a visualization title

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/f4a232b8-3584-407a-a9d4-d6251ef8e0fb/image.png)

-   In the above example, value of the variable `state_name` is used in a visualization title using `$state_name`

## Nested Variables and Hierarchical Select boxes

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/e409ff25-9cab-4f23-98ee-4dcaedc37400/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/dc70f907-a2e1-4773-8b04-2fe77ed1ab48/image.png)

-   A variable can be used in the query of another variable
-   Hence the drop-down values of one variable can be dependent on the value of another variable. This can help in creating hierarchical drop-downs as shown in the above example.

## References

-   [https://grafana.com/docs/grafana/latest/dashboards/variables/](https://grafana.com/docs/grafana/latest/dashboards/variables/)
-   [https://www.kaggle.com/datasets/shubhendra7/indian-cities-analysis?resource=download](https://www.kaggle.com/datasets/shubhendra7/indian-cities-analysis?resource=download)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDU4OTA2ODQ5LDE2MzA0MDQ1MDBdfQ==
-->