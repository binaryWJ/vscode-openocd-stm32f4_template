# vscode-openocd-stm32f4_template On Windows
# this is a template for stm32f4 debug in visual studio code by openocd
1. Software Prerequisite
   > VS code for windows, get from https://code.visualstudio.com/
     Extensions:
     . C/C++
     . C++ Intellisense
     . Cortex-Debug
   > openocd for windows, get from https://gnutoolchains.com/arm-eabi/openocd/
     after installed (add openocd binary path to system path), please check in command prompt.
     c:\>openocd -v
       Open On-Chip Debugger 0.11.0 (2021-11-18) [https://github.com/sysprogs/openocd]
       Licensed under GNU GPL v2
       ...
   > make for windows, get from https://sourceforge.net/projects/gnuwin32/files/make/
     after installed (add make binary path to system path), please check in command prompt.
     c:\>make -v
       GNU Make 3.81
       Copyright (C) 2006  Free Software Foundation, Inc.
       ...
   > ARM cortex-M toolchain, get from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
     after installed (add toolchain binary path to system path), please check in command prompt.
     check arm gcc version
     c:\>arm-none-eabi-gcc.exe -v
       Using built-in specs
       ...
       gcc version 11.2.1 20220111 (GNU Toolchain for the Arm Architecture 11.2-2022.02 (arm-11.16))
     check arm gdb version
     c:\>arm-none-eabi-gdb.exe -v
       GNU gdb (GNU Toolchain for the Arm Architecture 11.2-2022.02 (arm-11.16)) 11.2.90.20220202-git
       ...
       !!!! maybe you can't start the arm-none-eabi-gdb.exe and notice you do not find python27.dll, to solve this problem, please install python2.7.6 in you system, get from https://www.python.org/ftp/python/2.7.6/python-2.7.6.msi
2. Hardware Prerequisite
    > Jlink and Jlink Driver
    > Replace Jlink driver to WinUSB by Zadig.exe
      . get Zadig.exe from internet
      . Insert Jlink and correct detected in device manager in windows
      . Open Zadig.exe, options -> list all drivers, find jlink in left and select WinUSB right, the click Replace Driver (you can find guide in internet, if you want to recover jlink driver, you can use UsbDriverTool.exe)
    > now you can use openocd to connect to STM32F4 MCU
      c:\>openocd -f interface/jlink.cfg -c "transport select swd" -f target/stm32f4x.cfg
        Open On-Chip Debugger 0.11.0 (2021-11-18) [https://github.com/sysprogs/openocd]
        ...
        Info : stm32f4x.cpu: Cortex-M4 r0p1 processor detected
        ...
        Info : Listening on port 3333 for gdb connections
    > !!! Stop openocd command by Ctrl + C, because previous step will affect Debug (Debug will start openocd automatically, if you started yet, Debug process will report error)
3. Debug
    > Add a breakpoint in Core/Src/main.c
    > In VS code: Run -> Start Debugging (F5)
    > Debug STM32F4x in VS code by openocd successfully

