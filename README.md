# osTicket Help Desk Deployment on Azure

## Overview

Deployed and administered a full-stack help desk
environment on Microsoft Azure. Configured IIS 10,
PHP 7.3.8, and MySQL 5.5.62 from scratch and
administered osTicket v1.15.8 including SLA design,
role-based access control, department routing, and
complete ticket lifecycle management.

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

## Deployment

Provisioned a Windows 10 VM in Azure within a
dedicated resource group and virtual network.

![Resource Group](screenshots/ss01-resource-group.png)

![VM Running](screenshots/ss02-vm-running.png)

Connected via RDP and began server-side configuration.

![RDP Connected](screenshots/ss03-rdp-connected.png)

Enabled IIS with CGI support. CGI is the only
extension selected under Application Development,
required for PHP to communicate with IIS via FastCGI.

![CGI Enabled](screenshots/ss04-iis-cgi-enabled.png)

Confirmed IIS was operational by loading the
default page at localhost.

![IIS Running](screenshots/ss05-iis-welcome-page.png)

Created the C:\PHP directory and extracted
PHP 7.3.8 into it.

![PHP Folder](screenshots/ss06-php-folder.png)

Registered PHP 7.3.8 as the FastCGI handler
in IIS PHP Manager. Handler mapping confirmed active.

![PHP Registered](screenshots/ss07-php-registered-iis.png)

Installed MySQL 5.5.62 with standard configuration.
Created the osTicket database using HeidiSQL.

![Database Created](screenshots/ss11-heidisql-database.png)

## Configuration

Extracted osTicket into the IIS web root and
completed the browser-based installer. Three PHP
extensions were not enabled by default and were
activated via IIS PHP Manager.

Before enabling extensions:

![Before](screenshots/ss09-osticket-prereq-before.png)

Enabled php_imap.dll, php_intl.dll, and
php_opcache.dll. All required checks passing.

After enabling extensions:

![After](screenshots/ss10-osticket-prereq-after.png)

Installation completed with full MySQL
database connectivity confirmed.

![Installation Complete](screenshots/ss12-osticket-installed-success.png)

Post-installation hardening applied:
- Setup directory permanently deleted
- ost-config.php restricted to read-only
- Anonymous ticket creation disabled

## System Administration

Logged in to the Admin Control Panel. System logs
confirm installation timestamp and system activity.

![Admin Dashboard](screenshots/ss13-admin-panel-dashboard.png)

Configured three SLA tiers aligned with business
impact and response requirements.

| Tier | Response | Schedule | Scope |
|------|----------|----------|-------|
| Sev-A | 1 hour | 24/7 | Business-critical outages |
| Sev-B | 4 hours | 24/7 | High-impact disruptions |
| Sev-C | 8 hours | Business hours | Standard requests |

![SLA Configuration](screenshots/ss14-sla-configuration.png)

Configured departments, agents, and help topics.
SysAdmins and Support departments created with
distinct permission boundaries. Three agents
assigned with role-based access profiles.

![Departments](screenshots/ss15-departments.png)

![Agents](screenshots/ss16-agents-jane-john.png)

![Help Topics](screenshots/ss17-help-topics.png)

## Access Control

Department-level permissions are enforced across
all agent accounts. Agents only have visibility
into tickets belonging to their assigned department.
Escalation to a restricted department removes
access for lower-privileged agents immediately
with no manual intervention required.

## Ticket Operations

**Step 1: End-user submits ticket**

Karen reported the entire online banking system
was down and branch tellers could not authenticate.

![Ticket Submitted](screenshots/ss18-creating-ticket-enduser.png)

**Step 2: Agent John receives ticket**

Ticket arrived with Normal priority, no SLA,
no department, and no assignment.

![Queue View](screenshots/ss19a-ticket-unassigned-queue%20.png)

![Ticket Open](screenshots/ss19b-ticket-unassigned-queue%20.png)

**Step 3: Triage and escalation**

Priority set to Emergency. SLA set to Sev-A,
enforcing a 1-hour response window. Routed to
SysAdmins and assigned to Jane Doe.

![Triaged](screenshots/ss20-ticket-sev-a-assigned.png)

**Step 4: Access control enforcement**

After routing to SysAdmins, John received a hard
access denied. The ticket was no longer visible
in his queue. Department-level RBAC blocked
access completely, not just edit rights.

![Access Denied](screenshots/ss21-ticket-inaccessible-john.png)

**Step 5: Resolution**

Jane identified a backend server configuration
error and initiated a service restart.

![Investigation](screenshots/ss22a-jane-investigating-ticket.png)

Service restored. User confirmed access recovered.

![Resolution](screenshots/ss22b-jane-resolving-ticket.png)

Ticket closed with full audit trail retained.

![Closed](screenshots/ss22c-ticket-closing-popup.png)

![Closure Confirmed](screenshots/ss22d-ticket-closed-confirmed.png)

## Observations

Department-level RBAC is enforced at the system
level. Once a ticket moves to a restricted
department, lower-privileged agents lose visibility
entirely. This is a critical control in environments
where sensitive escalations need to be protected
from unauthorized access or modification.

Sev-A due date was automatically set to one hour
from ticket creation, confirming SLA enforcement
is system-driven and not manually applied.

## Technical Skills Demonstrated

Azure IaaS provisioning, IIS web server administration,
PHP FastCGI configuration, MySQL database management,
ITSM platform deployment, SLA design and enforcement,
role-based access control, ticket lifecycle management,
remote system administration, security hardening
