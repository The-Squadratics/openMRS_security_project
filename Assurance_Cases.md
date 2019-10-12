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

#### Claim 3 - The file upload functionality is resilient to arbitrary code execution. (Form Data)

#### Claim 4 - OpenMRS is acceptably secure against Authentication Abuse.

#### Claim 5 - System Administration (Module Management)

[Add approved claim here]

### Assurance Cases (Task 2) 
---

#### Case 1 - OpenMRS is resilient to XSS attacks.

![Assurance Case - XSS attack](https://user-images.githubusercontent.com/46797572/66692337-146b3b00-ec63-11e9-8f08-df9f9e72a5ee.jpeg)
[LucidChart - XSS Attack](https://www.lucidchart.com/invitations/accept/40c67994-33ff-42d8-8475-f9519a70bd46)


#### Case 2 - Database Query - Network Eavesdropping

![Network Eavesdropping Diagram](https://github.com/patricklind5ay/hello-world/blob/master/Assurance%20Case%20%233.png?raw=true)
[LucidChart - Network Eavesdropping](https://www.lucidchart.com/invitations/accept/0c5d3797-6286-4e28-aa67-1d86460855ec)

#### Case 3 - File Upload

![File Upload Diagram](https://user-images.githubusercontent.com/5983684/66694151-33bf9380-ec76-11e9-8cee-15833c840b3f.png)
[LucidChart - File Upload(https://www.lucidchart.com/documents/edit/d2f9499d-6957-408f-a73c-93dacae7377b/0_0?shared=true)

#### Case 3 - Form Data

![File Upload Diagram](https://github.com/patricklind5ay/hello-world/blob/master/Assurance%20Case%20%232.jpeg?raw=true)
[LucidChart - File Upload](https://www.lucidchart.com/invitations/accept/0c5d3797-6286-4e28-aa67-1d86460855ec)

#### Case 4 - OpenMRS is acceptably secure against Authentication Abuse.

![Authentication Abuse](https://user-images.githubusercontent.com/41209887/66692768-35ce2600-ec67-11e9-85bd-783e7fe26463.jpeg)
[LucidChart - Authentication - Login](https://www.lucidchart.com/documents/edit/1bc47d78-45fe-470c-a105-662cfba9bac1/0_0)

#### Case 5 - System Administration (Module Management)

[Add case here]

### Alignment of evidence with what the software (OpenMRS) supports (Task 3) 
---

#### Case 1 - File Upload

[Add case here]

#### Case 2 - Database Query - Network Eavesdropping

The first claim to support the Top Claim in this assurance is Claim C2 which claims that OpenMRS uses two-way encryption for security. This claim can be verified from the OpenMRS Wiki (https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-TwoWayEncryption) where it explains the usage of Two-Way encryption in OpenMRS. Following this claim down to C3, it claims that OpenMRS uses modern encryption algorithms. Again, referencing the wiki, we can see that OpenMRS uses the AES encryption standard with Cipher Block Chaining (CBC) with 16 byte random initialization vectors. These are widely accepted secure algorithms in the cybersecurity community. A packet-capture analysis is listed as another form of evidence, but we do not currently have access to such an analysis to provide further proof that the encryption is implemented effectively.
To avoid analysis of encrypted network traffic logging of network traffic would be necessary. It can be verified that OpenMRS offers these features from their documentation on their wiki (https://wiki.openmrs.org/display/docs/Log+Manager+Module, https://wiki.openmrs.org/display/docs/Usage+Statistics+Module). The third claim affirming network security deals with endpoint protection on the client accessing the OpenMRS web application. There is no evidence that can be found dealing with OpenMRS securing endpoints.

The other C2 Claim about OpenMRS is that it only allows pre-approved clients to access the system. No resource can be found that backs up this claim, however, the C3 claim below it can be verified with role-based access controls. OpenMRS claims that it can protect the integrity of specific files using single direction encryption or hash validation (https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-SingleDirectionEncryptionorHashValidation). This article from the wiki would affirm OpenMRS's ability to ensure that there are no unauthorized tampering of access control files by utilizing a SHA-512 + 128 character salt algorithm.


#### Case 3 - Form Data

[Add case here]

#### Case 4 - Login - Authentication Abuse

The first claim to support the Top Claim in this assurance is Claim C2 which claims that OpenMRS has the functionality of validating password complexity. OpenMRS requires the certain character to login to its page. It requires certain number of characters and only the authorized annotation has the ability to add or remove the user and their privileges. This can also be verified using the following page: https://wiki.openmrs.org/display/docs/Access+Control+in+OpenMRS 

The second claim to support the first claim in this assurance is Claim C3 which claims that OpenMRS has the functionality of two way encryption. The following link provides the evidence of this claim. https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-TwoWayEncryption . Referring to this link we can see that OpenMRS utilizes the AES/CBC/PKCS5Padding method for block cipher encryption and decryption. The initialization vector is an array of 16 bytes and will only properly decrypt or encrypt if paired with a specific secret key byte array. This is widely accepted algorithm in cybersecurity community. Furthermore, this documents also provides the proof for the another claim which states that OpenMRS uses hash validation functionality. When the attacker doesn’t possess the shared secret key which is responded by the server. So, the attacker uses the second connection to the server and sends it. This kind of attacks can be mitigated by using hash response from the server. 

The another C2 claim is OpenMRS provides the functionality of single direction encryption. The following link provides the proof for that claim https://wiki.openmrs.org/display/docs/Security+and+Encryption#SecurityandEncryption-SingleDirectionEncryptionorHashValidation . the hashMatches() method provides access to single direction encryption utilities by password validation and checks against both SHA1 and SHA-512 + 128 character salt algorithms. encodeString() method returns the parameter after being encoded using the OpenMRS default encryption which is currently hardcoded to SHA-512.


#### Case 5 - System Administration (Module Management)

[Add case here]


### Retrospective of Past Assignments (Task 4) 
---
In the meeting, each of the team members was asked to come up with at least two assurance claims on which we can have a discussion. We selected seven of them to be approved by the instructor. We discussed what factors should be chosen for coming up with the assurance cases. There was a small debate about if we should consider the individual features and data flow to come up with the assurance cases or keep our software in mind. After the approval of the claims, each of us took one claim each and discussed on the rebuttals and strategies to counter them using claims. There were no major blockers for this task. Once we had a good idea about how to approach each claim, there was no difficulty in coming up with the claims. Also, during the class, we had a good discussion about the evidence for all the claims and no major changes were made. 

### The-Squadratics GitHub
---
[__Team Repository__](https://github.com/The-Squadratics/openMRS_security_project)  
[__Team Project Board__](https://github.com/The-Squadratics/openMRS_security_project/projects/1)
