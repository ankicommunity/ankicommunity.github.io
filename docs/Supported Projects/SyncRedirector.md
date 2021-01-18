# SyncRedirector

Created originally for
[`docker-anki-sync-server`](/Supported%20Projects/anki-sync-server/),
SyncRedirector is a plugin with the intention to make redirecting the
synchronization url in the client a smoother experience.

## Supported desktop client versions

| Variant | Client support | GitHub | AnkiWeb ID |
| ------- | :------------ :| :----: | :--------: |
| Legacy  | 2.1.19 | [GitHub](https://github.com/ankicommunity/anki-desktop-addons/tree/main/SyncRedirector-legacy) | [**2124817646**](https://ankiweb.net/shared/info/2124817646) |
| Djankiserv Connect | Latest* | [GitHub](https://github.com/ankicommunity/anki-desktop-addons/tree/main/SyncRedirector) | [**1724518526**](https://ankiweb.net/shared/info/1724518526) |

<sup>*: with the new version we target the latest version of the Anki desktop client, however, we don't have a record of tested versions as of yet.</sup>

## Usage

1. Launch Anki
2. Go to Tools > Add-ons
3. Click on "Get Add-ons..."
4. Reference the SyncRedirector plugin with appropriate code (see the table above)
5. If you use `docker-anki-sync-server` on an external server or custom port:
      1. Select SyncRedirector and click Config
      2. Configure your sync urls
6. Restart Anki - optionally check your console output.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb - look for the Sync button in the main window. Although Anki is going to  ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.
