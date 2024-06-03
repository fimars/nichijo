---
title: "My posh profile"
description: ""
pubDate: "1/23 2024"
---

`cat $PROFILE`

```ps1
# https://github.com/gluons/powershell-git-aliases
Import-Module git-aliases -DisableNameChecking

Set-Alias -Name c -Value code

# λ "
function prompt {
    $color = Get-Random -Min 1 -Max 16
    $leaf = Split-Path -Path $(Get-Location) -Leaf -Resolve
    Write-Host ("" + $Leaf + " λ ") -NoNewLine `
     -ForegroundColor $Color
    return " "
}
```
