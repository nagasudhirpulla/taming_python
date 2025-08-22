# Reset Grafana admin password
-   Grafana admin password can be reset from command line.
-   This is particularly useful if we forget the admin password

## Steps

-   Open a command line as an administrator in the Grafana installation folder. For example `C:\Program Files\GrafanaLabs\grafana\bin` folder
-   Use `grafana-cli` command line tool to reset admin password as shown below

```bash
grafana-cli admin reset-admin-password <newpassword>

```

## Video
Watch the video [here](https://youtu.be/_hXOB5eKmaQ?si=TTibQj_LFwtXENsI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_hXOB5eKmaQ?si=TTibQj_LFwtXENsI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

-   Official docs - [https://grafana.com/docs/grafana/latest/cli/#reset-admin-password](https://grafana.com/docs/grafana/latest/cli/#reset-admin-password)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4MTQ2OTcxLC00MjAzNDkzMjFdfQ==
-->