# Nextflow Lint Pre-commit Hook

A pre-commit hook for running `nextflow lint` on Nextflow pipeline files.

## What is Nextflow Lint?

`nextflow lint` is a command provided by Nextflow that checks your pipeline scripts for common issues and best practices. It helps ensure your Nextflow workflows follow proper conventions and can catch potential problems early in development.

## Installation

### Prerequisites

- [Nextflow](https://www.nextflow.io/) must be installed and available in your PATH
- [pre-commit](https://pre-commit.com/) must be installed

### Setup

1. Add this hook to your `.pre-commit-config.yaml` file:

```yaml
repos:
  - repo: https://github.com/adamrtalbot/nf-lint-pre-commit
    rev: v0.1.0  # Use the ref you want to point at
    hooks:
      - id: nextflow-lint
```

2. Install the pre-commit hook:

```bash
pre-commit install
```

## Usage

Once installed, the hook will automatically run `nextflow lint` whenever you commit changes to `.nf` or `.config` files in your repository.

### Manual Execution

You can also run the hook manually:

```bash
# Run on all files
pre-commit run nextflow-lint --all-files

# Run on specific files
pre-commit run nextflow-lint --files main.nf
```

### Passing Arguments to Nextflow Lint

You can pass any `nextflow lint` arguments through the hook by adding them to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/adamrtalbot/nf-lint-pre-commit
    rev: v0.1.0
    hooks:
      - id: nextflow-lint
        # Basic linting with no arguments (default)
      
      # Or with formatting
      - id: nextflow-lint
        args: [-format]
        
      # Or with concise output
      - id: nextflow-lint
        args: [-output, concise]
        
      # Or with multiple options
      - id: nextflow-lint
        args: [-format, -sort-declarations]
        
      # Or with JSON output for CI systems
      - id: nextflow-lint
        args: [-output, json]
```

For detailed information about what `nextflow lint` checks, refer to the [Nextflow documentation](https://www.nextflow.io/docs/latest/reference/cli.html#lint).

## Troubleshooting

### Nextflow Not Found

If you get an error that nextflow is not found:

1. Make sure Nextflow is installed: `curl -s https://get.nextflow.io | bash`
2. Make sure it's in your PATH: `export PATH="$PATH:/path/to/nextflow"`
3. Verify installation: `nextflow -version`

### Hook Fails

If the lint check fails:

1. Review the output to understand what issues were found
2. Fix the issues in your Nextflow files
3. Commit again

### Skip Hook Temporarily

If you need to skip the hook for a specific commit:

```bash
git commit -m "Your commit message" --no-verify
```

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality in the GitHub Actions workflows
4. Ensure all CI tests pass
5. Submit a pull request

### Development Workflow

Please feel free to contribute to this project by opening an issue or a pull request.

### Running Tests Locally

You can test the hook directly during development:

```bash
# Install Nextflow (if not already installed)
curl -s https://get.nextflow.io | bash

# Test the hook directly
chmod +x nextflow-lint-hook
./nextflow-lint-hook

# Test with arguments
./nextflow-lint-hook -format
./nextflow-lint-hook -output concise

# Test with pre-commit
pip install pre-commit
pre-commit run --all-files
```

## License

This project is licensed under the MIT License.