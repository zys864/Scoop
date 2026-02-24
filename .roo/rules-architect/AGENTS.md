# Project Architecture Rules (Non-Obvious Only)

- Modular architecture splits functionality across three main directories: bin/, lib/, libexec/
- Dot sourcing is used instead of Import-Module for internal module loading
- Strict mode is intentionally turned OFF in entry points (opposite of typical PowerShell)
- Cross-platform capability exists despite being Windows-focused (supports $IsLinux/$IsMacOS)
- Conditional SQLite caching based on configuration (not always active)
- Manifest versioning uses @ syntax for specific version installations
- Resource cleanup requires explicit try/catch/finally blocks (no automatic disposal assumed)
- Security protocol manually configured to TLS 1.2 for compatibility across different .NET versions