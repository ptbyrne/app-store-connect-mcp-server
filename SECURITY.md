# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |

## Reporting a Vulnerability

We take security vulnerabilities seriously. If you discover a security issue, please report it responsibly.

### Preferred Method: Private Vulnerability Reporting

Please use GitHub's [private vulnerability reporting](https://github.com/ptbyrne/app-store-connect-mcp-server/security/advisories/new) feature to report security issues. This allows us to:

- Discuss the vulnerability privately
- Develop a fix before public disclosure
- Coordinate responsible disclosure

### What to Include

When reporting a vulnerability, please include:

1. **Description**: A clear description of the vulnerability
2. **Impact**: The potential impact if exploited
3. **Reproduction Steps**: Detailed steps to reproduce the issue
4. **Affected Versions**: Which versions are affected
5. **Suggested Fix**: If you have one (optional)

### What to Expect

- **Acknowledgment**: Within 48 hours of your report
- **Status Update**: Within 7 days with our assessment
- **Resolution**: We aim to address critical issues within 30 days

### Scope

This security policy applies to:

- The MCP server code in this repository
- Configuration and deployment guidance

**Out of Scope**:
- Issues in Apple's App Store Connect API itself
- Third-party dependencies (report to their maintainers, but let us know)

## Security Best Practices for Users

When using this MCP server:

1. **Protect your .p8 key file**: Never commit it to version control
2. **Use environment variables**: Store credentials securely
3. **Limit API key permissions**: Only grant necessary capabilities
4. **Rotate keys regularly**: Follow Apple's recommendations
5. **Monitor access logs**: Watch for unauthorized usage

## Acknowledgments

We appreciate security researchers who help keep this project secure. Contributors who report valid vulnerabilities will be acknowledged here (with permission).
