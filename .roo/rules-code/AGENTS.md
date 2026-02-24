# Project Coding Rules (Non-Obvious Only)

- Always use dot sourcing to load modules: `. "$PSScriptRoot\..\lib\<module>.ps1"` (not Import-Module)
- Configuration values must be converted to lowercase: `$name = $name.ToLowerInvariant()`
- Error handling requires explicit try/catch/finally blocks for resource cleanup (especially file streams)
- Functions should return explicit boolean values instead of implicit ones
- Strict mode must be turned OFF in main entry points with `Set-StrictMode -Off`
- Use manual security protocol optimization for TLS 1.2 support: `[System.Net.ServicePointManager]::SecurityProtocol = 3072`
- Conditional SQLite database loading pattern: `if (get_config USE_SQLITE_CACHE) { ... }`
- Function aliases must be redefined to prioritize local functions over built-ins
- Manifest version specification uses @ syntax: `scoop install app@version`