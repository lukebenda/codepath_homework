# Project 8 - Pentesting Live Targets

Time spent: **8** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:

* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.

## Blue

**Vulnerability #1: Session Hijacking/Fixation**

Description:

  **Session Hijacking**
  1. Open up the log in page and the hacktools/change_session_id.php script on two seperate browsers
  2. Log in on one browser (victim - Safari on right) then open a new tab and use the hacktools/change_session_id.php script to get the session ID.
  3. Copy the session ID.
  4. On the other browser (attacker - Chrome on left), go to the hacktools/change_session_id.php script and change the session ID to match the one that was just copied.
  5. Now, go to the log in page on the attacker browser and you will be logged in to the same account as the one on the victim browser without having to enter a username or password since it has the same session ID as the victim.
  
<img src="Blue-Session_Hijacking.gif">

  **Session Fixation**
  1. Open up the log in page and the hacktools/change_session_id.php script on two seperate browsers
  2. Open the hacktools/change_session_id.php script on the attacker browser (Chrome - left) and get a session ID. Copy the session ID.
  3. On the other browser (victim - Safari on right), go to the hacktools/change_session_id.php script and change the session ID to match the one that was just copied.
  4. Log in on the victim browser.
  5. The attacker can now log in on the attacker browser.
<img src="Blue-Session_Fixation.gif">

**Vulnerability #2: SQL Injection (SQLi)**

Description:
  1. Log into the site and navigate to the Salespeople page
  2. Select 'Show' for any salesperson
  3. Add ```' OR SLEEP(3)=0--'``` to the end of the url. The sleep() function allows you to specify the number of seconds it takes for the page to load (3 and 7 seconds are shown in the GIF)
<img src="Blue-SQLi.gif">

## Green

**Vulnerability #1: Cross-Site Scripting (XSS)**

Description:
  1. Go to the contact tab and fill out the form with a fake name and email and the following inside the feedback section: ```<script>alert('[Name] found the XSS');</script>```
  2. Then log in and proceed to the 'Feedback' section
  3. Here the alert will pop up, indicating that the attack was successful.

<img src="Green-XSS.gif">

**Vulnerability #2: Username Enumeration**

Description:
  1. When attempting to log in on the Green site with a existing username, the error message is presented in bold. Also, the html class is labeled **"failure"**.
  2. When attempting to log in on the Green site with a nonexisting username, the error message is presented in plaintext. The html class for this error is labeled **"failed"**.
  3. The other two sites do not have these discrepancies.
  4. The mistake that the developer of the Green site made was using different classes for a username that does exist and a username that does not exist. He/she also forgot to bold the error message's text for a nonexisting username. This vulnerability allows an attacker to determine whether or not a username exists.
<img src="Green-User_Enumeration.gif">


## Red

**Vulnerability #1: Insecure Direct Object Reference (IDOR)**

Description:
  1. Navigate to the 'Find a Salesperson' tab
  2. Select any salesperson
  3. In the URL, go to the end and change the ID to 10 or 11
  4. On the Red site, this will display informatoin that should only be accessible to a logged in user. If this attack is performed on the other two sites, they redirect to the main page.

<img src="Red-IDOR.gif">

**Vulnerability #2: Cross-Site Request Forgery (CSRF)**

Description:
  1. Go to the 'Salespeople' tab and view one of the salespeople. *There are no tokens used to identify an admin user on the Red site.* 
  2. Use the following HTML page with a hidden form to modify a salesperson's data
  ```
<!DOCTYPE html>
<html>
  <head>
	 <title>CSRF Page</title>
  </head>
  <body onload="document.CSRF.submit()">
    <form action=https://35.184.88.145/red/public/staff/salespeople/edit.php?id=12 method="POST" name="CSRF">
        <input type="text"   name="first_name"  value="Hacker"/>
        <input type="text"   name="last_name"   value="Guyyy"/>
        <input type="text"   name="phone"       value="123-456-7890"/>
        <input type="text"   name="email"       value="hackerguyyy@gmail.com"/>
    </form>
    <iframe name="hidden_iframe" style="display:none;"></iframe>
  </body>
</html>

<img src="Red-CSRF.gif">
```
3. When the page is opened in the browser, it changes the specified user on the actual Red site. 
4. Return to the Red site and refresh the page. The salesperson's data should be changed.


## Optional
**Bonus Objective 1:** Build on Objective #3 (SQL Injection). Experiment to see what other kinds of information you can get the database to reveal.

Description:
  1. Navigate to the 'Salespeople' section
  2. Select one of the names
  3. In the URL, paste the following SQL script: 
  ```
  ' AND 0 UNION SELECT 1,2,3,4,GROUP_CONCAT(table_name,0x2e,column_name,"\n") FROM information_schema.columns WHERE table_schema=database(); -- -
  ```
  4. The page will display all of the database's table and column names. 
  
<img src="Bonus-SQLi.gif">

**Bonus Objective 2:** Build on Objective #4 (Cross-Site Scripting). Experiment to see if you can use XSS to direct the user to a new URL.

Description:
  1. Navigate to the 'Contact' tab
  2. Fill in a fkae name and email
  3. In the feedback section, paste the following script: ```<script>document.location="https://www.google.com"</script>``` 
  4. Click Submit 
  5. Log in and click the 'Feedback' section <br>
  *Note: Series of alerts are from other students also hacking the site*
  6. The script will run and take the user to the specified link
  
<img src="Bonus-XSS.gif">

## Notes

**Describe any challenges encountered while doing the work**
It was difficult to figure out which attacks would work on each site. This was the most time consuming part of the assignment.  Nevertheless, I acknowledge that this is a major aspect of hacking and what makes the assignment far closer to real-world encounters. 
I also had the most difficulty completing the CSRF challenge. I discovered that ```<body onload="document.CSRF.submit()">``` and the name given to the form were different. This caused the page to load improperly and thus would not carry out a successful attack. Upon fixing this, the attack was successful.
