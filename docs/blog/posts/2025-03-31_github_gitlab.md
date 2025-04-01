---
title: "GitHub/GitLab: Decision Matrix Part 1 - Understanding CI Differences"
draft: false
authors:
  - heurtematte
date: 2025-03-31
tags:
  - CBI
categories:
  - GitHub/GitLab
  - CI
comments: true
---

The Eclipse Foundation gives projects the freedom to choose between [GitHub](https://github.com) and [GitLab](https://gitlab.eclipse.org) for hosting and managing their source code.

While both platforms are built on the same underlying Git technology, their platform approach brings a range of additional features.
Some of these features overlap, addressing common project needs (with subtle implementation differences), while others take entirely different approaches.

## What This Blog Post Series Will Cover

The next blog posts will dive into these differences, with a purely technical focus for developers, DevOps engineers, and infrastructure teams.
The goal? Highlighting key differences in approach, implementation, and alternative services provided by the Foundation.

We will cover the following topics in the next blog posts:

* CI pipelines (GitHub Workflows, GitLab Runners)
* Runner management and execution environments
* Quota models and build resource allocation
* Additional build-related services

## What This Blog Post Series Will not Cover

To keep things focused and digestible, we won’t be covering broader topics such as:

* Project visibility/SEO
* Data sovereignty and compliance
* Community engagement and contribution models

While these are critical considerations when selecting a platform, they deserve their own dedicated posts.

Before we jump into the details, it’s important to note that the versions of GitHub and GitLab offered by the Eclipse Foundation are enterprise-grade:

* GitHub Enterprise
* GitLab Ultimate

This is crucial because these versions unlock advanced features, such as extended security options; extra build times, that are not available in the public/community versions.


## GitHub Actions, GitLab CI, and Jenkins

GitHub Actions and GitLab CI are very similar in structure, syntax, and functionality:

* In both cases, CI/CD configuration files are written in YAML and stored closed to the code in the Git repository.
* Both are event-driven and get triggered by pushes, PR/MR, tags, issues, or on a schedule.
* Tasks can be defined in stages (e.g. build, test, publish, deploy).
* Both allow templating or re-use of tasks.
* Both feature plenty of integrations (via the [GitHub Marketplace](https://github.com/marketplace) or [GitLab CI extensions](https://gitlab.com/guided-explorations/ci-cd-plugin-extensions)).
While the GitHub Marketplace has more actions, GitLab has built-in security and governance checks.

At the end of the day, it’s a matter of preference. For most common CI tasks, both systems are equally easy to write, maintain, and execute.
Implementing specific use-cases can require more in-depth knowledge and might have a steep learning curve. 

The Eclipse Foundation also offers a fully managed [Jenkins instance for every project](https://ci.eclipse.org). It easily integrates with either GitHub or GitLab and provides an additional CI/CD approach.
Jenkins can be used instead of GitHub actions or GitLab CI, but also in combination with each respective system. Due to its [plugin-based structure](https://plugins.jenkins.io/), many scenarios can be covered.

## Who Manages the Runners?

GitLab CI relies on dedicated runners, deployed and managed by the Eclipse Foundation Releng team. Runners are provisioned with [GRaC (GitLab Runner as Code)](https://gitlab.eclipse.org/eclipsefdn/it/releng/gitlab-runner-service/gitlab-runner-as-code)
and all requests for GitLab CI require a [Helpdesk ticket](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/new) so that the Releng team can provision and configure runners.

Standard GitHub runners offered to public projects for free do not require maintenance from the Releng team.
[Larger and more powerful GitHub runners](https://docs.github.com/en/actions/using-github-hosted-runners/using-larger-runners/about-larger-runners) can be set up on demand with sponsoring from eligible Eclipse member organizations.

## Where Are My Builds Running?

The Eclipse Foundation’s build infrastructure is running on an OKD Kubernetes cluster (the upstream community project of OpenShift) on-premises.

[GitLab CI/CD runners](https://github.com/eclipse-cbi/cbi/wiki#gitlab-runners) and Jenkins builds are executed within the Eclipse Foundation’s build cluster, located in Canada.
GitHub Actions runners, run on GitHub’s cloud infrastructure.

The infrastructure where the runners are executed is essential because, as we will see later, it can have security implications depending on the measures implemented within these environments.

## External Runners

Projects can ask to connect  their own runners when they need:

* Higher performance (more CPU/RAM) than default runner configuration can provide
* Custom execution environments: RISC-V, ARM, ...

This requires a [Helpdesk ticket](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/new) and approval from the Eclipse Foundation security team.


## Next posts

That wraps up this first article! In future posts, we will cover:

* Resource Quotas
* Build images
* Secrets management
* Hosting static website
* Advanced security policies
