# Project Documentation Rules (Non-Obvious Only)

- "bin/" directory contains main entry points (scoop.ps1)
- "lib/" contains modularized library functions (core.ps1, manifest.ps1, etc.)
- "libexec/" contains individual command implementations (scoop-install.ps1, etc.)
- PowerShell 5.1 and 7+ are both supported (unusual for Windows-focused projects)
- PSScriptAnalyzer specifically allows 'PSAvoidUsingWriteHost' rule for colored output
- Cross-platform checks use $IsLinux/$IsMacOS despite being Windows-focused project
- Git change detection is used in CI to selectively run tests (not all tests every time)
- Helper tools (7z, lessmsi, innounp) are required for decompression testing