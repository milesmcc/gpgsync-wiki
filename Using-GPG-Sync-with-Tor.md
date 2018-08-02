It's simple to configure GPG Sync to download the fingerprints URL and refresh public keys from key servers using the Tor network. First, you need to install a system Tor on your computer.

* **Mac OS X:** The easiest way to install Tor and have it always run in the background in OS X is by using [Homebrew](http://brew.sh/). Install it if you don't already have it. Then install Tor and configure it to run in the background by typing this into your terminal:

  ```sh
  $ brew install tor
  $ brew services start tor
  ```

* **Linux:** Make sure you have a system Tor installed in the background. In Debian or Ubuntu, you can run `sudo apt install tor` to install it.

Now edit your GPG Sync keylist, click "Show advanced settings", and check the box next to `Load URL through SOCKS5 proxy (e.g. Tor)`. Leave the host as `127.0.0.1` and the port as `9050`, and save.