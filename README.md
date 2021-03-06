# Kernel Device Driver Rootkit

This project is not a normal driver. It is a "driverless driver" that uses an undocumented hack to work as a rootkit. 

## How it works
The **DriverEntry()** function is not actually the entrypoint for a normal driver, it is callback. Just like the WinMain() function is not actually the entrypoint for a native Win32 program. The EntryPoint() function in the project's source code is the replacement for the native driver entrypoint.

The **GsDriverEntry()** function is the _real_ entrypoint in a normal KMDF (Kernel Mode Driver Framework) driver. It performs essential initialization to support the /GS compiler option, designed to detect buffer overflow. After that's done it calls DriverEntry(). The project replaces this entrypoint with EntryPoint().

## How it is used
In order to utilize the driver, it must be installed as a service and then started. This must be done using the .sys file that the Kernel Driver generates when compiled. Afterwards, the driver can be debugged using any tool similar to [DebugView](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview).

## Disclaimer
The information provided by this repository is for general informational purposes only.
