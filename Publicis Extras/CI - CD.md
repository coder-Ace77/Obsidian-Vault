
---

DevSecOps - Extension of Devops , security is intergral part of team.

Goals: Speed and quality of security at same time.
Tradtional : Normally security is considered as separate teams. Not with Devops. So we need to add security into dev life cycle. 

We want it to be quick. 
Key to devops is speed and constant feedback. Continous integration - Checking code several times in a day. 
Continous Deleivery - Once test passed it gets released. 

Continous Delievery pipeline: 
1. Develop - Design and dev of an application includes sprint planning ,version control and unit testing
2. Inherit - Get software dependencies and bundle them in own code.
3. Build - CI build system runs all build steps and does acceptance testing
4. Deploy - Takes the software from artifact and give it to customer for use.
5. Operate - Application is up and running in production.

Inherit level may introduce many security vulnerabilities because a lot of code gets injected into the codebase. We can use tools which belong to some language and run checks to do so. Software composition analysis - Checks if you are using retired application.

Security testing in build stage means to test softare from outside. Infra testing , compliance testing , 
Dyanmic application security testing tools - DAST -> testing tools which are used by attackers.

Security in Deploy phase: Compliance and autitors. We want to automate as many security checks as possible.

CI static testing: Analsing source code for security testing. May give lot of false positives.
GOals: quick ,accurate etc.

Developer will put the code it will be built and checked by testing tool and get the report.

Continous Dynamic testing: A tool which tries to analyse the website and check for vulnerabilities. It is lang independent. 

Interative application security testing(IAST): It works by attaching to runtime. Testing happens when application works and provides feedback.

Continues Secret scanning: Look and scan the codebase and check if keys are present. The tool used must be accurate. 

Continous Library Scanning: Application library are source of security concern. Right tool must be quck and accurate and tool depends on language used.

Containous Container security: 