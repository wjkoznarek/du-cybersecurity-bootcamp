## Homework: Penetration Test Engagement

In this activity, you will play the role of an independent penetration tester hired by GoodCorp Inc. to perform security tests against their CEO’s workstation.

- The CEO claims to have passwords that are long and complex and therefore unhackable.

- You are tasked with gaining access to the CEO's computer and using a Meterpreter session to search for two files that contain the strings `recipe` and `seceretfile`.

- The deliverable for this engagement will be in the form of a report labeled `Report.docx`.


#### Reminders

- A penetration tester's job is not just to gain access and find a file. Pentesters need to find all vulnerabilities, and document and report them to the client. It's quite possible that the CEO's workstation has multiple vulnerabilities.
 
- If a specific exploit doesn't work, that doesn't necessarily mean that the target service isn't vulnerable. It's possible that something could be wrong with the exploit script itself. Remember, not all exploit scripts are right for every situation.
 
#### Scope
 
- The scope of this engagement is limited to the CEO's workstation only. You are not permitted to scan any other IP addresses or exploit anything other than the CEO's IP address.
 
- The CEO has a busy schedule and cannot have the computer offline for an extended period of time. Therefore, denial of service and brute force attacks are prohibited. 
 
- After you gain access to the CEO’s computer, you may read and access any file, but you cannot delete them. Nor are you allowed to make any configurations changes to the computer.
 
- Since you've already been provided access to the network, OSINT won't be necessary.
 
#### Lab Environment
 
For this week's homework, please use the following VM setup:
 
- Attacking machine: Kali Linux `root:toor`
- Target machine: DVW10 `IEUser:Passw0rd!`

**NOTE**: You will need to login to the **DVW10** VM and start the `icecast` service prior to beginning this activity using the following procedure:

- After logging into DVW10, type "icecast" in the Cortana search box and hit **Enter**.
- The icecast application will launch.
- Click on **Start Server**.
- You are now ready to being the activity.

#### Deliverables

- Submit your findings in the following document: [Report.docx](Resources/Report.docx)
- Remember that you should capture screenshots and commands of every step
 
### Instructions

 
1. Perform a service and version scan using Nmap to determine the IP of the CEO's machine (you should be able to tell which one is running Windows) and which services are up and running:

    - Run the Nmap command that performs a service and version scan against the target.


2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:
 
   - Run the SearchSploit commands to show available Icecast exploits.


3. Now that we know which exploits are available to us, let's start Metasploit:
 
   - Run the command that starts Metasploit:
    

4. Search for the Icecast module and load it for use.
 
   - Run the command to search for the Icecast module:
     

   - Run the command to use the Icecast module:

 
5. Set the `RHOST` to the target machine.
 
   - Run the command that sets the `RHOST`:

 
6. Run the Icecast exploit.
 
   - Run the command that runs the Icecast exploit.
      

 7. You should now have a Meterpreter session open.
 
   - Run the command that performs a search for a file containing the string `secretfile` on the target.


   - Run the command to performs a search for a file containing the string `recipe` on the target:


   - Run the command(s) that exfiltrates the files you found above and view their contents


 
#### Bonus
  
 
1. Run a Meterpreter post script that enumerates all logged on users.

2. Open a Meterpreter shell and gather system information for the target.
 
3. Run the command that displays the target's computer system information


#### Super Bonus

1. Find a way to determine the plaintext password for the local "Administrator" user on the victim machine

---

&copy; 2020 Trilogy Education Services, a 2U Inc Brand.   All Rights Reserved.
