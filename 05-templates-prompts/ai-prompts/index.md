# AI Prompts Library

The AI Prompts Library contains professionally crafted prompts optimized for government application development. These prompts are battle-tested and continuously refined based on real project outcomes.

## Prompt Categories

### 📦 Development Prompts (42 prompts)

#### Architecture & Design Prompts

**Government Application Architecture Prompt**
```yaml
name: "government-app-architecture"
category: "development"
tags: ["architecture", "government", "security", "azure"]
usage_count: 234
success_rate: 94%
```

```
You are an expert architect designing applications for the Government of Alberta. 

CONTEXT:
- Government environment with strict security requirements
- Azure government cloud infrastructure
- Need for SSO integration and audit trails
- Budget and timeline constraints typical for government projects
- Must serve diverse user groups including citizens and staff

REQUIREMENTS:
Create a system architecture that prioritizes:
1. Security and compliance with government standards
2. Scalability for province-wide deployment  
3. Integration with existing government systems
4. Accessibility (WCAG 2.1 AA compliance)
5. Bilingual support (English/French)
6. Comprehensive audit trails and compliance reporting

CONSTRAINTS:
- Must use Azure government cloud
- Requires SSO integration with government identity systems
- Must maintain comprehensive audit trails
- Performance requirements: sub-2s page loads, 99.9% uptime
- Budget: Government procurement processes and approval cycles

OUTPUT FORMAT:
Generate a detailed architecture document including:

## Executive Summary
[2-3 sentences describing the overall approach]

## System Architecture
- High-level component diagram
- Technology stack recommendations with rationale
- Data flow diagrams
- Integration points with existing systems

## Security Architecture
- Authentication and authorization strategy
- Data protection and encryption
- Network security considerations
- Threat model and mitigation strategies

## Deployment Strategy  
- Environment setup (dev/staging/production)
- CI/CD pipeline design
- Rollback and disaster recovery plans
- Monitoring and alerting strategy

## Implementation Roadmap
- Phase-based delivery plan
- Resource requirements and timeline
- Risk assessment and mitigation
- Success metrics and KPIs

TONE: Professional, detailed, government-appropriate
```

**API Design Prompt**
```yaml
name: "government-api-design"
category: "development"
tags: ["api", "rest", "documentation", "security"]
usage_count: 187
success_rate: 96%
```

```
Design a RESTful API for a Government of Alberta application.

REQUIREMENTS:
- Follow REST principles and government API standards
- Include comprehensive security measures
- Provide clear documentation for developers
- Support for audit logging and compliance
- Rate limiting and error handling
- Version management strategy

API DETAILS:
[Describe the specific API requirements here]

OUTPUT:
1. OpenAPI 3.0 specification
2. Authentication and authorization strategy
3. Error handling patterns
4. Rate limiting configuration
5. Audit logging requirements
6. API documentation structure
7. Testing strategy and examples

SECURITY CONSIDERATIONS:
- API key management
- OAuth 2.0 / OIDC integration
- Input validation and sanitization
- SQL injection prevention
- CORS configuration for government domains
```

#### Code Generation Prompts

**Secure Component Generator**
```yaml
name: "secure-component-generator"
category: "development"
tags: ["react", "security", "components", "accessibility"]
usage_count: 156
success_rate: 91%
```

```
Generate a React component for a Government of Alberta application.

COMPONENT REQUIREMENTS:
[Specify the component details here]

MANDATORY FEATURES:
1. WCAG 2.1 AA accessibility compliance
2. Bilingual support (English/French)
3. Input validation and sanitization
4. Error handling and user feedback
5. Government styling integration
6. Mobile-responsive design
7. Comprehensive testing

SECURITY REQUIREMENTS:
- XSS prevention
- CSRF protection where applicable
- Content Security Policy compliance
- Safe rendering of dynamic content

OUTPUT:
1. React component with TypeScript
2. Accessibility features (ARIA labels, keyboard navigation)
3. Comprehensive PropTypes or TypeScript interfaces
4. Jest/React Testing Library test suite
5. Storybook stories for documentation
6. CSS/styled-components following government design system

STYLING:
- Use government color palette
- Consistent typography and spacing
- Mobile-first responsive design
- High contrast mode support
```

