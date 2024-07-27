# My Memo CTF Writeup

## Challenge Information
- **Category**: Web  

## Objective
The objective of this challenge is to exploit the vulnerabilities of this web application to obtain the flag.

## Solution
<img width="692" alt="Screenshot 2024-07-28 at 1 00 36 AM" src="https://github.com/user-attachments/assets/037ce867-ec70-4532-beba-f45344b3c3e6">

To complete this challenge, I have created an account and login to access the memo application. After trying to inject some XSS payload into the comment section, I have concluded that it is not the right path to go.

<img width="409" alt="Screenshot 2024-07-28 at 1 07 45 AM" src="https://github.com/user-attachments/assets/2e2b9925-46cb-4855-932a-50967cd22cca">

After that, I have launched BurpSuite to monitor the sitemap and request/response being made when I enumerate and trying different payloads in the web application. While doing that, I have found out that one of the functions being called to obtain the memo of my account uses a parameter: **'userID'** to determine account. After manually changing the userID with random numbers, I have noticed the response has been changed, which indeed confirms that the manipulation of userID will enable me to access other user's memo.

<img width="1420" alt="Screenshot 2024-07-28 at 1 08 28 AM" src="https://github.com/user-attachments/assets/ab1b5701-ea96-49a5-9a07-cc2b693ca3ba">

<img width="501" alt="Screenshot 2024-07-28 at 1 08 48 AM" src="https://github.com/user-attachments/assets/9e5d2ecb-5b8f-425a-ab96-393014a57a50">

So, I have decided to bruteforce the parameter using the BurpSuite **"Intruder"** tools. By setting the payload up, which tries numbers from 0 - 100, I am able to get the response being made to access these user accounts.

<img width="1145" alt="Screenshot 2024-07-27 at 11 20 06 PM" src="https://github.com/user-attachments/assets/7bf9739f-ed1a-4766-bed5-f78030ab71cb">

After analysing the length of the response, I have found that userID: 69 (lmao), contains a comment revealing the admin password.

<img width="493" alt="Screenshot 2024-07-28 at 1 09 28 AM" src="https://github.com/user-attachments/assets/e87024b3-d684-456f-9bd2-102829271e92">

After obtaining the admin password, I navigate to the login page to try accessing the admin account with the credentials --> admin:admin71800. The error code shown after the attempt said the password has been expired, which requires resetting the password. 

<img width="1092" alt="Screenshot 2024-07-28 at 1 10 04 AM" src="https://github.com/user-attachments/assets/eedc9e5c-e392-4561-aafc-afe8ac0ff5f5">

After clicking and resetting the password and intercepting the request with BurpSuite, I have found out that there's a link in the source code.

<img width="907" alt="Screenshot 2024-07-28 at 1 10 15 AM" src="https://github.com/user-attachments/assets/fe7bf051-2521-410e-b28f-873337496c63">

After clicking the link, it redirects me to a memo page that belongs to the admin. The flag can be found printed at the bottom of the page.

## Flag

<img width="519" alt="Screenshot 2024-07-28 at 3 02 30 AM" src="https://github.com/user-attachments/assets/4b73d114-738f-4017-b3e0-6b37b612b044">

ihack24{ea082099722927625a51a3dd5b1057aa4b9867ac}

