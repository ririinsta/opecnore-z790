# OpenCore Z790 Build Config

### disclaimer
this works for me but might not for you. also thanks [XTVJ](https://github.com/xtvj) for the base efi folder that i mutilated to work for me.

Before running you need to do a few things. 
1. If you have a different card check and see if it is natively supported. If it is remove NootRX.kext and then do a OC snapshot, if it is not natively supported make sure it is supported by NootRX. 
2. If you are first installing make sure to disable NootRX if you need it.
3. Make sure you generate your own SMBIOS details.
4. Check your codec and make sure it matches up with mine. If not change your alcid accordingly.
5. If you have a different CPU make sure to change the RestrictEvents CPU name in config.plist.
6. If you have a WiFi card please go to the OpenCore guide to get it working. I do not have a supported WiFi card so this EFI does not have any wifi kexts.

### Build

- Motherboard：Gigabyte Z790 Aorus Elite AX (V1.0)
- CPU：i7-14700k
- GPU：Saphire RX6700XT
- Codec: ALC1220 (Layout 1)
- macOS：Sonoma 14.4
- OpenCore ：0.9.8
- Bios：(will update when i chcek)

### Guides

#### Disabling NootRX

1. Mount your EFI and open your config.plist in [Proper Tree](https://github.com/corpnewt/ProperTree).
  - If you are following this guide I have a feeling you have the slightest idea how to use it. If you do not I will have a basic tutorial somewhere here.
2. Go to Root>Kernel>Add>1
3. Find the Enabled key under this.
4. Switch the Enabled key from True to False.

#### Generating SMBIOS details

1. Mount your EFI and open your config.plist in [Proper Tree](https://github.com/corpnewt/ProperTree).
2. Go to Root>PlatformInfo>Generic
3. Leave Proper Tree open and in another window download and open [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
  - Once again I have a feeling you know how to use this tool but I will include a tutorial if you do not.
4. In GenSMBIOS generate new details for your SMBIOS (MacPro7,1 if you leave everything default)
5. After generating these details go back to ProperTree
6. Copy the serial from GenSMBIOS into the SystemSerialNumber field in ProperTree.
7. Copy Board Serial from GenSMBIOS into the MLB field.
7. Copy SmUUID from GenSMBIOS into the SystemUUID field.
8. For the ROM copy your PC's primary ethernet adapter's MAC Address into it.

#### Finding a layout for your motherboard

This is only for if the pre-selected layout does not work for you. This guide also assumes you already have macOS installed.

1. Download [Hackintool](https://github.com/benbaker76/Hackintool)
2. Launch Hackintool and make your way to the sound tab.
3. In Audio Info look for Codec Name
4. After finding your codec name find your codec [here](https://github.com/acidanthera/applealc/wiki/supported-codecs)
5. After finding your codec in the list look for the supported layouts.
6. Note down your layout and then mount your EFI and open your config.plist in [Proper Tree](https://github.com/corpnewt/ProperTree).
7. Find the key "boot-args" under Root>NVRAM>7C436110-AB2A-4BBB-A880-FE41995C9F82
8. Change alcid=1 in the boot-args to alcid=(your layout)

#### Changing your CPU name

1. Mount your EFI and open your config.plist in [Proper Tree](https://github.com/corpnewt/ProperTree)
2. Find the key revcpuname under Root>NVRAM>Add>4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102
3. Change the value of the key to whatever you want.

#### Using ProperTree

Using ProperTree is increadibly straight forward. I can not explain well enough how it works so I am going to link you to the [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/#creating-your-config-plist). Look through any of the config.plist guides and it will be very self explainitory.

#### Mounting Your EFI

This is also very very easy.

1. Download [Hackintool](https://github.com/benbaker76/Hackintool)
2. Launch Hackintool and make your way to the disks tab.
3. Under partition scheme find your hard drive's EFI partition.
4. Right click the partition and press Mount.
