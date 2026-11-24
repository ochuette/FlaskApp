# Theory questions

## 1. Why do we use GitHub secrets (DOCKER_USERNAME, DOCKER_PASSWORD) in ci.yml for authentication to Docker Hub?

- `ci.yml` is stored in the repository, so anyone who can read the repo (or its history) would see credentials written in it.
- Secrets are stored encrypted and injected only while the workflow runs.
- GitHub masks their values as `***` in the logs.
- They are not passed to workflows triggered from forked pull requests.
- They can be changed or rotated without editing any code.

## 2. What are the risks of storing sensitive information in CI/CD pipelines, and what are the best practices to reduce them?

**Risks**

- Secrets leaking through logs or `echo` commands.
- A malicious or compromised third-party action stealing them.
- Tokens with too many permissions or no expiry date.
- Secrets exposed to untrusted pull requests.
- Secrets committed to the repository by mistake.

**Best practices**

- Store credentials in GitHub secrets, never in plain text in files.
- Use access tokens with minimum permissions instead of passwords.
- Rotate tokens regularly.
- Pin actions to a specific version.
- Never print secrets in logs.
- Enable secret scanning.
- Restrict workflows on fork pull requests.
- Use short-lived credentials where possible.
