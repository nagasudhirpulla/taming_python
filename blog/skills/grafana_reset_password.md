# Reset Grafana admin password
-   Grafana admin password can be reset from command line.
-   This is particularly useful if we forget the admin password

## Steps

-   Open a command line as an administrator in the Grafana installation folder. For example `C:\\Program Files\\GrafanaLabs\\grafana\\bin` folder
-   Use `grafana-cli` command line tool to reset admin password as shown below

```bash
grafana-cli admin reset-admin-password <newpassword>

```

## References

-   Official docs - [https://grafana.com/docs/grafana/latest/cli/#reset-admin-password](https://grafana.com/docs/grafana/latest/cli/#reset-admin-password)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQyMDM0OTMyMV19
-->