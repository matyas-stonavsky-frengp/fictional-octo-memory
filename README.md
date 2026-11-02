Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned -Force
$p = $PROFILE.AllUsersAllHosts
if (-not (Test-Path $p)) { New-Item -Path $p -ItemType File -Force | Out-Null }
if (-not (Select-String -Path $p -Pattern 'OPS_PROMPT' -Quiet)) {
Add-Content -Path $p -Value @'
# OPS_PROMPT
function prompt { "[$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')] $env:USERDOMAIN\$env:USERNAME@$env:COMPUTERNAME PS $($executionContext.SessionState.Path.CurrentLocation)> " }
'@
}
. $p# fictional-octo-memory
