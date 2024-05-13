# Centralized Versus Decentralized broker

## Disclaimer

This architecture decision record is a fictional document created to demonstrate how to write an ADR.

## Status

Proposed

## Context

Our product, Tesselate ™, is a platform for accessing anonymized patient data as a service in near real-time. An
architecturally significant decision is whether we use a centralized or decentralized message broker.

### Why is this architecturally significant?

1. This decision has a measurable impact on scalability.
2. This decision has a quantifiable effect on operational complexity and management.
3. This decision has a measurable impact on security management.
4. This decision has a quantifiable effect on Data consistency and integrity.

### Business Considerations

1. This pilot program has yet to reach critical mass; Human resources are constrained to a small team.
2. Tesselate ™ is funded but will not generate revenue until it can deliver data to our business partners. Time to
   Market is the most significant concern for us. Our management doesn’t mind us taking reasonable shortcuts as long as
   they are not one-way decisions.

## Decisions

Research IO will implement a centralized broker.

## Consequences

### Rationale

This is a short-term decision. Deploying a centralized broker is better because:

1. **Single Point of Control**: A centralized message broker is easier for a small team to monitor and manage.
2. **Easier Security**: A single point of control means security measures can be more straightforward and Robust but
   easier to manage.
3. **Delaying difficulties with data integrity and consistency**: Designing a distributed broker means tackling issues
   with data consistency. This would unnecessarily increase lead time for a small team, considering our pilot program
   only consists of a few partners, and the benefits of a distributed system aren’t as pronounced in a smaller group.

### Tradeoffs

1. **Single Point of Failure**: A centralized message broker creates a single point of failure capable of hindering our
   entire system.
2. **Scalability**:  Centralized Message Brokers are difficult to scale horizontally. This is okay in the short term
   since we have a smaller network.
3. **Potential Bottleneck**: Our initial TPS is expected to peak at 650 TPS under abnormal conditions and is around 250
   TPS during normal operating conditions. Early prototyping has shown that we can handle this load. However, as the
   network grows, this will become a performance bottleneck.

### Mitigations

1. To address the single point of failure, we will deploy multiple message broker instances in a Multi-Region,
   Multi-Datacenter setup. We will use chaos testing to ensure that if one region/data center goes down, we will
   seamlessly scale to another region/data center.
2. To prevent bottlenecks in the short term, we will deploy multiple message broker instances and split traffic by
   region.

### Future Considerations

1. Our North Star vision for Tesselate ™ is an extensive, distributed network from which consumers can aggregate
   results. A centralized broker is limited by its ability to scale horizontally. In the short term, this is okay
   because we have a small network, but when this program reaches critical mass and wants to expand, we will need to
   re-architect the message broker.