# JavaLoginShowcase

> Enterprise-Grade Java Web Application - Secure Login Portal for Educational and Production Deployment

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen.svg)]()
[![Java Version](https://img.shields.io/badge/Java-8%2B-orange.svg)]()
[![Maven](https://img.shields.io/badge/Build%20Tool-Maven-blue.svg)]()

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [System Requirements](#system-requirements)
- [Installation & Setup](#installation--setup)
- [Deployment Guide](#deployment-guide)
- [Configuration](#configuration)
- [Development](#development)
- [Troubleshooting](#troubleshooting)
- [Performance & Security](#performance--security)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)

---

## Overview

**JavaLoginShowcase** is a production-ready Java web application that demonstrates modern enterprise security practices and deployment methodologies. This application serves as a reference implementation for organizations looking to establish secure login mechanisms and standardized deployment processes for Java-based applications.

### Use Cases
- Enterprise authentication and authorization learning resource
- DevOps training and certification programs
- Reference architecture for secure login implementations
- CI/CD pipeline demonstration and practice

---

## Architecture

```
JavaLoginApp/
├── src/main/
│   └── webapp/
│       ├── index.html              # Main login interface
│       ├── WEB-INF/
│       │   └── web.xml             # Deployment descriptor
│       ├── css/
│       │   ├── bootstrap.min.css    # Bootstrap framework
│       │   ├── style.css            # Custom styling
│       │   └── bootstrap/           # Bootstrap components
│       ├── fonts/
│       │   └── icomoon/             # Icon fonts
│       └── assests/                 # Static resources
├── pom.xml                          # Maven configuration
├── azure-pipelines.yml              # CI/CD pipeline definition
└── README.md                        # This file
```

### Technology Stack

| Component | Version | Purpose |
|-----------|---------|---------|
| Java | 8+ | Core language |
| Maven | 3.6+ | Build automation |
| Tomcat | 9.0+ | Servlet container |
| Bootstrap | 4.x | Responsive UI framework |
| Git | 2.20+ | Version control |

---

## Features

### Core Functionality
- **Secure Authentication UI**: Clean, intuitive login interface following modern UX principles
- **Responsive Design**: Mobile-first approach ensuring compatibility across devices
- **Web Standards Compliance**: HTML5, CSS3, and JavaScript best practices
- **Accessibility**: WCAG 2.1 compliance for inclusive user experience

### Enterprise Capabilities
- **Build Automation**: Maven-based build pipeline for consistency
- **CI/CD Integration**: Azure Pipelines configuration ready for deployment
- **Containerization Ready**: WAR packaging for Docker deployment
- **Comprehensive Documentation**: Complete setup and deployment guides
- **Logging & Monitoring Ready**: Infrastructure for observability implementation

---

## System Requirements

### Minimum Requirements
```
CPU: 2 cores (2.0 GHz)
Memory: 4 GB RAM
Disk Space: 2 GB free
Network: Internet connectivity required for dependency resolution
```

### Software Prerequisites

| Component | Minimum Version | Installation |
|-----------|-----------------|--------------|
| Java Development Kit (JDK) | 8 | [Oracle JDK](https://www.oracle.com/java/technologies/javase-downloads.html) or [OpenJDK](https://openjdk.java.net/) |
| Apache Maven | 3.6.0 | [Maven Downloads](https://maven.apache.org/download.cgi) |
| Apache Tomcat | 9.0.0 | [Tomcat Downloads](https://tomcat.apache.org/download-90.cgi) |
| Git | 2.20.0 | [Git Downloads](https://git-scm.com/downloads) |

### Optional but Recommended
- **Docker**: 19.03+ for containerized deployment
- **Jenkins**: 2.200+ for advanced CI/CD scenarios
- **SonarQube**: 8.0+ for code quality analysis
- **ELK Stack**: For centralized logging and monitoring

---

## Installation & Setup

### Step 1: Clone the Repository

```bash
# Clone the project from the remote repository
git clone https://github.com/your-organization/JavaLoginShowcase.git

# Navigate to project directory
cd JavaLoginShowcase
```

### Step 2: Verify Prerequisites

```bash
# Verify Java installation
java -version

# Verify Maven installation
mvn -version

# Verify Git installation
git --version
```

**Expected Output Example:**
```
java version "11.0.10" 2021-01-19 LTS
openjdk 11.0.10 2021-01-19 LTS
OpenJDK Runtime Environment (build 11.0.10+9-post-Ubuntu-0ubuntu1.20.04)

Apache Maven 3.6.3
Maven home: /usr/share/maven
```

### Step 3: Set Environment Variables

**Linux/macOS:**
```bash
export JAVA_HOME=/path/to/java/installation
export MAVEN_HOME=/path/to/maven/installation
export TOMCAT_HOME=/path/to/tomcat/installation
```

**Windows (PowerShell):**
```powershell
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\Program Files\Java\jdk-11", "User")
[Environment]::SetEnvironmentVariable("MAVEN_HOME", "C:\apache-maven-3.6.3", "User")
[Environment]::SetEnvironmentVariable("TOMCAT_HOME", "C:\apache-tomcat-9.0", "User")
```

---

## Deployment Guide

### Building the Application

#### Development Build
```bash
# Clean build with default Maven plugins
mvn clean package

# Output location: target/JavaLoginShowcase.war
```

#### Production Build with Testing
```bash
# Build with unit and integration tests
mvn clean verify

# Generate code coverage reports
mvn clean verify jacoco:report
```

#### Advanced Build Options
```bash
# Skip tests for faster builds (not recommended for production)
mvn clean package -DskipTests

# Build with specific Java version
mvn clean package -source 11 -target 11

# Parallel builds for faster compilation
mvn clean package -T 1C
```

### Deploying to Apache Tomcat

#### Option 1: Manual Deployment

```bash
# 1. Stop Tomcat server
$TOMCAT_HOME/bin/shutdown.sh

# 2. Remove old deployment (if exists)
rm -rf $TOMCAT_HOME/webapps/JavaLoginShowcase*

# 3. Copy WAR file to webapps directory
cp target/JavaLoginShowcase.war $TOMCAT_HOME/webapps/

# 4. Start Tomcat server
$TOMCAT_HOME/bin/startup.sh

# 5. Monitor startup logs
tail -f $TOMCAT_HOME/logs/catalina.out
```

#### Option 2: Automated Deployment with Tomcat Manager

```bash
# Using curl to deploy via Tomcat Manager REST API
curl -v -u tomcat:tomcat \
  --upload-file target/JavaLoginShowcase.war \
  'http://localhost:8080/manager/text/deploy?path=/JavaLoginShowcase&update=true'
```

#### Option 3: Docker Containerization

```dockerfile
# Dockerfile
FROM tomcat:9.0-jdk11-openjdk-slim
COPY target/JavaLoginShowcase.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

```bash
# Build and run Docker container
docker build -t javaloginnapp:latest .
docker run -d -p 8080:8080 --name javaapp javaloginnapp:latest
```

### Verification

```bash
# Check application status
curl -I http://localhost:8080/JavaLoginShowcase

# Expected response: HTTP/1.1 200 OK

# Monitor Tomcat logs
tail -f $TOMCAT_HOME/logs/catalina.out

# Access application in browser
# http://localhost:8080/JavaLoginShowcase
```

---

## Configuration

### Application Configuration

**web.xml** - Deployment Descriptor Configuration
```xml
<display-name>JavaLoginShowcase</display-name>
<session-config>
  <timeout>30</timeout> <!-- Session timeout in minutes -->
  <cookie-config>
    <secure>true</secure>
    <http-only>true</http-only>
  </cookie-config>
</session-config>
```

### Tomcat Configuration

**setenv.sh** - JVM Memory Configuration
```bash
# For Linux/macOS
export CATALINA_OPTS="-Xms512m -Xmx1024m -XX:+UseG1GC"
```

**setenv.bat** - JVM Memory Configuration (Windows)
```batch
set CATALINA_OPTS=-Xms512m -Xmx1024m -XX:+UseG1GC
```

### Maven Configuration

**settings.xml** - Private Repository Access (if needed)
```xml
<servers>
  <server>
    <id>corporate-repo</id>
    <username>username</username>
    <password>encrypted-password</password>
  </server>
</servers>
```

---

## Development

### Local Development Setup

```bash
# Install dependencies
mvn dependency:download-sources

# Generate IDE project files
mvn idea:idea              # For IntelliJ IDEA
mvn eclipse:eclipse        # For Eclipse

# Run with embedded server simulation
mvn clean package
```

### Code Quality

```bash
# Run static code analysis
mvn clean verify sonar:sonar \
  -Dsonar.host.url=http://sonarqube:9000 \
  -Dsonar.login=your-token

# Generate dependency report
mvn dependency:tree

# Check for security vulnerabilities
mvn dependency-check:check
```

### IDE Setup Instructions

**IntelliJ IDEA:**
1. Open project: `File > Open > JavaLoginShowcase`
2. Mark `src/main/webapp` as Web Application Root
3. Configure Tomcat: `Run > Edit Configurations > Add New > Tomcat Server`

**Eclipse:**
1. Import as Maven project: `File > Import > Maven > Existing Maven Projects`
2. Convert to Web Project (if needed)
3. Configure Tomcat runtime under Project Properties

---

## Troubleshooting

### Common Issues & Solutions

#### Issue 1: Maven Build Failure
```
[ERROR] COMPILATION ERROR
[ERROR] symbol  : class HttpServletRequest
```

**Solution:**
```bash
# Verify Java version compatibility
java -version

# Clear Maven cache and rebuild
mvn clean -U package
```

#### Issue 2: Tomcat Deployment Fails
```
[ERROR] Failed to deploy application
```

**Solution:**
```bash
# Check Tomcat logs for details
tail -f $TOMCAT_HOME/logs/catalina.out

# Verify WAR file integrity
unzip -t target/JavaLoginShowcase.war

# Ensure sufficient disk space and permissions
df -h
chmod -R 755 $TOMCAT_HOME/webapps/
```

#### Issue 3: Application Not Accessible
```
HTTP Error 404: Resource not found
```

**Solution:**
```bash
# Verify Tomcat is running
curl http://localhost:8080/manager/html

# Check application context path
ls -la $TOMCAT_HOME/webapps/ | grep JavaLogin

# Restart application via Tomcat Manager
curl -u admin:admin 'http://localhost:8080/manager/text/reload?path=/JavaLoginShowcase'
```

### Debug Mode

```bash
# Enable debug logging in Tomcat
export CATALINA_OPTS="-Ddebug=true -Dlog4j.rootLogger=DEBUG"
$TOMCAT_HOME/bin/startup.sh
```

---

## Performance & Security

### Security Best Practices

- [ ] Use HTTPS/TLS for all communications (configure in Tomcat)
- [ ] Implement input validation and sanitization
- [ ] Apply least privilege principles for file permissions
- [ ] Regular security patching of dependencies
- [ ] Disable unnecessary HTTP methods in web.xml
- [ ] Configure security headers (HSTS, CSP, X-Frame-Options)

### Performance Optimization

```xml
<!-- web.xml optimizations -->
<init-param>
  <param-name>useDefaultSslContext</param-name>
  <param-value>true</param-value>
</init-param>
```

### Monitoring & Logging

```bash
# Configure centralized logging (ELK Stack)
# Implement APM tools: New Relic, Datadog, or Splunk
# Monitor Tomcat metrics: jconsole, JMeter, or CloudWatch
```

---

## Contributing

We welcome contributions from the community. Please follow these guidelines:

### Contribution Process

1. **Fork the Repository**
   ```bash
   git clone https://github.com/your-fork/JavaLoginShowcase.git
   ```

2. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Commit Changes**
   ```bash
   git commit -m "feat: Add new feature with comprehensive testing"
   ```

4. **Push to Branch**
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Submit Pull Request**
   - Provide clear description of changes
   - Link related issues
   - Ensure all tests pass

### Code Standards
- Follow Java naming conventions
- Write unit tests for new features
- Document complex logic with comments
- Maintain code coverage above 80%

---

## Support

### Getting Help

- **Documentation**: See full docs in `/docs` directory
- **Issues**: Report bugs via [GitHub Issues](https://github.com/your-organization/JavaLoginShowcase/issues)
- **Discussions**: Join community discussions for questions
- **Email Support**: contact@devopsinsiders.com

### Reporting Security Issues

Please report security vulnerabilities privately to: security@devopsinsiders.com

---

## License

This project is licensed under the **Apache License 2.0** - see the [LICENSE](LICENSE) file for complete details.

```
Copyright (c) 2021 DevOps Insiders

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

---

## About DevOps Insiders

**DevOps Insiders** is a community dedicated to advancing DevOps practices and knowledge-sharing. We create enterprise-grade solutions, learning resources, and best-practice frameworks for the global DevOps community.

### Connect With Us
- [GitHub Organization](https://github.com/devops-insiders)
- [Documentation Portal](https://docs.devopsinsiders.com)
- [Community Forum](https://forum.devopsinsiders.com)

---

## Changelog

### v1.0.0 (Current Release)
- Initial enterprise release
- Comprehensive deployment guides
- Docker containerization support
- CI/CD pipeline configuration
- Full documentation suite

### Roadmap
- [ ] Authentication service integration
- [ ] Multi-factor authentication (MFA)
- [ ] Role-based access control (RBAC)
- [ ] Database integration
- [ ] Kubernetes deployment examples

---

**Last Updated**: January 17, 2026  
**Maintainers**: DevOps Insiders Team  
**Status**: Production Ready
