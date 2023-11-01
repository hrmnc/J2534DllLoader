# J2534DllLoader
Modified J2534 DLL Loader for the Think City TechCentre Diagnostic Software

Since the Omitec 3G VCI hardware that the TechCentre Diagnostic Software was designed for is near impossible to find, I have patched the J2534 DLL Loader to work with any J2534 hardware.

I have tested fault reading/clearing, live data, and actuator tests. I have not tested key programming. **USE AT YOUR OWN RISK**

I have tested this patch to work on a cheap GODIAG J2534 adapter like the one shown below. It works, but disconnects often. A higher quality J2534 adapter like one from Drew Tech or a Mongoose might work better.

<img src="https://github.com/hrmnc/J2534DllLoader/assets/2160109/e15bdf3f-19b0-47cb-8241-70ef26f74222)" alt="drawing" width="500"/>

## Installation
Simply replace the J2534DllLoader.dll file in C:\Program Files\Omitec Ltd\THINK TechCentre and edit the THINKDiagnostics.exe.config file (in the same directory) as follows:

1. Use *regedit* to check the name of your J2534 device in HKEY_LOCAL_MACHINE\SOFTWARE\PassThruSupport.04.04\\\**your_J2534_device\**. <br> In my case it is "GODIAG - J2534":
  ![j2534registry](https://github.com/hrmnc/J2534DllLoader/assets/2160109/46bcb8cb-ae89-414a-8a4e-1e3455ff94f7)
2. Edit the value of the "PassThru" key in THINKDiagnostics.exe.config to be your J2534 device name with "_DashOne" appended. <br> In my case it would be "GODIAG - J2534_DashOne":
  ![configuration](https://github.com/hrmnc/J2534DllLoader/assets/2160109/b49cc87f-680b-4e10-84d7-2945f788025e)
