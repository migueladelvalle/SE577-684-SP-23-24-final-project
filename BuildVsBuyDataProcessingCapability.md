# Build versus Buy data processing frameworks

## Disclaimer

This architecture decision record is a fictional document created to demonstrate how to write an ADR.

## Status

Proposed

## Context

Our product, Tesselate ™, is a platform for accessing anonymized patient data as a service in near real-time. Our
partner, HealthX, is a data management solutions company in the healthcare and life sciences space. They offer a data
processing suite. We must consider buying this suite or building data processing using open-source tools and
custom-built solutions.

## Why is this architecturally Significant?

1. **Cost, Resources, and Time to Market**: Buying a data processing suite can reduce up-front costs by reducing the
   development time required to implement our data processing layer.
2. **Expertise**: If we leverage a pre-built suite, then we get access to experts on the vendor side who already built
   and maintained the product.
3. **Scalability**: The decision will impact our solutions’ ability to scale and evolve.
4. **Maintenance and Support**: If we adopt the vendor’s suite, we can rely on them for support.

### Business Considerations

1. This pilot program has yet to reach critical mass; Human resources are constrained to a small team.
2. Tesselate ™ is funded but will not generate revenue until it can deliver data to our business partners. Time to
   market is our most significant concern. Our management doesn’t mind us taking reasonable shortcuts as long as they
   are not one-way decisions.

## Decisions

ResearchIO will build its processing capability. It will not buy it from a vendor.

## Consequences

### Rationale

1. **Strategic**: Our platform's data processing capabilities are a key value of our service offering. The senior
   leadership and strategy team want to avoid dependencies on third-party software and have the flexibility to reuse our
   processing suite freely across its ever-growing portfolio of projects.
2. **Expertise**: Our team is small but comprised of many experts in the fields of health and life sciences. We are the
   best at building out the processing of our product. This is also an opportunity to develop our core competencies
   further.
3. **Long-Term Cost Effectiveness**: Buying a processing suite upfront saves in the short term, but since processing is
   a vital part of this service offering, we want to invest more upfront to decrease our dependency on third parties and
   eliminate long-term licensing and support fees.
4. **Scalability and Flexibility**: The vendor suite is mature but has limited interoperability with any framework
   outside its proprietary language. Proprietary code is compiled and stored inside a closed-source persistence layer.
   Importing code to that persistence layer is a nontrivial process, making scaling difficult.
5. **Ability to migrate to a different solution**: The vendor’s suite uses proprietary code with limited compatibility
   with external frameworks. Nothing could be lifted and shifted if the solution needed to be migrated to an external
   framework. All logic would need to be translated into a different language or rewritten. The entire solution may need
   to be re-architected.

### Tradeoffs:

1. **Velocity**: We will need time to build out processing for the various data streams.
2. **Up-front cost**: There will be a more considerable upfront cost to develop our processing capabilities
3. **Maintenance and Support**: We will need to build our own maintenance and support capabilities, more so than if we
   had relied on a vendor product, because we lose the vendor expertise and the ability to rely on them for support. We
   are also solely responsible for our product’s ongoing updates and maintenance.

### Mitigations

1. To reduce upfront development efforts, we will not preclude open-source frameworks or limit any architectural style
   for data processing (e.g., Batch, Real-time, Event-driven, and Streaming). Where it makes sense to do so, we will
   encourage adopting and customizing Open-Source frameworks and resort to building custom solutions only if necessary.
2. We will encourage the development of reusable processing components.

### Future Considerations

1. We may reconsider buying or acquiring a vendor’s product if the product's capabilities complement our processing
   suite and it is cost-effective to do so.
