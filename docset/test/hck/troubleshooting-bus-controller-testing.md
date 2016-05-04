---
author: joshbax-msft
title: Troubleshooting Bus Controller Testing
description: Troubleshooting Bus Controller Testing
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 5319ad2e-3467-46f3-ac0e-b6738f99dce5
---

# Troubleshooting Bus Controller Testing


To troubleshoot bus controller test issues, follow these steps:

1.  Review the following Windows Hardware Certification Kit (Windows HCK) topics:

    -   [Troubleshooting Windows HCK Test Failures](troubleshooting-windows-hck-test-failures.md)

    -   One of the following topics, depending on the type of bus controller that you are testing:

        -   [Bluetooth Controller Testing Prerequisites](bluetooth-controller-testing-prerequisites.md)

        -   [Proximity Controller Testing Prerequisites](proximity-controller-testing-prerequisites.md)

        -   [Secure Digital Host Controller Testing Prerequisites](secure-digital-host-controller-testing-prerequisites.md)

        -   [USB Bus Controller Testing Prerequisites](usb-bus-controller-testing-prerequisites.md)

        -   [WITT I2C Testing Prerequisites](witt-i2c-testing-prerequisites.md)

2.  Verify that you have installed the latest Windows HCK filters and kit updates. For more information, see [Windows Hardware Certification Kit Filters](windows-hardware-certification-kit-filters.md).

3.  For a test failure, look for usable information in the Windows HCK Studio test log. If you find usable information, resolve the issue and rerun the test.

4.  If you cannot obtain a successful test result, contact [Windows HCK Support](windows-hck-support.md).

### <a href="" id="bluetooth"></a>Bluetooth controller test troubleshooting

The following table describes common issues that can occur during Bluetooth controller testing:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Issue</th>
<th>Resolution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failures finding Bluetooth devices during an Bluetooth Inquiry command</p></td>
<td><p>This failure can happen when you run a test in a noisy environment. Rerunning the test usually fixes this error. You can also try to bring the radios closer together. Make sure that the radios have a clear line of sight. Turn off other radios that may be causing interference.</p></td>
</tr>
<tr class="even">
<td><p>Failures connecting Bluetooth devices during Bluetooth Inquiry commands</p></td>
<td><p>This failure occurs when the test times out before the devices could be reconnected. Rerunning the test usually fixes this error.</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="witti2c"></a>WITT I²C controller test troubleshooting


The following table describes common issues that can occur during Windows Inter-Integrated Circuit (I²C) Testing Tool (WITT) controller testing:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Issue</th>
<th>Resolution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All tests failed with error message <strong>WITT device test interface is not found</strong>.</p></td>
<td><p>Review [WITT I2C Testing Prerequisites](witt-i2c-testing-prerequisites.md). Make sure that the WITT test peripheral driver is installed, ACPI table modified with sample ASL and four instances of WITT Test Driver are found in Windows HCK Device Manager.</p></td>
</tr>
<tr class="even">
<td><p>WITT firmware needs to be updated. The WITT firmware binary (i2c9665a.iic) is released as part of. When you install a new Windows HCK package, you should update the WITT firmware.</p></td>
<td><p>See [WITT I2C Testing Prerequisites](witt-i2c-testing-prerequisites.md) for instructions on how to upgrade the WITT firmware.</p></td>
</tr>
<tr class="odd">
<td><p>WITT device is in a bad state. Typically, the green LED on a WITT device should be lit when there is no traffic, and should blink when there is traffic. Otherwise, the WITT or I²C controller might be in a bad state.</p></td>
<td><p>Unplug the WITTs USB cable to power-cycle the device. If the controller is still not working, reboot the testing system.</p></td>
</tr>
</tbody>
</table>

 

## Related topics


[Device.BusController Testing](devicebuscontroller-testing.md)

[Troubleshooting Windows HCK](troubleshooting-windows-hck.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Troubleshooting%20Bus%20Controller%20Testing%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




