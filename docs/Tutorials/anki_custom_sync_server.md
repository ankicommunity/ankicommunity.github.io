# Configuring Anki to use a Custom Synchronization Server

After you have set up an Anki server by following one of our guides (or some
other way), here is how you can configure Anki to use your server instead AnkiWeb.

# URL to set on your Anki client devices

Suppose you're hosting `anki-sync-server` at `your_anki_server.tld`. In this case:

| What you need to publish     | Specify in AnkiDesktop       | Specify in AnkiDroid         |
| ---------------------------- | ---------------------------- | ---------------------------- |
| http://your_anki_server.tld/sync  | http://your_anki_server.tld/sync  | http://your_anki_server.tld/      |
| http://your_anki_server.tld/msync | http://your_anki_server.tld/msync | http://your_anki_server.tld/msync |


## AnkiDroid

Open the app, then slide off the menu from the left side. Go Settings > Advanced > Custom sync server and specify the same two urls you've specified on the desktop client.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb. Head to the main screen of the application (the list of decks) and slide down to synchronize (or use the icon next to the menu in the top right corner). Although Anki will ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.


## AnkiDesktop 

### Current version

This section is under construction, we're sorry for the inconvenience.

### 2.1.19

1. Launch Anki
2. Go to Tools > Add-ons
3. Click Get Add-ons...
4. Reference the SyncRedirector plugin with the code [**2124817646**](https://ankiweb.net/shared/info/2124817646)
5. If you use docker-anki-sync-server on an external server or custom port:
   1. Select SyncRedirector and click Config
   2. Configure your sync urls
6. Restart Anki - optionally check your console output.

From now on, you can synchronize your collection the same way you would if you were using AnkiWeb - look for the Sync button in the main window. Although Anki will ask for your AnkiWeb ID the first time, you need to enter the server credentials you've set up previously instead.
