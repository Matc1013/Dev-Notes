1. 以管理员身份启动bat

   ```bat
   @echo off&(cd/d "%~dp0")&(cacls "%SystemDrive%\System Volume Information" >nul 2>&1)||(start "" mshta vbscript:CreateObject^("Shell.Application"^).ShellExecute^("%~snx0"," %*","","runas",1^)^(window.close^)&exit /b)
   chcp 65001
   ```

2. 添加防火墙规则

   ```bat
   set RuleName=xxx
   set BinaryPath=xxx
   netsh advfirewall firewall add rule name=%RuleName% dir=in action=allow program="%BinaryPath%" enable=yes
   netsh advfirewall firewall add rule name=%RuleName% dir=out action=allow program="%BinaryPath%" enable=yes
   ```

3. 安装服务

   ```bat
   set ServiceName=xxx
   set DisplayName="xxx"
   set ServiceBinary="xxx"
   
   echo Checking if service exists...
   sc query %ServiceName% >nul 2>&1
   if %errorlevel% equ 0 (
       echo Service exists. Removing...
       sc stop %ServiceName%
       sc delete %ServiceName%
       echo Service removed successfully.
   )
   
   echo Installing service...
   sc create %ServiceName% binPath= %ServiceBinary% DisplayName= %DisplayName% start= auto
   echo Service installed successfully.
   
   echo Starting service...
   sc start %ServiceName%
   echo Service started successfully.
   ```

   

