# API Design Strategy: REST vs GraphQL

- **Status:** Accepted
- **Date:** 2026-04-13
- **Work Item:** PROJ-456-API-Design

## Context and Problem

We are building a new customer management API for our SaaS platform. The API will serve two primary clients:
1. **Mobile application** (iOS and Android) with limited bandwidth and battery constraints
2. **Web dashboard** for customer service representatives requiring rich data displays

Our development team consists of 5 engineers:
- 3 senior developers with 5+ years of REST API experience
- 2 mid-level developers with 2 years experience, new to GraphQL but motivated to learn modern API patterns

We need to make a strategic decision on API design approach that balances:
- Time-to-market (8-week delivery target)
- Long-term maintainability
- Client performance requirements
- Team learning investment

## Decision Drivers

- **Performance and latency requirements** for mobile clients (reducing network round trips is critical)
- **Flexibility in data fetching** to accommodate different needs between mobile and web clients
- **Team expertise and learning curve** (3/5 developers have deep REST experience)
- **API versioning and evolution strategy** (need to avoid endpoint proliferation)
- **Tooling and ecosystem maturity** (developer experience, debugging, monitoring)
- **Timeline constraints** (8 weeks to initial release)
- **Future scalability** (API will grow to serve 5+ additional client applications)

## Considered Options

1. **REST API** (traditional RESTful design)
2. **GraphQL API** (schema-driven, query-based approach)
3. **Hybrid approach** (REST for simple resources, GraphQL for complex queries) — *Rejected early due to maintenance complexity*

## Decision Outcome

Chosen option: **"GraphQL API"**, because it provides superior flexibility for mobile and web clients by allowing each to fetch exactly the data they need in a single request. This reduces the number of API calls, improves mobile app performance, and provides a schema-driven development model that serves as living documentation.

While there is an initial learning investment for 2 team members and setup time for GraphQL tooling, the team's motivation and the long-term benefits of schema-driven development justify the choice. The 8-week timeline is achievable with proper training allocation (1 week) and incremental delivery.

#### Consequences

