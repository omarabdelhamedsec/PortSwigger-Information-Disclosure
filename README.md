# 🔍 Information Disclosure Labs - PortSwigger Web Security Academy

**Platform:** PortSwigger Web Security Academy  
**Category:** Information Disclosure  
**Status:** All 5 Labs Solved ✅  

---

## 📸 Proof of Completion

![All Labs Solved Status](Screenshot%202026-08-18%20175353.png)

---

## 📋 Labs Summary & Walkthroughs

---

### 1. Information Disclosure in Error Messages
* **Level:** Apprentice
* **Concept:** Verbose error messages leaking sensitive stack traces or framework details.

#### Steps to Solve:
1. Browse to any product page (e.g., `/product?productId=1`).
2. Change the parameter to an invalid data type (e.g., `/product?productId=invalid_string` or a single quote `'`).
3. Send the request and observe the error message response.
4. Locate the leak showing the specific Apache Struts / framework version numbers.
5. Submit the exposed framework version number to solve the lab.

---

### 2. Information Disclosure on Debug Page
* **Level:** Apprentice
* **Concept:** Sensitive information exposed via publicly accessible debug / info pages.

#### Steps to Solve:
1. Open the main page and view the HTML source code or check Burp HTTP History.
2. Search for comments or links pointing to debug endpoints (e.g., `/cgi-bin/phpinfo.php` or `phpinfo`).
3. Navigate to the exposed debug page URL.
4. Search for the `SECRET_KEY` or environment variables within the page output.
5. Submit the revealed key to solve the lab.

---

### 3. Source Code Disclosure via Backup Files
* **Level:** Apprentice
* **Concept:** Developers leaving source code backup files (`.bak`, `~`, `.old`) exposed in public web directories.

#### Steps to Solve:
1. Inspect the `/robots.txt` or common endpoints to find backup directory references.
2. Locate the backup file endpoint (e.g., `/backup/ProductTemplate.java.bak`).
3. Open or download the backup file.
4. Read the source code to find hardcoded database credentials/passwords.
5. Submit the discovered password to solve the lab.

---

### 4. Authentication Bypass via Information Disclosure
* **Level:** Apprentice
* **Concept:** Administrative custom headers or hidden endpoints exposed in internal requests/responses.

#### Steps to Solve:
1. Access the `/admin` page and observe the response (Access Denied).
2. Inspect HTTP responses or trace headers via Burp Suite.
3. Identify custom headers like `X-Custom-IP-Authorization: 127.0.0.1` or `TRACE` verb response exposing internal headers.
4. Add the missing header into your request to `/admin`.
5. Access the Admin panel and delete user `carlos` to solve the lab.

---

### 5. Information Disclosure in Version Control History (Git)
* **Level:** Practitioner
* **Concept:** Sensitive data exposed via historical commits in publicly exposed `.git` repositories.

#### Steps to Solve:
1. Verify exposed Git directory at `/.git/`.


2. Download the `.git` directory locally:
   ```bash
   wget -r -np -R "index.html*" https://<LAB-ID>.web-security-academy.net/.git/
