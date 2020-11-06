# SyncRedirector

Created originally for
[`docker-anki-sync-server`](/Supported%20Projects/anki-sync-server/),
SyncRedirector is a plugin with the intention to make redirecting the
synchronization url in the client a smoother experience.

Right now it supports the legacy variant of
[`anki-sync-server`](/Supported%20Projects/anki-sync-server/)

| Variant | Client support | GitHub |
| ------- | :------------ :| :----: |
| Legacy  | 2.1.19 | [GitHub](https://github.com/ankicommunity/docker-anki-sync-server/tree/master/Addon%20for%20AnkiDesktop/SyncRedirector) |

## Usage

### Legacy variant

1. Launch Anki
2. Go to Tools > Add-ons
3. Click Get Add-ons...
4. Reference the SyncRedirector plugin with the code [**2124817646**](https://ankiweb.net/shared/info/2124817646)
5. If you use docker-anki-sync-server on an external server or custom port:
   1. Select SyncRedirector and click Config
   2. Configure your sync urls
6. Restart Anki - optionally check your console output.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb - look for the Sync button in the main window. Although Anki will ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.
