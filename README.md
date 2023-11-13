# J2534DllLoader
Modified J2534 DLL Loader for the Think City TechCentre Diagnostic Software

![Screenshot 2023-11-13 112936](https://github.com/hrmnc/J2534DllLoader/assets/2160109/85254f2c-8e50-4409-baf6-5759b0b488cc)

Since the Omitec 3G VCI hardware that the TechCentre Diagnostic Software was designed for is near impossible to find, I have patched the J2534 DLL Loader to work with any J2534 hardware.

I have tested fault reading/clearing, live data, and actuator tests. I have not tested key programming or flashing. **USE AT YOUR OWN RISK**
<!---
I have tested this patch to work on a cheap $20 GODIAG J2534 adapter, shown below, which can be found on eBay or Amazon. It works, but disconnects often. A higher quality J2534 adapter like one from Drew Tech or a Mongoose might work better.

<img src="https://github.com/hrmnc/J2534DllLoader/assets/2160109/e15bdf3f-19b0-47cb-8241-70ef26f74222)" alt="drawing" width="500"/>
--->
## Tested J2534 Adapters
Here are the J2534 devices that have been tested and the vehicles modules that they can talk to:
| Name | ABS | BMS | CDCM | EPHS | GEM | PATS | PCU | RAC | SRS | VCU |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| GODIAG GD101 J2534 | :heavy_check_mark: | :heavy_check_mark: | :grey_question: | :grey_question: | :heavy_check_mark: | n/a | :heavy_check_mark: | n/a | :heavy_check_mark: | :heavy_check_mark: |
| Peak PCAN-USB with PCAN-PassThru API |  | :heavy_check_mark: | :grey_question: | :grey_question: |  | n/a | :heavy_check_mark: | n/a | :heavy_check_mark: | :heavy_check_mark: |

Notes:
- PATS and RAC modules were not installed in North America vehicles, so I am unable to test it.
- CDCM and EPHS communicate over CAN bus, so they should work with either adapter. I suspect that there is an issue with my vehicle that is preventing me from talking to them.

<!--- ![image](https://github.com/hrmnc/J2534DllLoader/assets/2160109/e4a0856d-4f76-4d10-80b3-4c99682d1505) --->

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
3. (Optional) Replace Omitec.THINKDiagnostics.PlugIns.WebBrowsing.dll to disable loading the defunct think.no homepage (and resultant error popups) in ThinkCentre
