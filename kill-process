@ECHO OFF

powershell -executionpolicy ByPass ^
    $ar_name = 'kill-process.cmd'; ^
    $log_file = 'C:\Program Files (x86)\ossec-agent\active-response\active-responses.log'; ^
    function Write-Log { ^
        param($message); ^
        $log_line = (Get-Date).ToString('yyyy-MM-dd hh:mm:ss')+' active-response/bin/'+$ar_name+': '; ^
        $log_line += $message; ^
        $log_line ^| Out-File -FilePath $log_file -Append -Encoding ASCII}; ^
    $alert = Read-Host; ^
    $alert_dict = ConvertFrom-Json $alert; ^
    $alert_id = $alert_dict.parameters.alert.id; ^
    $alert_cmd = $alert_dict.command; ^
    $processname = $alert_dict.parameters.alert.data.win.eventdata.originalFileName; ^
    if ($alert_cmd -eq 'add') { ^
            Write-Log 'Starting with Alert ID',$alert_id -join ' '; ^
	    taskkill /F /IM $processname; ^
	    Write-Log 'Active Response - Kill Process:',$processname -join ' '; ^
            }; ^
    Write-Log 'Ended'

:Exit
