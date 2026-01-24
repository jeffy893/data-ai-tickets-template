# Credentials and Accounts Checklist

Use this checklist to track what accounts and credentials you need to set up to run all demos in this repository.

## 🔐 Required Accounts and Credentials

### ☐ 1. Snowflake Account

**What you need:**
- [ ] Snowflake account (sign up at https://signup.snowflake.com/)
- [ ] Account identifier (format: `xy12345.us-east-1` or `orgname-accountname`)
- [ ] Username
- [ ] Password or key-pair authentication
- [ ] Warehouse name (e.g., `COMPUTE_WH`)
- [ ] Database name (e.g., `ANALYTICS`)
- [ ] Schema name (e.g., `PUBLIC`)
- [ ] Role name (e.g., `ACCOUNTADMIN` or `SYSADMIN`)
- [ ] Duo Security app (if MFA is enabled)

**Where to find:**
- Account identifier: Snowflake web UI → Account menu → Copy account identifier
- Warehouse/Database/Schema: Ask your Snowflake admin or check web UI

**Setup command:**
```bash
snow connection add
```

---

### ☐ 2. Atlassian/Jira Account

**What you need:**
- [ ] Jira account (company Jira instance or cloud account)
- [ ] Jira instance URL (e.g., `https://your-company.atlassian.net`)
- [ ] Account email address
- [ ] API token (NOT your password)
- [ ] Project access permissions

**Where to get API token:**
1. Go to https://id.atlassian.com/manage-profile/security/api-tokens
2. Click "Create API token"
3. Give it a name (e.g., "CLI Access")
4. Copy the token immediately (you won't see it again)

**Setup:**
Configure in `~/.acli/config.properties` or via command line

---

### ☐ 3. GitHub Account

**What you need:**
- [ ] GitHub account (sign up at https://github.com/signup)
- [ ] Personal access token (classic) OR
- [ ] Browser authentication (easier)

**Where to get personal access token (if needed):**
1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Select scopes: `repo`, `workflow`, `admin:org`
4. Copy the token

**Setup command:**
```bash
gh auth login
# Choose: GitHub.com → HTTPS → Browser authentication (easiest)
```

---

### ☐ 4. Databricks Account

**What you need:**
- [ ] Databricks workspace (company workspace or trial at https://databricks.com/try-databricks)
- [ ] Workspace URL (e.g., `https://your-workspace.cloud.databricks.com`)
- [ ] Personal access token
- [ ] Workspace access permissions

**Where to get personal access token:**
1. Log into Databricks workspace
2. Click your user icon → User Settings
3. Go to "Access tokens" tab
4. Click "Generate new token"
5. Give it a name and lifetime (e.g., 90 days)
6. Copy the token immediately

**Setup command:**
```bash
databricks configure --token
# Enter workspace URL and token when prompted
```

---

### ☐ 5. AWS Account

**What you need:**
- [ ] AWS account (sign up at https://aws.amazon.com/)
- [ ] IAM user with programmatic access
- [ ] Access Key ID
- [ ] Secret Access Key
- [ ] IAM permissions for services you'll use (S3, Athena, etc.)
- [ ] Default region (e.g., `us-east-1`)

**Where to get access keys:**
1. Log into AWS Console
2. Go to IAM → Users → Your user
3. Security credentials tab
4. Click "Create access key"
5. Choose "Command Line Interface (CLI)"
6. Copy Access Key ID and Secret Access Key

**Setup command:**
```bash
aws configure
# Enter Access Key ID, Secret Access Key, region, and output format (json)
```

---

## 📋 Verification Checklist

After setting up all credentials, verify each one works:

```bash
# ☐ Snowflake
snow connection list
snow sql -q "SELECT CURRENT_VERSION()" --format csv

# ☐ Atlassian/Jira
acli --version
acli jira project list --limit 5

# ☐ GitHub
gh auth status
gh repo view

# ☐ Databricks
databricks workspace list /
databricks clusters list

# ☐ AWS
aws sts get-caller-identity
aws s3 ls
```

---

## 🔒 Security Best Practices

### DO:
- ✅ Store credentials securely (use CLI config files, not environment variables in code)
- ✅ Use API tokens instead of passwords where possible
- ✅ Set token expiration dates (30-90 days recommended)
- ✅ Rotate tokens regularly
- ✅ Use least-privilege access (only permissions you need)
- ✅ Keep credentials in `.gitignore` files

### DON'T:
- ❌ Commit credentials to Git repositories
- ❌ Share credentials via email or Slack
- ❌ Use the same token for multiple purposes
- ❌ Give tokens unlimited lifetime
- ❌ Use root/admin accounts for daily work

---

## 📁 Where Credentials Are Stored

After configuration, your credentials will be stored in:

```
~/.snowflake/config.toml          # Snowflake connections
~/.acli/config.properties          # Atlassian CLI config
~/.config/gh/hosts.yml             # GitHub CLI auth
~/.databrickscfg                   # Databricks profiles
~/.aws/credentials                 # AWS access keys
~/.aws/config                      # AWS configuration
```

**Important:** These files contain sensitive information. Never commit them to Git!

---

## 🆘 Troubleshooting

### "Authentication failed" errors
- Verify credentials are correct
- Check if tokens have expired
- Ensure you have necessary permissions
- Try regenerating tokens

### "Connection timeout" errors
- Check your internet connection
- Verify service URLs are correct
- Check if services are behind VPN/firewall

### "Permission denied" errors
- Verify IAM/role permissions
- Check workspace/project access
- Contact your admin for access

---

## ✅ Ready to Start

Once you've checked off all items above and verified each CLI tool works, you're ready to:

1. Explore the `videos/` folder for working examples
2. Review `.kiro/steering/` files for workflows
3. Start working on your first ticket!

For detailed installation instructions, see **`CLI_SETUP_GUIDE.md`**
