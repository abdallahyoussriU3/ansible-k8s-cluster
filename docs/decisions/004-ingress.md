# ADR 004: Ingress and North-South Traffic

- Status: Proposed
- Date: 2026-10-03

## Context

The project must eventually expose services externally in a secure, maintainable, and scalable way without exposing every service directly via NodePort.

## Decision

Do not select a production ingress implementation until the actual networking model and public exposure constraints are reviewed. The default direction is a modern ingress or Gateway API-oriented approach, with TLS automation planned as a later phase.

## Alternatives considered

- NodePort for all services
- NGINX Ingress
- Gateway API with an Envoy-based implementation
- Traefik

## Reason

NodePort is acceptable only for early testing, but it is not a long-term architecture. A gateway or ingress design should be evaluated once the public IP and firewall model is clear.

## Consequences

- initial cluster design remains intentionally minimal
- ingress is expected to be added later, not during the first bootstrap
- security rules must be locked down before external service exposure

## Open question

The final ingress stack depends on whether the environment supports cleaner public IP exposure and DNS patterns.
