# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 0.1.x   | :white_check_mark: |

## Reporting a Vulnerability

We take the security of ProxyDeck seriously. If you have discovered a security vulnerability, we appreciate your help in disclosing it to us responsibly.

### How to Report

**Please do NOT report security vulnerabilities through public GitHub issues.**

Instead, please report them via one of the following methods:

1. **Email**: Send an email to security@amslertec.ch with:
   - A description of the vulnerability
   - Steps to reproduce the issue
   - Potential impact of the vulnerability
   - Any possible mitigations you've identified

2. **GitHub Security Advisories**: Use [GitHub's private vulnerability reporting](https://github.com/pamsler/proxydeck/security/advisories/new)

### What to Include

Please include the following information in your report:

- Type of vulnerability (e.g., SQL injection, XSS, authentication bypass)
- Full paths of affected source files
- Step-by-step instructions to reproduce the vulnerability
- Proof-of-concept or exploit code (if possible)
- Impact assessment and potential attack scenarios

### Response Timeline

- **Initial Response**: Within 48 hours
- **Status Update**: Within 7 days
- **Resolution Target**: Within 30 days (depending on complexity)

### What to Expect

1. **Acknowledgment**: We will acknowledge receipt of your vulnerability report
2. **Communication**: We will keep you informed about our progress
3. **Credit**: We will credit you in our release notes (unless you prefer to remain anonymous)
4. **No Legal Action**: We will not pursue legal action against researchers who follow responsible disclosure practices

### Scope

The following are in scope for security reports:

- ProxyDeck application code
- Authentication and authorization mechanisms
- WAF bypass vulnerabilities
- SSL/TLS certificate handling
- API security issues
- Docker container security

### Out of Scope

- Vulnerabilities in third-party dependencies (please report to the respective projects)
- Social engineering attacks
- Physical security issues
- Denial of Service attacks that require significant resources

## Security Best Practices

When deploying ProxyDeck, please ensure:

1. Use strong, unique passwords for `ADMIN_USER` and `ADMIN_PASS`
2. Keep `JWT_SECRET` and `MFA_ENCRYPTION_KEY` secure and unique
3. Enable MFA for admin access
4. Keep the application updated to the latest version
5. Use firewall rules to restrict access to the management interface
6. Regularly review WAF rules and access logs

## Acknowledgments

We would like to thank the following security researchers for their responsible disclosures:

*No reports yet - be the first!*
