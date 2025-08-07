# Development Setup & Guidelines

## Table of Contents

- [Development Environment Setup](#development-environment-setup)
- [Codebase Structure](#codebase-structure)
- [API Documentation](#api-documentation)
- [Contributing Guidelines](#contributing-guidelines)
- [Testing Strategy](#testing-strategy)
- [Code Standards](#code-standards)
- [Integration Development](#integration-development)
- [Deployment Process](#deployment-process)
- [Troubleshooting Guide](#troubleshooting-guide)

## Development Environment Setup

### Prerequisites

**System Requirements**:
- Node.js 18+ with npm 8+
- Git 2.35+ with SSH key configured
- Azure CLI 2.40+ for cloud operations
- Docker Desktop (for containerized development)
- VS Code with recommended extensions

**Government-Specific Requirements**:
- Alberta government network access (VPN if remote)
- GitHub access with government organization membership
- Azure government subscription credentials
- SSL certificates for local HTTPS development

### Initial Setup

**1. Clone the Repository**
```bash
git clone https://github.com/AlbertaGov/GSD-DE.git
cd GSD-DE
```

**2. Environment Configuration**
```bash
# Copy environment template
cp .env.example .env.local

# Edit configuration for local development
nano .env.local
```

**3. Install Dependencies**
```bash
# Install Node.js dependencies
npm install

# Install development tools
npm install -g nodemon eslint prettier
```

**4. Database Setup**
```bash
# Initialize SQLite database
npm run db:init

# Seed with sample data
npm run db:seed
```

**5. Start Development Server**
```bash
# Start in development mode with hot reload
npm run dev

# Application available at https://localhost:8000
```

### Development Tools Configuration

**VS Code Extensions**:
- ESLint for code quality
- Prettier for code formatting
- Azure Tools for cloud integration
- REST Client for API testing
- GitHub Pull Requests for code review

**Local HTTPS Setup**:
```bash
# Generate self-signed certificates
npm run generate-certs

# Trust certificates (macOS)
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ./certs/localhost.crt

# Trust certificates (Windows)
certmgr.exe -add -c ./certs/localhost.crt -s -r localMachine TrustedPublisher
```

## Codebase Structure

### Project Organization

```
GSD-DE/
├── 🔧 Backend Services
│   ├── services/              # Business logic services
│   │   ├── database-service.js    # Database operations
│   │   ├── openai-service.js      # AI integration
│   │   ├── github-service.js      # GitHub API
│   │   └── workspace-service.js   # Project management
│   │
│   ├── routes/                # API route handlers
│   │   ├── auto-triage.js         # AI assessment endpoints
│   │   ├── task.js                # Task management API
│   │   ├── github.js              # Repository operations
│   │   └── workspace.js           # Workspace management
│   │
│   ├── middleware/            # Express middleware
│   │   ├── auth.js                # Authentication
│   │   ├── validation.js          # Input validation
│   │   └── security.js            # Security headers
│   │
│   └── utils/                 # Utility functions
│       ├── logger.js              # Structured logging
│       ├── config.js              # Configuration management
│       └── helpers.js             # Common utilities
│
├── 🎨 Frontend Components
│   └── static/
│       ├── js/                # JavaScript modules
│       │   ├── main.js            # Application entry point
│       │   ├── task-manager.js    # Core task management
│       │   ├── workspace-manager.js # GitHub integration
│       │   └── components/        # Reusable UI components
│       │
│       ├── css/               # Stylesheets
│       │   ├── styles.css         # Main styles
│       │   └── components.css     # Component styles
│       │
│       └── templates/         # HTML templates
│           ├── dashboard.html     # Main dashboard
│           ├── kanban.html        # Task board
│           └── submit-idea.html   # Idea submission
│
├── 🗄️ Database & Configuration
│   ├── database/              # Database files
│   ├── config/                # Configuration files
│   └── scripts/               # Utility scripts
│
└── 📋 Documentation & Testing
    ├── docs/                  # Technical documentation
    ├── tests/                 # Test suites
    └── wiki/                  # Project wiki (this documentation)
```

### Key Architecture Principles

**1. Modular Service Design**
- Each service handles a specific business domain
- Clear interfaces between services
- Dependency injection for testability
- Error handling with proper logging

**2. API-First Development**
- RESTful API design with OpenAPI documentation
- Consistent error responses and status codes
- Version management for backward compatibility
- Authentication and rate limiting

**3. Frontend Component Architecture**
- Vanilla JavaScript with ES6+ modules
- Component-based UI development
- Event-driven architecture
- Progressive enhancement approach

## API Documentation

### Core Endpoints

**Health & System Status**
```http
GET /api/health
Response: { status: "healthy", timestamp: "2025-01-15T10:30:00Z" }

GET /api/auto-triage/health
Response: { aiService: "operational", lastCheck: "2025-01-15T10:29:45Z" }
```

**Idea Submission & Assessment**
```http
POST /api/auto-triage
Content-Type: application/json
{
  "title": "Automate Building Permit Status Updates",
  "description": "Citizens currently have to call to check permit status...",
  "submitterEmail": "user@alberta.ca"
}

Response:
{
  "id": "idea-123",
  "rapidScore": 87,
  "assessment": {
    "roi": 85,
    "achievability": 92,
    "publicValue": 88,
    "innovation": 75,
    "deliverySpeed": 89
  },
  "recommendations": "High-value project with strong ROI potential...",
  "estimatedTimeline": "6-8 weeks",
  "estimatedCost": "$45,000"
}
```

**Task Management**
```http
GET /api/tasks
Response: [
  {
    "id": 1,
    "title": "Building Permit Portal",
    "status": "in-progress",
    "rapidScore": 87,
    "assignedTo": "dev-team-alpha",
    "createdAt": "2025-01-10T14:30:00Z"
  }
]

PUT /api/tasks/:id
Content-Type: application/json
{
  "status": "completed",
  "notes": "Deployed to production, monitoring looks good"
}
```

**GitHub Integration**
```http
POST /api/tasks/:id/create-github-workspace
Response: {
  "repositoryUrl": "https://github.com/AlbertaGov/building-permit-portal",
  "workspaceStatus": "created",
  "deploymentUrl": "https://building-permits-dev.azurewebsites.net"
}

GET /api/tasks/:id/github/status
Response: {
  "repository": "building-permit-portal",
  "lastCommit": "2025-01-15T09:15:00Z",
  "buildStatus": "success",
  "deploymentStatus": "deployed"
}
```

### Authentication

**Government SSO Integration**
```http
GET /auth/login
Redirects to: https://login.alberta.ca/oauth2/authorize...

POST /auth/callback
Handles: OAuth2 callback and session creation

GET /auth/user
Response: {
  "id": "user123",
  "email": "user@alberta.ca",
  "name": "Jane Smith",
  "ministry": "Service Alberta",
  "roles": ["developer", "idea-submitter"]
}
```

## Contributing Guidelines

### Git Workflow

**Branch Naming Convention**
```bash
# Feature branches
feature/ticket-123-building-permit-automation
feature/ai-assessment-improvements

# Bug fix branches  
fix/dashboard-loading-issue
hotfix/security-vulnerability-patch

# Release branches
release/v1.2.0
```

**Commit Message Format**
```bash
# Format: type(scope): description
feat(api): add RAPID scoring endpoint
fix(ui): resolve kanban drag-drop issue
docs(wiki): update deployment guide
test(integration): add GitHub API tests
```

**Pull Request Process**

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/new-assessment-algorithm
   git push -u origin feature/new-assessment-algorithm
   ```

2. **Development & Testing**
   - Write code following established patterns
   - Add/update tests for new functionality
   - Update documentation as needed
   - Test locally and in development environment

3. **Pre-PR Checklist**
   ```bash
   # Run code quality checks
   npm run lint
   npm run test
   npm run security-scan
   
   # Verify build works
   npm run build
   ```

4. **Create Pull Request**
   - Use PR template with complete description
   - Link to relevant issues or tickets
   - Request review from appropriate team members
   - Ensure CI/CD pipeline passes

5. **Code Review Process**
   - Address review feedback promptly
   - Update tests and documentation as needed
   - Maintain conversation until approval
   - Squash commits before merge if requested

### Code Review Standards

**Review Checklist**:
- [ ] Code follows established patterns and conventions
- [ ] Tests added/updated for new functionality
- [ ] Documentation updated (README, API docs, inline comments)
- [ ] Security considerations addressed
- [ ] Performance impact assessed
- [ ] Accessibility requirements met (for UI changes)
- [ ] Government compliance maintained

**Security Review**:
- [ ] Input validation and sanitization
- [ ] Authentication and authorization checks
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] Sensitive data handling
- [ ] Audit logging for critical operations

## Testing Strategy

### Test Pyramid Structure

**Unit Tests (70% of test coverage)**
```javascript
// Example: Testing AI service utility functions
describe('RAPID Score Calculation', () => {
  test('calculates weighted average correctly', () => {
    const scores = { roi: 85, achievability: 90, publicValue: 88, innovation: 75, deliverySpeed: 82 };
    const result = calculateRAPIDScore(scores);
    expect(result).toBe(84);
  });
  
  test('handles edge cases gracefully', () => {
    const invalidScores = { roi: null, achievability: 90 };
    expect(() => calculateRAPIDScore(invalidScores)).toThrow('Invalid score values');
  });
});
```

**Integration Tests (20% of test coverage)**
```javascript
// Example: Testing API endpoints
describe('Auto-Triage API', () => {
  test('POST /api/auto-triage returns valid assessment', async () => {
    const ideaData = {
      title: 'Test Idea',
      description: 'A test government service improvement'
    };
    
    const response = await request(app)
      .post('/api/auto-triage')
      .send(ideaData)
      .expect(200);
      
    expect(response.body).toHaveProperty('rapidScore');
    expect(response.body.rapidScore).toBeGreaterThan(0);
  });
});
```

**End-to-End Tests (10% of test coverage)**
```javascript
// Example: Testing complete user workflows
describe('Idea Submission Workflow', () => {
  test('user can submit idea and receive assessment', async () => {
    // Navigate to submission form
    await page.goto('/submit-idea.html');
    
    // Fill out form
    await page.fill('#idea-title', 'Automate Permit Processing');
    await page.fill('#idea-description', 'Citizens wait too long for permits...');
    
    // Submit and wait for results
    await page.click('#submit-button');
    await page.waitForSelector('.assessment-results');
    
    // Verify results displayed
    const rapidScore = await page.textContent('.rapid-score');
    expect(parseInt(rapidScore)).toBeGreaterThan(0);
  });
});
```

### Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage report
npm run test:coverage

# Run tests in watch mode during development
npm run test:watch

# Run specific test suite
npm test -- --grep "RAPID Score"

# Run end-to-end tests
npm run test:e2e

# Run security tests
npm run test:security
```

---

*This development guide provides comprehensive information for contributing to the GSD-DE project. For additional questions or support, please consult the team resources or reach out through the established channels.*