---
layout: post
title: HAME R1 router WIFI password
---

![_config.yml]({{ site.baseurl }}/images/hamer1.jpg)

Recently picked up - HAME R1 Portable 4400mAh Battery Powered 3G - off [ebay](http://www.ebay.com/sch/i.html?_from=R40&_trksid=p2047675.m570.l1313.TR0.TRC0.H0.XHAME+R1+router&_nkw=HAME+R1+router&_sacat=0). The item is advertised as _Wireless Router WIFI Router R1 3 in 1_. As it happens, the seller repackages the item so that they can ship more like a gift than a purchased product. Which is thoughtful but can end up forgetting a few things. In my case, the HAME comes with individual default password just below the default SSID at the back of the device.

Mine wasn't there. [Hametech](http://www.hametech.com/html/product/), the english website of the manufacturer is most useless as the support pages are long dead... Frustrated by the seller (By now, 4 messages sent to the seller via Skype, Ebay and Email) and now by the manufacturer; I resorted to youtube to see if I can find any HAME unboxings that will help or someone with such a problem in the comments section. Bupkis.

Hmmm, but as I was watching the videos, I made an observation regarding the WIFI passsword, there was a pattern. I picked up a similarity on the initial characters as they typed the password. The first 3 characters were always the same i.e. started with 7c3. The default password uses WPA encryption so the password has to have a minimum of 8 characters.

I also made a visual connection between the default SSID written at the back of the device as they typed. Hame SSID is in the format **HAME_R1_xxxx** with **xxxx** being the unique set of characters with each device. So if your device had SSID **HAME_R1_x123**, then you extract the characters after the last underscore and append them to 7c3. You end up with **7c3x123**

You still won't be able to connect as most devices validate password to meet the minimum no. of characters before allowing you to connect at all. I went back to two of the videos I had watched and as fate would have it, they both ended with 8 as the final character of the WIFI password.

So your working password (based on the above deductions) should be **7c3x1238**

If you stare at the format a for minute and analyse it. There are 7 characters before the last one. The last character is a number 8, the first is 7. The third character is always 3. The second is always c.

Youtube Videos: 

[ộ phát wifi hame r1](https://www.youtube.com/watch?v=9NwZI5jEbNI)

[HAME MPR-A1 Review](https://www.youtube.com/watch?v=z73NNcyo9yl)

For a good introduction on HAME routers. See [Hame 3G Wi-Fi Modem – Review, Manual Settings for Non Chinese Users](http://www.3ptechies.com/it-support/networking/hame-3g-wi-fi-modem-review-manual-settings-english.html)
