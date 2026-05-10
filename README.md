# Lab-Basic-password-reset-poisoning-APPRENTICE


# Password Reset Poisoning - Proof of Concept

## Overview

This project demonstrates a Proof of Concept (PoC) for a Password Reset Poisoning vulnerability discovered in a password reset functionality.

The vulnerability allows an attacker to manipulate the password reset link sent via email by injecting a malicious Host header. As a result, sensitive password reset tokens can be leaked to an attacker-controlled server.

---

# Vulnerability Details

## Vulnerability Type

* Password Reset Poisoning
* Host Header Injection

## Severity

* High

## CWE

* CWE-640: Weak Password Recovery Mechanism for Forgotten Password

---

# Lab Information

Platform:

* PortSwigger Web Security Academy

Lab:

* Basic Password Reset Poisoning

Difficulty:

* Apprentice

---

# Attack Scenario

The application generates password reset links using the value from the HTTP Host header.

An attacker can modify the Host header to point to an attacker-controlled domain, causing password reset emails to contain malicious links.

When the victim clicks the link, the password reset token is leaked to the attacker server.

---

# Vulnerable Request

```http
POST /forgot-password HTTP/2
Host: attacker-server.com
Content-Type: application/x-www-form-urlencoded

username=carlos
```

---

# Exploitation Steps

1. Login using:

   * Username: `wiener`
   * Password: `peter`

2. Trigger a password reset for your account.

3. Open the email client on the exploit server.

4. Observe the password reset link containing:

   ```text
   temp-forgot-password-token
   ```

5. Intercept the request in Burp Suite.

6. Send the request to Burp Repeater.

7. Change the `Host` header to:

   ```text
   YOUR-EXPLOIT-SERVER-ID.exploit-server.net
   ```

8. Change the username parameter to:

   ```text
   carlos
   ```

9. Send the request.

10. Open exploit server access logs.

11. Capture Carlos's password reset token.

12. Use the stolen token in the legitimate reset URL.

13. Reset Carlos's password.

14. Login as:

```text
carlos
```

---

# Impact

Successful exploitation can lead to:

* Account takeover
* Password reset token theft
* Unauthorized password changes
* Full user compromise

---

# Technologies Used

* Burp Suite
* HTTP Host Header Manipulation
* Exploit Server
* Password Reset Flow Abuse

---

# Remediation

* Do not trust user-supplied Host headers
* Use hardcoded trusted domains
* Validate Host header values
* Implement secure password reset mechanisms
* Bind reset tokens to intended domains

---

# Educational Purpose Only

This project is created strictly for:

* Ethical hacking practice
* Security research
* Web security learning
* CTF and lab environments

Do NOT test these techniques on unauthorized systems.

---

# Author

Security Research Practice Project
