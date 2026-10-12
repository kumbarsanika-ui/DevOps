# DevOps and Agile Interview Questions

## Agile and Azure DevOps

### 1. What is Azure Boards?

Azure Boards is the Azure DevOps service for planning, tracking, and discussing work. Teams use work items, backlogs, Kanban boards, sprint boards, queries, and dashboards to track progress from idea through delivery. It supports configurable workflows and links work to code changes and builds.

### 2. What is Jira?

Jira is Atlassian's work-management and issue-tracking product. Software teams commonly use Jira Software for Scrum and Kanban backlogs, boards, sprint planning, reporting, and configurable issue workflows. It can integrate with source control, CI/CD, and other Atlassian products.

### 3. What is Trello?

Trello is a visual work-management tool built around boards, lists, and cards. A team can represent workflow stages as lists and work as cards, then move cards as work progresses. It is quick to adopt for lightweight Kanban and general coordination; complex software delivery workflows may need more specialized tools or integrations.

### 4. What are Agile work items such as Epic, Feature, User Story, Task, Bug, and Issue?

Work-item names and hierarchy vary by product and process template, but commonly mean:

- **Epic:** A large strategic outcome that can span multiple releases or teams.
- **Feature:** A substantial capability that contributes to an epic and is delivered through smaller stories or tasks.
- **User story:** A user-focused requirement, often written as “As a [user], I want [capability], so that [benefit].” It should have clear acceptance criteria.
- **Task:** A specific piece of work, often a technical or implementation step, used to deliver a story or other item.
- **Bug:** A defect where actual behavior does not meet expected behavior.
- **Issue:** A general tracked item. In some tools it is the umbrella term for all work; in others it is a specific work-item type. Confirm the team's configured meaning.

Items are often organized hierarchically, for example Epic → Feature → User Story → Task. A bug may be linked at the level where the team plans and tracks it.

### 5. How do you organize work items on an Agile board?

Start with a prioritized backlog aligned to the product goal. Break larger outcomes into small, testable stories with acceptance criteria, estimate or size them using the team's conventions, and assign them to an iteration when appropriate. On the board, use columns for workflow states such as New, Active, Review, and Done; define explicit entry and exit criteria, limit work in progress, and use swimlanes or filters only when they help distinguish meaningful work. Review and refine the board regularly so it reflects reality.

### 6. What are Azure DevOps dashboards?

Azure DevOps dashboards are configurable collections of widgets that give a team or stakeholder a focused view of project status. Widgets can show items such as sprint burndown, velocity, query results, build status, test results, and deployment information. Dashboards support monitoring and discussion, but do not replace the underlying work-item data or agreed delivery metrics.

### 7. What are Azure Pipelines, and how do you create a pipeline?

Azure Pipelines is Azure DevOps's CI/CD service. It can build, test, package, and deploy applications from repositories such as Azure Repos or GitHub, using Microsoft-hosted or self-hosted agents.

A typical setup is to connect a repository, choose or write a pipeline definition, configure triggers, define build and test steps, publish an artifact or container image, and add deployment stages for target environments. YAML pipelines keep configuration with the code and support reviews and reuse. Protect production with environment approvals, checks, least-privilege permissions, and securely stored secrets. Validate the pipeline with a test run before relying on it for releases.

### 8. What are service connections, and how do you connect Azure DevOps to external services?

A service connection is a configured, permission-controlled connection between Azure DevOps and an external system, such as an Azure subscription, container registry, Kubernetes cluster, or cloud provider. Create the appropriate connection under project settings, select the authentication method, grant only the required permissions, and authorize it for the intended pipeline. Prefer workload identity federation or managed identities where supported; otherwise use securely stored, rotated credentials. Never place secrets directly in YAML or source control.

## DevOps Concepts

### 9. What is GitOps?

GitOps is an operational approach in which Git is the authoritative, declarative record of the desired state of systems such as infrastructure and Kubernetes applications. Changes are proposed through version-controlled commits and pull requests. An automated reconciler compares the declared desired state with the live state and applies or reports changes to reduce drift. Git history provides review and auditability; access controls and secrets management are still essential.

