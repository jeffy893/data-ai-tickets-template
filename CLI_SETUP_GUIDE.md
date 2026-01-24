# CLI Tools Setup Guide for Data Analysis

This guide explains what CLI tools you need to install and configure to run the demos in this repository.

## Required CLI Tools

### 1. Snowflake CLI (`snow`)

**Purpose:** Execute SQL queries, manage Snowflake objects, and interact with your data warehouse.

**Installation:**
```bash
# macOS (Homebrew)
brew tap snowflakedb/snowflake-cli
brew install snowflake-cli

# Or using pip
pip install snowflake-cli-labs
```

**Configuration:**
```bash
# Create connection configuration
snow connection add

# You'll need:
# - Account identifier (e.g., xy12345.us-east-1)
# - Username
# - Password or key-pair authentication
# - Default warehouse, database, schema, role
```

**Credentials Required:**
- Snowflake account credentials
- Duo Security for MFA (if enabled)
- Warehouse access permissions

**Documentation:** https://docs.snowflake.com/en/developer-guide/snowflake-cli/

---

### 2. Atlassian CLI (`acli`)

**Purpose:** Manage Jira tickets, create issues, post comments, and automate ticket workflows.

**Installation:**
```bash
# Download from Atlassian
# Visit: https://bobswift.atlassian.net/wiki/spaces/ACLI/overview

# macOS installation
# Download the .zip file and extract to /usr/local/bin or ~/bin
```

**Configuration:**
```bash
# Set up connection to your Jira instance
acli jira --server "https://your-domain.atlassian.net" \
  --user "your-email@company.com" \
  --password "your-api-token"

# Or create a config file at ~/.acli/config.properties
```

**Credentials Required:**
- Atlassian account email
- API token (generate at: https://id.atlassian.com/manage-profile/security/api-tokens)
- Jira project access permissions

**Documentation:** https://bobswift.atlassian.net/wiki/spaces/ACLI/overview

---

### 3. GitHub CLI (`gh`)

**Purpose:** Create pull requests, manage issues, and interact with GitHub repositories.

**Installation:**
```bash
# macOS (Homebrew)
brew install gh

# Linux (Debian/Ubuntu)
sudo apt install gh

# Windows (Scoop)
scoop install gh
```

**Configuration:**
```bash
# Authenticate with GitHub
gh auth login

# Follow the prompts to authenticate via browser or token
```

**Credentials Required:**
- GitHub account
- Personal access token (or authenticate via browser)

**Documentation:** https://cli.github.com/manual/

---

### 4. Databricks CLI (`databricks`)

**Purpose:** Manage Databricks workspaces, jobs, notebooks, and DBFS files.

**Installation:**
```bash
# Using pip
pip install databricks-cli

# Or using Homebrew
brew tap databricks/tap
brew install databricks
```

**Configuration:**
```bash
# Configure authentication
databricks configure --token

# You'll need:
# - Databricks workspace URL (e.g., https://your-workspace.cloud.databricks.com)
# - Personal access token
```

**Credentials Required:**
- Databricks workspace URL
- Personal access token (generate in User Settings > Access Tokens)
- Workspace access permissions

**Documentation:** https://docs.databricks.com/dev-tools/cli/

---

### 5. AWS CLI (`aws`)

**Purpose:** Interact with AWS services including S3, Athena, and other cloud resources.

**Installation:**
```bash
# macOS (Homebrew)
brew install awscli

# Linux
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Windows
# Download installer from: https://aws.amazon.com/cli/
```

**Configuration:**
```bash
# Configure AWS credentials
aws configure

# You'll need:
# - AWS Access Key ID
# - AWS Secret Access Key
# - Default region (e.g., us-east-1)
# - Default output format (json recommended)
```

**Credentials Required:**
- AWS Access Key ID
- AWS Secret Access Key
- IAM permissions for S3, Athena, and other services you'll use

**Documentation:** https://docs.aws.amazon.com/cli/

---

## Optional but Recommended Tools

### Enhanced Analysis Tools

```bash
# macOS installation (all at once)
brew install tree jq bat ripgrep fd fzf

# Individual installations:
brew install tree      # Directory visualization
brew install jq        # JSON processing
brew install bat       # Syntax highlighting
brew install ripgrep   # Fast search (rg)
brew install fd        # File finder
brew install fzf       # Interactive selection
```

### Data Science Tools

```bash
# CSV and data manipulation
brew install csvkit    # CSV toolkit
brew install duckdb    # Fast analytical SQL
brew install miller    # Data transformation (mlr)
brew install yq        # YAML/JSON processor
brew install xsv       # Fast CSV toolkit
brew install hyperfine # Benchmarking

# Python data science packages
pip install pandas numpy matplotlib seaborn plotly \
  snowflake-connector-python sqlalchemy openpyxl \
  xlsxwriter requests beautifulsoup4 scipy scikit-learn

# Jupyter for notebooks
pip install jupyterlab
```

---

## Verification

After installation, verify each tool is working:

```bash
# Snowflake CLI
snow --version
snow connection list

# Atlassian CLI
acli --version

# GitHub CLI
gh --version
gh auth status

# Databricks CLI
databricks --version
databricks workspace list /

# AWS CLI
aws --version
aws s3 ls  # Should list your S3 buckets if configured

# Optional tools
tree --version
jq --version
bat --version
rg --version
```

---

## Account Setup Summary

To run all demos, you'll need accounts and credentials for:

1. **Snowflake**
   - Account identifier
   - Username/password or key-pair
   - Warehouse, database, schema access
   - Duo Security (if MFA enabled)

2. **Atlassian/Jira**
   - Jira account email
   - API token
   - Project access permissions

3. **GitHub**
   - GitHub account
   - Personal access token or browser authentication

4. **Databricks**
   - Workspace URL
   - Personal access token
   - Workspace permissions

5. **AWS**
   - Access Key ID
   - Secret Access Key
   - IAM permissions for services used

---

## Troubleshooting

### Snowflake Connection Issues
- Verify account identifier format (include region)
- Check Duo Security timeout (15-minute lockout)
- Ensure warehouse is running and accessible

### Jira API Token Issues
- Generate new token at: https://id.atlassian.com/manage-profile/security/api-tokens
- Ensure token has appropriate permissions
- Check Jira instance URL format

### Databricks Authentication
- Verify workspace URL includes https://
- Check token hasn't expired
- Ensure you have workspace access

### AWS Credentials
- Verify credentials in ~/.aws/credentials
- Check IAM permissions for required services
- Ensure region is correctly configured

---

## Next Steps

Once all tools are installed and configured:

1. Review the `KIRO.md` file for AI assistant instructions
2. Explore the `.kiro/steering/` files for detailed workflows
3. Check the `videos/` folder for example implementations
4. Try running a simple query: `snow sql -q "SELECT CURRENT_VERSION()" --format csv`

For detailed usage examples, see the video demonstrations in the `videos/` folder.
