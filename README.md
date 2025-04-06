# 🔐 AWS Whitelist IP GitHub Action

Automatically **whitelist or revoke GitHub Actions' public IP** from an AWS EC2 Security Group.  
Useful for allowing temporary access (e.g., SSH or API access) to your EC2 instances during workflows.

## 🚀 Features

- Retrieves the public IP of the current GitHub Actions runner
- Whitelists or removes the IP from a specified AWS Security Group
- Supports custom port and AWS region
- Built with simple shell logic for easy debugging

---

## Usage

### Basic Example

```yaml
jobs:
  manage-security-group:
    runs-on: ubuntu-latest
    steps:
      - name: Whitelist GitHub Actions IP
        uses: bbharathkumarreddy/aws-whitelist-ip@v1.0
        with:
          security-group-id: sg-1234567890abcdef0
          action: whitelist
          port: 22
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Remove GitHub Actions IP
        uses: bbharathkumarreddy/aws-whitelist-ip@v1.0
        with:
          security-group-id: sg-1234567890abcdef0
          action: remove
          port: 22
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
```

## Inputs

| Name                  | Description                              | Required | Default  |
|-----------------------|------------------------------------------|----------|----------|
| `security-group-id`   | AWS Security Group ID                    | Yes      | N/A      |
| `aws-access-key-id`   | AWS Access Key ID                        | Yes      | N/A      |
| `aws-secret-access-key` | AWS Secret Access Key                 | Yes      | N/A      |
| `aws-region`          | AWS region of the Security Group         | Yes      | N/A      |
| `action`              | Choose 'whitelist' to add or 'remove' to revoke the IP | No       | `whitelist` |
| `port`                | Port to allow/revoke access on           | No       | `22`     |

## Outputs

| Name      | Description                          |
|-----------|--------------------------------------|
| `ipv4`      | The GitHub Actions Public IPv4 address |

## Contributing

Want to contribute? ✅