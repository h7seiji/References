# References

## Table of contents

- [Python](Python/Python.md)
- [Linux](Linux.md)

## Career

<https://80000hours.org/career-guide/>

## C++

- <https://cplusplus.com/doc/tutorial/>
- <https://medium.com/@CognitiveProgrammer/modern-c-programming-things-that-shouldnt-be-used-anymore-f7f046f09c04>

## Kubernetes

- <https://cloud.google.com/kubernetes-engine/kubernetes-comic/>

## Kafka/RabbitMQ

- <https://blog.devgenius.io/rabbitmq-vs-kafka-a-comprehensive-comparison-for-message-brokers-10ed6ac07332>

## Elasticsearch

- When to use Elasticsearch <https://towardsdatascience.com/system-design-cheatsheets-elasticsearch-673b98eebfff>

## Security

- <https://en.wikipedia.org/wiki/The_Power_of_10:_Rules_for_Developing_Safety-Critical_Code>

## Unreal Automation

- <https://horugame.com/gauntlet-automated-testing-and-performance-metrics-in-ue4/>
- <https://qiita.com/donbutsu17/items/69988ad7db88f74ea084>
- <https://edwardbeazer.com/functional-tests-with-gauntlet/>

## DDD

- <https://roluquec.medium.com/building-better-software-the-role-of-domain-storytelling-in-ddd-95091a93d89b>
- <https://code.likeagirl.io/the-ddd-way-towards-screaming-design-part-i-strategic-patterns-1079963d996b>

## Scalability

- <https://web.archive.org/web/20221030091841/http://www.lecloud.net/tagged/scalability/chrono>

## VSCode

### Navigation

-

### Extensions

#### Essentials

- Docker
- Python
  - Ruff
- GitLens
- Code Spell Checker
- markdownlint

#### Optional

### `settings.json`

`>Preferences: Open User Settings (JSON)`

```json
{
  "editor.formatOnSave": true,
  "[python]": {
    "editor.codeActionsOnSave": {
      "source.fixAll": "explicit",
      "source.organizeImports": "explicit"
    },
    "editor.defaultFormatter": "charliermarsh.ruff"
  },
  "python.analysis.typeCheckingMode": "basic",
  "explorer.confirmDragAndDrop": false
}
```

## Code Review

- Readability and maintainability: This is the first criterion and cannot be overstated enough.
- Uniform formatting: Whether the code with consistent indentation, spacing, and naming convention easy to understand?
- Testing and quality assurance: Whether it have meticulous testing and quality assurance processes?
- Boundary testing: Are we exploring extreme scenarios and boundary conditions to identify hidden problems?
- Security and performance: Are we ensuring security and performance in our source code?
- Architectural integrity: Whether the code is scalable, sustainable, and has a solid architectural design?

## Testing

- <https://tyrrrz.me/blog/unit-testing-is-overrated>
- <https://blog.xendit.engineer/stop-testing-your-code-06c46dbb6554>

- Smoke Testing: This is done after API development is complete. Simply validate if the APIs are working and nothing breaks.
- Functional Testing: This creates a test plan based on the functional requirements and compares the results with the expected results.
- Integration Testing: This test combines several API calls to perform end-to-end tests. The intra-service communications and data transmissions are tested.
- Regression Testing: This test ensures that bug fixes or new features shouldn’t break the existing behaviors of APIs.
- Load Testing: This tests applications’ performance by simulating different loads. Then we can calculate the capacity of the application.
- Stress Testing: We deliberately create high loads to the APIs and test if the APIs are able to function normally.
- Security Testing: This tests the APIs against all possible external threats.
- UI Testing: This tests the UI interactions with the APIs to make sure the data can be displayed properly.
- Fuzz Testing: This injects invalid or unexpected input data into the API and tries to crash the API. In this way, it identifies the API vulnerabilities.

## Technical Debt

- How To Deal With Technical Debt <https://medium.com/@techworldwithmilan/how-to-deal-with-technical-debt-b0065c1a794d>
- Conway's Law <https://martinfowler.com/bliki/ConwaysLaw.html>
- Technical Debt Quadrant <https://martinfowler.com/bliki/TechnicalDebtQuadrant.html>

## Management

