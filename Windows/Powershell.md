# Powershell tricks

- Get proxy
    
      Get-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings'

- Send mail

        Function Send-Mail($to, $subject, $body) {
        	$Outlook = New-Object -ComObject Outlook.Application
        	$Mail = $Outlook.CreateItem(0)
        	$Mail.To = $to
        	$Mail.Subject = $subject
        	$Mail.Body = $body
        	$Mail.Send()
        }