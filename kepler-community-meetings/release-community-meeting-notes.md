Kepler Release 0.4 Planning
===

###### tags: `kepler` `release`

:::info
- **Date:** 
    - Nov. 29, 2022
- **Agenda**
1. Update and progress `30min`
    - VM support and model estimator integration
         - Offline models are available, power estimate on VM is working. 
         - e2e test cases are available to verify kepler container and node metrics (Sam: can you add test case to detect new Pods and their metrics? Huamin to add issues. Prometheus client is used in e2e, metrics reading can be added)
         - Estimator sidecar will be verified and added to e2e test (not in this release)
         - What is the status of online model training and updating? (manual test first, Pang will share her sidecar and model server manifests)
    - test coverage
        - improved from lower 30s to 39%, need more unit test (Huamin to investigate which pkg needs more tests and create issues. Sam: create tests for each pkg. Internal pointer/connector makes test case hard to make, pointer value validation etc needs refactor. Some pkg requires bcc library, making mac user hard to add test cases, maybe conditional build tag? Huamin will create issues for mac/refactor)
    - Deployment
        - Operator
            - [v1alphav1](https://github.com/sustainable-computing-io/kepler-operator/tree/v1alpha1) (Parul will send a demo based on kind. TODO integrating model server. OperatorHub integration will happen later. Sally will help on deploying on OpenShift/MicroShift)
            - tested kepler-exporter on kind, cluster-prerequisite for openshift WIP
            - working on integration with estimator and offline models
            - TO-DO Parul: Document features present in current operator and what will be expected in the next release.
        - Helm (https://github.com/sustainable-computing-io/kepler-helm-chart)
            - PR ready, Sam commented/reviewed. Tested on kind (validated exporter and output). Still working on Prometheus and Grafana (may add in the future)
            - to investigate how to release the chart (maybe use github actions)
    - Docs
        - [Simplify end user doc](https://github.com/sustainable-computing-io/kepler/issues/418) (Nikki to make two contributions)
2. Issues `20min`
    - [0 process](https://github.com/sustainable-computing-io/kepler/issues/422) (Add logging)
    - [podEnergyStatLabels needs update](https://github.com/sustainable-computing-io/kepler/issues/408) (already in local repo, doesn't affect model training atm)
    - [block_device_used logging](https://github.com/sustainable-computing-io/kepler/issues/355) (let's lower the verbosity first)
3. Questions and Discussions `10min`
    - Release criteria and date to be finalized
        - https://github.com/sustainable-computing-io/kepler/issues/333 (Estimator/kepler: configmaps. Pang will share the examples (in the discussion and docs PR))
    - Should cgroup v1 be supported in cgroup metrics based models? (Let's document this and investigate more next release)
    - Shared e2e on all repos: 
        - Kepler(including estimator and model server)
        - Operator, helm



:::info
- **Date:** 
    - Nov. 14, 2022
- **Agenda**
1. Issues and progress `40min`
    -  Issues
        -  VM support, Estimator, Model Server usage
            -  VM: CPU host passthrough tested (with perf counters metrics), cgroup metric model comes next
                -  development in model branch: cgroup pkg issues found. cgroupo metrics not reached. The work function is not finalized, under debugging. Pang is working on it and will report an issue.
            -  Estimator sidecar: tested before the metric refactoring. Config names in env var (also in the dev branch): set estimator to true. Huamin to add debugging to the sidecar. 
            -  Kaiyi: update namespace in model server to kepler (in deployment and in Service endpoint)
        -  Process to ensure usability and performance
            -  Marcelo: metrics doc (including samples) updated, new grafana dashboard PR (not yet using all the metrics), all power sources are in their own metrics
            -  Separate metrics vs aggregating at the Prometheus: performance hit on prometheus should be avoided; Aggregating on the Kepler side can help the scalability. 
            - Having dedidcated power source metrics can be used by label based aggregation. End user can query/check individual or aggregate metrics based on the basic metrics.
        -  Docs
            -  mkdocs vs Sphinx vs Hugo: kepler-docs needs dev preview on local env. Hugo is used by k8s but not as easy as mkdocs. Sphinx provides apidocs, but so do mkdocs. Sphinx is complicated, not consistent preview on github pages and local vs code plugin.
            -  mkdocs also reports broken links, maybe a test needed to ensure all links valid (refer to https://github.com/redhat-et/microshift-documentation/blob/main/.github/workflows/broken-link-check.yml)
            -  kepler-docs approver: Marcelo, Parul, Pang
    -  Update
        -  Operator
            -  v1aphal1 branch: specs defined, main reconciler, abstraction in placeholder. Kepler-exporter: Parul, others: Kaiyi. Preview on kepler-exporter on bare metal in the next two weeks. 
        -  Helm
            -  helm chart PR drop today. Will need review. Prometheus/grafana integration. 
            -  reviewer: Sally
    -  Next
        -  Test coverage, e2e testing
            -  pkgs that need test coverage
                -  unit test: 
                    -  power pkg, simple to implement
                    -  cgroup
                    -  complex ones: comments + TODO
                    -  simple test cases now, refactor can come later.
                    -  system level: library dependency (how to mock them?), maybe borrow from k8s mock tests.
                    -  how to run focus test: vs code ginko plugin (huamin and sam to share the command, If/focus)
                    -  
            -  basic e2e test cases
                -  we deploy workload on kind cluster
                -  validate the kepler metrics with that workload
                -  gh uses ubuntu server, manifests with ebpf, that may cause issues with kepler (lib/modules bind mount)
                -  build on ubuntu or run containerized mode. 
                -  dind vs VM on GH action: the flow of creating Fedora derived OS on GH VMs. Kind is a dind. The limitation of kind? eBPF/bcc library dependency. Sam please create issues
        
2. Questions `20min`


:::info
- **Date:** 
    - Nov. 1, 2022
- **Agenda**
1. Walk through project board `40min`
	-  Release criteria: urgent + high priority tasks done
	-  Size
	    - Size is used to determine the development time and deadline of the task
	        - XL: 1+ months
	        - L: 2 weeks - 1 month
	        - M: 1-2 weeks
	        - S: < 1 week
	    - Early PR is recommended. 
	    - If the anticipated deadline goes beyond the release date, the priority of task is lowered and may be moved to next release.
2. Logistics `10min`
    - release tracking
        - biweekly meeting (for dev)
    - release date
        - Mid Dec (tentative, Dec 16th)
    - release captain
        - tracking the tasks and PRs, create tags for the issues that have release, priority, size (Parul)
        - tags that can be reused (Marcelo)
        - document everything release captain does so the process can be reused (Sally)
        - manage PR merge
3. Development process `10min`
   - task -> issue -> design -> PR -> test -> doc
   - only task PR before release, refactor PR will be merged after release
   - when merge conflicts exist, high priority PR and small PR are merged first
   - feature PRs must have test cases (i.e. do not drop test coverage)
   - bug fixes always have high priority

- **Participants:**
    - Huamin Chen
    - Chen Wang
    - Parul
    - Sally O'Malley
    - Sam Yuan
    - Kaiyi Liu
    - Chen Ji
    - Peng Hui Jiang
    - Marcelo Amaral
    - Sunyanan Choockotkaew
    - Ken Lu
    - Ruomeng Hao

::: note
- version scheme: incremental integer, decimal, periodical release
- milestone definition: 
    - support all clouds
    - accurate of power measurement
    - support all HW (x86, arm, s390x)   
- backlog project to track new ideas that not covered in current release
## Walk through project board

:dart: Goal
---
- e2e integration
    - owner: Huamin (also include e2e test)
    - with also include operator for deployment
    - also test API (maybe with mock data and long run test with read data)
    - (GPU test will be at risk)
    - platform: cpu architecture (e.g. icelake), linux distro (issues in 6.2 kernel) (Ken)
- test coverage
    - owner: Sally
    - platform: cpu architecture (e.g. icelake), linux distro (issues 6.2 kernel) (Ken)
- documentation
    - owner: Marcelo (metrics), Parul (overall), Pang (model server/estimator)
- basic feature
    - owner: Chen Wang
- deployment
    - owner: Peng Hui Jiang (helm) and Parul and Pang (Operator)

:books: Backlog
---
- Features
- Testing
- Documentation
- Deployment

:closed_book: Tasks
--
==Importance== (Urgent - Low) / Name / **Size** (Small - X Large)
### Feature
- PRs to review
    - Low / Detect kepler is running inside VM [PR #302](https://github.com/sustainable-computing-io/kepler/pull/302) / Small
        - Not needed at the moment
    - Medium / Use local model if no model server endpoint given [PR #384](https://github.com/sustainable-computing-io/kepler/pull/384) / Medium
    - Urgent / power: switch to model based estimator when the RAPL interface is not available [PR #388](https://github.com/sustainable-computing-io/kepler/pull/388)  / Small
        - Merged
- Issues to prioritize
    - Urgent / Difference between kepler-model-server and kepler estimator [issue #375](https://github.com/sustainable-computing-io/kepler/issues/375) / X Large
    - High / Kepler general energy metrics vs energy tracing metrics [issue #365](https://github.com/sustainable-computing-io/kepler/issues/365) / X Large
        - New metrics need to propose a new design if it involves new power source
        - Need general enhancement template for new proposals (will follow up on slack)
    - Low / Kepler on VM with Hardware Counters and RAPL [issue #367](https://github.com/sustainable-computing-io/kepler/issues/367) / X Large
    - Medium / Fix BPF dependency so that Kepler can always find containers [issue #364](https://github.com/sustainable-computing-io/kepler/issues/364)
        - find a use case.
    - Urgent / end-to-end integration with model server, estimator and kepler [issue #349](https://github.com/sustainable-computing-io/kepler/issues/349)
        - ansible expert needed
-  
### Test
- [ ] 
### Document
- [ ] 
### Deployment
- [ ] 
## Notes 
<!-- Other important details discussed during the meeting can be entered here. -->
