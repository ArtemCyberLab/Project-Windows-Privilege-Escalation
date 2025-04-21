Project Goal:
The project was focused on performing security testing of a web application hosted on the server with IP address 10.10.213.68. My goal was to identify vulnerabilities that could be exploited by attackers to gain unauthorized access to the application or server.

Tools Used:
For carrying out the tasks, various tools were used:

Nmap for port scanning and identifying open services.

Gobuster for discovering hidden directories and files on the server.

Hydra for brute-force attacks on login pages.

SQLmap for testing SQL injection vulnerabilities.

Nikto for finding common vulnerabilities, including XSS and others.

Steps Taken in Security Testing
Scanning and Information Gathering:
At the beginning of the project, I performed a port scan of the target server using Nmap to identify open ports and services. This allowed me to understand which ports and services were running on the server, which is crucial for further attacks.

Example command:

bash
Copy
Edit
nmap -sS -p- 10.10.213.68
Finding Hidden Files and Directories:
To find potentially vulnerable points on the server, I used Gobuster, which helped me locate hidden pages and folders that might contain vulnerabilities.

Example command:

bash
Copy
Edit
gobuster dir -u http://10.10.213.68 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
SQL Injection Testing:
I also checked the server for SQL injection vulnerabilities using SQLmap. This is important for assessing the potential for attacking the application's database.

Example command:

bash
Copy
Edit
sqlmap -u "http://10.10.213.68/Account/login.aspx?ReturnURL=/admin/" --data "ctl00$MainContent$LoginUser$UserName=admin&ctl00$MainContent$LoginUser$Password=wrong&ctl00$MainContent$LoginUser$LoginButton=Log+in" --risk=3 --level=5 --batch --dump
Brute-Force Attack on the Login Page:
For password cracking, I used Hydra. This allowed me to test the strength of the login page's security and identify any vulnerabilities if they existed. Example command for a brute-force attack:

bash
Copy
Edit
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.213.68 http-post-form "/Account/login.aspx?ReturnURL=/admin/:ctl00\$MainContent\$LoginUser\$UserName=^USER^&ctl00\$MainContent\$LoginUser\$Password=^PASS^&ctl00\$MainContent\$LoginUser\$LoginButton=Log+in:F=Email is invalid"
As a result of this attack, I was able to find the correct password for the admin account, which allowed me to successfully log into the system.

Looking for XSS and Other Vulnerabilities:
During testing, I checked the website for vulnerabilities such as XSS (cross-site scripting), which could be exploited to execute arbitrary code on the client-side. For this, I used Nikto.

Example command:

bash
Copy
Edit
nikto -h http://10.10.213.68
Privilege Escalation:
After gaining access to the admin panel via brute-force, I attempted to conduct further tests to check for privilege escalation and the possibility of using other vulnerabilities to gain full control over the server.

Exploiting Vulnerabilities:
Once access to the system was obtained, I conducted an analysis to identify other potential vulnerabilities for exploitation and leveraged my access to take further control.

Clearing Traces and Documentation:
At the end of the project, I removed all traces of my activity on the server and prepared a report detailing the findings, including discovered vulnerabilities, methods of exploitation, and recommendations for improving the system’s security.

Results
As a result of the tests, I was able to:

Successfully authenticate to the administrative panel after performing a brute-force attack.

Identify vulnerabilities in the system that could be exploited to access sensitive information.

Evaluate the system's level of security and provide recommendations for improving it.

Conclusion
The project allowed me to identify vulnerabilities in the application and demonstrated the potential risks if they were exploited. It also helped me improve my skills in penetration testing, using security testing tools, and analyzing the security of web applications.

