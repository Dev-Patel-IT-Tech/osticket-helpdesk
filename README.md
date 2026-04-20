# osTicket Help Desk Deployment on Azure

## Summary

Deployed and administered a full-stack help desk 
environment on Microsoft Azure. Configured the complete 
server infrastructure, IIS 10, PHP 7.3.8, MySQL 5.5.62, 
and administered osTicket v1.15.8 across SLA design, 
role-based access control, department routing, and 
ticket lifecycle operations.

## Environment

| Component | Specification |
|-----------|--------------|
| Platform | Microsoft Azure |
| VM | Windows 10 Pro, Standard_D2s_v3 (4 vCPUs) |
| Web Server | IIS 10 with CGI and FastCGI |
| Runtime | PHP 7.3.8 |
| Database | MySQL 5.5.62 |
| DB Client | HeidiSQL 12.3 |
| Application | osTicket v1.15.8 |
| Access | Remote Desktop Protocol (RDP) |

## Infrastructure Setup

Provisioned a Windows 10 VM in Azure within a dedicated 
resource group and virtual network. Connected via RDP 
and executed full server-side configuration.

![Resource Group](screenshots/ss01-resource-group.png)
![VM Running](screenshots/ss02-vm-running.png)
![RDP Connected](screenshots/ss03-rdp-connected.png)

Enabled IIS with CGI support, installed PHP Manager 
and the URL Rewrite module, created C:\PHP and 
extracted PHP 7.3.8 into it.

![CGI Enabled](screenshots/ss04-iis-cgi-enabled.png)
![IIS Running](screenshots/ss05-iis-welcome-page.png)
![PHP Folder](screenshots/ss06-php-folder.png)

Registered PHP 7.3.8 as the FastCGI handler in IIS 
PHP Manager. Installed MySQL 5.5.62 and created the 
osTicket database using HeidiSQL.

![PHP Registered](screenshots/ss07-php-registered-iis.png)
![Database Created](screenshots/ss11-heidisql-database.png)

## osTicket Installation

Extracted osTicket into the IIS web root. Three PHP 
extensions were not enabled by default and were 
activated via IIS PHP Manager.

Before enabling extensions:
![Before](screenshots/ss09-osticket-prereq-before.png)

After enabling php_imap.dll, php_intl.dll, 
and php_opcache.dll:
![After](screenshots/ss10-osticket-prereq-after.png)

Completed browser-based installation with MySQL 
database connection confirmed.

![Installation Complete](screenshots/ss12-osticket-installed-success.png)

Post-installation steps completed:
- Setup directory permanently removed
- ost-config.php restricted to read-only
- Anonymous ticket creation disabled

## Admin Panel

Logged in as admin. System logs confirm installation 
date and initial system activity.

![Admin Dashboard](screenshots/ss13-admin-panel-dashboard.png)

## SLA Configuration

Three-tier SLA structure configured based on 
business impact:

| Tier | Response | Schedule | Scope |
|------|----------|----------|-------|
| Sev-A | 1 hour | 24/7 | Business-critical outages |
| Sev-B | 4 hours | 24/7 | High-impact disruptions |
| Sev-C | 8 hours | Business hours | Standard requests |

![SLA Configuration](screenshots/ss14-sla-configuration.png)

## Departments, Agents, and Help Topics

Configured two departments (SysAdmins and Support), 
three agents with distinct permission profiles, 
and help topics covering common ticket categories.

![Departments](screenshots/ss15-departments.png)
![Agents](screenshots/ss16-agents-jane-john.png)
![Help Topics](screenshots/ss17-help-topics.png)

## Ticket Lifecycle: Banking System Outage (Sev-A)

**Step 1: End-user submits ticket**

Karen reported the entire online banking system 
was down and tellers could not log in.

![Ticket Created](screenshots/ss18b-creating-ticket-enduser.png)

**Step 2: Agent John receives ticket**

Ticket arrived in John's queue with no SLA, 
no department, and no assignment.

![Queue View](screenshots/ss19a-ticket-unassigned-queue.png)
![Ticket Open](screenshots/ss19b-ticket-unassigned-queue_.png)

**Step 3: Triage and escalation**

Priority set to Emergency, SLA set to Sev-A, 
routed to SysAdmins department, assigned to Jane Doe.

![Triaged](screenshots/ss20-ticket-sev-a-assigned.png)

**Step 4: RBAC enforcement**

After routing to SysAdmins, John's account received 
access denied. The ticket disappeared from his queue 
entirely because his role does not include SysAdmins 
department access.

![Access Denied](screenshots/ss21-ticket-inaccessible-john.png)

**Step 5: Resolution by Jane**

Jane investigated, identified a backend server 
configuration issue, restarted the service, 
confirmed restoration with Karen, and closed the ticket.

![Investigation Note](screenshots/ss22a-jane-investigating-ticket.png)
![Resolution Note](screenshots/ss22b-jane-resolving-ticket.png)
![Ticket Closed](screenshots/ss22c-ticket-closing-popup.png)
![Closure Confirmed](screenshots/ss22d-ticket-closed-confirmed.png)

## What I Took Away

The access denied on John's account was the most 
useful outcome of this project. It is easy to 
understand RBAC in theory. Watching a ticket vanish 
from an agent's queue the moment it escalates to a 
department they cannot access made it concrete. 
In a real environment that boundary is what stops 
lower-level agents from touching sensitive escalations.

The Sev-A due date appearing as exactly one hour 
from ticket creation confirmed the SLA configuration 
was enforced at the system level, not just as a label.

## Skills Demonstrated

Azure IaaS provisioning, IIS web server administration, 
PHP FastCGI configuration, MySQL database management, 
ITSM platform deployment, SLA design and enforcement, 
role-based access control, ticket lifecycle management, 
remote system administration, security hardening
