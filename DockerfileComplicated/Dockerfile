# start from the base windows server core image
FROM mcr.microsoft.com/windows/servercore:ltsc2019

# Enable OS features and roles
# This will install IIS web server and asp.NET
RUN dism.exe /online /enable-feature /all /featurename:iis-webserver /NoRestart
RUN powershell add-windowsfeature web-asp-net45 

# You can also use these commands
# Add-WindowsFeature Web-Server
# Add-WindowsFeature Web-Asp-Net

# Download and expand zip file
Invoke-WebRequest -Method Get -Uri https://github.com/rxtur/BlogEngine.NET/releases/download/v3.3.8.0/3380.zip -OutFile c:\BlogEngineNETSrc.zip ; \
# if necessary do this to move the file around >> COPY BlogEngineNETSrc.zip c:/
RUN powershell -Command \
    $ErrorActionPreference = 'Stop'; \
	[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; \
	Expand-Archive -Path c:\BlogEngineNETSrc.zip -DestinationPath c:\inetpub\wwwroot ; \
	Remove-Item c:\BlogEngineNETSrc.zip -Force

RUN powershell.exe remove-item C:\inetpub\wwwroot\iisstart.*
RUN powershell.exe icacls C:\inetpub\wwwroot /grant Everyone:F /t /q

# %windir%\system32\inetsrv\appcmd.exe list AppPool
# %windir%\system32\inetsrv\appcmd.exe set AppPool "DefaultAppPool" -processModel.identityType:ApplicationPoolIdentity
# %windir%\system32\inetsrv\appcmd.exe list app
# %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/BlogEngine" /applicationPool:"DefaultAppPool"
# ICACLS C:\inetpub\wwwroot\blogengine /grant "IIS AppPool\DefaultAppPool:F" /t /q

# Service monitor starts and runs our web app
# ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]
