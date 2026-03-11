# Security Policy

## Reporting a Vulnerability

Please report any security vulnerabilities by opening an issue or contacting the repository owner.

## Secure Coding Guidelines

### What Sensitive Data Must Never Be Pushed to Git Repositories
To maintain the security of the project, the following sensitive data should **never** be committed to version control:
- **API Keys & Tokens**: Passwords, AWS access keys, GitHub personal access tokens, Stripe API keys, etc.
- **Database Credentials**: Connection strings, usernames, and passwords for databases.
- **Private Keys**: SSH private keys, SSL/TLS certificates, and cryptographic keys.
- **Configuration Files with Secrets**: `.env` files, `application.yml`, or any file containing configuration secrets.
- **Personally Identifiable Information (PII)**: User names, email addresses, phone numbers, or any compliance-related data (e.g., HIPAA, GDPR).

If your code requires these variables, use environment variables or a secure secrets manager.

### Environment Variables and `.env` Files
Proper management of configuration is critical:
- **Never Commit `.env` Files**: By design, `.env` files contain sensitive credentials meant solely for your local environment or specific deployment servers. Adding a `.env` file to `.gitignore` ensures it never accidentally enters the source repository.
- **Use `.env.example`**: Instead of committing `.env`, commit a `.env.example` or `.env.template` file containing the *names* of the required environment variables (without the actual secret values). This shows other developers what variables they need to configure the project.
- **Secret Managers for Production**: In production environments, prefer dedicated secret management solutions (like AWS Secrets Manager, HashiCorp Vault, or GitHub Secrets) over flat files.

### The Risks of Committing Secrets
Committing secrets to a git repository, even briefly, can lead to severe consequences:
- **Unauthorized Access**: Attackers can use leaked credentials to access databases, cloud infrastructure, or third-party services.
- **Data Breaches**: Access to sensitive systems can lead to exfiltration of user data, resulting in compliance violations and loss of reputation.
- **Financial Loss**: Leaked cloud credentials can be used for malicious purposes like cryptomining, leading to massive unexpected bills.
- **Irreversible Exposure**: Once a secret is pushed to a remote repository, it must be considered compromised. Even if you remove it in a subsequent commit, it remains in the git history and might have already been cloned or scraped by bots.

### The Difference Between Public and Private Repositories
Understanding repository visibility is crucial for managing security:
- **Public Repositories**: Code is visible to anyone on the internet. Any pushed secret is instantly compromised and often scraped by automated bots within seconds. Absolute diligence is required to prevent leaks.
- **Private Repositories**: Code is visible only to explicitly authorized users. While this provides a layer of access control, it is **not** a reason to commit secrets. Internal threats, leaked access tokens, or misconfigurations can still expose private repositories. Always practice the principle of least privilege and keep secrets out of private repos as well.
