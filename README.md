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

## Infrastructure Configuration

Provisioned Azure VM within a dedicated resource group 
and virtual network. Configured IIS with CGI support, 
registered PHP 7.3.8 as the FastCGI handler, deployed 
MySQL with standard configuration, and installed osTicket 
into the IIS web root.

PHP extensions enabled for full functionality:
- php_imap.dll (inbound email parsing)
- php_intl.dll (internationalization support)
- php_opcache.dll (opcode cache and performance)

Post-installation hardening:
- Setup directory permanently removed
- ost-config.php restricted to read-only
- Anonymous ticket creation disabled

![VM Provisioned](screenshots/ss02-vm-running.png)
![IIS Operational](screenshots/ss05-iis-welcome-page.png)
![PHP Registered](screenshots/ss07-php-registered-iis.png)
![Installation Complete](screenshots/ss12-osticket-installed-success.png)

## SLA Framework

Three-tier SLA structure configured to reflect 
business impact and operational urgency:

| Tier | Response | Schedule | Scope |
|------|----------|----------|-------|
| Sev-A | 1 hour | 24/7 | Business-critical outages |
| Sev-B | 4 hours | 24/7 | High-impact disruptions |
| Sev-C | 8 hours | Business hours | Standard requests |

![SLA Configuration](screenshots/ss14-sla-configuration.png)

## Access Control Architecture

Department structure configured with explicit agent 
permission boundaries. Support-tier agents operate 
within defined ticket visibility scopes. Escalation 
to the SysAdmins department triggers automatic 
access restriction for lower-privileged agents, 
protecting ticket integrity across the escalation chain.

![Departments](screenshots/ss15-departments.png)
![Agents](screenshots/ss16-agents-jane-john.png)
![Help Topics](screenshots/ss17-help-topics.png)

## Ticket Operations

**Scenario: Banking System Outage (Sev-A)**

Ticket submitted by end-user reporting full 
mobile and online banking system failure.

Initial state, unassigned with Default SLA:
![Unassigned](screenshots/ss19b-ticket-unassigned-queue_.png)

Triage actions applied:
- Priority: Emergency
- SLA: Sev-A (1-hour enforcement active)
- Department: SysAdmins
- Assigned: Jane Doe

Post-triage state:
![Triaged](screenshots/ss20-ticket-sev-a-assigned.png)

Post-escalation, Support agent access denied:
![RBAC Enforced](screenshots/ss21-ticket-inaccessible-john.png)

Resolved by Jane Doe with full audit trail:
![Resolved](screenshots/ss22c-ticket-closing-popup.png)
![Closed](screenshots/ss22d-ticket-closed-confirmed.png)

## Skills Demonstrated

Azure IaaS provisioning, IIS web server administration, 
PHP FastCGI configuration, MySQL database management, 
ITSM platform deployment, SLA design and enforcement, 
role-based access control, ticket lifecycle management, 
remote system administration, security hardening# osticket-helpdesk
Deployed osTicket v1.15.8 on Microsoft Azure. Configured IIS, PHP, MySQL, SLA tiers, role-based access control, and managed full ticket lifecycle.