### 📚 Documentation Prompts (28 prompts)

#### API Documentation Prompt

**Government API Documentation Generator**
```yaml
name: "api-documentation-generator"
category: "documentation"
tags: ["api", "openapi", "documentation", "examples"]
usage_count: 143
success_rate: 98%
```

```
Generate comprehensive API documentation for a Government of Alberta service.

API SPECIFICATION:
[OpenAPI spec or API details will be provided here]

DOCUMENTATION REQUIREMENTS:
1. Clear overview and purpose statement
2. Authentication and authorization guide
3. Endpoint documentation with examples
4. Error codes and troubleshooting
5. Rate limiting and usage guidelines
6. SDK/client library information
7. Change log and versioning info

GOVERNMENT SPECIFIC REQUIREMENTS:
- Security compliance notes
- Data privacy and handling requirements  
- Audit logging capabilities
- Integration with government identity systems
- Bilingual documentation (English/French)

OUTPUT FORMAT:
## API Overview
[Purpose, scope, and key features]

## Getting Started
- Authentication setup
- Basic usage examples
- Environment configuration

## Authentication
- Supported authentication methods
- Token management
- Refresh token handling

## Endpoints
[For each endpoint:]
- Purpose and description
- HTTP method and path
- Parameters and request body
- Response format and examples
- Error scenarios and codes
- Rate limiting information

## Error Handling
- Standard error response format
- Common error scenarios
- Troubleshooting guide

## Security
- Security considerations
- Data handling requirements
- Compliance notes

## SDK and Tools
- Available client libraries
- Code examples in multiple languages
- Postman collections or similar

TONE: Professional, clear, government-appropriate
Include real-world examples relevant to government use cases
```

#### README Generator Prompt

**Government Project README Template**
```yaml
name: "government-readme-generator"
category: "documentation"
tags: ["readme", "project", "setup", "government"]
usage_count: 289
success_rate: 95%
```

```
Generate a comprehensive README.md for a Government of Alberta application.

PROJECT DETAILS:
[Project information will be provided here]

README STRUCTURE:
# [Project Name]

## Overview
Brief description of the project's purpose and key features

## Table of Contents
[Generated based on content]

## Features
- Key features and capabilities
- Government-specific compliance features
- Security and accessibility features

## Prerequisites
- System requirements
- Software dependencies
- Government-specific requirements (VPN, certificates, etc.)

## Installation
Step-by-step setup instructions including:
- Environment setup
- Dependency installation
- Configuration requirements
- Database setup (if applicable)

## Configuration
- Environment variables
- Configuration files
- Government-specific settings
- Security configuration

## Usage
- Basic usage examples
- Common workflows
- API usage (if applicable)
- Screenshots or diagrams where helpful

## Development
- Setting up development environment
- Running tests
- Contributing guidelines
- Code style and standards

## Deployment
- Deployment process
- Environment-specific considerations
- CI/CD pipeline information
- Azure deployment specifics

## Security
- Security considerations
- Compliance requirements
- Audit logging
- Data handling requirements

## Support
- Contact information
- Issue reporting process
- Government support channels

## License
[Government appropriate licensing]

REQUIREMENTS:
- Professional government tone
- Clear, step-by-step instructions
- Include troubleshooting common issues
- Reference government standards and compliance
- Mobile-friendly formatting
- Include badges for build status, security scans, etc.
```

### 🧪 Testing Prompts (19 prompts)

#### Comprehensive Test Suite Generator

**Government Application Test Suite**
```yaml
name: "government-test-suite-generator"
category: "testing"
tags: ["testing", "security", "accessibility", "compliance"]
usage_count: 127
success_rate: 93%
```

