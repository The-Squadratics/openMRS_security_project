### Code Analysis for Software Security Engineering
----

__Team:__ The Squadratics  
__Team Members:__ Mittranj Pansuriya, Patrick Lindsay, Jeson Rijal, Travis Ingram

### Assignment
---

The team must produce a markdown report that includes the following:

* (__Task 1__) A short summary of your code review strategy.
  * What challenges did you anticipate and how did your code review strategy attempt to address those challenges?
* (__Task 2__) Findings from manual code review of critical security functions identified in misuse cases, assurance cases and threat models.
* (__Task 3__) Findings from automated code scanning (if available). Include links to full reports.
* (__Task 4__) Summary of key findings from manual and/or automated scanning.
  * This summary may include categorization, mappings to CWEs, CAPECs, Risk Levels, etc.
* (__Task 5__) Links to any pull requests, issues, discussion, etc. from the team to the original project and any follow-up interactions.
* (__Task 6__) Provide a summary of your team reflection meeting.
  * What issues occurred?
  * What did you plan to change moving forward?
* Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task.


### Code Analysis for SSE - Code Review Strategy (Task 1)
---

The OpenMRS core is written in Java.  The system itself has many components and is modular in the sense that it allows plug-ins to be written and used for functionality that might not be incorporated in the core or that doesn't cover a specific use case.  These plug-ins are could potentially be written in another language but would still need to interact with the core API which is, again, based on Java and uses Spring framework.  The [developer guide](https://wiki.openmrs.org/display/docs/Developer+Guide) the project hosts recommends using Eclipse and Maven when writing plug-ins and has suggestions and guides to help folks get started.

Given the size and scope of this project a full manual review isn't feasible.  Our initial strategy will focus on using an automated tool to conduct the bulk of the code analysis.  There are a couple specific parts of the system that we have reviewed for other steps in this project, notably the `xxx` and `xxx`.  Those team members familiar with Java will spend some time manually reviewing those specific aspects and report back on what, if anything, they found.

We spent time researching the analysis tools available for Java and found many options.  Most of them are commercial packages, though, which put them out of reach.  One package that looked promising, though, was by [SonarQube](https://www.sonarqube.org).  They offer both a commercial package but also have an open source version that should meet our need.  So for the initially testing we've chosen to use that package for our code analysis.  If it doesn't work or the reported findings seem lacking we will try another option such as [FindBugs](https://github.com/findbugsproject/findbugs) or [PMD](https://pmd.github.io).


### Code Analysis for SSE - Findings from Manual Code Review (Task 2) 
---

[We need to add the findings from the manual code review here.]


### Code Analysis for SSE - Findings from Automated Code Scanning (Task 3) 
---

[We need to add the findings from the automated code review here, including links to the report or output of the tool.]

### Code Analysis for SSE - Summary of Key Findings from the Code Reviews (Task 4) 
---

[We need to add a summary of the key findings from the various code reviews here, including links and mappings to CWEs, CAPECs and so on.]

### Code Analysis for SSE - Documentation of any contact had with the OSS project (Task 5) 
---

[We need to add documentation of any contact (pull requests, issues, discussion) had with the OpenMRS project.]


### Team Retrospective (Task 6)
---

[We need to add a summary of our team retrospective here.]

### Rubric

---

|Criteria|Rating|Points|
|---|---|---|
|__Code Review Strategy__| - | ?? points|
|__Findings from Manual Code Review__| - | ?? points|
|__Findings from Automated Code Review__| - | ?? points |
|__Summary of Key Findings (CWE Mappings, Risk Levels,...__| - | ?? points |
|__OSS Project Pull Requests, Issues, Discussions__| - | ?? points |
|__Team Collaboration__| - | ?? points|


### The-Squadratics GitHub
---
[__Team Repository__](https://github.com/The-Squadratics/openMRS_security_project)  
[__Team Project Board__](https://github.com/The-Squadratics/openMRS_security_project/projects/1)
