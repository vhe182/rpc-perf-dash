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

The server polls the data storage unit for performance test logs. The frequency
of the polling will be adjusted after implementation so that it reflects the
rate that test results enter the data storage. The server is to maintain a
cache of frequently and recently accessed data. The server expects a json
result from the data store.

This data can then be received by the dashboard.

### Dashboard

The dashboard serves the purpose of allowing the user to make queries of the
results stored in the data storage unit. The dashboard provides a simple user
interface with a list of drop down menus for options such as: lab, config,
test, run, and metric. The dashboard communicates with the server (both
running on the same node) using an NGINX reverse proxy.

The query is made via HTML requests in the form of `GET /api/labs`,
`GET /api/labs/{lab id}`. The expected result is a json with the appropriate
test data. This json is then used to create the graph of the specified metrics
as they trend over the past 50 builds.

Our choice of developing a REST API provides the benefit that any graph
configured by a user can be sured via the URL link to that page.  This allows
for the fast sharing of performance test results between team members and
other teams.

## Rationale

1. Go vs. Python?
1. Angular JS 2 vs Angular JS 1?
1. Why build dashboard instead of using Grafana?

## Implementation

A description of the steps in the implementation, who will do them, and when.

### Writing the server API

Upon approval, tasks will be identified and given to the performance team.

### Building the dashboard

Upon approval, tasks will be identified and given to the performance team.

## Open issues (if applicable)

1. What data storage service should be used to store the test results?
  * The performance team has previously used [InfluxDB][1] to handle database
    duties. InfluxDB is well-suited to the task due to its optimization for
    time-series data. The perf team has also used it before so they are
    already familiar with the InfluxDB libraries.
  * Test results can be stored in files and orderedd in a series of
    directories. This method would require minimal setup and can be easily
    ported to another data storage system. An issue with this strategy is that
    the data will have to all follow the same formatting standards, this adds
    complexity and added time that the perf team will need to develop a format
    that can accomodate all of the KPIs and their varying metrics.
1. Should the server poll the data storage unit at a set rate or should the
   data storage unit push updates whenever they occur?
1. What tool will format and display the visualization of the data?
  * [D3][2]
  * [Angular Chart][3]
  * [Grafana][4]
  * Other tool?

[1]: https://www.influxdata.com/
[2]: https://d3js.org/
[3]: http://jtblin.github.io/angular-chart.js/
[4]: https://grafana.net/tour
