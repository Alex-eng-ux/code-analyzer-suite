# Severity Rating Guidelines

## Severity Levels

Every issue identified during code analysis must be assigned one of four severity levels. This ensures consistent prioritization across all dimensions and analysts.

### Critical

**Definition**: Issues that pose immediate risk to security, data integrity, or system availability.

**Characteristics**:
- Exploitable vulnerability with no authentication required
- Data loss or corruption in production
- System crash or denial of service
- Security breach exposing sensitive data
- Compliance violation (GDPR, HIPAA, SOC2)

**Action Required**: Fix immediately before deployment. Stop release if found in production.

**Examples**:
- SQL injection in authentication endpoint
- Hardcoded production database credentials
- Missing authorization check on admin endpoint
- Race condition causing financial transaction duplication
- Buffer overflow in C/C++ code

### High

**Definition**: Issues that significantly impact functionality, performance, or security under specific conditions.

**Characteristics**:
- Vulnerability requiring authentication or specific conditions
- Major performance degradation under load
- Significant logic flaw affecting core functionality
- Missing critical error handling
- Memory leak in long-running process

**Action Required**: Fix within 24-48 hours. Schedule emergency patch if in production.

**Examples**:
- XSS vulnerability in user-generated content display
- N+1 query in frequently accessed endpoint
- Missing rate limiting on API endpoints
- Incorrect business logic in payment processing
- Unhandled promise rejection causing process crash

### Medium

**Definition**: Issues that degrade code quality, maintainability, or introduce moderate risk.

**Characteristics**:
- Code smell or anti-pattern
- Moderate complexity exceeding guidelines
- Incomplete documentation
- Missing test coverage for non-critical paths
- Suboptimal but functional implementation

**Action Required**: Fix within current sprint or development cycle.

**Examples**:
- Function with cyclomatic complexity of 15-20
- Missing input validation on internal API
- Duplicate code blocks (3+ occurrences)
- Missing error handling for edge case
- Inefficient algorithm with limited impact

### Low

**Definition**: Minor issues that have minimal impact on functionality or risk.

**Characteristics**:
- Style inconsistency
- Missing or incomplete comments
- Minor optimization opportunity
- Documentation typo
- Non-critical formatting issue

**Action Required**: Fix when convenient or during refactoring.

**Examples**:
- Inconsistent naming convention
- Missing type hints in non-public API
- Commented-out code
- Minor whitespace or formatting issue
- Optional documentation improvement

## Severity Assignment Matrix

| Issue Type | Critical | High | Medium | Low |
|-----------|----------|------|--------|-----|
| Security vulnerability | Remote exploitable | Auth required | Defense gap | Hardening |
| Performance | System crash | Significant degradation | Suboptimal | Micro-optimization |
| Code quality | Untested critical path | High complexity | Style issue | Formatting |
| Architecture | Circular dependency | SOLID violation | Pattern inconsistency | Organization |
| Logic | Data corruption | Wrong result | Edge case | Minor behavior |

## Escalation Rules

1. **Multiple Mediums = High**: If 3+ Medium issues exist in the same function/module, escalate to High
2. **Pattern = Higher**: If the same issue pattern repeats across the codebase, escalate severity
3. **Context Matters**: Consider production impact, user-facing vs internal, data sensitivity
4. **Defense in Depth**: Missing validation at multiple layers escalates severity

## Severity Distribution Goals

A healthy codebase should have:
- 0 Critical issues
- 0-2 High issues per 1000 LOC
- 5-10 Medium issues per 1000 LOC
- 10-20 Low issues per 1000 LOC

If Critical issues are common, prioritize security training and code review processes.
If High issues dominate, focus on architecture and testing improvements.
