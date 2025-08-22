# ADR-001: Authentication Strategy - NextAuth Now, Ory Kratos Later

Date: 2025-08-22
Status: Accepted
Authors: Claude (AI Assistant), Taagero3

## Context

Rush2.ai requires a multi-tenant authentication system that supports:
- Social logins (Google, Apple, Facebook)
- Multi-tenant workspace isolation
- API key management for server-to-server auth
- Future enterprise SSO (SAML/OIDC)
- Per-tenant rate limiting
- Audit logging for compliance

## Decision

We will use a **phased approach**:
- **Phase 1 (MVP)**: NextAuth.js for user authentication
- **Phase 2 (Enterprise)**: Add Ory Kratos alongside NextAuth when needed

## Rationale

### Why NextAuth First:

1. **Immediate needs met (80% coverage)**:
   - Social logins work out of the box
   - User sessions and JWT tokens
   - Basic multi-tenancy with workspace switching
   - Magic links for email-only users
   - Quick 30-second onboarding flow

2. **Faster time to market**:
   - NextAuth integrates seamlessly with Next.js
   - No additional infrastructure needed
   - Well-documented, battle-tested
   - Can launch MVP within days, not weeks

3. **Simpler operations**:
   - Single PostgreSQL database
   - No separate identity service to maintain
   - Lower complexity for small team

### Where NextAuth Falls Short:

1. **API Key Management** - Doesn't handle machine-to-machine auth
2. **Per-tenant rate limiting** - Requires custom implementation
3. **Enterprise SSO (SAML)** - Only supports OAuth, not SAML
4. **Service accounts** - Temporal workflows need service identity
5. **Advanced RBAC** - Basic roles only

### Why Not Ory Kratos Now:

1. **Operational overhead** - Separate service to deploy and maintain
2. **Over-engineering** - Enterprise features not needed for MVP
3. **Complexity** - Steeper learning curve
4. **Cost** - Additional infrastructure costs

## Implementation Plan

### Phase 1 (Current):
```
Database: Single PostgreSQL on Railway
├── NextAuth tables (users, accounts, sessions)
├── Application tables (workspaces, members)
├── Custom API keys table
└── Redis for rate limiting
```

### Custom API Key Implementation:
```typescript
model ApiKey {
  id          String    @id @default(cuid())
  workspaceId String
  name        String
  key         String    @unique // hashed
  scopes      String[]  // ['read:content', 'write:content']
  lastUsedAt  DateTime?
  expiresAt   DateTime?
  createdAt   DateTime  @default(now())
  revokedAt   DateTime?
  
  workspace   Workspace @relation(fields: [workspaceId], references: [id])
}
```

### Phase 2 (When Needed):
Add Ory Kratos when we have:
- Enterprise customers requiring SAML
- Complex delegation workflows
- Regulatory compliance requirements
- 1000+ workspaces

Migration strategy:
1. Run both systems in parallel
2. New enterprise users → Ory Kratos
3. Existing users stay on NextAuth
4. Gradual migration with feature flags

## Consequences

### Positive:
- ✅ Faster MVP launch
- ✅ Lower initial complexity
- ✅ Proven solution for common use cases
- ✅ Easy migration path available
- ✅ Cost-effective for startup phase

### Negative:
- ⚠️ Technical debt for API key management
- ⚠️ Custom rate limiting implementation needed
- ⚠️ Future migration complexity
- ⚠️ No SAML support initially

### Mitigations:
- Build API key system with clean interfaces
- Document all custom auth code thoroughly
- Design database schema to support future migration
- Keep auth logic loosely coupled

## Database Requirements for Railway

Based on this decision, we need:

1. **PostgreSQL with pgvector extension**
   - All auth data (NextAuth tables)
   - Application data (workspaces, content)
   - Vector embeddings for AI features
   - Custom API keys table

2. **Redis**
   - Rate limiting (token buckets per tenant)
   - Session caching
   - Temporary data for workflows

## Review Notes

This decision prioritizes speed to market and operational simplicity over comprehensive enterprise features. The phased approach allows us to validate the product with real users before investing in complex identity infrastructure.

The key insight: "Don't let perfect be the enemy of good."

## References

- [NextAuth.js Documentation](https://next-auth.js.org/)
- [Ory Kratos Documentation](https://www.ory.sh/kratos/)
- [Rush2.ai PRD](../PRD/rush2ai.prd)
- [Multi-tenant SaaS patterns](https://aws.amazon.com/blogs/database/multi-tenant-saas-patterns/)