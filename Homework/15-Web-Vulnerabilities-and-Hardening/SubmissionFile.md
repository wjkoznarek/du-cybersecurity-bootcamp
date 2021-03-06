## Unit 15 Submission File: Web Vulnerabilities and Hardening


### Part 1: Q&A

#### The URL Cruise Missile

The URL is the gateway to the web, providing the user with unrestricted access to all available online resources. In the wrong hands can be used as a weapon to launch attacks.

Use the graphic below to answer the following questions:

| Protocol         | Host Name                 | Path                   | Parameters               |
| ---------------- | :-----------------------: | ---------------------- | ------------------------ |
| **http://**      | **`www.buyitnow.tv`**     | **`/add.asp`**           | **`?item=price#1999`**     |


1. Which part of the URL can be manipulated by an attacker to exploit a vulnerable back-end database system? 

Answer: Parameters

2. Which part of the URL can be manipulated by an attacker to cause a vulnerable web server to dump the `/etc/passwd` file? Also, name the attack used to exploit this vulnerability.

Answer: Path -  This would be called a dot-dot-slash or directory traversal
attack.
   
3. Name three threat agents that can pose a risk to your organization.

Answer: 
  - Nation States
  - Hacktivists/Activists
  - Organized Crime Groups

4. What kinds of sources can act as an attack vector for injection attacks?

Answer: 
  - SQL injection 
  - Cross-Site Scripting


5. Injection attacks exploit which part of the CIA triad?

Answer: Integrity

6. Which two mitigation methods can be used to thwart injection attacks?
  - Input Sanitation
  - Input Validation

----

#### Web Server Infrastructure
Web application infrastructure includes  sub-components and external applications that provide  efficiency, 
scalability, reliability, robustness, and most critically, security.

- The same advancements made in web applications that provide users these conveniences are the same components
that criminal hackers use to exploit them. Prudent security administrators need to be aware of how to harden 
such systems.


Use the graphic below to answer the following questions:

| Stage 1        | Stage 2             | Stage 3                 | Stage 4              | Stage 5          |
| :------------: | :-----------------: | :---------------------: | :------------------: | :--------------: |
| **Client**     | **Firewall**        | **Web Server**          | **Web Application**  | **Database**     |
   
   
1. What stage is the most inner part of the web architecture where data such as, customer names, addresses, account numbers, and credit card info, is stored?

Answer: Database

2. Which stage includes online forms, word processors, shopping carts, video and photo editing, spreadsheets, file scanning, file conversion, and email programs such as Gmail, Yahoo and AOL.

Answer: Web Application

3. What stage is the component that stores files (e.g. HTML documents, images, CSS stylesheets, and JavaScript files) that's connected to the Internet and provides support for physical data interactions between other devices connected to the web?

Answer: Web Server

4. What stage is where the end user interacts with the World Wide Web through the use of a web browser?

Answer: Client

5. Which stage is designed to prevent unauthorized access to and from protected web server resources?

Answer: Firewall

----


#### Server Side Attacks

In today’s globally connected cyber community, network and OS level attacks are well defended through the proper deployment of technical security controls such as, firewalls, IDS, Data Loss Prevention, EndPoint and security. However, web servers are accessible from anywhere on the web, making them vulnerable to attack.

1. What is the process called that cleans and scrubs user input in order to prevent it from exploiting security holes by proactively modifying user input.

Answer: Input Sanitation

2. Name the process that tests user and application-supplied input. The process is designed to prevent malformed data from entering a data information system by verifying user input meets a specific set of criteria (i.e. a string that does not contain standalone single quotation marks).

Answer: Input Validation

3. **Secure SDLC** is the process of ensuring security is built into web applications throughout the entire software development life cycle. Name three reasons why organization might fail at producing secure web applications.

Answer:
  - High cost
  - Insufficient support from management
  - Total reliance web application firewalls

4. How might an attacker exploit the `robots.txt` file on a web server?

Answer: Since this file tells a legitimate web crawler to skip pages/resources,
it would be a great target for a malicous crawler to specifically target those
sources or ignore it all together.

5. What steps can an organization take to obscure or obfuscate their contact information on domain registry web sites?

Answer: They can generally pay extra to hide more sensitive information in
a WHOIS record.
   
6. True or False: As a network defender, `Client-Side` validation is preferred over `Server-Side` validation because it's easier to defend against attacks.

   - Explain why you chose the answer that you did.

