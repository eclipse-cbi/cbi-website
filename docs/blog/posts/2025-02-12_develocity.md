---
draft: false

authors:
  - heurtematte
  
date: 2025-02-12

tags:
  - blog
  - develocity

categories:
  - Blog
---

# Develocity Evaluation Phase: Presentation with Gradle on Optimizing Pipelines for Eclipse Projects

The Eclipse releng team is currently evaluating the relevance of the [Develocity platform](https://gradle.com/develocity/) by Gradle Inc in understanding and optimizing their pipelines.

On Thursday, February 6, a dedicated presentation was held in collaboration with Gasper Kojek from Gradle to explore the platform's capabilities and discuss how it could benefit both Eclipse projects and
the releng team in addressing build challenges.

The session focused on the challenges, the evaluation phase, Develocity’s features and how it could enhance build performance, visibility, and reliability across Eclipse projects.

🎥 [Watch the Presentation Here](https://youtu.be/YWIbzmNFJVM)

Below is a summary from the session:

## 1. Challenges in CI/CD for Eclipse Projects

Eclipse projects face several build-related challenges, including:

* **Slow Build Identification**: Detecting bottlenecks in pipelines is difficult without proper monitoring.
* **Limited Build Performance Visibility**: Internal metrics (CPU, RAM, network usage) are not widely accessible, making debugging harder.
* **Build Failures & Flakiness**: Unstable builds reduce trust in CI services and require significant debugging effort.
* **Infrastructure Constraints**: Projects operate in a shared environment with limited resources, requiring efficient caching, parallelization, and optimization to maintain performance without increasing infrastructure costs.

Projects need pipelines that are **Fast, Safe, and Reliable**.

## 2. Develocity Evaluation Phase

The evaluation phase of Develocity started in January and runs until March, with a possible extension to June.

* Platform Access: [https://develocity-staging.eclipse.org](https://develocity-staging.eclipse.org)
* Current Participating Projects: **Mylyn, ESCET, Graphene, Buildship, Glassfish**

Post-Evaluation Goals:

* **Community Feedback**: Assess Develocity's value through user input and surveys.
* **Infrastructure Impact**: Evaluate impact on storage, CPU, and memory usage. And assess the effort needed to maintain Develocity operationally.

## 3. What is Develocity?

Develocity is a data platform & acceleration engine designed to improve developer productivity by providing insights into CI builds and enabling faster, more reliable builds.

### 3.1 Build Insights (Build Scans)

* Provides detailed build reports (dependencies, executed tasks, system metrics).
* Allows failure debugging through deep log analysis.
* Helps track long-term build performance trends.
* Supports Maven, Gradle, Bazel, SBT, NPM, Python, and Tycho (support in progress).

### 3.2 Build Acceleration Technologies

* **Build Caching**: avoids redundant work by reusing previous results.
* **Predictive Test Selection**: Uses machine learning to run only relevant tests.
* **Test Distribution**: Distributes tests across multiple agents for faster execution.

### 3.3 Real-world Example:

* Eclipse Store project reduced build time from 11 minutes to 50 seconds using build caching.
* Eclipse Jetty tests went from 47 minutes to 16 minutes with test distribution.

## 4. Live Demo Highlights

* **Develocity Dashboard**: Showed CI performance metrics, failure rates, and test flakiness.
* **Dependency Resolution View**: Helped track package versions and transitive dependencies.
* **Flaky Test Analysis**: Identified test inconsistencies across multiple CI runs.
* **Performance Optimization**: Demonstrated time saved by caching and test parallelization.

## 5. Key Takeaways:

* Develocity provides better CI visibility and performance optimization.
* It helps reduce build times, improve reliability/consistency, and optimize resource usage.
* The evaluation phase is ongoing, and projects are encouraged to participate.

## How to Join the Develocity Evaluation Phase?

* Create a [HelpDesk ticket](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/new) to onboard your project.

## Additional Resources:

* Develocity Evaluation Platform: [https://develocity-staging.eclipse.org](https://develocity-staging.eclipse.org)
* Provide feedback to help assess Develocity: [https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/5408](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/5408)
* Documentation: [https://eclipse-cbi.github.io/cbi-website/develocity/readme/index.html](https://eclipse-cbi.github.io/cbi-website/develocity/readme/index.html)
