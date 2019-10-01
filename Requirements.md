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

The use/misuse diagram details the following scenario.

```
Clinic Staff needs the ability to
 1. Uploads Patient Files
Attacker crafts a malicious file to
 1. Upload reverse shell
Clinic Staff
 2. Implements white listing based on file extension
Attacker
 2. Adds duplicate file extension (e.g. file.txt.jpg)
Clinic Staff
 3. Implements file type detector
Attacker
 3. Adds valid file type header before malicious code
Clinic Staff
 4. Removes upload directory execution privileges
Attacker
 4. Gives up (unlikely but still...)
```
![File Upload Diagram](https://user-images.githubusercontent.com/5983684/65918103-604af400-e3c8-11e9-988d-0f867d465b10.png)
[LucidChart - File Upload](https://www.lucidchart.com/invitations/accept/11f8124a-1a0c-45ff-9b48-6b94b72960f6)

#### Security Requirements

Work in progress

---

### Patrick Case - Data Flow (2 / 5)

#### Use Case

<<content here>>

---

### MJ Case - Data Flow (3 / 5)

#### Use Case

<<content here>>

---

### Jeson Case - Data Flow (4 / 5)

#### Use Case

<<content here>>

---

### Group Case - Data Flow (5 / 5)

#### Use Case

<<content here>>

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
