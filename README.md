# PagerTree 4 Design Specification
In this document you will find the following:
- The estimated timeline for the release of PT4
- Features we plan to add, deprecate, and continue supporting.
- Future items we plan to implement after the release of PT4
- Any special notes

If you are a current or prospective customer have any questions or concerns, please send an email to [support@pagertree.com](mailto:suppport@pagertree.com) detailing your questions or concerns.

## Timeline
ETA - Q1 2022 (revised), originally planned for Q3 2021

## General Features
This is a list of the features we already generally support. Unless it's in the deprecated section, assume that if PT3 has it, it will also be supported in PT4.

### Continued Support
- Accounts
- Teams
- Alerts
- Users
- On-Call Schedules
- Escalation Rules
- Notifications
- Integrations
- Broadcasts
- Maintenance Modes
- Stakeholders
- Routers and Notification Rules
- Reports
- Outgoing Webhooks
- Live Call Routing
- API Keys and API Access (* see special notes)
- ICal Export
- SSO

### Features Deprecated
- Automations
- Bridges

### Additions
- Postmortems
- Environments (think production/staging/test - an easy way for you to group your alerts and integrations)

### Major Improvements
- General
  - Search - Most pages will now search feature, to quickly search items in your account (powered by elastic search).
  - Documentation - Documentation on the object creation forms will be better. Documentation in the knowledge base will be less redundant.
  - I18n - PagerTree will support the following languages (English, Spanish, Dutch, French, & German).
  - Tagging - Most models will support tagging
  - Mobile - Better Mobile UI. Tables and calls to action are really hard to use in PT3. PT4 will fix this.
- Authentication and Security
  - 2 factor authentication (2FA)
  - Custom Security Roles - The ability for PagerTree admins to create custom security roles to attach to users.
  - SSO - Easier configuration (just point to metadata url).
- Accounts
  - Users can join multiple accounts (aka "organizations"). Especially helpful for consultancies.
- Users
  - Multiple emails per user
  - Multiple phones per user
- Alerts
  - Alert Aggregation - Better alert aggregation. PT3 provided minimal aggregation. PT4 plans to make aggregation a core feature for heavy lifting aggregation.
  - Public Pages (optional) - Make an alert publicly accessible via public URL. Additionally, subscribe emails (like a status page).
  - Custom alert urgencies - Continued support for critical/high/medium/low urgencies, with the option to edit the urgency description (useful for communicating when each urgency should be used) and also add custom urgencies.
  - Custom incident severities - Continued support for SEV-1 thru SEV-5 severities, with the option to edit the severity description (useful for communicating when each severity should be used, aka whats the customer impact level) and also add custom severities (in-case you use other sev levels in your organization).
  - Comments - Alerts will now have a comment history.
  - Subscribers - This could be stakeholders or individual emails.
- Integrations
  - Open source integrations - So the community can author their own integrations. Repo can be found here: [TODO]
- Teams
  - Notes sections
- Schedules / Event / Escalation Rules / Routers
  - Schedules and Escalation Rules have been decoupled from the Teams. By default, PT4 will make it look like a Team has one schedule and one escalation rule set, but under the hood they are decoupled, so that alerts can have dynamic schedules and escalation rules assigned to them using routers. By decoupling the schedules and escalation rules, PagerTree can now support multiple schedules per team (think "Default Calendar" vs "Christmas Calendar"). Teams can now also share calendars.
  - Events - Several bugs have been fixed in the scheduling, especially around the rotation feature.
- Stakeholders
  - Better messaging with the ability to send a one off stakeholder notification (think similar to a broadcast).
- Pages
  - Better placed "page this user" functionality. Its already in PT3, but it was really hard to find.
- Reporting
  - Easier filtering of data.
  - Monthly email to better show value PagerTree is providing to the customer.
- Billing 
  - Native support for yearly plans.
  - Auto Recharge - Option to enable auto recharge forever.
  - On Prem Licensing / "One-Click" Installs - Allows customers to install PagerTree in their own cloud to manage themseleves. This will require that customer provides keys for all underlying costs (servers, database, cache, notification providers (twilio, plivo, ect)) for a discounted price model. PagerTree will be released in several marketlplaces as a Platform as a Service (PaaS).
  - Referral Codes
- Specialty
  - Prometheus Endpoint - For scraping metrics to be used in combination with Grafana
  - CSV Export - Most pages will support a CSV export of data

## Future Items
Future Items we want to implement, but will be after the initial release of PT4. Think of this section as the future roadmap.
- Incident responder roles - Attach users as designated roles on incidents.
- Command line tool + API library - An easy to use cli for creating an alert. Similarly, easy to use libraries for easily creating alerts. Think `PagerTree.alerts.create!(title: '5xx Errors', urgency: 'critical', team: PagerTree.teams.find(name: 'DevOps'))` 
- In house live call routing - Purchase phone number and configure live call routing directly in PagerTree without having to have a seperate Twilio account
- Service Levels and Service Level Notifications - Notify users when the alert is at risk of breaching SLAs and SLOs.

## Special Notes
- API Keys and Access - We will be upgrading our API from v3 to v4. The v3 API will become **read-only** and customers will be required to upgrade to v4. Most underlying data structures will not change too much however, there will be some major changes. We will continue adding to this list, as the release date comes closer. We will also email our customer base notifying them of the changes.
  - "id" - The "id" field will be changing from a prefix id ("usr_xxxxxxx") to a ULID. We will continue to support the prefix id in a "prefix_id" attribute. If you just reference ids, your API access code should not need changing.
  - Camel cased attributes with be replaced with snake cased attributes. Namely tinyId -> tiny_id, createdAt -> created_at, updatedAt -> updated_at
