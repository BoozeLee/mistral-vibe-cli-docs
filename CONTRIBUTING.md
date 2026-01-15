# Contributing to Mistral Vibe CLI Documentation

🎉 First off, thanks for taking the time to contribute! 🎉

The following is a set of guidelines for contributing to the Mistral Vibe CLI Documentation. These are mostly guidelines, not rules. Use your best judgment, and feel free to propose changes to this document in a pull request.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Pull Requests](#pull-requests)
- [Styleguides](#styleguides)
  - [Documentation Styleguide](#documentation-styleguide)
  - [Git Commit Messages](#git-commit-messages)
- [Development Setup](#development-setup)
- [Additional Notes](#additional-notes)

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to [boozelee@users.noreply.github.com](mailto:boozelee@users.noreply.github.com).

## How Can I Contribute?

### Reporting Bugs

This section guides you through submitting a bug report. Following these guidelines helps maintainers and the community understand your report, reproduce the behavior, and find related reports.

**Before Submitting A Bug Report:**
- Check the [issues](https://github.com/BoozeLee/mistral-vibe-cli-docs/issues) for existing reports
- Ensure the bug was not already fixed in the latest version
- Check if the issue is related to the documentation content or the Mistral Vibe CLI itself

**How Do I Submit A Good Bug Report?**

Bugs are tracked as [GitHub issues](https://github.com/BoozeLee/mistral-vibe-cli-docs/issues). Create an issue and provide the following information:

1. **Use a clear and descriptive title** for the issue
2. **Describe the exact steps to reproduce** the problem
3. **Provide specific examples** to demonstrate the steps
4. **Describe the behavior you observed** after following the steps
5. **Explain which behavior you expected** to see instead
6. **Include screenshots and animated GIFs** if they help explain the problem
7. **Specify your environment**: OS, browser, etc.

### Suggesting Enhancements

This section guides you through submitting an enhancement suggestion, including completely new features and minor improvements to existing functionality.

**Before Submitting An Enhancement Suggestion:**
- Check the [issues](https://github.com/BoozeLee/mistral-vibe-cli-docs/issues) for existing suggestions
- Check if the enhancement is already implemented in the latest version
- Ensure the enhancement is related to documentation, not the CLI itself

**How Do I Submit A Good Enhancement Suggestion?**

Enhancement suggestions are tracked as [GitHub issues](https://github.com/BoozeLee/mistral-vibe-cli-docs/issues). Create an issue and provide the following information:

1. **Use a clear and descriptive title** for the issue
2. **Provide a step-by-step description** of the suggested enhancement
3. **Describe the current behavior** and **explain which behavior you expected**
4. **Explain why this enhancement would be useful** to most users
5. **List some other documentation** where this enhancement exists
6. **Specify which version** you're using
7. **Specify the name and version** of the OS you're using

### Pull Requests

The process described here has several goals:
- Maintain documentation quality
- Fix problems that are important to users
- Engage the community in working toward the best possible documentation
- Enable a sustainable system for maintainers to review contributions

Please follow these steps to have your contribution considered:

1. **Fork the repository** and create your branch from `master`
2. **Follow the styleguides** outlined below
3. **If you've added code** that should be tested, add tests
4. **If you've changed APIs**, update the documentation
5. **Ensure the test suite passes**
6. **Make sure your code lints**
7. **Issue that pull request!**

**Pull Request Template:**
```markdown
## Description

Please include a summary of the change and which issue is fixed. Please also include relevant motivation and context.

## Type of change

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Other (please describe):

## Checklist:

- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
```

## Styleguides

### Documentation Styleguide

- Use **Markdown** for all documentation
- Follow **GitHub Flavored Markdown** specifications
- Use **clear, concise language**
- **Be consistent** with existing documentation style
- Use **proper heading hierarchy** (##, ###, ####)
- **Code examples** should be in fenced code blocks with language specification
- **Tables** should be used for comparative information
- **Lists** should be used for step-by-step instructions

### Git Commit Messages

- Use the **present tense** ("Add feature" not "Added feature")
- Use the **imperative mood** ("Move cursor to..." not "Moves cursor to...")
- **Limit the first line to 72 characters or less**
- **Reference issues and pull requests** liberally after the first line
- Consider starting the commit message with an applicable emoji:
  - 🎨 `:art:` when improving the format/structure of the code
  - 🚀 `:rocket:` when improving performance
  - 🐛 `:bug:` when fixing a bug
  - 📝 `:memo:` when writing docs
  - 💄 `:lipstick:` when improving the UI
  - 🔧 `:wrench:` when changing configuration files
  - ⚡ `:zap:` when improving performance

## Development Setup

### Prerequisites

- GitHub account
- Git installed
- Basic Markdown knowledge
- Understanding of Mistral Vibe CLI

### Setup

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/your-username/mistral-vibe-cli-docs.git
   cd mistral-vibe-cli-docs
   ```
3. **Set up upstream** remote:
   ```bash
   git remote add upstream https://github.com/BoozeLee/mistral-vibe-cli-docs.git
   ```
4. **Create a new branch** for your changes:
   ```bash
   git checkout -b your-feature-branch
   ```

### Making Changes

1. **Make your changes** to the documentation
2. **Test your changes** by previewing the Markdown
3. **Commit your changes** with a descriptive message:
   ```bash
   git commit -m "📝 Add section about X feature"
   ```
4. **Push to your fork**:
   ```bash
   git push origin your-feature-branch
   ```
5. **Create a Pull Request** from your fork to the main repository

### Keeping Your Fork Updated

```bash
# Fetch the latest changes from upstream
git fetch upstream

# Merge the changes into your local master branch
git checkout master
git merge upstream/master

# Update your feature branch
git checkout your-feature-branch
git merge master
```

## Additional Notes

### Issue and Pull Request Labels

This repository uses the following labels to help organize and prioritize work:

- `bug` - Issues that need to be fixed
- `enhancement` - Feature requests and improvements
- `documentation` - Documentation-related issues
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention is needed
- `question` - Further information is requested
- `wontfix` - This will not be worked on

### Community

Join our community discussions and get help:
- **GitHub Discussions**: For questions and ideas
- **Issue Tracker**: For bugs and feature requests
- **Pull Requests**: For contributions

### Recognition

We appreciate all contributions! Contributors will be recognized in:
- **Contributors section** of the README
- **Release notes** for significant contributions
- **GitHub profile** through contribution activity

### License

By contributing, you agree that your contributions will be licensed under the **MIT License**.

## Questions?

If you have any questions about contributing, please:
1. Check the [existing issues](https://github.com/BoozeLee/mistral-vibe-cli-docs/issues)
2. Review the [documentation](https://github.com/BoozeLee/mistral-vibe-cli-docs)
3. Ask in the [GitHub Discussions](https://github.com/BoozeLee/mistral-vibe-cli-docs/discussions)
4. Contact the maintainers at [boozelee@users.noreply.github.com](mailto:boozelee@users.noreply.github.com)

Happy contributing! 🚀