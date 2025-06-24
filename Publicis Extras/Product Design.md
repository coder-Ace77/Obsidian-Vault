
---

#### Role of product designer:

These are problem solvers who understand UX , UI and design systems.

UX - User experience aka what users feel when they use product.
UI - User interface (beauty + experience)
Design Systems - A **design system** is a collection of reusable components, guidelines, and tools that help teams.

What do product designer do?

Working on ideas understand users and comming with user journey map / userflows.

#### Design thinking vs agile methology

Design thinking: A mindset to innovatively solve a problem.
Agile methology: An efficient development process that divides work into realistic managable portions.

### Full stack dev vs Product Engineer vs Site Reliability Engineer:

A **Full Stack Software Engineer** is responsible for developing complete features or applications, working across both the frontend (what users see) and the backend (servers, databases, APIs). They have a wide range of skills, often including web frameworks, databases, server-side languages, and deployment tools. 

A **Product Engineer** shares many technical skills with full stack engineers but operates with a stronger focus on the **user experience** and **business impact**. They not only build features but also contribute to product direction by working closely with designers, product managers, and sometimes marketing teams. They prioritize solving the right problems for users, often using A/B testing and metrics to validate their decisions. 

A **Site Reliability Engineer (SRE)** focuses less on building new features and more on keeping systems **reliable, scalable, and efficient**. Their day-to-day work includes monitoring, automating infrastructure, managing incidents, and optimizing system performance. SREs bring software engineering principles to operations, aiming to reduce manual work and ensure uptime and performance targets (like SLAs) are met. They often work with backend engineers and DevOps teams, building tooling and infrastructure that supports the engineering org as a whole.

**DevOps** is a combination of **development (Dev)** and **operations (Ops)** practices aimed at **automating**, **integrating**, and **improving collaboration** between software developers and IT operations teams. The goal of DevOps is to **shorten the software development lifecycle**, increase deployment frequency, and ensure high software quality and reliability. It emphasizes a culture of shared responsibility, continuous improvement, and automation throughout the delivery pipeline.

In practice, DevOps involves tools and processes like **CI/CD (Continuous Integration and Continuous Delivery)**, **infrastructure as code (IaC)**, **monitoring**, **automated testing**, and **deployment automation**. Teams use tools like GitHub Actions, Jenkins, Docker, Kubernetes, Terraform, and Prometheus to automate building, testing, deploying, and monitoring applications. This allows developers to release features more quickly, reliably, and safely, reducing manual work and human error.

#### Debrief SRE engineer:

At their core, the development teams want to launch new features and see them adopted by users. At _their_ core, the ops teams want to make sure the service doesn’t break while they are holding the pager. Because most outages are caused by some kind of change—a new configuration, a new feature launch, or a new type of user traffic—the two teams’ goals are fundamentally in tension.

DevOps is a ‘way’ in which an organization should operate, while SRE is simply a single unit in an organization that adheres to that ‘way’.

### Design Principles:

1. OOps
2. SOLID 
3. DRY , KISS and YAGNI principle

#### DRY Don't Repeat Yourself

- **Meaning**: Avoid duplicating code or logic. If you find the same code or logic appearing in multiple places, extract it into a single function, class, or module.

####  KISS – Keep It Simple, Stupid

- **Meaning**: Always aim for the simplest solution that works. Avoid over-engineering or making things more complex than necessary.

#### YAGNI You Aren’t Gonna Need It

- **Meaning**: Don’t implement functionality until it's actually required. Avoid writing code based on assumptions about future needs.


#### Test Driven development:

TDD is a development process where you **write a failing test first**, then write the **minimum code** needed to pass the test, and finally **refactor** the code while keeping tests green.

**Cycle (Red-Green-Refactor):**

1. **Red** – Write a test that fails.
2. **Green** – Write the code to make the test pass.
3. **Refactor** – Clean up the code while keeping the test passing.


#### Behaviour Driven Development:

BDD builds on TDD but focuses on the **behavior of the application** as expected by the user. It uses a **natural language** style for defining tests to enhance collaboration between developers, testers, and non-technical stakeholders.

- Uses **Given-When-Then** structure to describe behavior.
- Often supported by tools like **Cucumber, JBehave, SpecFlow**.

```gherkin
Scenario: Sum of two numbers
  Given the calculator is on
  When I add 2 and 3
  Then the result should be 5
```

| Feature       | TDD                  | BDD                            |
| ------------- | -------------------- | ------------------------------ |
| Focus         | Code correctness     | User behavior and expectations |
| Test style    | Unit tests           | Acceptance tests               |
| Test language | Programming language | Natural language (DSL)         |
| Stakeholders  | Developers           | Developers, testers, BAs       |
| Tools         | JUnit, NUnit, etc.   | Cucumber, SpecFlow, etc.       |

**Code refactoring** is the process of **improving the internal structure** of existing code **without changing its external behavior**.

### Goals of Refactoring:

- Improve **readability** and **maintainability**
- Reduce **code duplication**
- Simplify **complex logic**
- Improve **performance** (sometimes)
- Make the code **easier to test or extend**

#### Common refactoring techniques:

| Technique                 | Description                                  | Example Before → After                              |
| ------------------------- | -------------------------------------------- | --------------------------------------------------- |
| **Extract Method**        | Move part of code into a separate method     | Inline logic → `calculateTax()`                     |
| **Rename Variable**       | Give variables meaningful names              | `int a` → `int taxRate`                             |
| **Inline Variable**       | Replace unnecessary temporary variable       | `int result = a + b` → `return a + b`               |
| **Replace Magic Number**  | Use named constants instead of numbers       | `if (status == 2)` → `if (status == STATUS_ACTIVE)` |
| **Encapsulate Field**     | Make fields private and use getters/setters  | `obj.field` → `obj.getField()`                      |
| **Decompose Conditional** | Break complex `if` statements into methods   | `if (a && b && c)` → `if (isEligible())`            |
| **Remove Dead Code**      | Delete unused classes, methods, or variables | Unused helper functions                             |

#### Profiling a program:

**Profiling** is the process of analyzing a program to determine:
- How much time different parts of code take (CPU profiling)
- How much memory is being used (memory profiling)
- How many times functions are called (call frequency)
- Where performance bottlenecks occur

Profiling tools in java `VisualVM`, `JProfiler`, `YourKit`, `Java Mission Control`

### Engineering methologies:

#### Agile:

**Agile** is a software development methodology focused on **iterative progress, collaboration, and adaptability**. It emphasizes delivering small, working pieces of software in short cycles (called sprints), allowing teams to gather feedback early and often, adapt to changing requirements, and continuously improve. 

**Continuous Delivery (CD)** is a software development practice where code changes are automatically built, tested, and prepared for a release to production. It ensures that software is always in a deployable state, allowing teams to deliver updates quickly, reliably, and frequently with minimal manual intervention. Unlike Continuous Deployment, CD stops short of automatically deploying to production—instead, it enables **on-demand releases** through a controlled, repeatable process.

#### Devops

**DevOps** is a culture and set of practices that bridges the gap between **development (Dev)** and **operations (Ops)** teams to enable faster, more reliable software delivery. It emphasizes automation, collaboration, monitoring, and continuous improvement throughout the software lifecycle. A key part of DevOps is **CI/CD (Continuous Integration and Continuous Delivery/Deployment)**, which automates the process of integrating code changes (CI), testing them, and either preparing them for release (CD - Continuous Delivery) or automatically deploying them to production (CD - Continuous Deployment). Together, DevOps and CI/CD aim to shorten development cycles, reduce errors, and improve the speed and quality of software releases.
