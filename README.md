# xiaomi-debloat-list
If You Have any xiaomi smartphone  u can remove some inbuilt apps using ADB tool  to get smooth experience 
First You have to enable Developer option in your smartphone
Then you need a pc with ADB tool of xiaomi
UPDATE 2020-05-09: Added SIM Toolkit description.
UPDATE 2020-07-04 Added some apps, thanks to @thecrazyblack.
UPDATE 2020-11-23 Updated list of apps, thanks to new comments by @toast254, @swiesmann, @MarcelloDM, @satnited.

Xiaomi phones have impressive parameters for given price, but they come with a lot of unnecessary software. It eats battery and memory, sometimes shows annoying advertisement, and may have security issues. You can not uninstall this pre-installed apps like usual ones, and you can not even disable them from settings like in earlier Android versions.

Here is how to remove or disable unnecessary software without rooting phone. Works for MIUI 11 and 12 (based on Android 9 and 10), should work for other phones for recent Android versions. Thanks to this very useful but severely under-voted stackoverflow answer.

NOTE: I do not guarantee that this instructions won’t break your phone, blow it to flaming pieces or cause a sentient machines rebellion against humanity. You were warned.

To manage phone from command-line via USB you need adb - Android Debug Bridge, part of Android platform-tools. You can download the recent one for your OS here. If you are on Windows, you also need USB drivers for your device.

⚙️ Settings - About phone. Tap “MIUI version” multiple times. Now Developer Options are unlocked.
⚙️ Settings - Additional settings - Developer Options - [✔️] USB debugging.
Connect the phone to your computer via USB. Choose “File Transfer” mode instead of default “No data transfer”.
Open console in a directory where you unpacked platform tools.
./adb devices
Phone will prompt to add your computer’s key to allowed, agree to it.
./adb shell you have a shell on your device.
Now you need app package names, like com.miui.yellowpage for Mi Yellow Pages.

⚙️ Settings - Apps - Manage Apps. Tap on application, then tap info(ℹ️) button in the right corner. There you can see “APK name”, that’s what we need.
There are 2 options: disable app and uninstall app. I prefer disabling them, it’s easier to enable them back if you’ve broken something.

# Disable app
pm disable-user app.package.name
# Re-enable it
pm enable app.package.name

# Uninstall app
# Sometimes uninstall command may not work without -k option on un-rooted devices
# -k: Keep the data and cache directories around after package removal. 
pm uninstall --user 0 app.package.name
# Install uninstalled system app
pm install --user 0 $(pm dump app.package.name | awk '/path/{ print $2 }')
# Another way to install uninstalled system app
pm install-existing app.package.name
More details here: pm commad manual.

To be able to install apps back, you need to enable

⚙️ Settings - Additional settings - Developer Options - [✔️] Install via USB
On Xiaomi phone to enable this setting you need to sign in into Mi Account. You may just use your Google account to sign into it and then sign-out when you don’t need it anymore:

⚙️ Settings - Mi Account - sign-out.
Here is a list of Xiaomi and Google apps that I find unnecessary:

UNSAFE TO DISABLE/UNINSTALL

com.xiaomi.finddevice	Result: endless boot loop, some time after it will ask to erase the phone and start over. Guess how I learned that?
com.miui.securitycenter	Result: phone reboots only in recovery mode
com.android.contacts	Result: you lose the phone icon
com.mi.android.globalminusscreen	Xiaomi App Vault. Result: if you are logged in with Mi account, device becomes locked, to unlock you should bring it to Xiaomi Services Center. Settings -> Home Screen crashes Settings app. See comment by @satnited.
Xiaomi:

com.miui.analytics	Mi Analytics (Spyware?)
com.xiaomi.mipicks	GetApps - app store like Google Play from Xiaomi. The most annoying one, periodically shows advertisement.
com.miui.msa.global	MIUI Ad Services - also responsible for showing ads.
com.miui.cloudservice com.miui.cloudservice.sysbase com.miui.newmidrive	Mi Cloud
com.miui.cloudbackup	Mi Cloud Backup
com.miui.backup	MIUI Backup
com.xiaomi.glgm	Games
com.xiaomi.payment com.mipay.wallet.in	Mi Credit
com.tencent.soter.soterserver	Authorize payments in WeChat and other Chinese services, useless if you don’t live in China.
cn.wps.xiaomi.abroad.lite	Mi DocViewer(Powered by WPS Office)
com.miui.videoplayer	Mi Video
com.miui.player	Mi Music
com.mi.globalbrowser	Mi Browser
com.xiaomi.midrop	Mi ShareMe
com.miui.yellowpage	Mi YellowPages. Some kind of caller id app.
com.miui.gallery	MIUI Gallery - if you use another gallery app WARNING: @nihalanand697 reports disabling it isn’t safe. But I had no problems after uninstalling it.
com.miui.android.fashiongallery	Wallpaper Carousel
com.miui.bugreport com.miui.miservice	Mi Bug Report - if you not using this feature
com.miui.weather2	MIUI Weather. I prefer another weather app.
com.miui.hybrid com.miui.hybrid.accessory	Quick apps.
com.miui.global.packageinstaller	MIUI package installer. Without it Play Store app will be used. It shows ads, but I like that you can manage app permissions before starting it.
com.xiaomi.joyose	?? Some junk
