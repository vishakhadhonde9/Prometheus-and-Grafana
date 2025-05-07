# Dashboard -
Dashboard is interface through which you can visualize your data.



# Alram -

## Components of Grafana Alarm -
### Evaluation Query -
- The data Grafana uses to check the alarm condition.
- Comes from a panel’s query (like a Prometheus metric or SQL).

### Condition
- A rule based on the evaluation query.
- Example: “If the average CPU usage is above 80% for 5 minutes.”

### Evaluation Interval
- How often Grafana checks the condition (e.g., every 1 minute).

### For Duration
- The condition must stay true for this long to trigger the alert (e.g., 5 minutes).

### Alert State
- OK – Condition not met.
- Pending – Condition is true, but not for the full “For” duration yet.
- Alerting – Condition true long enough; alarm is triggered.

### Notification Channel (Contact Point)
- Where alerts are sent (e.g., Slack, email, Teams, webhook).
- You define these in Alerting --> Contact points.

### Notification Policy
- A routing rule that tells Grafana which alerts go to which contact points.

## Configure SMTP in Grafana -

- sudo vi /etc/grafana/grafana.ini

[smtp]
enabled = true
host = smtp.gmail.com:587
user = your_email@gmail.com
password = your_gmail_app_password
from_address = your_email@gmail.com
from_name = Grafana Alerts
ehlo_identity = localhost


- sudo systemctl restart grafana-server


| Email Provider                                         | SMTP Host                                      | Port                       |
|--------------------------------------------------------|------------------------------------------------|----------------------------|
| **Gmail**                                              | `smtp.gmail.com`                               | `587` (TLS) or `465` (SSL) |
| **Outlook / Hotmail / Live**                           | `smtp.office365.com`                           | `587`                      |
| **Yahoo Mail**                                         | `smtp.mail.yahoo.com`                          | `465` (SSL)                |
| **Zoho Mail**                                          | `smtp.zoho.com`                                | `587` (TLS)                |
| **iCloud Mail**                                        | `smtp.mail.me.com`                             | `587` (TLS)                |
| **ProtonMail (via Bridge)**                            | `127.0.0.1`                                    | Custom (Bridge app)        |
| **Custom domain (e.g., via GoDaddy, Namecheap, etc.)** | Depends on provider (check hosting/email docs) | Usually 465 or 587         |

