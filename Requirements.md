### OpenMRS - A patent-based medical record system


After looking at a number of different OSS projects we decided to assess `OpenMRS` for our semester project. Specifically, the `OpenMRS-core` which is a common platform that is used to build medical data systems.

---

### Identify five essential data flows (source-transformations-sink) through the software. Provide use-cases diagrams related to each of these data flows.

### File Upload - Data Flow (1 / 5)

#### Use Case

Users of OpenMRS want to be able to access patient information and add additional records easily and securely. There is not only an expectation that the files uploaded will be safe but a regulatory requirement that the information be protected.

One of the stated benefits of medical record systems is the portability of patient data.  In the past, medical records were often cumbersome to maintain and difficult to share between doctors and clinics.  Moving to a system that allows for quick access and easier sharing is certainly helpful.  But being able to move records from one system to another can still pose challenges.  Especially since allowing uploading of data into the system can expose it to bad actors with malicious intent.

#### Misuse Case

An attacker that knows the system is able to accept uploaded files could craft an attack that will grant them access to the system as a whole, potentially exposing not only patient medical data but possibly billing, insurance, and other financial information.

Given our scenario, a likely attack could originate from within the clinic itself.  In this case we have identified Doug, a disgruntled system admin.  Doug is dissatisfied with their salary and has decided to exfiltrate sensitive patient information for personal gain.

The use/misuse diagram details the following scenario.

```
The system enables
 1. Upload Patient Files
Doug crafts a malicious file to
 1. Upload reverse shell
The system should be able to
 2. Whitelist files based on the file extension
Doug
 2. Adds duplicate file extension (file.txt.jpg)
To mitigate attacks contained in specific file types
 3. File type detector
Doug
 3. Adds valid file type header before malicious code
The system
 4. Upload directory has no execution privileges
Attacker
 4. Gives up (unlikely but still...)
```

#### Use/Misuse Diagram
![File Upload Diagram](https://user-images.githubusercontent.com/5983684/66074945-f9554880-e549-11e9-975b-b7c1c1ed6dad.png)
[LucidChart - File Upload](https://www.lucidchart.com/invitations/accept/11f8124a-1a0c-45ff-9b48-6b94b72960f6)

#### Security Requirements

Clinicians and other users of the system have to be able to add new information, whether that's patient records or other clinic data.  They have an expectation that this functionality is safe and doesn't enable the system to be compromised by bad actors.

The use and misuse case detailed above documents a common scenario within the clinic.  The uploading of new data into the system.  The system provides this functionality but doesn't incorporate all of the potential mitigations we listed.  It does limit the types of files able to uploaded to `.txt` files but that appears to be it.

Instead, given the modular nature of the software, any remaining mitigations are expected to be handled by other systems.  In this case, the server side software, Apache. The `FileUpload` module does have options related to whitelisting and if properly updated, shouldn't execute files with double extensions.  Setting up and defining the privilege of specific directories on the server is also outside the scope of the core software.

---

### Patrick Case - Data Flow (2 / 5)

#### Use Case


#### Misuse Case


```
Clinic Staff needs the ability to

```

#### Use/Misuse Diagram
![File Upload Diagram](https://github.com/patricklind5ay/hello-world/blob/master/ReportGenerationMisuseCaseDiagram.PNG?raw=true)
[LucidChart - File Upload](https://www.lucidchart.com/invitations/accept/4e36ef7b-1742-4650-87f3-20a76443e20f)

#### Security Requirements

Work in progress

---

### MJ Case - Data Flow (3 / 5)

#### Use Case

[content here]

---

### Jeson Case - Data Flow (4 / 5)

#### Use Case

[content here]

---

### Group Case - Data Flow (5 / 5)

#### Use Case

[content here]

---

### Derive security requirements for each of the use cases using misuse case diagrams. 

---

### Assess the alignment of security requirements with advertised features of the software.  Incorporate project documentation and observations about the codebase as evidence to support the conclusions reached.

---

### Provide a summary of the `OpenMRS` project documentation for security-related configuration and installation issues.

The security-related configuration documentation provided for the OpenMRS project is not centrally located but spread out over numerous documents on the OpenMRS wiki.

The project does provide...

Some examples of the documentation provided are listed below.

* [Technical Overview](https://wiki.openmrs.org/display/docs/Technical+Overview)

* [Data Management](https://wiki.openmrs.org/display/docs/How+to+Delete+or+Erase+All+Patients+and+Patient+Data)

* [Data Model](https://wiki.openmrs.org/display/docs/Data+Model)

* [Security and Encryption](https://wiki.openmrs.org/display/docs/Security+and+Encryption)

* Controlling User Access (Roles and Privileges)
  * All done under [`Manage Users`](https://wiki.openmrs.org/pages/viewpage.action?pageId=3346872)

* [Application Configuration](https://wiki.openmrs.org/display/docs/Application+Configuration)

* [Overriding OpenMRS Default Properties](https://wiki.openmrs.org/display/docs/Overriding+OpenMRS+Default+Runtime+Properties)

* [Monitoring OpenMRS Implementation](https://wiki.openmrs.org/display/docs/Monitoring+Your+OpenMRS+Implementations+to+Ensure+It%27s+Running)

* [Configuring User Password Strength](https://wiki.openmrs.org/display/docs/Configuring+User+Password+Strength)
---

### GitHub Repository

The GitHub repository can be [found here](https://github.com/The-Squadratics/openMRS_security_project).

---

### GitHub Project Board

The project board can be [found here](https://github.com/The-Squadratics/openMRS_security_project/projects/1).
