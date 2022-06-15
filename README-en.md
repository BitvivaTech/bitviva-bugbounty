![bitexen-bugbounty-img](src/bitexen-bugbounty-img.png)

# Bitexen Vulnerability Reporting Program

Welcome to the Bitexen Vulnerability Reporting Program. As one of Turkey's largest crypto exchanges, providing a secure platform to our customers is one of our main priorities. Therefore, we invite everyone to join the Bitexen Vulnerability Reporting Program. With this program, we encourage researchers and hackers to responsibly find, report and help us fix security vulnerabilities.

As with similar vulnerability reporting programs, Bitexen Vulnerability Reporting Program has very clear and simple rules to protect both us and those who report vulnerabilities.

You can send your questions about the Bitexen Vulnerability Reporting Program to bugbounty@bitexen.com.

Thanks for participating and happy hunting! ¯\\\_(ツ)\_/¯

## Rules

- The first report for the same vulnerability is accepted.
- Reports for vulnerabilities already known by Bitexen are not accepted.
- Do not share the vulnerabilities found on other platforms without Bitexen's permission. Reports that are found to be shared will lose their reward.
- Reports sent for vulnerabilities specified as out of scope are not accepted.
- Care should be taken not to damage the systems and the confidentiality of personal data.
- Other user data should not be accessed or changed, and all tests should be performed with the accounts under your control. You can forward vulnerabilities that may authorize access to user data without verifying or only by verifying them on your own accounts.
- Social engineering methods (phishing, vishing, smishing, etc.) and physical attacks (computer theft, SIM card copying, etc.) should not be used. DoS attacks should not be attempted.
- Reports can be submitted in Turkish or English.
- All details about the vulnerability must be shared and a PoC must be given. You can access the sample report formats at [report-templates](https://github.com/Bitexen/bitexen-bugbounty/tree/master/report-templates) page.
- In cases where chain security vulnerabilities are detected by using more than one security vulnerabilities, separate reporting can be made.

## Risk Categorization

We have classified the reported vulnerabilities into four categories based on their impact. Vulnerabilities not listed will be evaluated based on their potential impact.

### Critical

- Unauthorized token or money withdrawal from user accounts
- Exposure of sensitive user information (identity data, address, phone)
- Remote code execution on Bitexen servers
- Access to user accounts by bypassing login or MFA functions (Social engineering and brute force attacks are excluded)
- Transaction by bypassing the business logic (changing the price in coin purchases, etc.)
- Affecting encryption, signing, authentication functions

### High

- Exposure of user wallet information (tokens owned, amount of money, etc.)
- Remote code execution on Bitexen servers (unauthorized user)
- Servers with critical data left in public access (Ex. AWS S3)
- Detecting XSS (except Reflected and self XSS) vulnerability by bypassing CSP

### Medium

- Running code on mobile device via Bitexen applications

### Low

- Non-critical information disclosure vulnerabilities on servers that cannot be combined with another attack

## Rewards

The table below shows the largest prize amount to be rewarded in the specified category. In case a valid report is submitted, the amount of the reward will be calculated based on the report. You can earn additional rewards for high quality reporting, assisting in the reporting and resolution process.

| Critical   | High       | Medium    | Low       |
|------------|------------|-----------|-----------|
| USD 3.000  | USD 1.000  | USD 250   | USD 50    |

Bitexen reserves the right to change the specified prize amounts without notice. The current reward amount on the date the report is submitted to Bitexen is taken into account. The prize won will be transferred to Bitexen accounts as BTXN or USDT according to your preference.

### Reward Criteria

- Bitexen employees and their first degree relatives cannot win rewards.
- You must be at least 14 years old to be eligible for the reward.
- Detected vulnerabilities should not be shared publicly.
- There should be no legal obstacles to the giving of the reward.

## Scope

| Target Application | Domain/Adres                                               |
|--------------------|------------------------------------------------------------|
| Domain             | www.bitexen.com/*                                          |
| Domain             | bitexen.com/*                                              |
| Android App        | Bitexen (com.bitexen.exchange)                             |
| IOS App            | Bitexen (ID 1388036461)                                    |
| Smart Contract     | 0xe6cc10ef4de1ccfb821c99c04abfe1859d8eab8f (BTXN) (ERC20)  |
| Smart Contract     | 0xbcf91e60a6719eb3e9308addf1f7c6185c2af889 (XNP) (ERC20)   |

Note: You can find the codes of smart contracts at https://etherscan.io/.

## Out of Scope

- Domains and applications not listed in scope (Critical or high level vulnerabilities may be considered in scope)
- Vulnerable libraries and versions (Can be considered in scope if there is an impacting PoC or exploitation method)
- Theoretical, non-PoC-enabled or ineffective attacks
- Automated tool and scan reports
- Non-repeatable vulnerabilities
- Brute force and social engineering attacks
- DoS attacks (When you find a security vulnerability that may be a DoS cause, forward it without verification)
- Self XSS
- Attacks based on the use of weak or leaked passwords
- CSRF vulnerabilities in input and output functions
- Security flaws in HTTP headers
- Cookie flag missing
- Vulnerabilities on non-critical servers that could lead to information disclosure
- Attacks that require Bitexen employee account or internal network access
- Attacks that require MITM or physical access
- Cache Poisoning vulnerabilities
- SSL/TLS configuration deficiencies (using TLS 1.1 etc.)
- E-Mail configuration deficiencies (SPF/DMARC/DKIM records etc.)
- Open Redirects vulnerabilities that cannot be proven to have an effect (such as cookie theft)
- Absence of rate limiting (in systems with rate limiting, bypassing the rate limit will be considered within the scope)
- UX and UI problems
- Username enumeration vulnerabilities
- Vulnerabilities that can only be exploited in outdated browsers, operating systems or platforms
- Vulnerabilities found in third-party applications used
- Deficiencies in "Best Practice" accepted controls
- Vulnerabilities on mobile devices that require root, jailbreak or device modification

You can send your questions about systems/vulnerabilities that are not specified as out of scope.

## Testing and Reporting

You can help us by following the methods below so that we do not confuse the traffic generated during your tests with the attacker traffic.

- You can use custom HTTP headers. (Example: X-BTXN-VDP: <user email address>)
- You can specify your IP address in the report.

Be sure to only use accounts that you control during the testing process. If you have found a vulnerability to run commands on systems, just use the ```id``` and```hostname``` commands. Do not use automated tools. If you have found a potentially damaging vulnerability, contact us to obtain additional testing permissions before verifying.

Allowed/not allowed actions for remote code execution vulnerabilities:

- Allowed
  - Harmless command attempts on input fields on the web frontend (such as ``whoami```, ``hostname```, ``ifconfig```)
  - File uploads that run a harmless command as hard-coded
  - Commands ``id`` and``hostname`` for proof of exploited vulnerability
- Not Allowed
  - File uploads (webshell etc.) that can lead to free command execution
  - File deletion, editing, changing permissions
  - Actions that may affect normal operations (reboot etc.)
  - Commands and file accesses executed other than those required for proof of vulnerability

The following information should also be provided when reporting remote code execution vulnerabilities:

- Source IP address, destination IP address and port information
- Timestamp
- Requests and responses to the server
- Files and directories that were accessed intentionally or unintentionally during the test.

We will be happy if you would use our report draft :)

## Safe Harbor

Bitexen will not take any legal action for researches and reports made in accordance with the rules specified on this page.

In case of sending a report, it is considered that the rights of the submitted content are transferred to Bitexen.

In case the security vulnerabilities in the reports submitted within the scope of the program are related to the products and services, network structures, systems, applications and information of third parties other than Bitexen, the relevant reports are not considered within the scope of the Bitexen Vulnerability Reporting Program and therefore the relevant third parties may initiate legal action in such a reporting situation and We would like to inform you that we, as Bitexen, are not responsible for the situation. Bitexen does not allow security research other than its own products and services and does not provide any person with an authorization in this regard.

You can access the document, which includes detailed rules and legal information about the Bitexen Vulnerability Reporting Program, from the page [policy-details](https://github.com/Bitexen/bitexen-bugbounty/tree/master/policy-details).

Happy hunting! ᕕ( ᐛ )ᕗ

_Bitexen Vulnerability Reporting Program has been prepared to receive controlled news about security vulnerabilities that may be found in our systems and to encourage researchers. If you think that the security of your Bitexen account has been compromised, change your password as soon as possible and contact our support team via support@bitexen.com._
