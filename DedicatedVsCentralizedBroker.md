# Dedicated vs Centralized Broker

## Disclaimer

This architecture decision record is a fictional document created for the purpose of demonstrating how to write an ADR.

## Status

Proposed

## Context

Our company, ResearchIO, recently partnered with InterSystems on a Pilot program for the Tesselate platform. This
partnership allows ResearchIO to access its HealthShare Health Connect product as a Broker at a significant discount.
For our pilot program, we must choose whether to deploy Healthshare as a centralized broker or to have dedicated
instances of it on a per-hospital basis. Our decision will be driven by whatever allows us to go to market the fastest
while enabling flexibility for future changes.

Deploying a centralized broker would allow us to be more agile in the short term as we pilot this program for the first
batch of partners because we would only need to manage a single multi-tenant instance. However, prospective clinical
partners are wary of a multi-tenant setup. Another consideration is that managing integrations on a single instance will
increase overhead as we add sources in the long term. This is a factor we need to carefully consider in our
decision-making process, as it could impact the scalability and efficiency of our operations.

Deploying dedicated brokers would be more attractive to potential clinical partners because of the isolation and
security it provides. However, this deployment type requires managing separate instances, which may split the available
developers between managing instances and new development. The dedicated approach also increases our hosting and
maintenance costs. There is also a risk of underutilization, where clinical partners don’t upload enough data.

## Decisions

ResearchIO will implement a centralized broker as a preferred approach while delaying development for prospective
clinical partners requiring a dedicated instance.

## Consequences

### Rationale

A centralized broker is the preferred approach because:

•    **Velocity**: In the short term, we can dedicate the most resources to new development and integrating clinical
partners if we have less overhead for managing the HealthShare Instances. More instances mean more overhead.

•    **Stability**: Core updates can be managed more easily in application namespaces than by pushing out changes to
different application instances.

•    **Business Oppurtunity**: • Due to regulatory concerns, not offering dedicated instances was a showstopper for some
clinical partners. As we advance, it must be maintained as an option to avoid alienating potential partners and losing
their interest.

### Tradeoffs considered.

•    **Complexity**: Having two deployment styles adds complexity to the architecture.

• Single point of failure for the dedicated instance

### Mitigation Strategies

• The business will prioritize development for partners onboarding to the centralized instance. When enough partners
express interest in dedicated servers, we will revisit this decision to discuss switching. This will allow the program
to reach critical mass before further investment.

• We will need a multi-Region, multi datacenter clone to mitigate having a single broker instance.

### Future Considerations

• As the system evolves, we must reconsider moving to dedicated instances if the complexity of maintaining a single
centralized broker becomes too much to manage.