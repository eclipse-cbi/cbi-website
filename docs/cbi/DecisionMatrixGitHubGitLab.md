# GitHub/GitLab Decision Matrix

This decision matrix provides a detailed comparison between GitHub and GitLab across multiple dimensions relevant to projects hosted at the Eclipse Foundation. The goal is to help projects make informed decisions based on factors such as Code Management, Continuous Integration, platform features available, data governance, infrastructure, ...

Each criterion is assessed side-by-side for both platforms, highlighting key differences and considerations. This matrix is intended as a living document and may evolve as new features or policies are introduced by either platform.

| Criteria | GitHub | GitLab |
| --- | --- | --- |
| **Contract & licensing** {:colspan=3} |
| Eclipse Foundation contract with the platform | 10 years | 3-year renewable term (GL OSS program participant) |
| Available Version | Enterprise Cloud | Ultimate 17.8.5 |
| Policies applied | [GitHub policies + Eclipse foundation policies](https://docs.github.com/en/site-policy) | [Eclipse Foundation policies, Private policy](https://www.eclipse.org/legal/privacy/) |
| **Infrastructure & Hosting** {:colspan=3} |
| Data Location | [Default in the US, with possible data residency in the EU.(NOTE: data stored outside region)](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency) | EU (France, OVH Datacenter) |
| Data Sovereignty | GH is 100% GitHub, with optional backups managed by EF (not in place) | EF-owned data, with backups in Canada |
| SLA | [GitHub SLA](https://github.com/customer-terms/github-online-services-sla) | [Eclipse IT SLO](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/wikis/IT-Service-Level-Objectives) |
| Service Status | [GitHub Status](https://www.githubstatus.com/) | [Eclipse status](https://www.eclipsestatus.io/) |
| **Authentication** {:colspan=3} |
| Authentication | GitHub account (must be specified in EF account for invitation/permissions/ECA) | EF account |
| 2FA | Activated and enforced at enterprise organization level | Activated and enforced globally |
| **Code Management** {:colspan=3} |
| Git version | Not disclosed | 2.47.0 |
| Git Large File Storage (LFS) | [Setup gitlfs, Storage and bandwidth quotas](https://docs.github.com/en/repositories/working-with-files/managing-large-files) | Set up at project level: No quotas yet defined. |
| Code search | [Native search, across all GitHub repositories](https://github.com/search) | [Native search, advanced search is not set up, across Eclipse GitLab repositories](https://docs.gitlab.com/user/search/) |
| Mono repo and git sub-module | Supported | Supported |
| **Permissions** {:colspan=3} |
| Project Lead | Maintain | Maintainer (control over sub-groups and projects) |
| Committer | Write | Developer |
| Contributor | Triage | Reporter |
| Organization setup | GitHub Self-Service with Otterdog (PL approval) | Via UI only PL can apply changes (at project and sub-group levels) Modification at Group Level can only be changed by EF IT team |
| **External Contribution** {:colspan=3} |
| Community interaction | GitHub issues, PR, and discussion | GitLab issues, MR, [GitHub discussion can be simulated in GitLab](https://gitlab.com/gitlab-org/gitlab/-/issues/15641) |
| Fork | Fork with GitHub Account (ECA integrated via GitHub app). GitHub handle needs to be defined in Eclipse Account for ECA check to work. | Fork with EF account (ECA integrated within GitLab) |
| **CI & Build Infrastructure** {:colspan=3} |
| Native CI | [GitHub actions](https://docs.github.com/en/actions) | [GitLab CI](https://docs.gitlab.com/ci/) |
| CI Libraries | [Marketplace actions](https://github.com/marketplace?type=actions) | [Template examples EF templates](https://docs.gitlab.com/ci/examples/) |
| Runner request | GitHub action is activated by default, or can be changed with [Otterdog](https://otterdog.eclipse.org/) | Request by a [HelpDesk ticket](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/issues/new) (Runner creation and CI feature activation) |
| Runner type | Default runners from enterprise plan, extra cost for specific configuration runner e.g. large runner | Runners in EF infra; hosted runners accepted outside of EF Infrastructure accepted after security check |
| Runner for forked projects | Default GitHub free plan | No shared runners, User have to register their own runner. |
| Runner concurrency | [Defined at enterprise level: 500 concurrent jobs shared among all EF GitHub organizations](https://docs.github.com/en/actions/administering-github-actions/usage-limits-billing-and-administration) | [Starting with 4 concurrency runners with 1 resource pack]((https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#resource-pack-configuration)) |
| Runner sizing | [4cpu, 16GB RAM GitHub Allocation.<br/> Larger runner through sponsoring](https://docs.github.com/en/actions/using-github-hosted-runners/using-github-hosted-runners/about-github-hosted-runners) | [Small: 0.5 CPU/1GB RAM,<br/> Medium: 2 CPU/4GB RAM,<br/> Large: 4 CPU/8GB RAM (only through sponsoring)](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#resource-pack-configuration). <br/> [Can be overridden up to max resource pack allowed combine with concurrency](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#push-the-limits). See Resource Pack |
| Runner storage quotas | 14GB | 50GB |
| Runner storage location | GitHub cloud | Build storage: Datacenter in Canada, Artifacts: EU Datacenter |
| Runner OS/architecture | VM approach:<br/>Linux (x64/arm64),<br/> Windows (x64),<br/> macOS (intel/arm64) | Container approach:<br/> Linux (x64) (Ubuntu by default),<br/> Windows(x64) |
| Build infrastructure | GitHub cloud runner (Azure datacenter) | EF cluster based on OKD. <br/>**NOTE: OKD comes with security measure like non-root, drop all CAPS ...** |
| Build/artifact retention | Artifact and log retention: Max 180 days | Archive jobs not set, Artifacts retention: 14 days |
| Registry | [GitHub Package Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry) | [GitLab Registry is deactivated.](https://docs.gitlab.com/user/packages/) <br/> Nexus via [repo.eclipse.org](https://repo.eclipse.org) is proposed |
| Build Container support | Container client: kaniko, buildah, podman, ... | [EF Buildkit infrastructure](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#build-container-image-buildkit) |
| Running services | [Service containers](https://docs.github.com/en/actions/use-cases-and-examples/using-containerized-services/about-service-containers) | [GitLab CI Services Resource pack quotas applied to services](https://docs.gitlab.com/ci/services/) |
| Runner statistics | None. [Develocity](https://develocity.eclipse.org) can be used | Grafana dashboard (only internally for now, will be made public later). [Develocity](https://develocity.eclipse.org) can be used in addition |
| Secrets management | Otterdog applies internal secrets to GitHub org/projects secrets.  PL can request creation of specific secrets via ticket | Integrated with internal tooling, PL can add manually their secrets via UI |
| **Code Security/Compliance** {:colspan=3} |
| Security tooling | [Code scanning, secrets scanning, Dependabot](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning) | [Security tooling integrated via CI, with reports generation](https://docs.gitlab.com/user/application_security/detect/) |
| Security Dashboard | [otterdog dashboard](https://otterdog.eclipse.org/) | None |
| IP/license Compliance | [Dash Tool GitHub Action](https://github.com/eclipse-dash/dash-licenses?tab=readme-ov-file) | [Dash Tool integration Built-in compliance feature GitBab-CI integration (soon)](https://www.eclipse.org/projects/handbook/) |
| **Project Management** {:colspan=3} |
| Project Management | [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects) | [GitLab Plan and Track Work](https://docs.gitlab.com/topics/plan_and_track/) |
| **Documentation** {:colspan=3}|
| Wiki | [Available](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis) | [Available](https://docs.gitlab.com/user/project/wiki/) |
| Website (Pages) | [GitHub Pages](https://docs.github.com/en/pages) | [GitLab Pages](https://docs.gitlab.com/user/project/pages/) are disabled.<br/> EF project-website process is proposed as an alternative. |
| Doc as code support | [GitHub Flavored Markdown, mermaid, all GitHub markup](https://github.github.com/gfm/) | [GitLab Flavored Markdown, asciidoc, plantuml, marmaid, ...](https://docs.gitlab.com/user/markdown/) |
| **Advanced Features** {:colspan=3} |
| Mirroring | [Manual or via GitHub Action](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) | [Mirroring available: push, pull, bi-directionnal methods](https://docs.gitlab.com/user/project/repository/mirror/) |
| AI agent | [Copilot](https://github.com/features/copilot) | [GitLab Duo is disabled](https://about.gitlab.com/gitlab-duo/) |
| Remote development | [Codespaces](https://github.com/features/codespaces) | [Web IDE, Workspace](https://docs.gitlab.com/user/project/web_ide/) |
| Discussions | [Discussions](https://docs.github.com/en/discussions) | [GitHub discussion can be simulated in GitLab](https://gitlab.com/gitlab-org/gitlab/-/issues/15641) |
| External app | [Marketplace](https://github.com/marketplace) | [Integrate with GitLab](https://docs.gitlab.com/integration/) |
| Merge Train | [Merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue) | [Merge train](https://docs.gitlab.com/ci/pipelines/merge_trains/) |
| Service desk | [None](https://github.com/orgs/community/discussions/52053) | [Service desk is disabled](https://docs.gitlab.com/user/project/service_desk/) |
| Code owner | [Code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) | [Code owners](https://docs.gitlab.com/user/project/codeowners/) |
| **Visibility** {:colspan=3} |
| Web Referencing | Well referenced by search engines (tested with Google) | Less referenced by search engine due to hosted instance (tested with Google). <br/> [Sitemap issue for public repository](https://gitlab.com/gitlab-org/gitlab/-/issues/36835). <br/> Repositories can be mirrored to GitHub |
| Contributor Visibility | Displayed on the Organization/Project page. <br/> **IMPORTANT: Members have to make their profile public** | Displayed on the Members page. All members are public |
| Metrics | Insights page: Pulse, Contributors activities, Commits, Forks, watch, stars... | Analyze page: Analytics Dashboard, Contributor, Repo, Code Review Analytics, insights, watch, stars... |
| Eclipse Project Adoption Rate | [266 (source: otterdog)](https://otterdog.eclipse.org/index) | [63 (source: GitLab Eclipse Group)](https://gitlab.eclipse.org/eclipse) |
