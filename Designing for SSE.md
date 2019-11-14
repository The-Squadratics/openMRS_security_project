### Designing for Software Security Engineering

----

__Team:__ The Squadratics  
__Team Members:__ Mittranj Pansuriya, Patrick Lindsay, Jeson Rijal, Travis Ingram

### Assignment
---

The team must produce a markdown report that includes the following:

* (__Task 1__) Develop threat models for critical data-flows through the software.
  * Misuse and assurance cases will provide starting points for examination.
  * Include threat model diagrams and threat analysis.
    * Level 0 Diagrams for each use case
    * Consolidate and present DFDs for remaining cases
* (__Task 2__) Using threat model analysis, review OSS project for design related issues. Summarize your observations.
* (__Task 3__) Provide a summary of your team reflection meeting.
  * What issues occurred?
  * What did you plan to change moving forward?
* Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task.

### Designing for SSE - Threat Models (Task 1)
---

#### Level 0 Data Flow Diagrams
 
 Here are the Level 0 Data Flow Diagrams for the use cases we developed in previous assignments.
 
 * File Upload - Level 0 DFD
 ![Level 0 File Upload](https://user-images.githubusercontent.com/46797572/68782284-c13c2d80-05fe-11ea-8868-19ca29a46577.JPG) 
 
 * Module Update - Level 0 DFD
 ![Level 0 Module Update](https://user-images.githubusercontent.com/46797572/68782282-c0a39700-05fe-11ea-88b4-93edd0f9c13a.JPG)

 * Form Data - Level 0 DFD
 ![Level 0 Form Data](https://user-images.githubusercontent.com/46797572/68782286-c13c2d80-05fe-11ea-9e4a-6149d0cdc2d9.JPG)

 * Login by the user - Level 0 DFD
 ![Level 0 Login](https://user-images.githubusercontent.com/46797572/68782287-c13c2d80-05fe-11ea-9f7f-6d0e2687fb60.JPG)
 
 * Server Query - Level 0 DFD
 ![Level 0 Server Query](https://user-images.githubusercontent.com/46797572/68782283-c13c2d80-05fe-11ea-8ca2-94e76c8e0ad7.JPG)


#### Consolidate Data Flow 1 - [User Input via Form Data]
 * Threat Model Diagram 
 ![Level 1 Threat Model](https://user-images.githubusercontent.com/46797572/68784063-97d0d100-0601-11ea-98f7-01593ab82be9.JPG)

 * Threat Model Analysis
 [Threat Modeling Report.pdf](https://github.com/The-Squadratics/openMRS_security_project/files/3842984/Threat.Modeling.Report.pdf)

### Designing for SSE - OpenMRS Review / Observations / Summary (Task 2) 

---
The summary of our observations are documented below.  We used STRIDE as a means of categorizing the threats and possible mitigations. The information was taken from project documentation found on the [OpenMRS Wiki](https://wiki.openmrs.org) as well as the [codebase itself](https://github.com/openmrs/openmrs-core).

### Spoofing

Spoofing mitigations involve strong authentication mechanisms, including complex password requirements, multi-factor authentication, re-authentication for sensitive actions, requiring HTTPS, and slow password hashes.

A secure implementation of a medical record system would enforce strong password complexity requirements through the banning of common passwords and requiring long, alphanumeric passwords. Requiring a secure web transfer protocol like HTTPS should be a minimum as well. For added security, requiring multi-factor authentication as well as re-authentication when performing susceptible activities such as password changes are helpful.

OpenMRS allows different configurations for password requirements, leaving the specific parameters open to the administrators to dictate. It uses secret questions set up by users for password resets. OpenMRS works with Apache Tomcat and has configurations laid out that necessitate making sure "all Tomcat applications require HTTPS to operate." OpenMRS does support use of third party authentication mechanisms, which is the only way to implement a multi-factor authentication approach. OpenMRS does not require re-authentication for sensitive administrator level changes.

### Tampering

Mitigations for tampering most commonly include the santization of input data and authorization mechanisms.

A secure OpenMRS program should have input validation involving datatypes, length (null terminators), character types, and format using an approved list validation approach.

OpenMRS contains a Validator Module that sanitizes the input by referring to a concept dictionary with pre-approved parameters for each concept (object or field). Additionally, OpenMRS utilizes role-based and location-based access control with flags denoting required privilege levels for each module.

### Repudiation

Standard mitigation strategies for Repudiation typically include the following;
* Return of last modified date for all the file passing through the servlet.

OpenMRS has the feature of returning the last modified date which includes the time and date of every file which are passed through the jsp (.withjstl) servlet. This feature helps keep track of every file passing through the jsp servlet.

### Information Disclosure

Standard mitigation strategies for information disclosure type threats typically include the use of data encryption that makes use of established standards and follows industry best practices for key management.

Interactions between the front end `client` and the OpenMRS backend are handled by an API written in Java.  In our scenario, the system is set up and used on an intranet and so data isn't flowing back and forth on the open internet.

Still, the API is written in such a way that any requests and associated responses are still processed using HTTPS and TLS to ensure communications are kept reasonably secure.

### Denial of Service

Standard mitigation strategies for this category of threat typically include the following;
* The use of firewall rules and other network protections to ensure attacks aren't able to reduce the availability of the system.
* The use of disk and processor quotas to prevent excessive use of system resources by rogue processes or network attacks.
* Making Http request and taking encrypted username and password as a parameter and allowing log sleeping for 3 seconds incase of bad     username or password

Given that this system and its associated processes are deployed internally and not exposed to external networks or the internet at large, this category of threat is not something the system protects against.

Network protections like those detailed above would be implemented by the clinic system administrators when planning out and setting up a given installation of OpenMRS. OpenMRS has the feature of encription username and password and also allows the logging sleep for 3 second feature in case of bad username and password.

### Elevation of Privilege

Standard mitigation strategies for Elevation of Privilege type threats typically include the following;
* Input validation
* Access control lists, Roles, and Groups
* Ensuring the least amount of access and information is available for given users or system / process actions
* Use of installization script from absolute path

In the context of OpenMRS, there are two different type of privilege elevation, those done within the system and those within the machine the system is running on. For OpenMRS, the application itself and associated processes do not need to be run with admin privileges so we do not concern ourselves with that aspect.

No single instance of OpenMRS will be set up exactly the same.  Still, the system has implemented robust [access controls](https://wiki.openmrs.org/display/docs/Access+Control+in+OpenMRS) that allow administrators to set and monitor how the users of the system interact with it and what data they can view and modify.

These access controls are [implemented](https://wiki.openmrs.org/display/docs/Privilege+Checking+for+Access+Control+in+OpenMRS) in such a way that data requests that are initiated from the web front-end make use of specific services (AuthorizationAdvice) that will make additional calls depending on the request and perform checks using the `hasPrivilege()` methods available in most classes.
Only after running through the various Context / User / Role checks will the data be made available.  If the user does not have access, then access will be denied. OpenMRS loads the input file using 'file.getAbsolutePath()' which installizes scripts from absolute path once the username and password are authenticated by the OpenMRS. 

In this way OpenMRS is able to mitigate threats of privilege escalation within processes and data requests that occur.


### Team Retrospective (Task 3)
---

Even though we've managed to complete each assignment our group continues to struggle a little with regards to task distribution, communication, and follow through.  For this assignment we did meet twice and spent time working through and discussing the relevant threats and producing the initial Data-Flow Diagrams.

These meetings went okay and were helpful for everyone. One of the problems we kept running into was how to interrupt the assignment instructions and what was expected of us.

For the final assignment and the presentation we are going to try and be better about defining tasks, communicating any issues or problems we individually encounter, asking for help when needed, and following through.

### Rubric

---

|Criteria|Rating|Points|
|---|---|---|
|__Quality of Threat Models__
Proper wording of model elements
Clean, coherent, and valid DFD diagram| - | 30 points|
|__Mitigation Quality__
Quality of analysis to mitigate threats| - | 20 points|
|__Quality of Observations__
Observations from OSS project align with the high-priority threats identified from the DFD diagram analysis | - | 30 points |
|__Project Planning and Coordination__| - | 20 points|

[__Threat Modeling Assignment__](https://robinagandhi.github.io/swa/slides/lecture-4/design-for-software-se.html#66)

### The-Squadratics GitHub
---
[__Team Repository__](https://github.com/The-Squadratics/openMRS_security_project)  
[__Team Project Board__](https://github.com/The-Squadratics/openMRS_security_project/projects/1)