```
Generate a comprehensive test suite for a Government of Alberta application.

APPLICATION DETAILS:
[Application information will be provided here]

TEST CATEGORIES REQUIRED:

1. UNIT TESTS
- Component/function testing
- Edge case handling
- Error condition testing
- Mock external dependencies

2. INTEGRATION TESTS  
- API endpoint testing
- Database integration testing
- External service integration
- Authentication flow testing

3. SECURITY TESTS
- Input validation testing
- Authentication/authorization testing
- XSS and injection prevention
- HTTPS and certificate validation
- Rate limiting verification

4. ACCESSIBILITY TESTS
- WCAG 2.1 AA compliance testing
- Keyboard navigation testing
- Screen reader compatibility
- Color contrast validation
- Mobile accessibility

5. PERFORMANCE TESTS
- Load testing scenarios
- Response time validation
- Memory usage testing
- Database query optimization

6. COMPLIANCE TESTS
- Government security standard compliance
- Data privacy requirement validation
- Audit trail verification
- Bilingual content testing

OUTPUT:
Generate test files including:
- Jest/Vitest unit tests
- Cypress/Playwright end-to-end tests
- Performance testing with Artillery or k6
- Accessibility testing with axe-core
- Security testing scenarios
- CI/CD integration scripts

TESTING STANDARDS:
- Minimum 80% code coverage
- All critical paths tested
- Negative case testing
- Government-specific compliance validation
- Automated testing in CI pipeline

Include setup instructions, mock data, and test documentation.
```

#### Security Test Cases Prompt

**Government Security Test Generator**
```yaml
name: "security-test-generator"
category: "testing"
tags: ["security", "penetration", "compliance", "vulnerability"]
usage_count: 98
success_rate: 96%
```

```
Generate security test cases for a Government of Alberta application.

APPLICATION SECURITY PROFILE:
[Application details and security requirements]

SECURITY TEST CATEGORIES:

1. AUTHENTICATION TESTS
- Login/logout functionality
- Session management
- Password policy enforcement
- Multi-factor authentication
- SSO integration testing
- Account lockout mechanisms

2. AUTHORIZATION TESTS
- Role-based access control
- Privilege escalation prevention
- Resource access validation
- API endpoint authorization
- Data access restrictions

3. INPUT VALIDATION TESTS
- SQL injection prevention
- XSS prevention
- Command injection testing
- File upload security
- Input sanitization validation

4. SESSION SECURITY TESTS
- Session fixation prevention
- Secure cookie configuration
- Session timeout validation
- CSRF protection
- Secure transmission

5. API SECURITY TESTS
- Rate limiting effectiveness
- API key management
- OAuth 2.0 flow validation
- Data exposure prevention
- Error information leakage

6. INFRASTRUCTURE TESTS
- HTTPS enforcement
- TLS configuration validation
- Security header verification
- Certificate validation
- Network security testing

OUTPUT:
For each test category, provide:
- Test case descriptions
- Expected results
- Test scripts (where applicable)
- Validation criteria
- Government compliance mapping
- Risk assessment for failures

COMPLIANCE MAPPING:
Map each test to relevant government security standards and requirements.
Include severity levels and remediation guidance.
```

### 🚀 Deployment Prompts (15 prompts)

#### Azure Infrastructure as Code Prompt

**Government Azure Infrastructure Generator**
```yaml
name: "azure-infrastructure-generator"
category: "deployment"
tags: ["azure", "infrastructure", "terraform", "government"]
usage_count: 156
success_rate: 94%
```

```
Generate Azure infrastructure as code for a Government of Alberta application.

APPLICATION REQUIREMENTS:
[Application details and requirements will be provided here]

INFRASTRUCTURE REQUIREMENTS:
- Government cloud compliance
- High availability and disaster recovery
- Security and network isolation
- Monitoring and logging
- Cost optimization
- Scalability considerations

COMPONENTS TO INCLUDE:
1. Resource Group organization
2. App Service or Container Apps
3. Database (SQL Database, PostgreSQL, etc.)
4. Storage accounts
5. Key Vault for secrets
6. Application Insights
7. Load balancer (if needed)
8. CDN configuration
9. Backup and recovery
10. Network security groups

TERRAFORM CONFIGURATION:
Generate Terraform files including:

main.tf - Core infrastructure resources
variables.tf - Configurable parameters
outputs.tf - Resource information outputs
terraform.tfvars.example - Configuration template
provider.tf - Azure provider configuration

AZURE ARM TEMPLATES (Alternative):
If Terraform not preferred, provide ARM templates with:
- Main template
- Parameter files for each environment
- Nested templates for complex resources

SECURITY CONFIGURATION:
- Network isolation and security groups
- Key Vault integration for secrets
- Managed identities where possible
- Encryption at rest and in transit
- Audit logging configuration
- Backup and disaster recovery

MONITORING:
- Application Insights setup
- Log Analytics workspace
- Alert rules and action groups
- Performance monitoring
- Cost monitoring and budgets

ENVIRONMENTS:
Provide configurations for:
- Development
- Staging/Testing
- Production

Include deployment scripts and CI/CD integration guidance.
```

