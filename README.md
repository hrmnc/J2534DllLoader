# J2534DllLoader
Modified J2534 DLL Loader for the Think City TechCentre Diagnostic Software

Since the Omitec 3G VCI hardware that the TechCentre Diagnostic Software was designed for is near impossible to find, I have patched the J2534 DLL Loader to work with any J2534 hardware.

I have tested fault reading/clearing, live data, and actuator tests. I have not tested key programming or flashing. **USE AT YOUR OWN RISK**
<!---
I have tested this patch to work on a cheap $20 GODIAG J2534 adapter, shown below, which can be found on eBay or Amazon. It works, but disconnects often. A higher quality J2534 adapter like one from Drew Tech or a Mongoose might work better.

<img src="https://github.com/hrmnc/J2534DllLoader/assets/2160109/e15bdf3f-19b0-47cb-8241-70ef26f74222)" alt="drawing" width="500"/>
--->
## Tested adapters

| Name | Notes |
| ----------- | ----------- |
| GODIAG GD101 J2534 | Connection drops frequently, not recommended for programming/flashing |
| Peak PCAN-USB with PCAN-PassThru API | Works for CAN functions  |

## Installation
Simply replace the J2534DllLoader.dll file in C:\Program Files\Omitec Ltd\THINK TechCentre and edit the THINKDiagnostics.exe.config file (in the same directory) as follows:

1. Use *regedit* to check the name of your J2534 device in HKEY_LOCAL_MACHINE\SOFTWARE\PassThruSupport.04.04\\\**your_J2534_device\**. <br> In my case it is "GODIAG - J2534":
  ![j2534registry](https://github.com/hrmnc/J2534DllLoader/assets/2160109/46bcb8cb-ae89-414a-8a4e-1e3455ff94f7)
2. Add your J2534 device to the THINKDiagnostics.exe.config file. The configuration flags differ between ThinkCentre v1.0.3 and v2.0.3:
- **For ThinkCentre version 1.0.3:** <br>
     Edit the "PassThru" key to be your J2534 device name with "_DashOne" appended. In my case it would be "GODIAG - J2534_DashOne":
     ![configuration](https://github.com/hrmnc/J2534DllLoader/assets/2160109/b49cc87f-680b-4e10-84d7-2945f788025e)
- **For ThinkCentre version 2.0.3:** <br>
     Edit "PassThruName" key to be your J2534 device name. In my case it would be "GODIAG - J2534":
     ![configuration203](https://github.com/hrmnc/J2534DllLoader/assets/2160109/c8e027d7-a222-432a-ad69-60256e2b73e1)
