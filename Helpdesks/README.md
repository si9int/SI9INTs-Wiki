### Description

This article summarizes the so called "TicketTrick" by Nti De Ceukelaire, describing how access to internal communication platforms (like Slack, Workplace, Yammer) of different companies can be gained by abusing mail-behavior of hosted help-desks or bug-/issue trackers. [Original article on Medium](https://medium.com/intigriti/how-i-hacked-hundreds-of-companies-through-their-helpdesk-b7680ddc2d4c).

### Content
E-mails sent to an address like `support@company.com` sometimes turned up in an online portal such as Zendesk, Kayako, FreshDesk, WHCMS. Most of the configured helpdesks don't do an e-mail address verification when signing up for an account. This can be abused under the following circumstances:

- Support tickets can be created through e-mail
- Support tickets are accessible by users with an unverified e-mail address

**Example (Slack; patched)**  
The following describes how to issue was exploited by gaining access to Slack via helpdesk:
```
1. Register on the helpdesk with the mail address "feedback@slack.com"
2. Register on the Slack workspace via "support@company.com"
3. Read verification mail throughout the support tickets (any mail to support@company will be forwarded to the related user)
```
This can also be used to reset password of an account associated with `support@company.com`.   

Therefore an attacker only have to determine the mail-address sending out the password-reset.
Services who are reflecting sent e-mails and doesn't require a mail-verification (or allow to change the e-mail after verification without verification) are vulnerable too.
