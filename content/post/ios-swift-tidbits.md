---
title: "iOS Swift Tidbits"
date: 2018-06-15T19:46:27-07:00
description: Some swift code samples that have been handy.
draft: true
twitter:
 image: https://lukeeckley.com/images/avatar@2x.jpg
---
![Swift Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Swift_logo_with_text.svg/160px-Swift_logo_with_text.svg.png)

Currently learning some iOS programming in Swift. These are probably only useful to me, but they are little things I've discovered.


## Keep App in Portrait Mode
{{< highlight swift >}}
// To prevent the app from rotating. Keep it in portrait mode
override var shouldAutorotate: Bool {
	return false
}
    
override var supportedInterfaceOrientations: UIInterfaceOrientationMask {
	return .portrait
}
{{< /highlight >}}

## Hide the Status Bar
{{< highlight swift >}}    
// To hide the stats bar while the app is open
override var prefersStatusBarHidden: Bool {
	return true
}
{{< /highlight >}}

## Device Resolutions
Look at Apple's site for any updated info here: [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/adaptivity-and-layout/)

Device	       	| Portrait dimensions |	Landscape dimensions
----------------|---------------------|-----------------------
12.9" iPad Pro 	| 2048px × 2732px     |	2732px × 2048px
10.5" iPad Pro 	| 1668px × 2224px     |	2224px × 1668px
9.7" iPad	| 1536px × 2048px     |	2048px × 1536px
7.9" iPad mini 4| 1536px × 2048px     |	2048px × 1536px
iPhone X	| 1125px × 2436px     |	2436px × 1125px
iPhone 8 Plus	| 1242px × 2208px     |	2208px × 1242px
iPhone 8	| 750px × 1334px      |	1334px × 750px
iPhone 7 Plus	| 1242px × 2208px     |	2208px × 1242px
iPhone 7	| 750px × 1334px      |	1334px × 750px
iPhone 6s Plus	| 1242px × 2208px     |	2208px × 1242px
iPhone 6s	| 750px × 1334px      |	1334px × 750px
iPhone SE	| 640px × 1136px      |	1136px × 640px
