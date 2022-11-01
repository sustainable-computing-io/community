Kepler Release 0.4 Planning
===

###### tags: `kepler` `release`

:::info
- **Date:** 
    - Nov. 1, 2022
- **Agenda**
1. Walk through project board `40min`
	-  Release criteria: urgent + high priority tasks done
	-  Size
	    - Size is used to determine the development time and deadline of the task
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
   - issue -> design -> PR -> test -> doc
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

::: note
- version scheme: incremental integer, decimal, periodical release
- milestone definition: 
    - support all clouds
    - accurate of power measurement
    - support all HW (x86, arm, s390x)   

## Walk through project board

:dart: Goal
---
- e2e integration
    - owner: Huamin (also include e2e test)
    - with also include operator for deployment
    - also test API (maybe with mock data and long run test with read data)
    - (GPU test will be at risk)
- test coverage
    - owner: Sally
- documentation
    - owner: Marcelo (metrics), Parul (overall)
- basic feature
    - owner: Chen Wang
- deployment
    - owner: Peng Hui Jiang (helm) and Parul (Operator)

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
- [ ] 
### Test
- [ ] 
### Document
- [ ] 
### Deployment
- [ ] 
## Notes 
<!-- Other important details discussed during the meeting can be entered here. -->
