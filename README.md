# Sierra-on-thinkpadT430s


clover : https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/

https://clover-wiki.zetam.org/Fixing-DSDT#technical-background

////////////////////////////////////////////////////////////////
网卡 Atheros ar9285
\System\Library\Extensions\IO80211Family.kext\Contents\PlugIns\AirPortAtheros40.kext\Contents 
添加				<string>pci168c,2b</string>

蓝牙 

Get idProduct and idVendor from System Report > USB > Bluetooth or use Linux to get it

Convert from hex to decimal

0x21e6 = 8678
0x0a5c  = 2652

Modify stock IOBluetoothFamily.kext

vi /System/Library/Extensions/IOBluetoothFamily.kext/Contents/PlugIns/BroadcomBluetoothHostControllerUSBTransport.kext/Contents/Info.plist

Find IOKitPersonalities

Add additional stanza including idProduct and idVendor found in previous step

		<key>PID 8448 0x2100 VID 2652 0xA5C</key>
		<dict>
			<key>CFBundleIdentifier</key>
			<string>com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport</string>
			<key>Dongles</key>
			<dict>
				<key>Unknown</key>
				<string>Unknown Model</string>
			</dict>
			<key>IOClass</key>
			<string>BroadcomBluetoothHostControllerUSBTransport</string>
			<key>IOProviderClass</key>
			<string>IOUSBDevice</string>
			<key>idProduct</key>
			<integer>8448</integer>
			<key>idVendor</key>
			<integer>2652</integer>
		</dict>
		
		
		
		
		
		                        Device (PRTB)
                        {
                            Name (_ADR, 0x04)
                            Method (_UPC, 0, Serialized)
                            {
                                Return (UP11)
                            }

                            Method (_PLD, 0, Serialized)
                            {
                                Return (PL11)
                            }
                            Method (_DSM, 4, NotSerialized)
                            {
                                If (LEqual (Arg2, Zero))
                                {
                                    Return (Buffer (One){0x03})
                                }

                                Return (Package ()
                                {
                                    "vendor-id", Buffer() { 0x5c, 0x0a, 0x00, 0x00 },
                                    "device-id", Buffer() { 0xe8, 0x21, 0x00, 0x00 }
                                })
                            }
                        }
