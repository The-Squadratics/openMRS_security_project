### Assurance Cases

----

__Team:__ The Squadratics  
__Team Members:__ Mittranj Pansuriya, Patrick Lindsay, Jeson Rijal, Travis Ingram

### Assignment
---

The team must produce a markdown report that includes the following:

* (__Task 1__) Using security requirements, identify five assurance claims
* (__Task 2__) Prepare a convincing argument in support of the claims. Document this argument using an assurance case for each of the claims.
* (__Task 3__) Assess the alignment of the planned evidence with that available (or can be made available) from the OSS project. Highlight the gaps.
* (__Task 4__) Provide a summary of your team reflection meeting.
  * What issues occurred?
  * What did you plan to change moving forward?
* Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task.

---

|Criteria|Rating|Points|
|---|---|---|
|Quality of Assurance Cases| - | 40 points|
|Breadth and Depth of Assurance Arguments| - | 40 points|
|Project Planning and Coordination| - | 20 points|

[__Assurance Case Exercise__](https://robinagandhi.github.io/swa/slides/lecture-2/assurance-case-exercise.html)

### Assurance Claims (Task 1)
---

#### Claim 1 - OpenMRS is resilient to XSS attacks.

#### Claim 2 - OpenMRS is adequately secure against network eavesdropping.

#### Claim 3 - Form Data

The file upload functionality is resilient to arbitrary code execution.

#### Claim 4 - Login

[Add approved claim here]

#### Claim 5 - System Administration (Module Management)

[Add approved claim here]

### Assurance Cases (Task 2) 
---

#### Case 1 - File Upload

[Add case here]

#### Case 2 - Database Query - Network Eavesdropping

![File Upload Diagram](https://github.com/patricklind5ay/hello-world/blob/master/Assurance%20Case%20%233.png?raw=true)
[LucidChart - File Upload](https://www.lucidchart.com/invitations/accept/0c5d3797-6286-4e28-aa67-1d86460855ec)

#### Case 3 - Form Data

[Add case here]

#### Case 4 - Login

[Add case here]

#### Case 5 - System Administration (Module Management)

[Add case here]

### Alignment of evidence with what the project (OpenMRS) supports (Task 3) 
---

#### Case 1 - File Upload

[Add case here]

#### Case 2 - Database Query - Network Eavesdropping

The first claim to support the Top Claim in this assurance is Claim C2 which claims that OpenMRS uses two-way encryption for security. This claim can be verified from the OpenMRS Wiki (https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-TwoWayEncryption) where it explains the usage of Two-Way encryption in OpenMRS. Following this claim down to C3, it claims that OpenMRS uses modern encryption algorithms. Again, referencing the wiki, we can see that OpenMRS uses the AES encryption standard with Cipher Block Chaining (CBC) with 16 byte random initialization vectors. These are widely accepted secure algorithms in the cybersecurity community. A packet-capture analysis is listed as another form of evidence, but we do not currently have access to such an analysis to provide further proof that the encryption is implemented effectively.
To avoid analysis of encrypted network traffic logging of network traffic would be necessary. It can be verified that OpenMRS offers these features from their documentation on their wiki (https://wiki.openmrs.org/display/docs/Log+Manager+Module, https://wiki.openmrs.org/display/docs/Usage+Statistics+Module). The third claim affirming network security deals with endpoint protection on the client accessing the OpenMRS web application. There is no evidence that can be found dealing with OpenMRS securing endpoints.

The other C2 Claim about OpenMRS is that it only allows pre-approved clients to access the system. No resource can be found that backs up this claim, however, the C3 claim below it can be verified with role-based access controls. OpenMRS claims that it can protect the integrity of specific files using single direction encryption or hash validation (https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-SingleDirectionEncryptionorHashValidation). This article from the wiki would affirm OpenMRS's ability to ensure that there are no unauthorized tampering of access control files by utilizing a SHA-512 + 128 character salt algorithm.


#### Case 3 - Form Data

[Add case here]

#### Case 4 - Login

[Add case here]

#### Case 5 - System Administration (Module Management)

[Add case here]


### Retrospective of Past Assignments (Task 4) 
---

Summary of team reflection / retrospective meeting
 * Issues
 * Planned changes

### The-Squadratics GitHub
---
[__Team Repository__](https://github.com/The-Squadratics/openMRS_security_project)  
[__Team Project Board__](https://github.com/The-Squadratics/openMRS_security_project/projects/1)
