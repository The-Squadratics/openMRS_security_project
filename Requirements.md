### OpenMRS - A patent-based medical record system


After looking at a number of different OSS projects we decided to assess `OpenMRS` for our semester project. Specifically, the `OpenMRS-core` which is a common platform that is used to build medical data systems.

---

### Identify five essential data flows (source-transformations-sink) through the software. Provide use-cases diagrams related to each of these data flows.

### Clinician - File Upload Data Flow (1 / 5)

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

Since most of the mitigations detailed above are handled outside the system there aren't many links to provide. An example from the [StartupErrorFilter.java](https://github.com/openmrs/openmrs-core/blob/4a0feb8da351088f25fdc4e6d324a1f277aa3410/web/src/main/java/org/openmrs/web/filter/startuperror/StartupErrorFilter.java) file does show the Apache modules that are expected when installing and running the system.

When examining this particular module, Apache does provide [documentation](https://commons.apache.org/proper/commons-fileupload/apidocs/org/apache/commons/fileupload/FileUpload.html) on how it could be used, including mitigations like the ones we outlined above.

---

### Clinic Admin - Database Data Flow (2 / 5)

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

### Front Desk Clerk - Form Data Flow (3 / 5)

#### Use Case

[content here]

#### Misuse Case


#### Use/Misuse Diagram
![Patient Registration Misuse Case](https://user-images.githubusercontent.com/46797572/66089608-ac6f7300-e545-11e9-97d7-c4d5425ac16e.jpeg)
[LucidChart - File Upload](https://www.lucidchart.com/documents/edit/90a38756-7675-49f2-81f1-2f44c61ca1bb/0_0)

#### Security Requirements

---

### Doctor/Nurse - Browser Data Flow (4 / 5)

#### Use Case

User of OpenMRS want to be able to login to the application securely. So, the user not only expects but wants to believe that the website is safe, secured and the patient information is protected. 

Ability to access the patient records for the doctors and other staff through their account has really made easier in these years. If we talk about the past, it was hard for doctors and other staff to view the patient history and conflict might have arrived in scheduling the appointment. Also, the system gives each individual member of the clinic to login their account which has really made easier in this days especially for doctors to see what patient has been going through. But this technology can still pose some challenges from the bad actor who has the wrong intention. 


#### Misuse Case

An attacker who knows that the system will allow to access patient information as well as other medical record could use any mechanism of attack which will allow them grant access to the system.

The use/misuse diagram details the following scenario.
```
Staff needs an authorization to 
 1. Login to the application 
Attacker
 1. Abuses the authentication using authentication abuse 
Staff
 2. Validates password complexity and use at least certain number of characters in the password
Attacker
 2. Inject bad data or use successful experiments to impersonate an authorized user using exploitation of trusted credentials
Staff
 3. Can implement encrypting or signing the season ID which can protect the ID if intercepted 
Attacker 
 3. Impersonate a legitimate user and can get access to the system by abusing an authentication protocol susceptible to reflection attack in order to defeat it.
Staff
 4. Use HMAC to hash the response from the server or introduce a random nonce with each new connection which will ensure that the  attacker cannot employ two connections to attack the authentication protocol
Attacker 
 4. Give Up
```

#### Use/Misuse Diagram
![Capture](https://user-images.githubusercontent.com/41209887/66078918-98694880-e528-11e9-9926-61e213bae0c7.JPG)
[LuciChart - File Upload](https://www.lucidchart.com/documents/edit/de0a5a4b-f9c9-44d2-81bc-b90e4d78e8e4)

#### Security Requirements

The most important requirement for the system is its security. The user of the application wants to login to their system. So they do want their login information be protected and be kept away from the bad actors.

The use as well as misuse cases which are listed above in the document are the common scenario within the system. The login feature for the given application. It does provide the functionality, but this system doesn’t include all the mitigation we listen above in the documentation. It doesn’t have the system of encrypting the session id, use of HMAC to hash response etc. But to some extent it does has the functionality like validating the password complexity and use of the minimum certain character length to the password. Also, most of the mitigations detailed above in the document are handled outside the system there aren’t links to be provided. Moreover, it does have the feature of authentication by checking the existed user in the database system. 

HTTP Apache has provided the module [mod_auth_form](https://httpd.apache.org/docs/2.4/mod/mod_auth_form.html) and has shown the basic example of the configuration. This auth_form also includes the mitigation we have included in the above documents. so this can be the good example for the login form.



### System Admin - Data Flow (5 / 5)

#### Use Case

[content here]

#### Misuse Case

[content here]

---

#### Use/Misuse Diagram
![SystemAdmin Misuse Case](https://user-images.githubusercontent.com/46797572/66096445-98853a80-e560-11e9-9729-5b26675a05e7.jpeg)
[LucidChart - File Upload](https://www.lucidchart.com/documents/edit/879f5a52-9aca-450a-bfda-e4d9656520a1/0_0)

#### Security Requirements

[content here]

---

### Summary of the `OpenMRS` project documentation for security-related configuration and installation issues.

The security-related configuration documentation provided for the OpenMRS project is not centrally located but spread out over numerous documents on the OpenMRS wiki. They do provide an overview of how the system is intended to be [set up and run](https://wiki.openmrs.org/display/docs/Installing+OpenMRS), but since every installation will likely differ, possibly quite dramatically, it's hard to cover all the different situations in the documentation.

The project does provide an installation "wizard" to help folks get the basics installed.  The wiki also has more technical information about to how do a basic installation and some of the issues that folks should be mindful of.

The main issues, as has been mentioned before, often come up in the environment in which the core OpenMRS software is running and not necessarily in the software itself.  The wiki goes into detail about setup of this environment because it encompasses things like the host OS, Java, Apache / Tomcat, MySQL and so on.  These are all important aspects and each has their own potential issues.  The [wiki goes into detail](https://wiki.openmrs.org/display/docs/Printable+Installation+Guide) about what to look out for such as suggestions on software versions to use.

Some examples of other documentation provided by the project are listed below.

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
