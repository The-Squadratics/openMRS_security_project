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

### Tampering

### Repudiation

### Information Disclosure

### Denial of Service

### Elevation of Privilege


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
