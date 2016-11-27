# Sierra-on-thinkpadT430s

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
