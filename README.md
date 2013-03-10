muttvcardsearch
============

ABOUT
------------
muttvcardsearch is a small mutt carddav search utility for your Owncloud or SOGo server.
It is written in C++ and depends *only* on [libcurl](http://curl.haxx.se/libcurl/) and [sqlite3](http://www.sqlite.org/). It supports multiple servers.

The vcard code is entirely based on [libvcard](http://code.google.com/p/libvcard), but does not need QT and also fixes some
major bugs I found in [libvcard](http://code.google.com/p/libvcard/) (parsing vcards from file,
parsing attribute values containing a colon...). It is not feature complete, i.e. not
all functions from *libvcard* are implemented at this time but it works quiet well for me.
I plan to implement all features from the original *libvcard*-library (currently 1.0.2).

I wrote *muttvcardsearch* using QtCreator, so currently you will need Qt to **build** the project
but not to run it. I plan to support *cmake* too, so stay tuned ;)

INSTALL
------------
first, install
* libcurl / libcurl-dev
* sqlite3 / sqlite3-dev

then

1. clone the repository
2. cd into the new repository
3. execute `qmake; make; sudo make install`

Call muttvcardsearch without arguments to see how to configure it.
After that set your query command in your .muttrc
* `set query_command = "muttvcardsearch '%s'"`

If you like to have your data cached locally use *--create-local-cache* as the first and only option.
This will download all your contacts into ~/.config/muttvcardsearch/cache.sqlite3. A new search should
then search the local cache first and if your query does not return any data it will search the server.

The utility will automatically insert new records not found in the cache but found online.

TODO
------------
* add option *--update-local-cache* to refresh the cache instead to force you to re-create it every time you made a change on your server. This will only work after the migration away from libvcard (this requirement has been met with version 1.4)
* add option to save a contact into your vcard store (just like abook)
* support cmake