- <https://medium.com/@rociofernn/i-have-canceled-this-type-of-meeting-and-my-team-is-thriving-4317be1081cc>
- Westrum's organization model <https://itrevolution.com/articles/westrums-organizational-model-in-tech-orgs/>

### Technical Lead vs Engineering Manager

<https://betterprogramming.pub/why-an-engineering-manager-should-not-review-code-46f87c08db66>

| Area           | Tech Lead | Eng Manager     |
|----------------|-----------|-----------------|
| Architecture   | Leads     | Weighs In       |
| Execution      | Leads     | Coaches         |
| On-Call        | Leads     | Builds Policy   |
| Bug Triage     | Leads     | Supports        |
| Team Process   | Supports  | Leads           |
| Team Strategy  | Supports  | Leads (with PM) |
| Prioritization | Supports  | Leads (with PM) |
| Stakeholders   | Supports  | Leads           |
| Career/Growth  | Supports  | Leads           |
| Hiring         | Supports  | Leads           |

### Ownership

- Accountability: Who must ensure that the work on X gets completed, and done so correctly and safely
- Responsibility: People who should be tasked with doing the actual work on X
- Expertise: People who best understand X (or some relevant component of it), often because they’ve built it, and can inform how work should be done
- Authorization: People who are able to commit or approve changes to code, data or other assets associated with X

## Misc

- How To Do Research Like A Boss <https://www.reddit.com/r/writing/comments/30tqkh/how_to_do_research_like_a_boss/>
- Google Dorking <https://medium.com/infosec/exploring-google-hacking-techniques-using-google-dork-6df5d79796cf>
- The Absolute Minimum Every Software Developer Must Know About Unicode <https://tonsky.me/blog/unicode/>
- Latency Numbers Every Programmer Should Know <https://gist.github.com/jboner/2841832>
- SDLC <https://aws.amazon.com/what-is/sdlc/>
- EC2 vs Fargate vs Lambda <https://mikaelvesavuori.medium.com/which-is-cheaper-serverless-or-servers-1b18816ce7f6>
- Diagram as Code <https://github.com/mingrammer/diagrams>
- The best design is the one where complexity is kept minimal, and where locality is kept maximum. <https://unetworkingab.medium.com/multi-threading-is-always-the-wrong-design-a227be57f107>
- 7 AI Tools Every Software Developer Needs to Know <https://alex-omeyer.medium.com/7-ai-tools-every-software-developer-needs-to-know-2023-361929746ec4>
- Estimations <https://medium.com/@techworldwithmilan/all-estimations-are-wrong-but-none-are-useful-2550586d35e6>
- Recruiter autoresponse <https://index.medium.com/career-advice-nobody-gave-me-never-ignore-a-recruiter-4474eac9556>
- <https://alex-omeyer.medium.com/9-ai-tools-every-software-developer-needs-to-try-1a3f888b52e>
- <https://ek121268.medium.com/these-are-the-top-15-essential-vscode-extensions-to-boost-your-productivity-as-a-developer-8e04f0a97f5>
- <https://medium.com/bitgrit-data-science-publication/a-roadmap-to-learn-ai-in-2024-cc30c6aa6e16>

## Backlog

- <https://blog.bitsrc.io/best-practices-for-api-security-6d8242587caf>
- <https://medium.com/@mbarkin.narin/mastering-software-system-design-advanced-problem-solving-with-layered-architectures-9647ad2b7314>
- <https://medium.com/@aserdargun/advanced-oop-in-python-a5f6130da291>
- <https://towardsdatascience.com/advanced-python-dot-operator-809d0eb5d841>
- <https://towardsdatascience.com/advanced-python-metaclasses-e32d46e0ebe3>
- <https://towardsdatascience.com/advanced-python-functions-3be6810f92d1>
- <https://newsletter.systemdesign.one/p/aws-scale>
- <https://newsletter.systemdesign.one/p/actor-model>
- <https://newsletter.systemdesign.one/p/prime-video-microservices>
- <https://newsletter.systemdesign.one/p/scalable-software-architecture>
- <https://www.youtube.com/watch?v=RrKRN9zRBWs&t=4s>
- <https://www.boot.dev/tracks/backend>
- <https://www.ryanestrada.com/learntoreadkoreanin15minutes/>