### 10. What are the advantages and disadvantages of DevOps?

**Advantages:** Faster and more frequent delivery, earlier feedback, repeatable automation, improved collaboration between development and operations, more consistent environments, and quicker detection and recovery from failures.

**Challenges:** Adoption requires cultural and organizational change, investment in automation and platform skills, and ongoing maintenance of pipelines and infrastructure. Poorly designed automation can spread mistakes quickly; excessive deployment speed without testing, security, observability, or rollback practices can increase risk. DevOps is a way of working, not simply a tool purchase or a reason to remove necessary controls.

### 11. What is the role and importance of DevOps in full-stack development?

DevOps connects application development with the systems that build, test, release, and operate it. For a full-stack team, this can mean automating checks for frontend and backend code, managing configuration and infrastructure as code, packaging services, deploying database and application changes safely, and monitoring performance and errors in production. Shared ownership and production feedback help teams deliver end-to-end features reliably rather than treating deployment and operations as a separate handoff.

## Related Comparisons and Processes

### 12. What is the difference between Azure DevOps, Git, GitHub, and GitOps?

- **Azure DevOps:** Microsoft's suite of services for planning and delivery, including Boards, Repos, Pipelines, Test Plans, and Artifacts.
- **Git:** A distributed version-control system for tracking changes to files and coordinating work through branches and commits.
- **GitHub:** A hosted platform for Git repositories and collaboration, with features such as pull requests, issues, Actions, and security tooling.
- **GitOps:** A way to operate systems by storing desired state in Git and using automation to reconcile live systems with that state.

They are related but not substitutes for one another: Git is a technology, GitHub and Azure DevOps are platforms, and GitOps is an operating practice that can use either platform.

### 13. What is the difference between Docker and containers? How do they help in DevOps?

A **container** is an isolated process and its packaged dependencies that runs using the host operating system's kernel. **Docker** is a company and ecosystem of tools and services commonly used to build, distribute, and run container images; Docker is not the container itself. Other compatible runtimes and image tools also exist.

Containers make application environments more portable and repeatable across development, testing, and production. In DevOps, pipelines can build and test an image once, store it in a registry, and promote that same image through environments. Containers do not by themselves guarantee security, compatibility, or identical behavior across hosts, so images need maintenance, scanning, and runtime controls.

### 14. What is the DevOps process? How does it work, and what are the architectures of Azure DevOps and GitOps?

DevOps is a continuous cycle rather than a single linear process:

1. **Plan:** Prioritize goals and define work and acceptance criteria.
2. **Code:** Collaborate using version control, branches, and reviews.
3. **Build and test:** Run automated compilation, unit, integration, security, and quality checks as appropriate.
4. **Package and release:** Produce versioned artifacts or images and promote them through controlled environments.
5. **Deploy and operate:** Provision infrastructure, release changes, and manage configuration with automation.
6. **Observe and learn:** Monitor service health and user outcomes, respond to incidents, and feed the findings into planning.

**Azure DevOps architecture:** Azure DevOps is a set of connected services, not one mandatory pipeline design. Boards manages planning; Repos stores source; Pipelines orchestrates jobs and stages on hosted or self-hosted agents; Artifacts stores packages; Test Plans supports test management. Pipelines can consume work and source, build and test it on agents, publish artifacts, and deploy through environments and service connections. Permissions, approvals, and integrations connect the services.

**GitOps architecture:** A Git repository holds the declarative desired state. A CI pipeline may validate changes and build application artifacts; after review and merge, a GitOps controller running near the target environment watches the repository (or an artifact registry), compares desired state with live state, and reconciles differences. The controller reports status and drift. This pull-based model usually lets the controller initiate changes from inside the environment, reducing the need for an external deployment system to have direct inbound access. Secrets should be managed separately or encrypted and access-controlled, not committed as plaintext.