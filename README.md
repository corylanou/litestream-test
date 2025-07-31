# Litestream Test Repository

This repository contains comprehensive test configurations and scripts for testing [Litestream](https://litestream.io/), a streaming replication tool for SQLite databases.

**Litestream Source Repository**: [https://github.com/benbjohnson/litestream](https://github.com/benbjohnson/litestream)

## Purpose

This repository serves as a testing ground for:

- Different Litestream configuration formats and options

- Replication strategies (file-based and S3-compatible)
- Database restoration from replicas

- LTX (Litestream Transaction) format testing
- Configuration validation and error handling

## Repository Structure

```text
├── *.yml                    # Various Litestream configuration files
├── create-test-db.sql       # SQL script to create test database
├── TEST-PLAN.md            # Detailed test plan documentation
├── LITESTREAM_LTX_TESTING_REPORT.md  # Test results and findings
├── TODO.md                 # Current task list based on Ben Johnson's feedback
├── CLAUDE.md               # Project guidelines for Claude
├── docs/images/            # Screenshots and images for documentation
└── litestream-source       # Source configuration file

```

## Configuration Files

- **litestream-test.yml**: Main test configuration with S3 and file replicas

- **litestream-defaults.yml**: Configuration using default settings
- **litestream-old-format.yml**: Legacy format configuration

- **litestream-invalid.yml**: Invalid configuration for error testing
- **file-replica.yml**: File-based replication only configuration

## Prerequisites

1. [Litestream](https://litestream.io/install/) installed

2. SQLite3 installed
3. (Optional) S3-compatible storage with credentials configured

4. (Optional) MinIO client (`mc`) for S3 testing

## Usage

### 1. Create Test Database

```bash
sqlite3 test.db < create-test-db.sql

```

### 2. Run Litestream with Different Configurations

```bash

# Main configuration with S3 and file replicas
litestream replicate -config litestream-test.yml

# File-only replication
litestream replicate -config file-replica.yml

# Test with defaults
litestream replicate -config litestream-defaults.yml

```

### 3. Restore from Replicas

```bash

# Restore from S3
litestream restore -config litestream-test.yml test.db restored-s3.db

# Restore from file replica
litestream restore -config file-replica.yml test2.db restored-file.db

# Restore using S3 URL directly
litestream restore -o restored-url.db s3://your-bucket/path/to/db

```

### 4. Validate Configurations

```bash

# This should fail with validation errors
litestream replicate -config litestream-invalid.yml

```

## Test Scenarios

The repository includes tests for:

1. **Basic Replication**: Testing file and S3 replication

2. **Configuration Formats**: Old vs new YAML format compatibility
3. **Default Settings**: Testing implicit default values

4. **Error Handling**: Invalid configuration detection
5. **Restoration**: Database recovery from different replica types

6. **LTX Format**: Transaction log format and compatibility

## Environment Variables

For S3 replication, configure:

- `AWS_ACCESS_KEY_ID`

- `AWS_SECRET_ACCESS_KEY`
- `AWS_ENDPOINT` (for S3-compatible services like MinIO)

## Notes

- Database files (*.db) and replicas are excluded from version control

- The `litestream` and `mc` binaries should be installed separately
- See TEST-PLAN.md for detailed testing procedures

- See LITESTREAM_LTX_TESTING_REPORT.md for test results
- See TODO.md for current development tasks and issues to address

## Contributing

This is a test repository for exploring Litestream functionality. Feel free to add new test cases or configuration scenarios.

## License

This test repository is for educational and testing purposes.
