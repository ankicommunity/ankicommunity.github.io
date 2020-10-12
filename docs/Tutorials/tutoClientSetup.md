Client Setup
============

# Tested Clients / server combinations

|    Date    | AnkiDesktop version | AnkiDroid version |                      ankisyncd version                       | Tester       |
| :--------: | :-----------------: | :---------------: | :----------------------------------------------------------: | ------------ |
| 2020-02-06 |       2.1.19        |       2.9.1       | [2.1.0 + 2bfccf7f](<https://github.com/kuklinistvan/anki-sync-server/tree/docker-release>) | kuklinistvan |
[Learn more about what "tested" means here.](Testing.md)

# AnkiDroid

Ensure you're using a supported version :

|                            | Main                                                         | Mirror                                                       | Size     | SHA256                                                       |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| AnkiDroid APK for Android  | [2.9.1](https://fdroid.tetaneutral.net/fdroid/archive/com.ichi2.anki_20901300.apk) | [2.9.1](https://mega.nz/file/YFoFER5S#BiMMDxyhdl_u9I1TC-v_bBYakM5DTTM5CybJb4pu4oY) | 10.7 MB  | `511ef65b8dcb65a7f99f9942c4fcee5134f137ce23c677cf1ea3b26c7c3f34c5` |

Open the app, then slide off the menu from the left side. Go Settings > Advanced > Custom sync server and specify the same two urls you've specified on the desktop client.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb. Head to the main screen of the application (the list of decks) and slide down to synchronize (or use the icon next to the menu in the top right corner). Although Anki will ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.
if you get an issue like "Authentication not allowed over insecure http" you may need to setup https


# Anki Desktop

Ensure you're using a supported version :  
|                            | Main                                                         | Mirror                                                       | Size     | SHA256                                                       |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| AnkiDesktop  for GNU/Linux | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-linux-amd64.tar.bz2) | [2.1.19](https://mega.nz/file/lVxRgRwI#Oqohl1M0Ju9RrYa7D6uV5SOtwgqVxkxPKqNYxcOh858) | 127.7 MB | `ada59237b8b3774712d6309821db4b6cb1d2c625284302aa09bc7313ada76fc0` |
| AnkiDesktop for Windows  | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-windows.exe) | [2.1.19](https://mega.nz/file/5MwhxLjT#TLGA03KMbnRmDiHO3A-Yfm-y6xNgW3eiDUgEk-TXYyU) | 97,3 MB  | `90be6a3e5a6f4373ba3342bd3dfbe61e9013bb2a4acced2fcdd594b4c651a665` |
| AnkiDesktop for Mac OS X | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-mac.dmg) | [2.1.19](https://mega.nz/file/dc4HXbKZ#m17YAdB5-SZ_rET23g8VT12Y-ECMB6rd1UIUfmKMEHg) | 127,5 MB | `9be3e3bdf884f865e15f308e72b1ed0213c061d27102f80d01897d5355eef8e7` |


1. Launch Anki
2. Go to Tools > Add-ons
3. Click Get Add-ons...
4. Reference the SyncRedirector plugin with the code [**2124817646**](https://ankiweb.net/shared/info/2124817646)
5. If you use docker-anki-sync-server on an external server or custom port:
   1. Select SyncRedirector and click Config
   2. Configure your sync urls
6. Restart Anki - optionally check your console output.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb - look for the Sync button in the main window. Although Anki will ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.


# URL to set on your Anki client devices

| What you need to publish     | Specify in AnkiDesktop       | Specify in AnkiDroid         |
| ---------------------------- | ---------------------------- | ---------------------------- |
| http://127.0.0.1:27701/sync  | http://127.0.0.1:27701/sync  | http://127.0.0.1:27701/      |
| http://127.0.0.1:27701/msync | http://127.0.0.1:27701/msync | http://127.0.0.1:27701/msync |

127.0.0.1 is the loopback address. it work only for you're local device,
your local ip addresse should look like 192.168.1.XXX (try to use a static one as a DHCP assigned one will change every once in a while)
>  Do not put trailing slashes!

# Troobleshooting

If you encounter some error by following thoses procedures and you find out how to fix please create a Push request adding how to solve the problem here.

