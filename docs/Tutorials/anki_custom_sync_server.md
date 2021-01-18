# Redirecting Anki to a custom synchronization server

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

[SyncRedirector usage](/Projects/SyncRedirector/)
