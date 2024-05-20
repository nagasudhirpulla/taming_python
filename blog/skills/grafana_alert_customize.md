# Customize Grafana email alerts

- The alert email sent by Grafana can be customized. The default alert email looks something like this

![grafana_alert_email_image_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_alert_email_image_demo.png?raw=true)

- Even though the default alert email is very informative, there might be some customization requirements like removal or change of Grafana logo, change in colors etc.

## Notification template in Grafana

- Grafana alert content is created from Go templating variables.
- The official guide to understand Go templating language used Grafana alerts can be found at https://grafana.com/docs/grafana/latest/alerting/configure-notifications/template-notifications/using-go-templating-language/

Let us explore the options to customize Grafana alert content

## Option 1 - Edit contact point Message (Limited customization)

- In the email contact point editing screen there is a provision to customize email message as shown below

![grafana_email_message_customize.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_email_message_customize.png?raw=true)

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

![grafana_custom_email_message_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_custom_email_message_demo.png?raw=true)

- The Grafana logo, footer, colors etc cannot be customized with this approach. For complete customization, the email template HTML file in Grafana needs to be edited

## Option 2 - Edit the Email alert HTML template

- The email alert template is present as the file “ng_alert_notification.html” in the grafana→public→emails folder (Example: “C:\Program Files\GrafanaLabs\grafana\public\emails\ng_alert_notification.html”)
- All the email HTML code can be edited in this file. Keep a backup of the original HTML file for safety before editing
- HTML content can be easily commented out by surrounding with `{{/*` `*/}}` tags
- Customization like removing logo, changing logo URL, font size, colors, removing content, footers, adding extra content etc., can be done very easily
- Restart Grafana after making changes
- If email is not sent after making changes in HTML, check Grafana logs located in the grafana.log file (”C:\Program Files\GrafanaLabs\grafana\data\log\grafana.log”) to check if there are errors in the email HTML file.
- An example email after commenting out Grafana logo, Alert folder heading and Number of alerts heading can be shown below

![grafana_custom_email_html_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_custom_email_html_demo.png?raw=true)

## References

- Grafana Go templating language guide - https://grafana.com/docs/grafana/latest/alerting/configure-notifications/template-notifications/using-go-templating-language/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2NTg2NDU0MiwtNTQ2ODM4NDYzLC0xNj
kxNjY4OTY0XX0=
-->