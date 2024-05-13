# Cloud Computing Model

## Disclaimer

This architecture decision record is a fictional document created to demonstrate how to write an ADR.

## Status

Proposed

## Context

Our product, Tesselate ™, is a platform for accessing anonymized patient data as a service in near real-time. Our deployment strategy uses a cloud-based approach. We need to choose a cloud computing model that suits our needs.

### Business Considerations

1.	This pilot program has yet to reach critical mass; Human resources are constrained to a small team.
2.	Tesselate ™ is funded but will not generate revenue until it can deliver data to our business partners. Time to Market is our most significant concern. Our management doesn’t mind us taking reasonable shortcuts as long as they are not one-way decisions.

## Decision

The Tesselate ™ team will take a hybrid approach, using a platform-as-a-service (PaaS) model.

### Rational

1.	**Constant flow of data**: The hospital’s feeds will provide constant throughput, which can result in long-running processes that lend themselves more to PaaS. FaaS is not a fit because it is better for short-lived, sporadic workloads.
2.	**Abstraction of infrastructure**: Because the team is smaller, they prefer managing as much of the infrastructure as possible without going into FaaS. We preclude FaaS because we expect constant throughput from the site with the possibility of longer workloads, which does not lend itself well to FaaS.
3.	**Scale-out preference**: Our team prefers to design components that scale horizontally, which is synergistic with PaaS.
4.	 **Cost**: adopting PaaS reduces upfront infrastructure costs because the runtime, containers, operating system, and hardware are all managed by the platform provider.

###tradeoffs

1.	**Security**: In a PaaS model, the cloud provider and the application team share the responsibility of securing the environment. This limits our vendor choices since hospital systems may require a BAA for us to satisfy HIPAA requirements.
2.	 **Vendor Lock-In**: Every Vendor implements PaaS slightly differently. Some offer proprietary services and APIs unique to them. If we rely on those features, it will be easier to migrate away from that vendor.
