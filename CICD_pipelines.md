# CI/CD DevOps

## Disclaimer

This architecture decision record is a fictional document created to demonstrate how to write an ADR.

## Status

Proposed

## Context

Our product, Tesselate ™, is a platform for accessing anonymized patient data as a service in near real-time. We want to
use continuous integration (CI) and continuous Deployment (CD) systems to enable an optimal development experience.

### Why is this architecturally significant?

1. This decision impacts how developers will manage code changes.
2. This decision has a measurable impact on how fast and frequently a developer can integrate changes and deploy code.
3. This decision impacts how we automate tests and builds.
4. This decision impacts the feedback loop that will notify developers of build/test results.

### Business Considerations

1. This pilot program has yet to reach critical mass; Human resources are constrained to a small team.
2. Tesselate ™ is funded but will not generate revenue until it can deliver data to our business partners. Time to
   Market is our most significant concern. Our management doesn’t mind us taking reasonable shortcuts as long as they
   are not one-way decisions.

### Decision

Our Project will use a fully managed version of TeamCity CI/CD.

### Consequences

### Alternatives Considered

1. Jenkins
2. GitHub Actions
3. Concourse CI

### Rationale

1. **Maintenance**: Because the team is more minor, we require a highly scalable solution with low maintenance overhead.
   A fully managed version of the TeamCity cloud eliminates the need to maintain our infrastructure for CI/CD.
2. **Scalability**: TeamCity features distributed builds and advanced parallelism features, such as build chains and
   dependencies. It also has many options for scaling both horizontally and vertically.
3. **Support**: TeamCity has a large, active community. JetBrains provides customer support and regular updates to the
   tool.
4. **User-Friendly Interface** TeamCity is known to be easy to use, install, and configure.

### Tradeoffs

1. **Cost**: TeamCity is costly compared to other options on this list. This could be limiting if we want to expand
   operations and onboard new developers to the project.
2. **Complexity**: There is a learning curve for using advanced features like build chains, templates, and custom
   configurations.

### Future Considerations

1. Over time, we may move to a self-hosted version of TeamCity to save on licensing costs. This will add maintenance
   overhead as DevOps teams must manage the infrastructure. However, our North Star vision is to maintain an extensive,
   distributed network for aggregating medical data, requiring a large team. At that time, licensing fees may surpass
   the cost of self-hosting and maintenance. 
