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

The OpenMRS core is written in Java.  The system itself has many components and is modular in the sense that it allows plug-ins to be written and used for functionality that might not be incorporated in the core or that doesn't cover a specific use case.  These plug-ins are could potentially be written in another language but would still need to interact with the core API which is, again, based on Java and uses the Spring framework.  The [developer guide](https://wiki.openmrs.org/display/docs/Developer+Guide) the project hosts recommends using Eclipse and Maven when writing plug-ins and has suggestions and guides to help folks get started.

Given the size and scope of this project a full manual review isn't feasible.  Our initial strategy will focus on using an automated tool to conduct the bulk of the code analysis.  There are a couple specific parts of the system that we have reviewed for other steps in this project, notably the `xxx` and `xxx`.  Those team members familiar with Java will spend some time manually reviewing those specific aspects and report back on what, if anything, they found.

We spent time researching the analysis tools available for Java and found many options.  Most of them are commercial packages, though, which put them out of reach.  One package that looked promising was by [SonarQube](https://www.sonarqube.org).  They offer both a commercial package but also have an open source (`Community`) version that should meet our need.  So for the initial testing we've chosen to use that package for our code analysis.  If it doesn't work or the reported findings seem lacking we will try another option such as [FindBugs](https://github.com/findbugsproject/findbugs) or [PMD](https://pmd.github.io).


### Code Analysis for SSE - Findings from Manual Code Review (Task 2) 
---

[We need to add the findings from the manual code review here.]


### Code Analysis for SSE - Findings from Automated Code Scanning (Task 3) 
---

### Automated Testing Findings

#### SonarQube - Overview

[SonarQube](https://www.sonarqube.org) is an automated code analysis tool intended to be used as part of the software development pipeline, typically in conjunction with continuous integration.  When first run it scans the codebase and provides the development team a wealth of information about the reliability, maintainability, security, and test coverage of the project.  It also provides a toolset for managing and tracking issues from inception to resolution.

The tool is comprised of a scanner that is installed and integrated into the build environment (through Maven, Jenkins, Gradle, or another tool) which communicates and feeds information to a server, database, and web frontend.  All information and tracking is done through the website.  This basic functionality is available through the `Community` edition while added features and options are commercially available via plug-ins.

#### SonarQube - Setup / Initial Scan

Getting SonarQube set up was a non-trivial task.  The documentation seems to assume that potential users will be well seasoned developers with experience in continuous integration workflows.  We managed to get things up and running but the documentation leaves something to be desired.

Granted, some of the issues we ran into were due to our project and not because of SQ.  For example, in order to set up and build `openMRS`, we needed to have the Java 8 development kit installed.  But the SQ server requires Java 11 or later.  So juggling two different installations of Java to build and run different programs was challenging.

Once we managed to build `openMRS` the SQ scan was relatively easy.  There were some options that needed to be added to the Maven config file but that was about it.  The scanner found our server / database okay and once completed we were able to access the web interface with all the findings.

Ideally we'd be able to simply provide a public link to the results of our automated analysis.  Unfortunately getting all this set up and built on an external server would present too many challenges.  As a result we've taken screen shots of the relevant and representative portions of the web interface and presented them below with comments.  We'd be happy to provide additional information if necessary.

#### SonarQube Findings

As mentioned above, SQ presents a wealth of information about the code base. The basic categories they provide are broken down below.

* **Bugs**
  * Code that is demonstrably wrong or likely to yield unexpected behavior
* **Vulnerabilities**
  * Code issues that can or could be exploited by bad actors
* **Security Hotspots**
  * Security-sensitive code that requires manual review to assess whether a vulnerability exists
* **Code Smells**
  * Code that could confuse maintainers or give them pause.

![SQ_About](https://user-images.githubusercontent.com/5983684/69763286-53315380-1132-11ea-81ab-303085b7ef79.PNG)

----

In addition to the `type` of issue SQ also provides a [hierarchy of severity](https://docs.sonarqube.org/latest/user-guide/issues/) when it comes to problems it finds.  The severity scale is broken down below.

* **Blocker**
  * A bug that has a high probability of impacting the behavior of the application and is in need of immediate attention.  This could include a memory leak or an unclosed database connection.
* **Critical**
  * A bug with a low probability of impacting the application or an issue related to a specific security flaw.  Examples include empty catch block or SQL injection.
  * These are items that should be reviewed as soon as possible
* **Major**
  * These are quality flaws which could highly impact developer productive such as unused parameters, duplicate code, or blocks without test coverage.
* **Minor**
  * These are quality flaws that could slightly impact developer productivity and are often thought of as code consistency / convention.
* **Info**
  * Neither a bug nor a quality flaw, just findings about the codebase.

----
Here are some of the raw numbers the scan provided.

* **Lines of Code**
  * **~75K**
* **Reliability**
  * **150 Bugs**
* **Security**
  * **123 Vulnerabilities**
  * **54 Security Hotspots**
* **Maintainability**
  * **90 Days of Technical Debt**
  * **4.3K Lines of Code (Code Smells)**
* **Test Coverage**
  * **56.5%**
  * **4.1K Unit Tests**
* **Duplications**
  * **2.7% Code Duplication**
  * **197 Duplicate Code Blocks**

![SQ_overview](https://user-images.githubusercontent.com/5983684/69763291-59273480-1132-11ea-816c-49daa8e128bb.PNG)

----

#### Specific Security Issues

There were numerous issues found by the automated scan, as evidenced by the numbers presented above.  A more detailed description of the issues can be found below.

The issues identified can be broken down into the following severity categories.

* **Blocker 204**
* **Critical 580**
* **Major 1.3K**
* **Minor 2.3k**
* **Info 171**

These issues are further categorized within specific areas.  For example, SQ is able to track and map types of vulnerabilities back to specific CWEs, SANS Top 25, and the OWASP Top 10 among others.


[Additional issues will be added here along with the associated screenshots]


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
