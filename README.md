Instructions to self-sign
-------------------------

Windows Driver Kit 7.1 all command located under \bin\amd64\ except if indicated otherwise. Execute:

makecert.exe -r -pe -sv OpenBenchLogicSniffer(Test).pvk -n CN=OpenBenchLogicSniffer(Test) OpenBenchLogicSniffer(Test).cer

pvk2pfx.exe -pvk OpenBenchLogicSniffer(Test).pvk -spc OpenBenchLogicSniffer(Test).cer -pfx OpenBenchLogicSniffer(Test).pfx

Inf2cat.exe /driver:. /os:7_x64,7_X86
(Windows Driver Kit 7.1 located under bin\selfsign\)

Signtool.exe sign /v /f OpenBenchLogicSniffer(Test).pfx /n OpenBenchLogicSniffer(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll mchpcdc.cat

certmgr.exe /add OpenBenchLogicSniffer(Test).cer /s /r localMachine root
(Need to run this with administrator privilege)


Instructions to Install
-----------------------

Add OpenBenchLogicSniffer(Test).cer to local machine using certmgr.exe (last command above) or through Windows Explorer. In Device Manager choose Logic Sniffer CDC-232 under Other devices. Right click, choose Update Driver, choose to install driver manually from known location. Specify path to mchpcdc.inf file.   