Answer: False, client-side validation can be bypassed and a malicous user may
do this and make special packets that request restricted information or injects
code into the server.

----

#### Web Application Firewalls

WAFs are designed to defend against different types of HTTP attacks and various query types such as SQLi and XSS.

WAFs are typically present on web sites that use strict transport security mechanisms such as online banking or 
e-commerce websites.

1. Which layer of the OSI model do WAFs operate at?

Answer: Layer 7 - Application Layer

2. A WAF helps protect web applications by filtering and monitoring what?

Answer: Generally WAFs are going to look at HTTP traffic, it looks at the
actual content of the packets so it can find attacks, such as SQLi. 

3. True or False: A WAF based on the negative security model (Blacklisting) protects against known attacks, and a WAF based on the positive security model (Whitelisting) allows pre-approved traffic to pass.

Answer: True

----

#### Authentication and Access Controls

Security enhancements designed to require users to present two or more pieces of evidence or credentials when logging into an account is called multi-factor authentication.

- Legislation and regulations such as The Payment Card Industry (PCI) Data Security Standard requires the use of MFAs for all network access to a Card Data Environment (CDE).

- Security administrators should have a comprehensive understanding of the basic underlying principles of how MFA works.

1. Define all four factors of multifactor authentication and give examples of each:

   - Factor 1: Biometric - Facial recognition, fingerprint sensor, and eye scan

   
   - Factor 2: Standard inputs - PIN, passwords
   
   
   - Factor 3: Physical keys - smartcards, hard tokens

   
   - Factor 4: Location - GPS detection, verification code to a landline.

   
2. True or False: A password and pin is an example of 2-factor authentication.

Answer: False
   
3. True or False: A password and `google authenticator app` is an example of 2-factor authentication.

Answer: True
   
4. What is a constrained user interface? 

Answer: A GUI designed to hide or restrict menus, options, features, and other
objects to act as an access control to the person using the interface. 

----

### Part 2: The Challenge 

In this activity, you will assume the role of a pen tester hired by a bank to test the security of the bank’s authentication scheme, sensitive financial data, and website interface.


#### Lab Environment   

We'll use the **Web Vulns** lab environment. To access it: 
  - Log in to the Azure Classroom Labs dashboard. 
  - Find the card with the title **Web Vulns** or **Web Vulnerability and Hardening**.
  - Click the monitor icon in the bottom-right. 
  - Select **Connect with RDP**.
  - Use Credentials (`azadmin:p4ssw0rd`)

- The lab should already be started, so you should be able to connect immediately. 

