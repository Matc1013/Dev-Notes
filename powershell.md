**1.批量添加exe联网防火墙规则**

```powershell
Get-ChildItem -Path "C:\xx\Programs" -Filter *.exe -Recurse | ForEach-Object {
    $ruleName = "XXX_Block"
    New-NetFirewallRule -DisplayName $ruleName -Direction Outbound -Program $_.FullName -Action Block
}
```
