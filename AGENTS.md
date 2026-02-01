# AGENTS.md - OneStop AntiBot Service

## Project Overview

This repository contains the OneStop AntiBot Service - a comprehensive solution for bypassing bot protection systems including Akamai, Kasada, DataDome, and Cloudflare. The service is designed specifically for **legal use cases** such as price scraping, market analysis, and monitoring.

## Project Structure

```
solver-akamai/
├── README.md          # Main project documentation
├── AGENTS.md          # This file - agent workspace configuration
├── .github/           # GitHub workflows and templates
│   └── PULL_REQUEST_TEMPLATE.md
└── src/               # Source code (to be added)
    ├── solvers/       # Bot detection bypass modules
    │   ├── akamai/
    │   ├── kasada/
    │   ├── datadome/
    │   └── cloudflare/
    ├── api/           # API endpoints and handlers
    ├── utils/         # Shared utilities
    └── tests/         # Test suites
```

## Tech Stack & Architecture

### Core Technologies
- **Backend:** Node.js/Python (TBD based on implementation)
- **API Framework:** Express.js/FastAPI
- **Database:** PostgreSQL (analytics), Redis (caching)
- **Monitoring:** Custom analytics via OneStopDash
- **Auth:** API key-based authentication

### Service Architecture
- **Microservice-based** approach for different solver types
- **Rate limiting** per API key
- **Health monitoring** integration with OneStopDash
- **Scalable** infrastructure for high-volume requests

## Development Guidelines

### Git Workflow
1. **🚨 ALWAYS PRIVATE** - This repo must remain private (security-sensitive)
2. **Feature branches** - Never commit directly to main
3. **Pull Requests** - All changes go through PRs with @codex review
4. **Conventional Commits** - Use `feat:`, `fix:`, `chore:`, `security:`, etc.
5. **Squash & Merge** - Keep main history clean

### Code Standards

#### Security First
- **No hardcoded credentials** - Use environment variables
- **API key validation** on every request
- **Rate limiting** per key and IP
- **Input sanitization** for all user data
- **Audit logging** for all requests

#### Performance
- **Async/await** patterns for non-blocking operations
- **Connection pooling** for database connections
- **Caching strategies** for frequently accessed data
- **Load balancing** considerations

#### Error Handling
- **Structured error responses** with consistent format
- **Proper HTTP status codes** (200, 400, 401, 429, 500, etc.)
- **Detailed logging** without exposing sensitive data
- **Graceful degradation** when solvers fail

### API Design Principles

#### Request Format
```json
{
  "solver_type": "akamai|kasada|datadome|cloudflare",
  "target_url": "https://example.com",
  "user_agent": "custom_user_agent",
  "proxy": "optional_proxy_config",
  "timeout": 30
}
```

#### Response Format
```json
{
  "success": true,
  "data": {
    "solved_token": "encrypted_token",
    "session_id": "session_identifier",
    "expires_at": "2024-02-01T12:00:00Z"
  },
  "metadata": {
    "solve_time_ms": 1234,
    "solver_version": "v1.2.3"
  }
}
```

#### Error Response
```json
{
  "success": false,
  "error": {
    "code": "SOLVER_FAILED",
    "message": "Failed to solve challenge",
    "details": "Additional context (sanitized)"
  },
  "request_id": "unique_request_identifier"
}
```

## Legal & Compliance

### Strict Legal Use Only
- **Price monitoring** and comparison services
- **Market research** and analysis
- **Public data** collection for legitimate purposes
- **Performance testing** of own services

### Prohibited Uses
- **Account takeovers** (ATO)
- **Unauthorized access** to protected systems
- **Fraud** or malicious activities
- **DDOS** or abuse of target services

### Implementation Requirements
- **Terms of Service** validation for each API key
- **Usage monitoring** and anomaly detection
- **Automatic suspension** for suspicious patterns
- **Legal compliance** logging and reporting

## Environment Setup

### Required Environment Variables
```bash
# Database
DATABASE_URL=postgresql://user:pass@host:port/db
REDIS_URL=redis://host:port

# API Configuration
API_PORT=3000
API_RATE_LIMIT=100  # requests per minute per key
JWT_SECRET=your_jwt_secret

# Solver Configurations
AKAMAI_CONFIG_PATH=/path/to/akamai/config
KASADA_CONFIG_PATH=/path/to/kasada/config
# ... additional solver configs

# Monitoring
ANALYTICS_ENDPOINT=http://81.104.34.49:8123
ONESTOP_DASH_URL=http://dashboard.url
```

### Local Development
```bash
# Install dependencies
npm install  # or pip install -r requirements.txt

# Set up environment
cp .env.example .env
# Edit .env with your configuration

# Run development server
npm run dev  # or python app.py

# Run tests
npm test  # or pytest
```

## Monitoring & Analytics

### OneStopDash Integration
- **Request tracking** by API key and solver type
- **Success/failure rates** monitoring
- **Response time** analytics
- **Error pattern** detection

### Health Checks
- **Solver availability** monitoring
- **Database connectivity** checks
- **External dependencies** status
- **Rate limit** status per key

### Alerting
- **High failure rates** (>10% in 5 minutes)
- **Slow response times** (>10 seconds average)
- **Suspicious usage patterns**
- **Service downtime**

## Testing Strategy

### Unit Tests
- **Solver modules** individual testing
- **API endpoints** validation
- **Authentication** mechanisms
- **Rate limiting** functionality

### Integration Tests
- **End-to-end** API flows
- **Database** operations
- **External service** interactions
- **Error handling** scenarios

### Load Testing
- **Concurrent requests** handling
- **Rate limit** enforcement
- **Performance** under load
- **Memory/CPU** usage patterns

## Deployment

### Production Checklist
- [ ] Environment variables configured
- [ ] Database migrations applied
- [ ] SSL certificates installed
- [ ] Rate limiting configured
- [ ] Monitoring dashboards setup
- [ ] Backup procedures tested
- [ ] Security audit completed

### Scaling Considerations
- **Horizontal scaling** with load balancers
- **Database sharding** for high volume
- **Cache invalidation** strategies
- **CDN integration** for static assets

## Support & Maintenance

### Contact Information
- **Technical Issues:** [Enquiry@jevi.dev](mailto:Enquiry@jevi.dev)
- **Discord Community:** [Join Our Discord](https://discord.gg/UFQk3hKzar)
- **Documentation:** This repository's wiki

### Maintenance Windows
- **Scheduled maintenance** during low-traffic hours
- **Emergency patches** with minimal downtime
- **Version updates** with backward compatibility
- **Security updates** prioritized immediately

## Agent Instructions

### When Working on This Project
1. **Read this file first** - understand the legal requirements
2. **Check legal compliance** before any feature addition
3. **Test security** implications of all changes
4. **Update documentation** with any API changes
5. **Monitor performance** impact of modifications

### Code Review Focus
- **Security vulnerabilities** scanning
- **Legal compliance** verification
- **Performance** impact assessment
- **API consistency** maintenance
- **Error handling** completeness

### Deployment Safety
- **Never deploy** without security review
- **Always test** in staging environment first
- **Monitor** production metrics post-deployment
- **Have rollback plan** ready
- **Document** all changes and impacts