- **Good, because** mobile app performance improves significantly by reducing network round trips (fetch entire user profile + orders + preferences in one query vs. 3-4 REST calls)
- **Good, because** web dashboard can request exactly the data it needs for each view, eliminating over-fetching and under-fetching issues
- **Good, because** the GraphQL schema provides strong typing and serves as living API documentation (auto-generated docs via GraphiQL)
- **Good, because** it reduces backend logic complexity for handling multiple client types (clients specify their data needs rather than backend creating multiple endpoints)
- **Good, because** schema evolution is more flexible than REST versioning (additive changes don't break existing clients)
- **Bad, because** initial setup time increases by approximately 2 weeks (tooling configuration, team training, schema design)
- **Bad, because** caching strategy requires careful design (cannot rely on standard HTTP caching mechanisms as easily as REST)
- **Bad, because** debugging and monitoring require GraphQL-specific tools (Apollo Studio, GraphQL Playground)
- **Bad, because** query complexity limits must be implemented to prevent expensive queries from impacting system performance
- **Neutral, because** the learning investment for 2 team members will pay dividends in future projects (transferable skill)

#### Implementation

1. **Week 1:** 
   - Set up Apollo Server (Node.js) as GraphQL runtime
   - Configure development environment and tooling (GraphiQL, Apollo Studio)
   - Conduct team training session on GraphQL fundamentals (schema design, queries, mutations)
   
2. **Weeks 2-3:** 
   - Design initial GraphQL schema (types: User, Order, Product, CustomerService)
   - Implement resolvers for core queries (getUser, listOrders, searchProducts)
   - Set up authentication and authorization middleware (JWT-based, integrated with existing auth system)

3. **Weeks 4-6:**
   - Develop mobile client integration (React Native with Apollo Client)
   - Develop web dashboard integration (React with Apollo Client)
   - Implement query complexity analysis and rate limiting
   - Configure caching strategy (Redis for resolver-level caching)

4. **Weeks 7-8:**
   - Performance testing and optimization (identify N+1 query issues, implement DataLoader)
   - Security review (query depth limiting, cost analysis)
   - Staging deployment and client testing
   - Production deployment with monitoring (Apollo Studio, CloudWatch metrics)

#### Confirmation

Success will be confirmed by:
1. **Performance metrics:** Mobile app API latency < 200ms (p95), web dashboard < 150ms (p95)
2. **Developer velocity:** New features require fewer backend changes (clients can query existing schema fields in new combinations)
3. **Team competency:** All 5 developers can confidently write queries, mutations, and resolvers within 4 weeks
4. **Documentation quality:** Schema serves as primary API documentation (no separate wiki maintenance)
5. **Client satisfaction:** Mobile team reports improved data fetching efficiency

#### Stakeholders

- **Mobile Development Team** (primary client, prioritizes performance and data efficiency)
- **Web Development Team** (primary client, prioritizes flexibility and rapid iteration)
- **Backend Engineering Team** (implementers, responsible for schema design and resolver performance)
- **Product Management** (timeline constraints, feature prioritization)
- **DevOps Team** (deployment, monitoring, infrastructure for GraphQL server)
- **Security Team** (authentication, authorization, query security)

## Pros and Cons of the Options

### REST API

- **Good, because** the team has extensive experience (3 out of 5 developers have 5+ years REST expertise)
- **Good, because** tooling and ecosystem are mature and well-documented (Postman, Swagger, extensive community resources)
- **Good, because** HTTP caching mechanisms are straightforward (standard Cache-Control headers, CDN integration)
- **Good, because** it's a well-understood pattern for most developers (lower onboarding risk for future hires)
- **Bad, because** mobile clients will require multiple requests to fetch related data (e.g., user profile requires separate calls for /users/:id, /users/:id/orders, /users/:id/preferences → N+1 problem)
- **Bad, because** API versioning can lead to endpoint proliferation over time (/api/v1/users, /api/v2/users, /api/v2/users/extended)
- **Bad, because** clients often receive more data than they need (over-fetching) or need multiple calls to assemble a view (under-fetching)
- **Bad, because** maintaining multiple endpoints for different client needs creates backend complexity

### GraphQL API

- **Good, because** clients can fetch exactly the data they need in a single request (mobile: `query { user { id, name, orders { id, total } } }`)
- **Good, because** the schema provides strong type safety and serves as living documentation (auto-generated API docs)
- **Good, because** schema evolution is additive (new fields don't break existing clients, backward compatibility by default)
- **Good, because** it reduces backend logic complexity for handling multiple client types (clients specify their data needs declaratively)
- **Good, because** introspection enables powerful developer tools (GraphiQL, Apollo Studio, auto-complete in IDEs)
- **Neutral, because** 2 team members are new to GraphQL, but the team has requested training and is motivated to learn modern API patterns
- **Bad, because** there is a learning curve for team members unfamiliar with schema-driven development (estimated 1-2 weeks to proficiency)
- **Bad, because** caching is more complex than standard HTTP caching (requires resolver-level caching, normalized cache on client)
- **Bad, because** query complexity must be actively managed (implement query depth limits, cost analysis, rate limiting)
- **Bad, because** debugging and monitoring require GraphQL-specific tools (Apollo Studio, custom logging for query performance)
- **Bad, because** initial setup time is higher than REST (Apollo Server configuration, schema design, resolver implementation)

### Hybrid Approach (REST + GraphQL)

- **Good, because** allows gradual migration (start with REST, add GraphQL for complex queries)
- **Good, because** leverages existing REST expertise while introducing GraphQL incrementally
- **Bad, because** maintaining two API paradigms increases complexity (two documentation systems, two monitoring approaches)
- **Bad, because** clients must understand when to use REST vs. GraphQL (inconsistent developer experience)
- **Bad, because** team must maintain expertise in both approaches (cognitive overhead)
- **Decision:** Rejected early in analysis due to maintenance burden and inconsistent client experience

## More Information

### Related Decisions
- **ADR-0003:** Use Azure Cloud for infrastructure (GraphQL server will deploy to Azure App Service)
- **ADR-0012:** JWT-based authentication (GraphQL mutations will validate JWT tokens via middleware)

### References
- [GraphQL Best Practices](https://graphql.org/learn/best-practices/)
- [Apollo Server Documentation](https://www.apollographql.com/docs/apollo-server/)
- [REST vs GraphQL Analysis (Internal Wiki)](https://wiki.company.com/architecture/rest-vs-graphql)

### Assumptions
- Mobile clients have modern HTTP/2 support (required for GraphQL batching optimization)
- Team can allocate 1 week for GraphQL training without impacting 8-week delivery timeline
- Existing authentication system (JWT) can integrate with GraphQL middleware
- Redis is available for resolver-level caching (already in infrastructure)

## Follow-On Information

- **Next Review Date:** 2026-10-13 (6 months post-implementation)
- **Success Metrics to Track:**
  - API latency (p50, p95, p99)
  - Number of queries per client session (should decrease vs. REST baseline)
  - Developer velocity (time to implement new features)
  - Schema evolution rate (frequency of breaking vs. non-breaking changes)

## Record History

* **Proposed**: 2026-04-10
* **Accepted**: 2026-04-13
* **Last Reviewed**: N/A
* **Deprecated**: N/A
* **Superseded by**: N/A
* **Date Superseded**: N/A
* **Archived:** N/A
