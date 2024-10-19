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

![grafana%20custom%20variable%20configuration.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20custom%20variable%20configuration.png?raw=true)

![grafana%20custom%20variable%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20custom%20variable%20demo.png?raw=true)

### Text box variable

-   The variable value can be defined by the user in a textbox

![grafana%20textbox%20variable%20configuration.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20textbox%20variable%20configuration.png?raw=true)

![grafana%20textbox%20variable%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20textbox%20variable%20demo.png?raw=true)

## Using variable in the query of a visualization

![grafana%20variable%20in%20viz%20query%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20variable%20in%20viz%20query%20demo.png?raw=true)

-   Variable value can be used in a query of the visualization as shown in the above image
-   In the above example, using `$state_name` in the query will use value of the `state_name` variable
-   The above example uses a variable in an infinity datasource query. In a similar way, variables can be used in any datasource queries (like PostgreSQL, JSON, SQL Server etc.)

## Using variable in a visualization title

![grafana%20variable%20in%20viz%20title%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20variable%20in%20viz%20title%20demo.png?raw=true)

-   In the above example, value of the variable `state_name` is used in a visualization title using `$state_name`

## Nested Variables and Hierarchical Select boxes

![grafana%20nested%20variable%20config%20example.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20nested%20variable%20config%20example.png?raw=true)

![grafana%20nested%20variable%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana%20nested%20variable%20demo.png?raw=true)

-   A variable can be used in the query of another variable
-   Hence the drop-down values of one variable can be dependent on the value of another variable. This can help in creating hierarchical drop-downs as shown in the above example.

### Video
Video on this post can be seen [here](https://youtu.be/sj4XF0ZRY-g?si=8FSInMc1XdJlx2W3)

## References

-   Official documentation - [https://grafana.com/docs/grafana/latest/dashboards/variables/](https://grafana.com/docs/grafana/latest/dashboards/variables/)
-   Sample dataset used - [https://www.kaggle.com/datasets/shubhendra7/indian-cities-analysis?resource=download](https://www.kaggle.com/datasets/shubhendra7/indian-cities-analysis?resource=download)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczODgxMjM5MiwtMjA3OTcwMDE3OSwtMT
AwMDU3NDk5OCwxNjMwNDA0NTAwXX0=
-->