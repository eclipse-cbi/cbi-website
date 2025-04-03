# GitHub/GitLab Decision Matrix

This decision matrix provides a detailed comparison between GitHub and GitLab across multiple dimensions relevant to projects hosted at the Eclipse Foundation. The goal is to help projects make informed decisions based on factors such as Code Management, Continuous Integration, platform features available, data governance, infrastructure, ...

Each criterion is assessed side-by-side for both platforms, highlighting key differences and considerations. This matrix is intended as a living document and may evolve as new features or policies are introduced by either platform.

| Category | Criteria | GitHub | GitLab |
| --- | --- | --- | --- |
| 01.Contract & licensing | Eclipse Foundation contract with the platform | 10 years | 3-year renewable term (GL OSS program participant) |
| 01.Contract & licensing | Available Version | Enterprise Cloud | Ultimate 17.8.5 |
| 01.Contract & licensing | Policies applied | [Github policies + Eclipse foundation policies](https://docs.github.com/en/site-policy) | [Eclipse Foundation policies, Private policy](https://www.eclipse.org/legal/privacy/) |
| 02.Infrastructure & Hosting | Data Location | [Default in the US, with possible data residency in the EU.(NOTE: data stored outside region)](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency) | EU (France, OVH Datacenter) |
| 02.Infrastructure & Hosting | Data Sovereignty | GH is 100% GitHub, with optional backups managed by EF (not in place) | EF-owned data, with backups in Canada |
| 02.Infrastructure & Hosting | SLA | [GitHub SLA](https://github.com/customer-terms/github-online-services-sla) | [Eclipse IT SLO](https://gitlab.eclipse.org/eclipsefdn/helpdesk/-/wikis/IT-Service-Level-Objectives) |
| 02.Infrastructure & Hosting | Service Status | [GitHub Status](https://www.githubstatus.com/) | [Eclipse status](https://www.eclipsestatus.io/) |
| 03.Authentication | Authentication | Github account (must be specified in EF account for invitation/permissions/ECA) | EF account |
| 03.Authentication | 2FA | Activated and enforced at enterprise organization level | Activated and enforced globally |
| 04.Code Management | Git version | Not disclosed | 2.47.0 |
| 04.Code Management | Git lfs | [Setup gitlfs  Storage and bandwidth quotas](https://docs.github.com/en/repositories/working-with-files/managing-large-files) | Set up at project level: No quotas yet defined. |
| 04.Code Management | Code search | [Native search, accross all GitHub repositories](https://github.com/search) | [Native search, elastic search is not set up, accross Eclipse Gitlab repositories](https://docs.gitlab.com/user/search/) |
| 04.Code Management | Mono repo and git sub-module | Supported | Supported |
| 05.Permission | Project Lead | Team Project Leads | Maintainer (control over sub-groups and projects) |
| 05.Permission | Committer | Team Committers | Developper |
| 05.Permission | Contributor | Team Contributors | Reporter |
| 05.Permission | Organization setup | Github Self-Service with Otterdog (PL approval) | Via UI only PL can apply changes (at project and sub-group levels) Modification at Group Level can only be changed by EF IT team |
| 06.External Contribution | Community interaction | GitHub issues, PR, and discussion | GitLab issues, MR, [GitHub discussion can be simulated in GitLab](https://gitlab.com/gitlab-org/gitlab/-/issues/15641) |
| 06.External Contribution | Fork | Fork with GitHub Account (ECA integrated via GitHub app) GitHub handle needs to be defined in Eclipse Account for ECA check to work. | Fork with EF account (ECA integrated within GitLab) |
| 07.CI & Build Infrastructure | Native CI | [GitHub actions](https://docs.github.com/en/actions) | [GitLab CI](https://docs.gitlab.com/ci/) |
| 07.CI & Build Infrastructure | CI Libraries | [Marketplace actions](https://github.com/marketplace?type=actions) | [Template examples EF templates](https://docs.gitlab.com/ci/examples/) |
| 07.CI & Build Infrastructure | Runner request | Github action is activated by default, or can be changed with Otterdog (.eclipsefdn repository) | Request by a helpdesk ticket (Runner creation and CI feature activation) |
| 07.CI & Build Infrastructure | Runner type | Default runners from enterprise plan, extra cost for specific configuration runner e.g. large runner | Runners in EF infra; hosted runners accepted outside of EF Infrastructure accepted after security check |
| 07.CI & Build Infrastructure | Runner for forked projects | Default GitHub free plan | No shared runners, User have to register their own runner. |
| 07.CI & Build Infrastructure | Runner concurrency | [Defined at enterprise level: 500 concurrent jobs shared among all EF GitHub organizations](https://docs.github.com/en/actions/administering-github-actions/usage-limits-billing-and-administration) | [Starting with 4 concurrency runners with 1 resource pack]((https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#resource-pack-configuration)) |
| 07.CI & Build Infrastructure | Runner sizing | [4cpu, 16GB RAM Github Allocation Larger runner through sponsoring](https://docs.github.com/en/actions/using-github-hosted-runners/using-github-hosted-runners/about-github-hosted-runners) | [Small: 0.5 CPU/1GB RAM, Medium: 2 CPU/4GB RAM, Large: 4 CPU/8GB RAM (only through sponsoring)](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#resource-pack-configuration) [Can be overridden up to max resource pack allowed combine with concurrency](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#push-the-limits) See Resource Pack |
| 07.CI & Build Infrastructure | Runner storage quotas | 14GB | 50GB |
| 07.CI & Build Infrastructure | Runner storage location | Azure cloud | Build storage: Datacenter in Canada, Artifacts: EU Datacenter |
| 07.CI & Build Infrastructure | Runner OS/architecture | VM approach: Linux(x64/arm64), Windows(x64), macOS(intel/arm64) | Container approach: Linux (x64)(Ubunty by default), Windows(x64) |
| 07.CI & Build Infrastructure | Build infrastructure | GitHub cloud runner (Azure datacenter) | EF cluster based on OKD NOTE: OKD comes with security measure like non root, drop all CAPS ... |
| 07.CI & Build Infrastructure | Build/artifact retention | Artifact and log retention: Max 180 days | Archive jobs not set, Artifacts retention: 14 days |
| 07.CI & Build Infrastructure | Registry | [GitHub Package Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry) | [GitLab Registry is deactivated Nexus via repo.eclipse.org is proposed](https://docs.gitlab.com/user/packages/) |
| 07.CI & Build Infrastructure | Build Container support | Container client: kaniko, buildah, podman, ... | [EF Buildkit infrastructure](https://eclipse-cbi.github.io/cbi-website/gitlab-runner-service/index.html#build-container-image-buildkit) |
| 07.CI & Build Infrastructure | Running services | [Service containers](https://docs.github.com/en/actions/use-cases-and-examples/using-containerized-services/about-service-containers) | [Gitlab CI Services Resource pack quotas applied to services](https://docs.gitlab.com/ci/services/) |
| 07.CI & Build Infrastructure | Runner statistics | None  Develocity can be used | Grafana dashboard (only internally at the moment, plan to expose) Develocity can be used in addition |
| 07.CI & Build Infrastructure | Secrets management | Otterdog applies internal secrets to GitHub org/projects secrets.  PL can request creation of specific secrets via ticket | Integrated with internal tooling, PL can add manually their secrets via UI |
| 08.Code Security/Compliance | Security tooling | [Code scanning, secrets scanning, Dependabot](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning) | [Security tooling integrated via CI, with reports generation](https://docs.gitlab.com/user/application_security/detect/) |
| 08.Code Security/Compliance | Security Dashboard | [otterdog dashboard](https://otterdog.eclipse.org/) | None |
| 08.Code Security/Compliance | IP/license Compliance | [Dash Tool Github Action](https://github.com/eclipse-dash/dash-licenses?tab=readme-ov-file) | [Dash Tool integration Built-in compliance feature GitBab-CI integration (soon)](https://www.eclipse.org/projects/handbook/) |
| 09.Project Management | Project Management | [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects) | [GitLab Plan and Track Work](https://docs.gitlab.com/topics/plan_and_track/) |
| 10.Documentation | Wiki | [Available](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis) | [Available](https://docs.gitlab.com/user/project/wiki/) |
| 10.Documentation | Doc as code support | [GitHub Flavored Markdown, mermaid, all github markup](https://github.github.com/gfm/) | [GitLab Flavored Markdown, asciidoc, plantuml, marmaid, ...](https://docs.gitlab.com/user/markdown/) |
| 11.Advanced Features | Mirroring | [Manual or Github Action](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) | [Mirroring available: push, pull, bi-directionnal methods](https://docs.gitlab.com/user/project/repository/mirror/) |
| 11.Advanced Features | Website (Pages) | [GitHub Pages](https://docs.github.com/en/pages) | [GitLab Pages is disabled EF project-website process is proposed as an alternative](https://docs.gitlab.com/user/project/pages/) |
| 11.Advanced Features | AI agent | [Copilot](https://github.com/features/copilot) | [GitLab Duo is disabled](https://about.gitlab.com/gitlab-duo/) |
| 11.Advanced Features | Remote development | [Codespaces](https://github.com/features/codespaces) | [Web IDE, Workspace](https://docs.gitlab.com/user/project/web_ide/) |
| 11.Advanced Features | Discussions | [Discussions](https://docs.github.com/en/discussions) | [GitHub discussion can be simulated in GitLab](https://gitlab.com/gitlab-org/gitlab/-/issues/15641) |
| 11.Advanced Features | External app | [Marketplace](https://github.com/marketplace) | [Integrate with GitLab](https://docs.gitlab.com/integration/) |
| 11.Advanced Features | Merge Train | [Merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue) | [Merge train](https://docs.gitlab.com/ci/pipelines/merge_trains/) |
| 11.Advanced Features | Service desk | [None](https://github.com/orgs/community/discussions/52053) | [Service desk is disable](https://docs.gitlab.com/user/project/service_desk/) |
| 11.Advanced Features | Code owner | [Code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) | [Code owners](https://docs.gitlab.com/user/project/codeowners/) |
| 12.Visibility | Web Referencing | Well referenced by search engine (test with google) | [Less referenced by search engine due to hosted instance (test with google) Sitemap issue for public repository Repositories can be mirrored to GitHub](https://gitlab.com/gitlab-org/gitlab/-/issues/36835) |
| 12.Visibility | Contributor Visibility | Displayed on the Organization/Project page IMPORTANT: Members have to make their profile public | Displayed on the Members page All members are public |
| 12.Visibility | Metrics | Insights page: Pulse, Contributors activies, Commits, Forks, watch, stars... | Analyze page: Analytics Dashboard, Contributor, Repo, Code Review Analytics, insights, watch, stars... |
| 13.Adoption | Eclipse Project Adoption Rate | [266 (source: otterdog)](https://otterdog.eclipse.org/index) | [63 (source: GitLab Eclipse Group)](https://gitlab.eclipse.org/eclipse) |