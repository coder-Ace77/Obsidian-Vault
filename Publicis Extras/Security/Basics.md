
---

#### Input validation issues:

Client server injection - sql injection , 
Cross site scriptiing -  xss -> Attacker injects a script to attacker. Fix -> validation before input. Blacklisting / whitelisting - eg email must have @ , validation must be applied server side.
Spoofing attack: certificates , TLS etc.
Session management issues: Session hjacking - If session generation id is predictable , attacker may guess the next session id -> Always use secure random number genereator. Session creation must be secured and session token must be destroyed after log out.

Error messages given to clients exposing stack trace can expose the system.
Only error exist must be displayed not the internal system info.

Logs: Events must be logged , errors must be logged. Should not be apprearing - Credentials , connection string etc. Provide a set of methods to write to logs. 

Broken access control -> When one gets control of information which it should not.
Injection -> when an application accepts data as input and process it as instrauction. Bad actor can inject some malicious code which can be taken as instruction.

The **OWASP Top 10** is a standard awareness document published by the **Open Worldwide Application Security Project (OWASP)**. It highlights the most critical web application security risks, helping developers and security professionals understand and mitigate common vulnerabilities.

Here are the **OWASP Top 10 (2021 edition)** — the latest as of now:

---

**1. Broken Access Control**  
Improper enforcement of access restrictions allows users to act outside their intended permissions. Examples include accessing unauthorized data, modifying other users' records, or escalating privileges.

**2. Cryptographic Failures**  
Previously called "Sensitive Data Exposure", this refers to failures in protecting data in transit or at rest using proper encryption, such as using weak ciphers, misconfigured SSL/TLS, or not encrypting sensitive information at all.

**3. Injection**  
Occurs when untrusted input is sent to an interpreter (e.g., SQL, OS commands). SQL injection, command injection, and LDAP injection are common types. Attackers can manipulate queries to access or corrupt data.

**4. Insecure Design**  
Refers to flaws in the architecture or design of an application, such as missing security controls or insecure workflows, that cannot be mitigated by simple fixes. It emphasizes the need for secure-by-design principles.

**5. Security Misconfiguration**  
Caused by insecure default settings, open cloud storage, verbose error messages, unnecessary features, or outdated software. It's one of the most common and easily exploitable issues.

**6. Vulnerable and Outdated Components**  
Using libraries, frameworks, or other software modules with known vulnerabilities can expose the entire application to attacks, especially if they’re not kept up to date or patched.

**7. Identification and Authentication Failures**  
Weak authentication mechanisms, like predictable credentials, broken session management, or lack of multi-factor authentication, allow attackers to impersonate users or gain unauthorized access.

**8. Software and Data Integrity Failures**  
Involves issues like relying on untrusted plugins, libraries, or CI/CD pipelines without verifying integrity. An example is failing to validate updates via digital signatures.

**9. Security Logging and Monitoring Failures**  
Without proper logging, monitoring, and alerting, attacks can go undetected, and incident response becomes difficult. This includes missing logs, inadequate alerts, or lack of visibility.

**10. Server-Side Request Forgery (SSRF)**  
Occurs when a server-side application fetches a remote resource based on user input without proper validation. Attackers can exploit SSRF to access internal systems or services.