# Cases export review (2026-11-03)

`../Cases__1.csv` contains 16 open reports about this repository. Five repeat earlier
reports. The separate `../web-project-lab4/zammad/seed/tickets.json` describes a
different attendance project with professors, QR sessions, absence requests and
`uv.lock`; those features do not exist here.

| CSV report | Result in this repository |
|---|---|
| Paper list import fails above 6 MB | Backend regression accepts an 11 MB image under its 15 MB per-image limit. A live upload through ngrok remains to be checked. |
| Clear leaves search text; blur resets page | Search text follows the URL filter, Clear empties both, and unchanged blur does not reset pagination. |
| CSV formula injection; repeated Admin & Analytics report | Formula-leading text is escaped in both CSV and XLSX exports. |
| Rejected attendance counted present; repeated Admin & Analytics report | Absentees, dashboard event counts and summary turnout exclude rejected submissions. Status totals still show them. |
| Insecure default secrets | Production rejects default or missing JWT/admin/database credentials. Local Compose requires secrets and binds ports to loopback. Grafana reader password comes from configuration. |
| Tokens survive password reset; repeated Authentication & Frontend report | A stored token version invalidates old tokens on password change, admin password reset and sign out. Existing tokens are invalidated by the deployment migration. |
| Admin list pagination and per-event query loop | User/event endpoints now page at 200 records; the frontend loads all pages. Attendance summary computes expected counts from one membership query. |
| Event-title search empties rate charts; repeated Admin & Analytics report | Rate calculations now include matching event titles as well as matching students. |
| Event form invalid/past dates and raw errors | New-event date inputs constrain past and reversed times; the form validates and shows readable messages. |
| Bcrypt ignores password bytes after 72 | Registration, admin reset, password change and login reject passwords over 72 UTF-8 bytes. |
| Naive date filters skew PostgreSQL results | The API requires a timezone offset for date filters, then converts to UTC. |

The Zammad tickets are not imported into this repo or this issue list because they
describe a different application and cannot be applied here without changing the
product's feature set.
