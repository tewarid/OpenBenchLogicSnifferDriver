Instructions to self-sign
-------------------------

Windows Driver Kit 7.1 all command located under \bin\amd64\ except if indicated otherwise. Execute:

makecert.exe -r -pe -ss PrivateCertStore -n CN=OpenLogicSniffer.org(Test) OpenLogicSniffer.cer

Signtool.exe sign /v /s PrivateCertStore /n OpenLogicSniffer.org(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll mchpcdc.cat

Inf2cat.exe /driver:. /os:7_x64,7_X86
(Windows Driver Kit 7.1 located under bin\selfsign\)

certmgr.exe /add OpenLogicSniffer.cer /s /r localMachine root
(Need to run this with administrator privilege)


Instructions to Install
-----------------------

Add certificate to local machine using the last command above. In Device Manager choose the Open Bench LogicSniffer device (appears as Logic Sniffer CDC-232 under Other devices). Right click, choose Update Driver, choose to install driver manually from known location. Specify path to mchpcdc.inf file.   
