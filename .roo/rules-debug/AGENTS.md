# Project Debug Rules (Non-Obvious Only)

- PowerShell scripts require specific modules: Pester 5.2+, BuildHelpers 2.0.1+, PSScriptAnalyzer 1.17.1+
- Tests can be run with either PowerShell 5.1 or PowerShell 7+ (both supported)
- Windows-only tests are skipped on Linux/macOS using $IsLinux/$IsMacOS automatic variables
- Security protocol is manually configured to TLS 1.2 (3072) for compatibility
- SQLite cache is conditionally loaded based on USE_SQLITE_CACHE config setting
- Decompression tests require helper tools (7z, lessmsi, innounp) in CI environment
- Test execution can be limited via Git change detection in CI environments