- Refer to the [lab setup instructions](https://cyberxsecurity.gitlab.io/documentation/using-classroom-labs/post/2019-01-09-first-access/) for details on setting up the RDP connection.

Once the lab environment is running, open the HyperV manager and make sure that the OWASPBWA and Kali box is running.

- Then, login to the Kali VM and navigate to the IP address of the OWASPBWA machine.

- Click the option for 'WebGoat' and start the WebGoat app.

- Use the credentials: `guest:guest`

On the bottom of the left side of the screen, click on `Challenge` and then choose `The Challenge`.

**Note:** A common issue with this lab is the Challange activity failing to start successfully. Hit the `Restart the Lesson` button in the top right if you get an error starting the activity.

### The Challenge Instructions

#### Challenge #1

Your first mission is to break the authentication scheme. There are a number of ways to accomplish this task.

- **Hint #1:** Sometimes, form fields are shy!

- **Hint #2:** Find the hidden JavaScript.

- **Hint #3:** You can appened `source?source=true` to the URL to read the source code. 

Please include a screenshot here of the hidden JavaScript:

  - URL manipulation to include `source?source=true` to see the server side
    source code.

  ![source=true](Images/screenshots/15-challenge1-view-source.png)

  - Inspected the webpage code to find hidden elements

  ![source=true](Images/screenshots/15-challenge1-hidden-fields.png)

  - First I typed in garbage input and hit login to get a failed attempt.
    TamperData returned a base64 value in the user value in the cookie header. 
  - Converted the cookie from base64 value to text, this gave me the username.

  ![source=true](Images/screenshots/15-challenge1-cookie-username.png)
  
After completing the first challenge, you will be provided with an option to continue to the next challenge.
  - Successful login with the following credentials
    - Username: `youaretheweakestlink`
    - Password: `goodbye`

  ![source=true](Images/screenshots/15-challenge1-complete.png)

#### Challenge #2

Next, steal all of the credit card numbers from the database. 

- **Hint #1**: Sometimes cookies wear different clothes to change their appearances.

- **Hint #2**: Break your way into the conversation and inject your own ideas.

Please include a screenshot here of all the credit card numbers from the database. 

##### Notes
- Take the Base64 value of the username cookie, and add our SQLi code `' OR
  '1'='1` and used TamperData to replace the cookie value with the SQLi.

  ![source=true](Images/screenshots/15-challenge2-cookie-base64.png)

After completing the second challenge, you will be provided with an option to continue to the next challenge.

  ![source=true](Images/screenshots/15-challenge2-complete.png)

#### Challenge #3

Your final act is to deface the website using command injection. Follow the walkthrough below to help you get started. 

- After completing the second challenge, you will be provided with an option to continue to the next challenge.

   ![cracked credit cards](Images/credit_cards-cracked.png)

- There should be two webpages at the bottom of the window. The one on top is the original, and the one on the bottom is the defaced webpage.

   ![original webpage](Images/original_defaced.png)

- Start Foxy Proxy (WebScarab) to send all GET/POST requests from Firefox to the WebScarab proxy intercept.

   ![Foxy Proxy](Images/foxy_proxy_scab.png)

- Click **TCP** and then the **View Network** button and send the request to WebScarab.

   ![View Network](Images/view_network_tcp.png)

- The WebScarab window will open. 

   - In the **URL Encoded** tab, find the **File** and **Value** form fields. 
   - This is where you will perform your command injection.
   
   ![File Field](Images/webscarab_file_value_field.png)

- Next, perform a test and see if this shell is vulnerable to command injection. 

   - Type the following command into the Value field: `tcp && whoami && pwd`.
   
       - **Note:** Windows users can type `tcp && dir`. `dir` will return the directory as proof of vulnerability.
   
   - Click **Accept Changes**.
   
   ![whoami](Images/whoami_pwd_image.png)
   
   - On the next window, click **Accept Changes** twice.
   
   ![accept](Images/webscarab_2nd_window.png)
 
- Scroll to the bottom of the **Current Network Status** window and observe the results for both of the `whoami` and `pwd` commands.

   ![whoami & pwd](Images/whoami_pwd.png)

   - The results show that we are the root user and our current working directory is `/var/lib/tomcat6`.

   - This verifies the vulnerability, so proceed to the next step.

- Next, we'll locate the `webgoat_challenge_guest.jsp` file. 

   - Type the following command: `tcp && cd / && find . -iname webgoat_challenge_guest.jsp`.
   
      - **Note**: Windows users will need to type: `tcp && dir /s 'webgoat_challenge_guest.jsp'`
   
   ![find command](Images/webscarab_find_command.png)
   
   - The absolute path is: `./owaspbwa/owaspbwa-svn/var/lib/tomcat6/webapps/WebGoat/webgoat_challenge_guest.jsp`.
   
   ![absolute path](Images/webscarab_abolute_path.png)
   
   - Remember, our present working directory is `/var/lib/tomcat6`. Therefore, the relative path is `webapps/WebGoat/webgoat_challenge_guest.jsp`.
   
**Now it's your turn**   

- Now that we know where the webpage is, your task will be to deface the website. Keep in mind the following:
  - Use **WebScarab** to perform command injection.
  - When performing command injection, you will need to select a field that WebScarab can return commands to. These fields are typically located in a drop down. 
  - You will also need to locate and edit the the webpage's source code: `webgoat_challenge_guest.jsp`
  - Your final command will:
    - Change to the location of the `webgoat_challenge_guest.jsp` file.
    - **and** echo `You've been hacked by...` followed by your name, to the `webgoat_challenge_guest.jsp` file.

  - Used webscarab to edit the `file` field inserted `tcp && whoami && pwd`
  ![pwd](Images/screenshots/15-challenge3-pwd.png)

  - Used webscarab to edit the `file` field, inserted `tcp && cd / && find . -iname webgoat_challenge_guest.jsp`
  ![find-jsp](Images/screenshots/15-challenge3-find-jsp.png)
    
  - Used webscarab to edit the `file` field, inserted `tcp && cd webapps/WebGoat/ && echo "You have been hacked by Will Koznarek" > webgoat_challenge_guest.jsp`
  ![find-jsp](Images/screenshots/15-challenge3-complete.png)

Please include a screenshot of the defaced website. 

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  
