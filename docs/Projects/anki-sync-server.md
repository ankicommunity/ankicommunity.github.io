# `anki-sync-server`

As of yet we can provide you these variants of the synchronization server*.


| Variant | Anki Desktop version | Anki Droid version | GitHub url | DockerHub url |
|--------|:--------------------:|:------------------:|:----------:|:----------:|
| [Legacy](#legacy-variant) |    2.1.19            |  2.9.1          | [GitHub](https://github.com/ankicommunity/docker-anki-sync-server) | [DockerHub](https://hub.docker.com/r/kuklinistvan/anki-sync-server) |
| [djankiserv](#djankiserv)  | latest * | latest * | [GitHub](https://github.com/ankicommunity/djankiserv) | pending ** |

\*, \*\*: [see below](#djankiserv)

## djankiserv

A modern, Django-based implementation with the goal to support the latest Android and desktop clients.

At the moment:

* \*: with the new version we target the latest version of clients, however, we don't have a record of tested versions.

* \*\*: we do not have an *official* production-ready Docker image.

## Legacy variant

The legacy variant is based on the original
[`anki-sync-server`](https://github.com/ankicommunity/anki-sync-server).
    
This is the battle-tested version. It does not support the most recent Anki
clients, however, as of writing, it is the version that you can probably safely
rely on.

Download mirrors for the old Anki clients (including the Android version) are
provided in the [GitHub
repository](https://github.com/ankicommunity/docker-anki-sync-server).



