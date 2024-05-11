# Seperate Concerns for Data Processing and Storage from Integration Engine

## Disclaimer

This architecture decision record is a fictional document created for the purpose of demonstrating how to write an ADR.

## Status

Proposed

## Context

Our company, ResearchIO, is developing a new platform for retrieving real-time clinical data. We have partnered with
InterSystems and are using HealthShare as an integration engine. While the technology has many special features, we must
decide whether to couple our solution by using its built-in tools for data processing or create a layer of separation to
delineate data retrieval and indexing from processing and storage. Our decision will be driven by whatever allows us to
go to market the fastest while enabling flexibility for future changes.

## Decision

We will create a layer of separation between the HealthShare integration engine and our data processing and storage.

## Consequences

### Rationale

A layer of separation is the preferred approach because:

1. Flexibility: HealthShare has a built-in integrated development environment and a toolchain, making it possible to
   build an entire system from front end to back end. The toolchain uses a proprietary programming language called
   ObjectScript, which has limited compatibility with other technologies. By separating the concern of retrieval and
   indexing, which is HealthShare’s forte as an integration engine, from processing and storage, we get greater
   flexibility with how we want to process our data.
2. Ability to migrate to a different solution—If we cannot use HealthShare as an integration engine, we need a different
   solution for retrieving and indexing data. We retain our processing and storage capabilities, which minimizes the
   impact.

### Tradeoffs:

1. Velocity: Setting up a separate layer to build processing from scratch will take time and effort and introduce
   development time and cost compared to using an existing tool with mature features. This means sacrificing time and
   money to create more options while being less tightly coupled with HealthShare.
2. Maintenance and Support: By offloading processing and storage to a separate layer, we lose vendor support and
   introduce responsibility for the layer’s ongoing updates, maintenance, and support.