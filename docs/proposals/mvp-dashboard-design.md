*This proposal template was taken from:*
[Go github repo](https://github.com/golang/proposal/blob/master/design/TEMPLATE.md)
*All credit goes to the original authors of this document.*

# Proposal: Performance Dashboard MVP

Author(s): Carlos Torres, Besan Abu Radwan, Victor Hugo Estrada

Last updated: 2017-01-12

## Abstract

We propose a dashboard/server that allows for the automated retrieval, and
display of performance tests results from any of the RPC-QE labs. This tool
will allow our team to identify performance issues and regressions as well as
facilitate the sharing of lab results with other teams.

## Background

Viewing performance test results from any of the QE labs as it trends across
time is tedious and repetitive. To view this data, the following actions must
take place:

1. Run Performance Test within Jenkins
1. Retrieve log file
1. Format data
1. User investigates data for information regarding performance issue
1. Display the data in a format that is easy to understand (graphs)
1. Share the visualizations of the tests with other developers

This set of actions occurs everytime there is a need to investigate lab
performance. These actions also requires a lot of time, meaning that by the
time the issue is resolved, it is too late to apply the solution becuase the
current release has already moved forward. Automating these actions allows more
time for developers to invest in development and investigation of performance
issues and shrinks the feedback cycle from the moment performance issues are
introduced in the code to the moment when a solution can be proposed.

Sharing these easily digestable performance results with other team members
currently requires a large portion of the team's time.  This can be minimized
by allowing other teams to have access to the dashboard/server so that they
can query the relevant test builds.

## Proposal

![alt text](../images/perf-dash-proposal-diagram.png "Perf-Dash Diagram")

### Server API

The system we propose requires the development of a server API that will be
used to serve queries that a user makes via the dashboard. To speed up the
initial development process, these queries will be hardcoded for test results.
Adding query build functionality for the user is a feature that will be
developed in future development cycles.

The server polls the data storage unit for performance test logs. The frequency of
the polling will be adjusted after implementation so that it reflects the rate
that test results enter the data storage. The server is to maintain a cache of
frequently and recently accessed data. The server expects a json result from
the data store.

This data can then be received by the dashboard.

### Dashboard

The dashboard communicates with the server using an NGINX reverse proxy. This
is needed because the dashboard and server services both sit on the same node.

## Rationale

1. Go vs. Python?
1. Angular JS 2 vs Angular JS 1?
1. Why build dashboard instead of using Grafana?

## Implementation

A description of the steps in the implementation, who will do them, and when.

## Open issues (if applicable)

A discussion of issues relating to this proposal for which the author does not
know the solution. This section may be omitted if there are none.

1. What data storage service should be used to store the test results?
1. Should the server poll the data storage unit at a set rate or should the
   data storage unit push updates whenever they occur?
1. What tool will format and display the visualization of the data?
  * D3
  * ggplot
  * Grafana
  * Some other tool?
