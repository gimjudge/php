# php
https://community.apachefriends.org/f/viewtopic.php?f=16&t=70797
php_printer 5.6.8 Working DLL
Postby pylonx » 18. May 2015 22:57

Hello, Friends and Friends of Friends.

php_printer.dll hasn't had a PECL version since 4.0.7 so I've been rebuilding the dll using a few steps I learned by asking for help here. You can see those posts Below.
https://community.apachefriends.org/f/viewtopic.php?f=16&t=53348
https://community.apachefriends.org/f/viewtopic.php?f=16&t=68967

The Following is specifically what I did for XAMPP with PHP 5.6.8

Working PHP_PRINTER.DLL for PHP 5.6.8 for Windows can be found here:
https://github.com/gimjudge/php

The guide I Heavily used in this process:
https://wiki.php.net/internals/windows/stepbystepbuild

All links checked as of 2015-05-18

Step 1
Download and INSTALL Microsoft Visual Studios, a Free Version should be available.
I used Microsoft Visual Studio Ultimate 2012
https://www.microsoft.com/en-us/downloa ... x?id=30678

Step 2
Download php-sdk-binary tools
I downloaded (php-sdk-binary-tools-20110915.zip)
http://windows.php.net/downloads/php-sdk/

Step 3
Unzipped this file into the c:\php-sdk folder you may have to create.

Step 4
Open Visual Studios Command Prompt (Windows 7 Search)
CODE: SELECT ALL
VS2012 x86 Native Tools Command Prompt


Step 5
Proceeded with the following instructions:
CODE: SELECT ALL
cd c:\php-sdk\
bin\phpsdk_setvars.bat
bin\phpsdk_buildtree.bat phpdev


Step 6
Open the php-sdk\phpdev Copy and paste vc9 and rename it vc11

Step 7
Download the the source that matches your version of PHP
http://windows.php.net/downloads/releases/
I downloaded (php-5.6.8-src.zip) which is in the Archives now
http://windows.php.net/downloads/releases/archives/

Step 8
Unzip this file into C:\php-sdk\phpdev\vc11\x86
Will look like:
C:\php-sdk\phpdev\vc11\x86\php-5.6.8-src\

Step 9
Download the dependencies
I downloaded (deps-5.6-vc11-x64.7z)
http://windows.php.net/downloads/php-sdk/

Step 10
Place Dependencies in 
C:\php-sdk\phpdev\vc11\x86\

Step 11
Get your extension's build files. php_printer was here (http://svn.php.net/repository/pecl/printer/trunk/)
I had to change all the pval to zval int the printer.
"Open 'printer.c' and replace all instances of 'pval' with 'zval' and it should compile."
I put those files into C:\php-sdk\phpdev\vc11\x86\php-5.6.8-src\ext\printer

Step 12
Proceeded with the following code commands in the "VS2012 x86 Native Tools Command Prompt"
CODE: SELECT ALL
cd c:\php-sdk\phpdev\vc11\x86\php-5.6.8-src
buildconf
configure --enable-printer=shared


Also have used:
CODE: SELECT ALL
c:\php-sdk\phpdev\vc11\x86\php5.5-201406241830>configure --disable-all --enable-printer=shared


CODE: SELECT ALL
configure --disable-all --enable-printer=shared --enable-phpdbg


Step 13
CODE: SELECT ALL
nmake


Step 14 
Once it's down you should see a "Release_TS" folder in the C:\php-sdk\phpdev\vc11\x86\php56 folder
In that folder you should find your dll
