## Generate an authority key

First you must generate an authority key, which will be used to verify the integrity of the keylist. For higher security, I recommend that you store this key on an OpenPGP smart card such as a YubiKey. Here is an example authority key:

```sh
$ gpg2 --list-keys --fingerprint "GPG Sync Example Authority"
pub   rsa4096/980EA13A 2016-07-07 [SC] [expires: 2017-07-07]
      Key fingerprint = 2646 A274 C86C 618D 6DB9  23A1 F0B6 DC77 980E A13A
uid         [ultimate] GPG Sync Example Authority
sub   rsa4096/9484EB1D 2016-07-07 [E] [expires: 2017-07-07]
```

## Create the keylist
Now create a list of all of the fingerprints (the _keylist_) that your organization uses. I recommend that you manually compare each person's fingerprint before adding it to this list. And while this isn't required by GPG Sync, it's a good idea to sign each person's key with your authority key, and have them sign the authority key back, so you can build an internal web of trust.

Each fingerprint in the keylist should have its own line. Spaces within fingerprints are optional. Comments (which start with `#` characters) and whitespace is ignored, so feel free to mark up your fingerprints file with notes. It's good practice to explain who each key belongs to in a comment. Here's my example `fingerprints.txt`.

```
# Micah Lee
927F 419D 7EC8 2C2F 149C  1BD1 403C 2657 CD99 4F73 # Micah Lee <micah@micahflee.com>
0B14 9192 9806 5962 5470  0155 FD72 0AD9 EBA3 4B1C # (REVOKED) Micah Lee <micah@micahflee.com>

# TODO: add other keys

91C0 C982 A41F 8D39 3953  1A71 FAB7 37F9 C5C1 CA80 # First Look warrant canary key
```

## Sign the keylist

Next, create a detached signature of your keylist using your authority key. Here's how I'm doing it in my example:

```sh
$ gpg2 -u 980EA13A --detach-sign fingerprints.txt
```

This creates a second file, `fingerprints.txt.sig`, which contains the signature.

## Publish the keylist

Finally, upload `fingerprints.txt` and `fingerprints.txt.sig` to a website (if you'd like, you could maintain this file in a public git repository) and make a note of the URL, as well as the authority key fingerprint. You'll need to give the signing key fingerprint and the URL of `fingerprints.txt` to each member of your organization in order to configure GPG Sync on their computers.

## Update the keylist

Each time there is a key change in your organization, you need to add the new fingerprints to `fingerprints.txt`, re-sign it with your authority key, and re-upload it to the **same URL**.