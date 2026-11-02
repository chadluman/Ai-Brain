---
name: feature-flag-rollout-design
description: Design and review feature flags, kill switches, gradual rollouts, canaries, entitlement gates, experiment assignments, configuration changes, and flag retirement. Use when code deployment must be separated from behavior exposure or blast radius must be controlled.
---

# Feature Flag and Rollout Design

## Outcome

Create a controlled, observable, reversible rollout with deterministic evaluation, safe defaults, bounded administrative authority, and a mandatory path to remove temporary flag debt.

## Required Inputs

- change, affected journey, users or workloads, risk, dependencies, and expected duration
- evaluation location, targeting attributes, identity stability, latency, availability, and privacy needs
- exposure steps, control group, success and guardrail signals, owner, and decision schedule
- failure behavior, cache and propagation delay, offline behavior, provider limits, and rollback needs
- entitlement, experiment, operations, or emergency purpose and audit requirements

## Safety and Permission Constraints

- A flag is a production control plane. Restrict change access, use strong authentication, log changes, review broad targeting, and protect SDK or service credentials.
- Do not put secrets or unnecessary personal data in flag configuration or evaluation context. Server-enforce security and paid entitlements; a client flag is not authorization.
- Define the safe default for missing, stale, invalid, timed-out, or unreachable flag data. Emergency controls must work during dependency failure.
- A production targeting change, experiment exposure, paid entitlement change, or global kill switch is R3 and requires immediate authorization, observable thresholds, and recovery steps.
- Flags do not replace tests, compatible data migrations, or deploy rollback. Old and new paths may both need support through the rollout.

## Workflow

1. Classify the flag as release, operational, experiment, permission or entitlement, or long-lived configuration. Reject a flag when a normal versioned configuration or deployment is clearer.
2. Record owner, purpose, creation date, default, environments, target population, dependencies, expiry date, removal issue, and emergency authority.
3. Define stable evaluation context and privacy-minimized attributes. Specify server or client evaluation, cache, propagation, consistency, and provider-outage behavior.
4. Ensure both paths preserve authorization, accessibility, data integrity, performance, observability, and schema compatibility.
5. Predefine exposure stages, dwell time, sample or cohort, user and system guardrails, success thresholds, automatic pause, manual stop, and rollback.
6. Test default, on, off, stale, malformed, missing, rapidly changed, cross-device, anonymous-to-signed-in, and dependency-failure behavior.
7. Roll out to the smallest useful cohort, compare with a control where appropriate, and increase exposure only after the observation gate.
8. Decide ship, revise, or stop. Remove the losing path, flag checks, configuration, unused telemetry, and provider objects by the expiry date.

## Required Output

- flag classification, contract, owner, expiry, and safe default
- evaluation, privacy, caching, consistency, and outage design
- exposure stages, approval gates, success metrics, guardrails, and stop rules
- test and canary evidence by path and failure state
- rollback, emergency operation, audit, and communications plan
- cleanup change and verification that temporary paths are removed

## Completion Gate

Do not call a rollout complete while the temporary flag or losing code path remains without a justified long-lived owner, and do not expand exposure when guardrails, evaluation integrity, or rollback are unverified.

## Conditional Reference

Read [Flag and Rollout Evidence](references/flag-rollout-evidence.md) when choosing a flag interface, canary evaluation, or rollout gates.
