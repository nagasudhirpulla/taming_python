# Customize Grafana email alerts

- The alert email sent by Grafana can be customized. The default alert email looks something like this

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/93ea6454-aecc-4600-b656-487e8fe1098d/Untitled.png)

- Even though the default alert email is very informative, there might be some customization requirements like removal or change of Grafana logo, change in colors etc.

## Notification template in Grafana

- Grafana alert content is created from Go templating variables.
- The official guide to understand Go templating language used Grafana alerts can be found at https://grafana.com/docs/grafana/latest/alerting/configure-notifications/template-notifications/using-go-templating-language/

Let us explore the options to customize Grafana alert content

## Option 1 - Edit contact point Message (Limited customization)

- In the email contact point editing screen there is a provision to customize email message as shown below

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/71b50a85-beab-4b41-8c46-f9ea6ee2faff/Untitled.png)

- The default email message will be replaced with the “Message” input of the contact point configuration screen
- Template variables can be used to render the alert information in the email message
- For example, we can use a custom email message something like

```html
Testing out the custom email message

{{ range .Alerts }}
  Status: {{ .Status }}
  Starts at: {{ .StartsAt }}
  Name: {{ .Labels.alertname }}
  
  Values:
  {{ range $refID, $value := .Values }}
    {{ $refID }}={{ $value }}
  {{ end }}
{{ end }}

```

- The new alert will look like the following

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/8dd10d62-884a-4612-b621-9137a7e17d4c/Untitled.png)

- The Grafana logo, footer, colors etc cannot be customized with this approach. For complete customization, the email template HTML file in Grafana needs to be edited

## Option 2 - Edit the Email alert HTML template

- The email alert template is present as the file “ng_alert_notification.html” in the grafana→public→emails folder (Example: “C:\Program Files\GrafanaLabs\grafana\public\emails\ng_alert_notification.html”)
- All the email HTML code can be edited in this file. Keep a backup of the original HTML file for safety before editing
- HTML content can be easily commented out by surrounding with `{{/*` `*/}}` tags
- Customization like removing logo, changing logo URL, font size, colors, removing content, footers, adding extra content etc., can be done very easily
- Restart Grafana after making changes
- If email is not sent after making changes in HTML, check Grafana logs located in the grafana.log file (”C:\Program Files\GrafanaLabs\grafana\data\log\grafana.log”) to check if there are errors in the email HTML file.
- An example email after commenting out Grafana logo, Alert folder heading and Number of alerts heading can be shown below

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/170cc36d-b626-42ec-8d44-1864277692b3/Untitled.png)

## References

- Grafana Go templating language guide - https://grafana.com/docs/grafana/latest/alerting/configure-notifications/template-notifications/using-go-templating-language/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTE2Njg5NjRdfQ==
-->