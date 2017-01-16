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

![Diagram 1](../images/perf-dash-proposal-diagram.png)

## Rationale

A discussion of alternate approaches and the trade offs, advantages, and
disadvantages of the specified approach.

## Implementation

A description of the steps in the implementation, who will do them, and when.

## Open issues (if applicable)

A discussion of issues relating to this proposal for which the author does not
know the solution. This section may be omitted if there are none.
