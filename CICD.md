# CI/CD

- <https://octopus.com/devops/>
- <https://www.jetbrains.com/teamcity/ci-cd-guide/ci-cd-best-practices/>
- <https://www.linkedin.com/pulse/20-devops-interview-questions-every-engineer-should-know-alex-muradov-wtome/>

## Do

- Treat your infrastructure as code:
  - Use version control for your infrastructure code.
  - Make use of bug tracking/ticketing systems.
  - Have peers review changes before applying them.
  - Establish infrastructure code patterns/designs.
  - Test infrastructure changes like code changes.
- Put developers into integrated teams of no more than 12 self-sustaining members.
- Have all developers commit code to the main branch frequently, with no long-running feature branches.
- Consistently adopt a build system such as Maven or Gradle across your organization and standardize builds.
- Bake security into your code pipeline.
- Have developers build unit tests toward 100% coverage of the code base.
- Ensure that unit tests are 70% of the overall testing in duration, number, and scope.
- Ensure that unit tests are up-to-date and not neglected. Unit test failures should be fixed, not bypassed.
- Treat your continuous delivery configuration as code.
- Establish role-based security controls (that is, who can do what and when):
  - Monitor/track every resource possible.
  - Alert on services, availability, and response times.
  - Capture, learn, and improve.
  - Share access with everyone on the team.
  - Plan metrics and monitoring into the lifecycle.
- Keep and track standard metrics:
  - Number of builds.
  - Number of deployments.
  - Average time for changes to reach production.
  - Average time from first pipeline stage to each stage.
  - Number of changes reaching production.
  - Average build time.
- Use multiple distinct pipelines for each branch and team.

## Don’t

- Have long-running branches with large complicated merges.
- Have manual tests.
- Have manual approval processes, gates, code reviews, and security reviews.

## Comment

Having gone back and forth between product dev and platform/ops a few times I can tell you a few things that consistently frustrate me when I’m on the dev side.

The common theme in all these is that automation and configuration should be checked into repos, readable by as many engineers as possible, and largely open to contributions from outside the ops and security teams.

- Lack of access to prototype my own deployment solutions. If I’m forced to submit tickets and wait days to get a new staging setup for something speculative that’s not even fully figured out yet, we won’t get far with new product ideas. Common failure mode here is an ops team requiring all deploys go through their pet terraform modules, ansible playbooks, or helm charts but not allowing the rest of engineering the ability to meaningfully improve the situation when the current abstractions start to fall over.

- Lack of visibility to debug my own production problems. If we can’t have logs, metrics, and traces in staging and production I’m going to have a bad time.

- Lack of access to a “break glass” function for shelling into a misbehaving container or server in order to run some exploratory commands. If when can’t see a clear answer in our logs to a mysterious networking issue then it’s time to fire up netcat, dig, tcpdump, etc. Please make that possible or at least provide ready access to an SRE who will do that for me in a timely fashion.

- Lack of agency over build and deploy tooling. If my CI pipelines are only editable by a separate team they’d better be running on the order of seconds to a few minutes, with clear logging, ability to capture artifacts, and an eye towards minimizing rebuilds and external dependencies.

- Lack of scaling options. If you’re going to push everyone into a specific production hosting style, make sure we can add more app servers quickly when needed AND that we can scale a server vertically when that’s the right call.
