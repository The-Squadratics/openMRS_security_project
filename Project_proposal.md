### The Squadratics
### CYBR 8430 - Project Proposal
### OpenMRS - A patent based

#### Project Proposal: 2-3 page markdown document that describes the following:

* An open-source software project your team has chosen. From here on, it will be referred to as “software”.

We selected `OpenMRS` for our project, specifically the `OpenMRS-core`.

---

* An assumed/hypothetical operational environment (e.g., home, office, enterprise, bank, government, etc.) where the users will expect security functionality from the software in its intended use.

Electronic medical records are standard in most western or developed countries but due to their cost and the technical overhead they entail they haven't been adopted	as much in developing nations, especially in rural areas.  This project aims to change that by providing an open source solution that healthcare providers and facilities can adopt regardless of their financial means.

Our examination will focus on a the core use case of electronic medical records, managing patient records at a small facility. We will be examining this...

---
### Security Needs of the Users
#### The security needs of the users of OpenMRS in its operational environment are:
* Access Control including authorization, authentication, and access approval of the users to the software.
* Data Security including prevention of accidental and malicious viewing, changing, or deleting of data.
* Application Security including lack of bugs or flaws in coding logic that could result in future vulnerabilities leading to software breaches.
* Network Security including confidence that the data will reach the intended recipient without unauthorized users being able to see or interact with the data or software.

---

* Motivation for selecting this project

This project is aimed at `resource constrained` hospital and health care providers. Those that don't typically have the ability to implement a commercial system to mange patient records.

---

* Open source project description (What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.)

### Project Description

OpenMRS (stands for Open Medical Record System) was initially created in 2004 to create a database in a medical clinic in Kenya and has since grown to be in use on 6 continents. The collection of volunteers are from across the world and from many different backgrounds. ["The mission is to improve health care delvery in resource-constrained areas through the use of a scalable, open source medical record system."](https://openmrs.org/about/mission/) The overall goal of the mission is to help create a world where lower costs and higher capacity of the IT tools allows the community to further close the disparity between poor and wealthy countries by alleviating the work of medical professionals and provide them the tools to provide more beneficial results in health care.

OpenMRS is a common platform used to build up medical data systems using few resources. The software is based on a conceptual database platform, so it is not dependent on data types, allowing for necessary customization. The client-server design allows for maximum availability and it stores all potentially relevant data so it is a concept dictionary at its core.

* Contributors: 324 direct Github contributors
* Activity: 
   * 140 releases
   * 10,803 commits (with the most recent commit coming less than 3 hours ago)
   * 72 pending pull requests
   * 43 branches
   * 2,413 forks
* Use and Popularity: OpenMRS is used in almost 50 deployments across 6 continents with uses spanning from research and development to     evaluation and clinical.
* Languages Used: 96.2% Java, 2.9% SQLPL, less than 1% other languages
* Documentation Sources: 
   * OpenMRS Website: https://openmrs.org/
   * OpenMRS demo: https://openmrs.org/demo/
   * OpenMRS Github: https://github.com/openmrs/openmrs-core
   * OpenMRS Wiki: https://wiki.openmrs.org/

---

### License and Contributions

This project uses the Mozilla Public License v2.0.  It contains the following [permissions, conditions, and limitations](https://choosealicense.com/licenses/mpl-2.0/).

#### Permissions
* Commercial use
* Distribution
* Modification
* Patent use
* Private use

#### Conditions
* Disclose source
* License and copyright notice
* Same license (All releases must use this license)

#### Limitations
* Liability (Limitation of liability)
* Trademark use (Does NOT grant trademark rights)
* Warranty (Does NOT provide any warranty)


### Contributing

This project has provided a detailed, step-by-stem `Contributing` document that outlines the steps that should be taken when making a contribution to the project.  [It can be found here](https://github.com/openmrs/openmrs-core/blob/master/CONTRIBUTING.md).

----

### Summary of Security-related History

The `openMRS` project was created in 2004.  Since then it has grown to include many different modules, all of which have their own code repositories.  Our work will focus on the [`openMRS-core`](https://github.com/openmrs/openmrs-core) which, unfortunately, doesn't have a complete or comprehensive history of the changes that were made.  It does however provide some information about the current development practices.  There is also a Wiki dedicated to the project as a whole which we will use, but not all of the information found there is necessarily relevant to our particular project.

In addition, it's worth noting that the project as a whole doesn't seem to have a clearly defined security policy or stated goals.  In reviewing various meeting notes/minutes found on the [Wiki](https://wiki.openmrs.org/display/RES/2017-01-23+Project+Management+Meeting), the topic does come up and they are trying.  But like many open source projects, there currently isn't any single reference document.  Instead, security features are listed or detailed within the application documentation itself.  One example being the [User Access](https://wiki.openmrs.org/pages/viewpage.action?pageId=3346872) pages which describe how roles and privileges function and are set up.

#### Known Vulnerabilities

The list of currently [known vulnerabilities](https://snyk.io/test/github/openmrs/openmrs-core?targetFile=api%2Fpom.xml) include the types of issues listed below.  Many of these are introduced through libraries and modules that the core software uses like Java Spring, Jackson Validator, Hibernate core, and MySQL.

* Denial of Service
* Deserialization of Untrusted Data
  * As defined in [CWE-502](https://cwe.mitre.org/data/definitions/502.html)
* XML External Entity Injection (XXE)
* Access Restriction Bypass
  * More information can be found in the [accompanying report](https://snyk.io/vuln/SNYK-JAVA-ORGSPRINGFRAMEWORK-31650)
* Java Security Manager Bypass
  * More information can be found in the [accompanying report](https://snyk.io/vuln/SNYK-JAVA-ORGHIBERNATE-30098)
* Directory Traversal
  * More information can be found in the [accompanying report](https://snyk.io/vuln/SNYK-JAVA-ORGSPRINGFRAMEWORK-32202)
* Privilege Escalation
  * More information can be found in the [accompanying report](https://snyk.io/vuln/SNYK-JAVA-MYSQL-174574)

There is also documentation that details general vulnerabilities that can be present in any [Java based application](https://wiki.openmrs.org/display/docs/Top+Vulnerabilities+in+Java+Web+Applications). They also have a few pages that discuss [security and encryption](https://wiki.openmrs.org/display/docs/Security+and+Encryption) but they are quite out of date.

#### Feature Addition / Removal

While the project does maintain comprehensive issue tracking though [JIRA](https://issues.openmrs.org/secure/Dashboard.jspa) and pull requests through [GitHub](https://github.com/openmrs/openmrs-core/pulls?utf8=✓&q=security), tracking specific security related changes is difficult.  By searching for relevant keywords we were able to find issues related to security issues that have been closed over the years.  For example, [Upgrade Apache Commons Collections](https://github.com/openmrs/openmrs-core/pull/1758).

---

### GitHub Repository

The GitHub repository can be [found here](https://github.com/The-Squadratics/openMRS_security_project).

---

### GitHub Project Board

The project board can be [found here](https://github.com/The-Squadratics/openMRS_security_project/projects/1).

