# Deployment & Infrastructure

## Table of Contents

- [Deployment Overview](#deployment-overview)
- [Azure Integration Guide](azure-integration.md)
- [CI/CD Pipeline Setup](cicd-setup.md)
- [Environment Configuration](environment-config.md)
- [Security Requirements](security-requirements.md)
- [Monitoring & Maintenance](monitoring.md)
- [Troubleshooting](deployment-troubleshooting.md)

## Deployment Overview

GSD-DE's deployment architecture is designed around the principle of "automated deployment with government security compliance." Every application deployed through GSD-DE follows the same proven patterns, ensuring consistency, security, and reliability.

## Core Deployment Philosophy

### One-Click Government Deployment
GSD-DE transforms complex government deployment processes into simple, automated workflows:

- **Infrastructure as Code**: All Azure resources defined in version-controlled templates
- **Security by Default**: Government security standards built into every deployment
- **Compliance Automation**: Automated validation against government requirements
- **Zero-Downtime Deployment**: Blue-green deployment patterns for production updates

### Deployment Pipeline Architecture

```
GitHub Repository → Build Pipeline → Security Scan → Staging Deploy → Testing → Production Deploy → Monitoring
```

**1. Source Control Integration**
- GitHub webhook triggers deployment pipeline
- Branch-based environment deployment (dev/staging/production)
- Pull request validation with automated testing

**2. Build & Package**
- Automated dependency installation and vulnerability scanning
- Code compilation and asset optimization
- Container image creation with security hardening
- Infrastructure template validation

**3. Security & Compliance**
- Static Application Security Testing (SAST)
- Dependency vulnerability scanning
- Infrastructure security policy validation
- Government compliance checking

**4. Environment Deployment**
- Automated Azure resource provisioning
- Application deployment with health checks
- Database migration and data seeding
- SSL certificate configuration and validation

**5. Validation & Testing**
- Smoke tests and health check validation
- Performance testing and load validation
- Security penetration testing
- Accessibility compliance verification

**6. Monitoring & Alerting**
- Application performance monitoring setup
- Log aggregation and analysis configuration
- Alert rules and notification channels
- Backup and disaster recovery validation

## Environment Structure

### Development Environment
**Purpose**: Individual developer testing and feature development

**Azure Resources**:
- App Service (Free/Shared tier for cost optimization)
- SQL Database (Basic tier with minimal storage)
- Storage Account (LRS for development files)
- Application Insights (Basic monitoring)

**Characteristics**:
- Automatic deployment on feature branch commits
- Simplified security (development credentials)
- Limited resource allocation (cost control)
- Frequent resets and data refresh

**Access**:
- Development team members
- Automated testing systems
- No external access (internal network only)

### Staging Environment
**Purpose**: Pre-production validation and user acceptance testing

**Azure Resources**:
- App Service (Standard tier with scaling capability)
- SQL Database (Standard tier with backup)
- Storage Account (GRS for reliability testing)
- Application Insights (Full monitoring suite)
- Key Vault (Production-like secrets management)

**Characteristics**:
- Deployment requires pull request approval
- Production-equivalent security configuration
- Performance testing and load validation
- Stakeholder access for user acceptance testing

**Access**:
- Development and testing teams
- Business stakeholders for UAT
- Security team for compliance validation
- Limited external access (VPN required)

### Production Environment
**Purpose**: Live government services serving Alberta citizens

**Azure Resources**:
- App Service (Premium tier with auto-scaling)
- SQL Database (Premium tier with geo-redundancy)
- Storage Account (RA-GRS with CDN integration)
- Application Insights (Advanced monitoring and analytics)
- Key Vault (Full secrets management with HSM)
- Traffic Manager (Multi-region load balancing)
- Azure Front Door (Global CDN and WAF)

**Characteristics**:
- Manual deployment approval required
- Full government security compliance
- 99.9% uptime SLA with disaster recovery
- Comprehensive monitoring and alerting
- Audit logging and compliance reporting

**Access**:
- Production operations team only
- Automated monitoring and deployment systems
- Public internet access (citizens and government staff)
- Full security controls and access logging

## Deployment Templates

### Standard Web Application Template

**Infrastructure Components**:
```yaml
# Azure Resource Manager Template
resources:
  - name: app-service-plan
    type: Microsoft.Web/serverfarms
    properties:
      tier: Standard
      capacity: 2
      
  - name: web-app
    type: Microsoft.Web/sites
    properties:
      serverFarmId: "[resourceId('Microsoft.Web/serverfarms', 'app-service-plan')]"
      httpsOnly: true
      siteConfig:
        minTlsVersion: '1.2'
        alwaysOn: true
        
  - name: sql-server
    type: Microsoft.Sql/servers
    properties:
      administratorLogin: "[parameters('sqlAdminUsername')]"
      administratorLoginPassword: "[parameters('sqlAdminPassword')]"
      
  - name: sql-database
    type: Microsoft.Sql/servers/databases
    properties:
      collation: SQL_Latin1_General_CP1_CI_AS
      tier: Standard
```

**Security Configuration**:
- HTTPS enforcement with minimum TLS 1.2
- Managed identity for Azure resource access
- Key Vault integration for secrets management
- Network security groups with government IP restrictions
- Web Application Firewall (WAF) protection

**Monitoring Setup**:
- Application Insights for performance tracking
- Log Analytics for centralized logging
- Azure Monitor alerts for critical issues
- Health check endpoints for availability monitoring

### API Service Template

**Specialized for Backend Services**:
- Container deployment with Docker
- API Management integration
- Rate limiting and throttling
- OpenAPI documentation generation
- Service-to-service authentication

### Database Integration Template

**For Data-Intensive Applications**:
- Azure SQL Database with backup policies
- Connection pooling and performance optimization
- Data encryption at rest and in transit
- Audit logging for data access
- Disaster recovery with geo-replication

## Deployment Automation

### GitHub Actions Workflow

```yaml
name: GSD-DE Government App Deployment
on:
  push:
    branches: [main, staging, develop]
  pull_request:
    branches: [main]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Security Scan
        uses: github/super-linter@v4
      - name: Vulnerability Assessment
        run: npm audit --audit-level high
        
  build-and-test:
    needs: security-scan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install Dependencies
        run: npm ci
      - name: Run Tests
        run: npm test
      - name: Build Application
        run: npm run build
        
  deploy-staging:
    needs: build-and-test
    if: github.ref == 'refs/heads/staging'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Azure Staging
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'gsd-app-staging'
          publish-profile: ${{ secrets.AZURE_STAGING_PROFILE }}
          
  deploy-production:
    needs: build-and-test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to Azure Production
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'gsd-app-production'
          publish-profile: ${{ secrets.AZURE_PRODUCTION_PROFILE }}
```

### Azure DevOps Pipeline

```yaml
trigger:
  branches:
    include:
      - main
      - staging
      - develop

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: SecurityAndCompliance
  jobs:
  - job: SecurityScan
    steps:
    - task: SonarCloudPrepare@1
    - task: npmAuthenticate@0
    - task: Npm@1
      inputs:
        command: 'ci'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run test:security'
        
- stage: Build
  dependsOn: SecurityAndCompliance
  jobs:
  - job: BuildApplication
    steps:
    - task: Npm@1
      inputs:
        command: 'ci'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'
    - task: PublishBuildArtifacts@1
      
- stage: DeployStaging
  dependsOn: Build
  condition: eq(variables['Build.SourceBranch'], 'refs/heads/staging')
  jobs:
  - deployment: DeployToStaging
    environment: 'Staging'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            inputs:
              azureSubscription: 'Government-Staging'
              appName: 'gsd-staging-app'
              
- stage: DeployProduction
  dependsOn: Build
  condition: eq(variables['Build.SourceBranch'], 'refs/heads/main')
  jobs:
  - deployment: DeployToProduction
    environment: 'Production'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            inputs:
              azureSubscription: 'Government-Production'
              appName: 'gsd-production-app'
```

## Government Security Requirements

### Mandatory Security Controls

**Authentication & Authorization**:
- Single Sign-On (SSO) integration with government identity systems
- Multi-factor authentication (MFA) for administrative access
- Role-based access control (RBAC) with least-privilege principles
- Session management with appropriate timeout policies

**Data Protection**:
- Encryption at rest using Azure-managed keys
- Encryption in transit with TLS 1.2 minimum
- Personal information protection compliance
- Data residency within Canadian borders

**Network Security**:
- Web Application Firewall (WAF) protection
- DDoS protection and traffic filtering
- Network segmentation and isolation
- VPN access for administrative functions

**Audit & Compliance**:
- Comprehensive audit logging of all activities
- Log retention policies meeting government requirements
- Regular security assessments and penetration testing
- Compliance reporting and certification

### Security Validation Pipeline

**Automated Security Checks**:
1. **Static Application Security Testing (SAST)**: Code analysis for vulnerabilities
2. **Dynamic Application Security Testing (DAST)**: Runtime security testing
3. **Dependency Scanning**: Third-party library vulnerability assessment
4. **Infrastructure Security**: Cloud configuration validation
5. **Compliance Checking**: Government standard adherence verification

**Manual Security Reviews**:
- Security architecture review for complex applications
- Privacy impact assessment for citizen-facing services
- Penetration testing by certified security professionals
- Compliance audit and certification process

## Monitoring & Observability

### Application Performance Monitoring

**Azure Application Insights Integration**:
- Real-time performance metrics and alerting
- User behavior analytics and error tracking
- Dependency tracking and failure analysis
- Custom metrics for business KPIs

**Key Metrics Tracked**:
- Response time and throughput
- Error rates and exception details
- User satisfaction and engagement
- Resource utilization and scaling needs

### Infrastructure Monitoring

**Azure Monitor Setup**:
- Virtual machine and container monitoring
- Database performance and query analysis
- Network traffic and security events
- Storage utilization and backup status

**Alert Configuration**:
- Critical system failures (immediate notification)
- Performance degradation (proactive alerts)
- Security incidents (security team notification)
- Cost optimization opportunities (weekly reports)

### Log Management

**Centralized Logging**:
- Azure Log Analytics for log aggregation
- Structured logging with correlation IDs
- Log retention policies meeting government requirements
- Search and analysis capabilities for troubleshooting

**Security Event Logging**:
- Authentication and authorization events
- Data access and modification tracking
- System configuration changes
- Security policy violations

## Disaster Recovery & Business Continuity

### Backup Strategy

**Application Backups**:
- Daily automated database backups with point-in-time recovery
- Application configuration and code stored in version control
- Static assets and user uploads backed up to geo-redundant storage
- Infrastructure templates for rapid environment recreation

**Recovery Procedures**:
- Documented recovery time objectives (RTO: 4 hours)
- Recovery point objectives (RPO: 1 hour)
- Regular disaster recovery testing and validation
- Staff training on emergency procedures

### High Availability Design

**Multi-Region Deployment**:
- Primary deployment in Canada Central
- Secondary deployment in Canada East
- Automatic failover with Azure Traffic Manager
- Data synchronization between regions

**Scaling & Load Management**:
- Auto-scaling based on CPU and request metrics
- Load balancing across multiple instances
- Database read replicas for performance
- CDN integration for static content delivery

---

*This deployment architecture ensures that every GSD-DE application meets government security standards while providing the reliability and performance that Alberta citizens expect from their digital services.*