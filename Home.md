![GPG Sync](https://github.com/firstlookmedia/gpgsync/blob/master/logo/logo.png)

GPG Sync works like this:

* The techie generates an "authority key". Then they create a list of GPG fingerprints that all members of your organization should keep updated, digitally sign this list with the authority key, and upload it to a website so that it's accessible from a public URL.
* All members of the organization install GPG Sync on their computers and configure it with the authority key's fingerprint and the URL of your signed fingerprint list. (Now, all of your members will automatically and regularly fetch this URL and then refresh all of the non-revoked keys on the list from a key server.)
* When new keys in your organization are added, the techie adds them to the fingerprint list, re-signs it with the authority key, and uploads it to the same URL. If users migrate to new keys, the techie leaves their old fingerprints on the list so that all other members can tell that their old keys were revoked.

Now each member of your organization will have up-to-date public keys for each other member, and key changes will be transitioned smoothly without any further work or interaction.

Here are some features:

* Works in Mac OS X and Linux
* Creates system tray applet that launches automatically on boot
* Downloads from HKPS key server by default, but customizable
* Supports fetching fingerprints URL over Tor or other SOCKS5 proxies
* Makes sure non-revoked public keys are refreshed once a day
* Works seamlessly with the web of trust

If you'd like to test out GPG Sync without creating your own authority key and fingerprints file, you can use one that [we created for testing](https://github.com/firstlookmedia/gpgsync/blob/master/fingerprints/README.md).