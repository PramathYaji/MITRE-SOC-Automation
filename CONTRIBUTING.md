# Contributing to SOC-in-a-Box

Thank you for your interest in contributing to SOC-in-a-Box! This document provides guidelines for contributions.

## How to Contribute

### Reporting Issues

If you find a bug or have a suggestion:

1. Check if the issue already exists
2. Create a new issue with:
   - Clear title and description
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - System information (OS, Docker version)
   - Relevant logs

### Submitting Changes

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Test thoroughly**
5. **Commit with clear messages**
   ```bash
   git commit -m "Add: Brief description of changes"
   ```
6. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Create a Pull Request**

## Contribution Areas

### Detection Rules

Adding new Wazuh detection rules:

1. Use rule IDs in range 100000-199999
2. Map to MITRE ATT&CK technique
3. Include test cases
4. Document in detection-rules/README.md

Example:
```xml
<rule id="100XXX" level="12">
  <if_sid>parent_rule</if_sid>
  <field name="field_name" type="pcre2">regex_pattern</field>
  <description>Clear description</description>
  <mitre>
    <id>TXXXX.XXX</id>
  </mitre>
  <group>category,tags,</group>
</rule>
```

### Playbooks

Adding Shuffle playbooks:

1. Export playbook JSON from Shuffle
2. Place in `playbooks/shuffle/`
3. Document in `playbooks/README.md`
4. Include:
   - Purpose
   - Trigger conditions
   - Required integrations
   - Expected outcome

### Attack Scenarios

Adding attack scenarios:

1. Create in `docs/attack-scenarios/`
2. Include:
   - Objective
   - MITRE ATT&CK techniques
   - Step-by-step commands
   - Expected detections
   - Safety warnings

### Documentation

Improving documentation:

- Fix typos and grammar
- Add clarifications
- Include examples
- Update outdated information
- Add troubleshooting tips

## Code Style

### Bash Scripts

```bash
#!/bin/bash
# Script description
# Author: Your Name

set -e  # Exit on error

# Clear variable names
WAZUH_MANAGER="wazuh.manager"

# Functions with clear purposes
function check_service() {
    docker ps | grep -q "$1"
}

# Proper error handling
if ! check_service "$WAZUH_MANAGER"; then
    echo "Error: Wazuh manager not running"
    exit 1
fi
```

### PowerShell

```powershell
# Script description
# Author: Your Name

# Use approved verbs
function Test-WazuhAgent {
    param(
        [string]$AgentName
    )
    
    # Clear logic
    $service = Get-Service -Name "WazuhSvc" -ErrorAction SilentlyContinue
    if ($service -and $service.Status -eq "Running") {
        return $true
    }
    return $false
}
```

### Documentation

- Use Markdown format
- Include code examples with syntax highlighting
- Add tables for structured data
- Use headers for organization
- Include links to related docs

## Testing

Before submitting:

1. **Test your changes**
   - Deploy in clean environment
   - Verify all components work
   - Test attack scenarios

2. **Check documentation**
   - Ensure accuracy
   - Update affected sections
   - Fix broken links

3. **Verify detection rules**
   - Test with actual attacks
   - Confirm MITRE mapping
   - Check for false positives

## Commit Messages

Format:
```
Type: Brief description (50 chars max)

Detailed explanation if needed (wrap at 72 chars)

Fixes: #issue_number (if applicable)
```

Types:
- `Add:` New feature or file
- `Fix:` Bug fix
- `Update:` Modification to existing feature
- `Docs:` Documentation changes
- `Refactor:` Code restructuring
- `Test:` Adding or updating tests

Examples:
```
Add: PowerShell download detection rule

Implements detection for PowerShell download-and-execute
patterns using Invoke-WebRequest and downloadstring.

Maps to MITRE T1059.001 and T1105.
Tested with Atomic Red Team test cases.

Fixes: #42
```

## Pull Request Guidelines

### Title
Clear and descriptive:
- ✅ `Add ransomware detection rules`
- ❌ `Update rules`

### Description
Include:
```markdown
## Changes
- What was changed
- Why it was changed

## Testing
- How you tested
- Results

## Related Issues
Fixes #123
Relates to #456

## Checklist
- [ ] Code tested locally
- [ ] Documentation updated
- [ ] No breaking changes
- [ ] Follows project style
```

## Review Process

1. Maintainer reviews PR
2. Feedback provided if changes needed
3. Once approved, PR is merged
4. Changes appear in main branch

## Recognition

Contributors will be acknowledged in:
- README.md contributors section
- Release notes
- Project documentation

## Questions?

- Open an issue for questions
- Join discussions
- Contact maintainers

## Code of Conduct

### Our Standards

- Be respectful and inclusive
- Accept constructive criticism
- Focus on what's best for the project
- Show empathy towards others

### Unacceptable Behavior

- Harassment or discrimination
- Trolling or insulting comments
- Personal or political attacks
- Publishing others' private information

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to SOC-in-a-Box! 🛡️
