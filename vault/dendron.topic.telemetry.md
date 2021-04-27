---
id: 84df871b-9442-42fd-b4c3-0024e35b5f3c
title: Telemetry
desc: ''
updated: 1619460642181
created: 1619460500071
---

## Overview

The term **telemetry** refers to the collection of certain usage data to help _improve the quality of a piece of software_. Dendron uses telemetry primarily for collecting usage data.

This page describes the overall telemetry approach for Dendron, what kind of data is collected and how to opt-out of data collection.

## Why does Dendron collect metrics?

Telemetry helps us better understand _how many users_ are using our products and _how often_ they are using our products. Unlike many telemetry services, our telemetry implementation is intentionally **limited in scope**.

We use telemetry to answer the following questions: 
  - how many people are actively using Dendron?
  - how performant is Dendron over time and how do new changes impact performance?
  - what features are most useful for users?

## What is not collected

Dendron will **never** collect data inside your notes. We believe that your personal knowledge is for your eyes alone. 

## What is collected

The below is a collection of common fields that are collected

|          Field | Attributes | Description                                                                            |
| -------------: | :--------: | :------------------------------------------------------------------------------------- |
|      `extensionVersion` |  _string_  | Currently installed version of the product (e.g. `1.0.0-rc0`)                          |
|      `ideVersion` |  _string_  | Currently installed version of the IDE (e.g. `1.0.0-rc0`)                          |
|      `ideFlavor` |  _string_  |  The specific IDE in question(e.g. `VSCodium`)                          |
|         `arch` |  _string_  | Client's operating system architecture (e.g. `amd64`).                                 |
|           `os` |  _string_  | Client's operating system (e.g. `darwin`).                                             |
| `nodeVersion` |  _string_  | Client's node version (e.g. `v12.12.0`).                                               |
|    `anonymousId` |  _string_  | Random, non-identifiable signature UUID (e.g. `91b014df3-9dda-4a27-a8a7-15474fd899f8`) |
|    `timestamp` |  _string_  | When the request was made   |



## When is data collected?

Data is collected in scenarios that are described below. 

### Startup 

When Dendron initializes, we collect data about on initialization time. This helps us measure the performance impact of changes that run before startup as well as improvements to our indexing performance over time. 

|          Field | Attributes | Description                                                                            |
| -------------: | :--------: | :------------------------------------------------------------------------------------- |
|      `duration` |  _number_| Number of seconds for startup
|      `numNotes` |  _number_| Number of notes across all vaults |
|      `numVaults` |  _number_| Number of vaults in workspace |
|      `noCaching` |  _boolean_| Check whether caching is disabled |


### Installation/Upgrade 
When Dendron is first installed or upgraded, we collect information about both previous and current versions. This helps us plan deprecation policies. 


|          Field | Attributes | Description                                                                            |
| -------------: | :--------: | :------------------------------------------------------------------------------------- |
|      `previousVersion` |  _string_| Previous version of Dendron |


### Telemetry Toggle
When telemetry is disabled or enabled, we collect information about the event to let us get an estimate of the number of untracked clients

## How to opt out of data collection

You can disable telemetry from Dendron either on a per-workspace level or globally. To disable on a workspace level, set [[noTelemetry|dendron.topic.config#notelemetry]] to `true` in `dendron.yml`.

To disable telemetry across all workspaces, you can run the [[Disable Telemetry|dendron.topic.commands#disable-telemetry]] command.
