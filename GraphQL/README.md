### Description

GraphQL is a data query language developed by Facebook and publicly released in 2015.
It is an alternative to REST API. This article concludes some techniques which can be used to test the implementation of GraphQL. Thanks to Doyensec.

### Basics

The following is how a basic GraphQL query is defined (response-type: JSON)
```
query {user{id email firstName lastName}}
```
- There is an electron-based IDE for exploring GraphQL API's
github.com/andev-software/graphql-ide

The following keywords should be kept in mind when searching for GraphQL interaction
```
graphql.php, /graphql, /graphiql
graphql/console
graphql.php?debug=1
```
There is a little tool which enumerates GraphQL endpoints: [github.com/doyensec/graph-ql](https://github.com/doyensec/graph-ql).
Queries should be intercepted and checked for: Broken Access Controls, IDOR, SQL/No-SQL Injections and Information Disclosure.   
Nested Queries like:
```
query {stories{title body comments{ [ ... ] }}}}}}}
```
Can exhaust the backend server and create a DoS.  
It might be also helpful to guess certain attributes which are not delivered by the request itself. 

### Examples

**H1: 291531**
Using an introspection query to reveal the defined system with all required details (thanks to craigbeck):
```
https://gist.githubusercontent.com/craigbeck/b90915d49fda19d5b2b17ead14dcd6da/raw/e50819812a7a8a95b303ac0ea1464e2679e3e4bc/introspection-query.graphql
```

**H1: 342978**
Information disclosure (number of whitelisted hackers) due a specific query:
```
{"query": "query {team(handle:\\"security\\"){id,name,handle,whitelisted_hackers{total_count}}}"}
```

**H1: 283847**
The GraphQL token (`X-Auth-Token`) didn't expire so the user was able to change the password even if the affected account singed out.

**H1: 276174**
It was possible to access restricted information by smuggling in an additional parameter into the GraphQL request:
```
POST
{currentUser {email currentAccount {name capabilities {name [ ... ]
---
POST
{currentUser {email currentAccount {name licenseKey capabilities {name [ ... ]
```
