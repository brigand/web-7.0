Title: Connecting to freenode
Slug: chat
---

The freenode network can be accessed via the [freenode
webchat](//webchat.freenode.net) or using an IRC client such as irssi, WeeChat,
ERC, HexChat, Smuxi, Quassel or mIRC.

You can connect to freenode by pointing your IRC client at `chat.freenode.net`
on ports 6665-6667 and 8000-8002 for plain-text connections, or ports 6697, 7000
and 7070 for SSL-encrypted connections.

## Accessing freenode Via SSL

freenode provides SSL client access on all servers, on ports 6697, 7000 and
7070. Users connecting over SSL will be given user mode +Z, and _is using a
secure connection_ will appear in WHOIS (a 671 numeric). Webchat users will not
currently appear with +Z or the 671 numeric, even if they connect to webchat
via SSL.

In order to verify the server certificates on connection, some additional work
may be required. First, ensure that your system has an up-to-date set of root
CA certificates. On most linux distributions this will be in a package named
something like ca-certificates. Many systems install these by default, but some
(such as FreeBSD) do not.  For FreeBSD, the package is named ca\_root\_nss,
which will install the appropriate root certificates in
/usr/local/share/certs/ca-root-nss.crt.

Certificate verification will generally only work when connecting to
**`freenode.net`**. If your client thinks the server's certificate is invalid,
make sure you are connecting to `chat.freenode.net` rather than any other name
that leads to freenode.

For most clients this should be sufficient. If not, you can download the root
certificate from
[LetsEncrypt](https://letsencrypt.org/certificates/).

Client SSL certificates are also supported, and may be used for identification
to services. See [this kb article](kb/using/certfp). If you have connected with
a client certificate, _has client certificate fingerprint
f1ecf46714198533cda14cccc76e5d7114be4195_ (showing your certificate's SHA1
fingerprint in place of _f1ecf46..._) will appear in WHOIS (a 276 numeric).

## Accessing freenode Via Tor

freenode is also reachable via [Tor<i class="fa fa-external-link"
aria-hidden="true"></i>](https://www.torproject.org/), bound to some
restrictions. You can't directly connect to chat.freenode.net via Tor; use
the following hidden service as the server address instead:

    ajnvpgl6prmkb7yktvue6im5wiedlz2w32uhcwaamdiecdrfpwwgnlqd.onion

If you are using an old version of Tor (before 0.3.5) that does not support
v3 addresses, you should instead use the following address:

    freenodeok2gncmy.onion

The hidden service requires SASL authentication. In addition, due to the abuse
that led Tor access to be disabled in the past, we have unfortunately had to
add another couple of restrictions:

- You must log in using SASL `EXTERNAL` or `ECDSA-NIST256P-CHALLENGE` (more
  below)
- If you log out while connected via Tor, you will not be able to log in
  without reconnecting.

If you haven't set up the requisite SASL authentication, we recommend SASL
EXTERNAL. You'll need to generate a client certificate and add that to your
NickServ account. This is documented [in our knowledge base](kb/using/certfp).

Connecting using SASL EXTERNAL requires that you connect using SSL encryption.

Note that due to the SSL certificates not matching the hidden service, you
might have to disable the verification in your client. If your client supports
*key* pinning, you can verify our Tor server's public key fingerprint:

    E0:1B:31:80:56:D9:78:C4:2B:2D:3F:B2:DB:81:AB:03:15:59:BF:04:7E:31:E8:60:5F:98:07:A1:BB:8F:A3:0D

You'll then want to tell your client to try the `EXTERNAL` mechanism. We lack
comprehensive documentation for this, but it's a feature in most modern
clients, so please check their docs for instructions for now.
