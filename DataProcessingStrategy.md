# Data processing Strategy

## Disclaimer

This architecture decision record is a fictional document created to demonstrate how to write an ADR.

## Status

Proposed

## Context

Our product, Tesselate ™, is a platform for accessing anonymized patient data as a service in near real-time. As a part
of our design process, we need a strategy for processing data at scale.

We have partnered with HealthX, a data management solutions company in the healthcare and life sciences space. Their
integration engine allows us to pull data from various hospital source systems using protocols like FHIR, HLL7, DICOM,
and more. The integration engine will pass that data to us for processing.

### Key Functional considerations

1. Our processing mechanism will receive this data in various formats and must redact Personal Identity Information to
   anonymize the data.
2. Our processing must associate that data with an anonymous identity.
3. Each hospital will require a core set of the same and custom processing to remove PII data from site-specific
   locations.
4. Our processing will store the data in some persistence layer.

### Key Considerations

1. Our processing strategy must allow us to achieve the functionality above in a manner that favors horizontal scaling.
2. Our processing strategy must allow modular and reusable functions across multiple hospital deployments.
3. Our deployment strategy must allow us to define clear contextual boundaries around specific functions so that they
   can be managed and maintained.

## Decisions

Use the Microservice architecture style as a reference for designing and deploying data processing components.

### Rationale

1. **Modularity and Reusability**: Each Microservice can encapsulate a specific hospital’s processing logic. Functions
   within those services could be written so they are modifiable/ reusable at other sites.
2. **Service Boundaries**: clear boundaries are defined for each microservice.
3. **scalability**:  Microservices can be deployed in a disposable manner that favors scaling out (Horizontal scaling).

### Tradeoffs

1. **complexity**: Adopting a Microservice approach means managing many artifacts, requiring a repository, a CI/CD
   pipeline, tests, documentation, and more. This complexity can place a serious burden on a team.
2. **Costs**: Increased complexity means higher operational costs.
3. **Debugging is harder**: Each Service will have its logs to investigate whenever a failure occurs.

### Mitigations

1. Reduce Artifacts by grouping microservice setups by data source.
2. Where possible, share data sources.  
