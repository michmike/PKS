FROM mcr.microsoft.com/windows/servercore:ltsc2019

# Enable OS features and roles
RUN dism.exe /online /enable-feature /all /featurename:iis-webserver /NoRestart
RUN powershell add-windowsfeature web-asp-net45 

# Download and expand zip file
COPY BlogEngineNETSrc.zip c:/
RUN powershell -Command \
    $ErrorActionPreference = 'Stop'; \
	[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; \
	Expand-Archive -Path c:\BlogEngineNETSrc.zip -DestinationPath c:\inetpub\wwwroot ; \
	Remove-Item c:\BlogEngineNETSrc.zip -Force

RUN powershell.exe remove-item C:\inetpub\wwwroot\iisstart.*
RUN powershell.exe icacls C:\inetpub\wwwroot /grant Everyone:F /t /q
#	Invoke-WebRequest -Method Get -Uri https://github.com/rxtur/BlogEngine.NET/releases/download/v3.3.8.0/3380.zip -OutFile c:\BlogEngineNETSrc.zip ; \
