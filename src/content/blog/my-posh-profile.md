---
title: 'posh profile'
description: ''
pubDate: '1/23 2024'
---

### Microsoft.PowerShell_profile.ps1

```ps1
# https://github.com/gluons/powershell-git-aliases
Import-Module git-aliases -DisableNameChecking

# oh-my-posh
# oh-my-posh init pwsh  --config "$env:POSH_THEMES_PATH\huvix.omp.json"  | Invoke-Expression
Set-Alias -Name c -Value code


# Imports End
#
#
# Code Start


# function Prompt { "λ " }
function prompt {
    $color = Get-Random -Min 1 -Max 16
    $leaf = Split-Path -Path $(Get-Location) -Leaf -Resolve
    Write-Host ("" + $Leaf + " λ ") -NoNewLine `
     -ForegroundColor $Color
    return " "
}
```