#### CI/CD Pipeline Generator

**Government CI/CD Pipeline Template**
```yaml
name: "government-cicd-pipeline"
category: "deployment"
tags: ["cicd", "azure-devops", "github-actions", "security"]
usage_count: 203
success_rate: 97%
```

```
Generate a CI/CD pipeline for Government of Alberta application deployment.

APPLICATION DETAILS:
[Application information will be provided here]

PIPELINE REQUIREMENTS:
- Automated testing at multiple levels
- Security scanning and compliance checks
- Code quality validation
- Automated deployment to multiple environments
- Rollback capabilities
- Government approval workflows

PIPELINE STAGES:

1. SOURCE CONTROL
- Git workflow (feature branches, pull requests)
- Code review requirements
- Branch protection rules

2. BUILD STAGE
- Dependency installation and caching
- Code compilation/transpilation
- Asset optimization
- Container image building (if applicable)

3. TEST STAGE
- Unit test execution
- Integration test execution
- Code coverage reporting
- Performance test execution

4. SECURITY STAGE
- Static code analysis (SonarQube, CodeQL)
- Dependency vulnerability scanning
- Container security scanning
- Infrastructure security validation

5. QUALITY STAGE
- Code quality metrics
- Technical debt assessment
- Compliance validation
- Documentation generation

6. DEPLOY STAGE
- Environment-specific deployment
- Blue-green or rolling deployment
- Health checks and validation
- Rollback mechanisms

7. POST-DEPLOY
- Smoke tests
- Performance monitoring
- Alert configuration
- Audit logging

OUTPUT:
Generate pipeline files for:

GITHUB ACTIONS:
```yaml
name: Government Application CI/CD
on: [push, pull_request]
jobs:
  # Complete workflow definition
```

AZURE DEVOPS:
```yaml
# Azure Pipelines YAML
trigger: [main, develop]
pool:
  vmImage: 'ubuntu-latest'
stages:
  # Complete pipeline definition
```

ENVIRONMENT CONFIGURATION:
- Development: Automated deployment on feature branch merge
- Staging: Automated deployment with approval gate
- Production: Manual approval with change management integration

SECURITY INTEGRATION:
- Government security scanning tools
- Compliance validation checkpoints
- Secret management integration
- Audit trail generation

Include setup instructions and troubleshooting guides.
```

## Prompt Usage Guidelines

### Selecting the Right Prompt

1. **Match to Use Case**: Choose prompts that closely match your specific requirements
2. **Check Success Rates**: Higher success rates indicate well-tested prompts
3. **Review Usage Stats**: Popular prompts often have better documentation and examples
4. **Consider Complexity**: Start with simpler prompts for proof-of-concept work

### Customizing Prompts

1. **Replace Placeholders**: Fill in application-specific details in brackets
2. **Adjust Scope**: Modify requirements based on project constraints
3. **Add Context**: Include relevant background information
4. **Specify Constraints**: Add any additional technical or business constraints

### Best Practices

1. **Be Specific**: Provide detailed context and requirements
2. **Include Examples**: Reference similar successful projects when available
3. **Validate Output**: Always review and test AI-generated code/documentation
4. **Iterate and Refine**: Use feedback to improve prompts over time
5. **Share Improvements**: Contribute successful modifications back to the library

## Prompt Performance Metrics

### Success Rate Categories
- **🟢 90-100%**: Production-ready, well-tested prompts
- **🟡 80-89%**: Good prompts with minor refinement needs
- **🟠 70-79%**: Experimental prompts requiring careful review
- **🔴 <70%**: Under development, use with caution

### Usage Analytics
- **Most Used**: API documentation and README generators
- **Highest Success**: Infrastructure and deployment prompts
- **Fastest Growing**: Security testing and compliance prompts
- **Most Refined**: Architecture and design prompts

---

*The AI Prompts Library is continuously updated based on real-world usage and feedback from government development teams. Each prompt is versioned and tracked for effectiveness.*