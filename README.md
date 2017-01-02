# How to create a self-signed driver for Open Bench Logic Sniffer

These instructions explain how to self-sign [Open Bench Logic Sniffer](https://www.seeedstudio.com/Open-Workbench-Logic-Sniffer-p-612.html) driver to use on Windows 7/8. Windows 10 comes with built-in support for virtual serial ports - no driver installation is required.

## Instructions to self-sign

Windows Driver Kit 7.1 all command located under \bin\amd64\ except if indicated otherwise.

Execute:
```powershell
makecert.exe -r -pe -sv OpenBenchLogicSniffer(Test).pvk -n CN=OpenBenchLogicSniffer(Test) OpenBenchLogicSniffer(Test).cer

pvk2pfx.exe -pvk OpenBenchLogicSniffer(Test).pvk -spc OpenBenchLogicSniffer(Test).cer -pfx OpenBenchLogicSniffer(Test).pfx

# For Windows Driver Kit 7.1 command located under bin\selfsign\
Inf2cat.exe /driver:. /os:7_x64,7_X86

Signtool.exe sign /v /f OpenBenchLogicSniffer(Test).pfx /n OpenBenchLogicSniffer(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll mchpcdc.cat

# Need to run command with administrator privilege
certmgr.exe /add OpenBenchLogicSniffer(Test).cer /s /r localMachine root
```

## Instructions to Install

Add OpenBenchLogicSniffer(Test).cer to local machine using certmgr.exe (last command above) or through Windows Explorer. In Device Manager, choose Logic Sniffer CDC-232 under Other devices. Right click, choose Update Driver, choose to install driver manually from known location. Specify path to mchpcdc.inf file.   
