# AGENTS.md

This file provides guidance to agents when working with code in this repository.

## Stack
- PowerShell 5.1+ project for Windows application management
- Uses Pester 5.2+ for testing framework
- Uses PSScriptAnalyzer for linting with custom settings
- Requires BuildHelpers module for CI/CD

## Build/Lint/Test Commands
- Run all tests: `./test/bin/test.ps1`
- Run specific test file: `Invoke-Pester -Path "test/Scoop-<specific>.Tests.ps1"`
- Lint with PSScriptAnalyzer: Tests automatically run during test execution
- Run tests with PowerShell 5.1: `pwsh -Command "./test/bin/test.ps1"`
- Run tests with PowerShell 7+: `pwsh -Command "./test/bin/test.ps1"`

## Code Style Guidelines
- Uses custom PSScriptAnalyzer settings that specifically allow 'PSAvoidUsingWriteHost' rule (for colored output)
- Modules are loaded via dot sourcing: `. "$PSScriptRoot\..\lib\<module>.ps1"`
- Functions often return early with explicit boolean values instead of implicit
- Strict mode is turned OFF with `Set-StrictMode -Off` in main entry points
- Uses `$IsLinux`, `$IsMacOS` automatic variables for cross-platform checks (though project is Windows-focused)

## Architecture Notes
- bin/: Contains main entry points (scoop.ps1)
- lib/: Contains core library functions split by functionality (core.ps1, manifest.ps1, etc.)
- libexec/: Contains individual command implementations (scoop-install.ps1, scoop-search.ps1, etc.)
- test/: Contains Pester tests organized by functionality

## Critical Patterns
- Configuration values are stored lowercase: `$name = $name.ToLowerInvariant()`
- Error handling uses try/catch with specific finally blocks for resource cleanup (especially file streams)
- Security protocol optimization is handled manually to support TLS 1.2
- SQLite database is conditionally loaded based on config: `if (get_config USE_SQLITE_CACHE) { ... }`
- Function aliases are redefined to prioritize local functions over built-ins
- Manifests can specify specific app versions using @ syntax: `scoop install app@version`

## Testing Specifics
- Tests are tagged with Pester tags (e.g., 'Linter', 'Scoop', 'Windows')
- Windows-only tests are skipped on Linux/macOS with conditional logic
- CI environment variables are checked for selective test execution
- Decompression tests require special helper tools (7z, lessmsi, innounp)
- Git changed file detection is used to selectively run tests in CI
- Tests must pass on both PowerShell 5.1 and PowerShell 7+