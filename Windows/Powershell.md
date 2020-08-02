# Powershell tricks

Get proxy

    Get-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings'

Send mail

```Powershell
Function Send-Mail($to, $subject, $body) {
    $Outlook = New-Object -ComObject Outlook.Application
    $Mail = $Outlook.CreateItem(0)
    $Mail.To = $to
    $Mail.Subject = $subject
    $Mail.Body = $body
    $Mail.Send()
}
```

Get Uptime

    # V3.0
    (Get-CimInstance -ClassName Win32_OperatingSystem).LastBootUpTime 
    
    # V2.0
    Get-WmiObject Win32_OperatingSystem | Select-Object LastBootUpTime
    (Get-WmiObject -Class Win32_OperatingSystem).LastBootUpTime 

    $object = Get-WmiObject -Class Win32_OperatingSystem
    $lastboot = $object.LastBootUpTime
    $object.ConvertToDateTime($lastboot)
