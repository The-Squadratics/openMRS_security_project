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

#### SonarCloud

When our initial automated analysis was run we were unaware of [SonarCloud](https://sonarcloud.io/about).  We've since gone back and checked and the `openMRS` codebase was scanned last year and the output / findings are similar to our own.

That scan can be [found here](https://sonarcloud.io/dashboard?id=OMC).

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

#### Additional Findings

As mentioned above, SQ breaks down issues it finds into specific categories. The totals for the project as a whole are listed below, followed by a more specific classification.

The issues identified are broken down based on the categories mentioned above.

* **Blocker 204**
* **Critical 580**
* **Major 1.3K**
* **Minor 2.3k**
* **Info 171**

----

When looking at the `Bugs` section the tool will display the a list of what it found.  The interface presents the bug and where it is within the codebase along with additional details about when it was introduced and an estimation on how long it might take to fix.  Each one is also classified based on the definitions above.

The breakdown for the 150 bugs it found are listed below.

* **Blocker 44**
* **Critical 9**
* **Major 81**
* **Minor 16**
* **Info 0**

![SQ_Issues_Bugs_Overview](https://user-images.githubusercontent.com/5983684/69997180-2f4a8500-1519-11ea-8f69-cfc6ce4a4d76.PNG)

Moreover, when looking at the specific file ModuleResourcesServlet.java in the web module we found 67 issues which directly affects the file upload. One of the major issue that implied here was nullable moduleId. Furtherover, if we look at the bugs in the web module two major bugs were encountered

![sonarcube1](https://user-images.githubusercontent.com/41209887/70352387-a9884b80-1830-11ea-9cb1-a53e8bec27fa.JPG)

----

The `Vulnerability` section follows the same layout as the `bugs` section.  Each issue is listed with links to the specific location within the codebase as well as other details.  The tool breaks down the issues into the following severity categories.

* **Blocker 22**
* **Critical 4**
* **Major 0**
* **Minor 97**
* **Info 0**

![issues_vulnerabilities](https://user-images.githubusercontent.com/5983684/69997296-6d47a900-1519-11ea-9f14-34c604e51dc1.PNG)

Here, looking at the web module of the OpenMRS, we can see three Vulnerability. Out of which two are the minor vulnerability where as one is the major vulnerability encountered. 

![sonarcube5](https://user-images.githubusercontent.com/41209887/70352962-ee60b200-1831-11ea-8461-fba7a11efd5f.JPG)

----

These issues are further categorized within specific areas or `Security Hotspots`.  For example, SQ is able to track and map types of vulnerabilities back to specific CWEs, SANS Top 25, and the OWASP Top 10 among others.  It uses its own classification to distinguish problems related to Authentication or weak cryptography or cross-site scripting.

![SQ_Measures_SecHotspot_Overview](https://user-images.githubusercontent.com/5983684/69997218-438e8200-1519-11ea-9719-821d7222c3ed.PNG)

if we look at the specific file in OpenMRS i.e. openmrs/web/filter, we can see one security hotspot issue in the file StartupFilter.java

![sonarcube6](https://user-images.githubusercontent.com/41209887/70353470-0a188800-1833-11ea-8178-2537a4eafd18.JPG)

----

There are additional areas that SQ examines in addition to bugs or vulnerabilities. It also looks at the maintainability, test coverage and code duplication.  While these areas might not directly cause the application to crash or expose it to compromise, they are still very important metrics that have a large effect on how the application preforms and the ability for developers to work within it.

SQ assigns a time-to-fix value for each identified issue.  The total of these is listed as `Technical Debt`.  For openMRS, the total is roughly 90 days.  Which isn't ideal but still classified as an `A` by SQ.

The total text coverage available with this project is currently sitting at roughly `56.5%` with a total of `4.1K` unit tests.

![SQ_Measures_Debt-Coverage_Overview](https://user-images.githubusercontent.com/5983684/69997237-4c7f5380-1519-11ea-859a-c08df00ed32c.PNG)

----

The code duplication was at `2.7%` with only `197` duplicate blocks. We're not sure how to conceptualize this but that seems like a small number given the overall size of the codebase.

![SQ_Measures_Dupe_Overview](https://user-images.githubusercontent.com/5983684/69997251-5608bb80-1519-11ea-88d7-dbd7b3c92d73.PNG)

----

Overall `SonarQube` appears to be a valuable resource for most any development team.  It provides a wealth of information about the codebase, straightforward ways to classify and view that information, as well as tools for managing and iterating on the fixes necessary to improve it.


### Code Analysis for SSE - Summary of Key Findings from the Code Reviews (Task 4) 
---

#### Automated Code Analysis - Summary

Analyzing a large code base such as `openMRS` is challenging.  It's nearly impossible to do so manually which is where automated tools like `SonarQube` come into play.  It enables development teams to define the rules and heuristics they want to use to determine overall code quality and can then integrate a tool like SQ into the pipeline and use it to manage any issues that crop up.

Our analysis has shown that in general, `openMRS` doesn't suffer from any glaring issues based on the default rules and settings used during our scan.  It `Passed` for what that's worth.  As mentioned in the findings section, though, there are a number of **Bugs** and potential **Vulnerabilities** that need to be reviewed and addressed.

Many of the main `Blockers` that were identified by SQ relate to potential DoS attacks.  These can be mapped back to [CWE-459 - Incomplete Cleanup](https://cwe.mitre.org/data/definitions/459.html) as well as [CWE-609 - Double-Checked Locking](https://cwe.mitre.org/data/definitions/609.html).  The first has to do with the use of _Stream Resources_ and temporary files creation.  Failing to close connections could lead to these files growing larger than the space allocated for them, causing a Denial of Service.

![SQ_Issues_CWE459](https://user-images.githubusercontent.com/5983684/70299066-6ccd3d80-17b9-11ea-928e-fee51eccd32f.PNG)

These appear to be legitimate issues and something that should be investigated by the development team further.  What's especially concerning is the age of these specific items.  Many of them have been in the codebase for 6, 8, or even 12 years.  This is another area that we might well communicate back to the `openMRS` community.

Looking at the two major bugs found in the web module, the first one has to do with the catch statement on java exception of try and catch. Whereas other major bug has to do with the date formating which is nullable in the page WebUtil.java

![sonarcube5](https://user-images.githubusercontent.com/41209887/70354702-ec005700-1835-11ea-9fc9-50eef5c30405.JPG)

----

It's also worth pointing out that automated tools aren't to be trusted explicitly.  They are simply parsing the codebase and applying a rule set as best it can.  And the documentation for SQ is clear when pointing this out.  They reiterate that many types of items flagged should be manually reviewed to verify an issue actually exists.

![SQ_Issues_CWE-259](https://user-images.githubusercontent.com/5983684/70298861-bf5a2a00-17b8-11ea-9dcf-a82afb929e80.PNG)

Examples of this are instances where sections of code were flagged with _Authentication_ issues and tagged referencing [CWE-259 - Hard-coded Passwords](https://cwe.mitre.org/data/definitions/259.html).  In reviewing these sections we found that there were no actual credentials used but that a variable name simple contained the word, password.

`public static final string GP_PASSWORD_CUSTOM_REGEX = "security.passwordCustomRegex";`

There are undoubtedly many instances of this throughout the codebase but, again, when used properly the tool is doing its job calling out potential issues for developers to actually check.

----

SonarQube provides standards information about all the issues it finds. It will tag issues with keywords such as CWE,CERT, OWASP, SANS or use its own classification.  This has the potential to help out the development team quite a bit when it comes time to research and correct issues and bugs.

The following were the most reported CWEs based on the automated analysis.

![SQ_Issues_CWE-493](https://user-images.githubusercontent.com/5983684/70298868-c5500b00-17b8-11ea-95f1-6bbb9f50f88f.PNG)

* [CWE-493 - Critical Public Variable Without FINAL Modifier](https://cwe.mitre.org/data/definitions/493.html)
* [CWE-409 - Improper Handling of Highly Compressed Data](https://cwe.mitre.org/data/definitions/409.html)
* [CWE-326 - Inadequate Encryption Strength](https://cwe.mitre.org/data/definitions/326.html)
* [CWE-20 - Improper Input Validation](https://cwe.mitre.org/data/definitions/20.html)
* [CWE-327 - Use of a Broken or Risky Cryptographic Algorithm](https://cwe.mitre.org/data/definitions/327.html)

Even though there were only a couple instances of the last item listed, CWE-327, that item is something we plan to bring to the attention of the `openMRS` development team. It could be a relatively quick fix and something that has a tangible impact on the security of the software as a whole.

----

#### Manual Code Review - Summary

[We need to add a summary of the key findings from any manual code reviews here, including links and mappings to CWEs, CAPECs and so on.]

### Code Analysis for SSE - Documentation of any contact had with the OSS project (Task 5) 
---

Currently there has been no direct contact with the OpenMRS team or personnel. All of our findings have been from reviewing the GitHub codebase and the various documentation on their wiki. We hope to create pull requests with our findings soon.


### Team Retrospective (Task 6)
---

The team received a much needed break over the holiday but that also affected our ability to meet as a group to discuss in person the various assignments. Travis really stepped up and took the initiative to keep the progress on the project moving and breaking down the tasks in the GitHub markdown document. The workload and specific tasks for this assignment took us all off guard at first and the whole group owes Travis a big thank you for his continued effort. 

We are all getting very busy towards the end of the semester which is also affecting our coordination efforts. We continue to use Slack to keep the team up to date on our current work. However, lack of in-person meetings has left us a little disoriented on our goals. We have noticed that team meetings allow us to be very honest and forward with our feelings, thoughts, and task assignements. We hope to be able to meet up soon and continue with the final push for our project to put forward the best product that we can.

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
