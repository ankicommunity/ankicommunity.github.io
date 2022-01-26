# HTTPS Encryption with Apache Proxy

**Before you proceed, consider the warning!**

!!! warning "AnkiDroid may not verify encryption certificates"

    I ([@kuklinistvan](https://github.com/kuklinistvan)) did not verify personally, but I've read somewhere in an issue that AnkiDroid accepts
    any SSL certificate it gets while initiating the encrypted connection.

    This is a problem, because it can be very easily hijacked which can render the encryption completely useless.

    Keep in mind that at the moment this is kind of a gossip. Please, if you, as the reader can confirm or refute this - for example, with an experiment -, contact us at [Gitter](https://gitter.im/ankicommunity/community). It can be easily the case that it is no longer true (if it has ever been), but some paranoia is very useful when it comes to encryption.

    I just did not want to mislead you :)

## Install Apache2 on your operating system

On Linux, look up the manuals and install the appropriate packages from
the system package manager.

1. Install these software components:

    * Apache2
        * mod_proxy
        * mod_ssl

2. Enable the mods with:

        a2enmod proxy
        a2enmod proxy_http
        a2enmod ssl

3. Restart Apache2 service.

## Get a certificate

Unfortunately, managing SSL certificates and PKI in general is not a quick topic. At the end of the day, you need to get a certificate for your server
that is trusted both by your Android device and your computer.

You can either:

* Get your server online and get a free certificate from [Let's Encrypt](https://letsencrypt.org/)
* Create an in-house Certificate Authority, install its certificate to your Android device and to your computer and issue a certificate for the server with that

!!! warning "Do not underestimate the importance of the measurements!"

    We **highly advise** you to learn about this topic in depth at [Web Service Security
    Tutorial](https://sites.google.com/site/ddmwsst/) - otherwise, there is a high
    chance of creating false encryption, which does not actually protect you.


<!-- ## Generate the certificate and install them on the phone
now you need to generate a self signed certificate. you can do so with the following command

    openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem

It generate two files. Move them somewhere safe and add the path to these two file in the following config
(DISCLAIMER, the forementioned  command may not be best practice but hey, it works)
Transfer the cert.pem file to the phone where you run AnkiDroid as you need to import is (save it on your phone and go under the correct setting. For android look for biometrics and security -> other security settings -> install from local storage -->

## Create or extend a `<VirtualHost>`

Here is a VirtualHost with SSL and proxying enabled.

    <VirtualHost *:443>
        ServerName anki.my.fancy.server.net
    
        <Location /sync>
            ProxyPass http://127.0.0.1:27701/sync
            ProxyPassReverse http://127.0.0.1:27701/sync
        </Location>
        <Location /msync>
            ProxyPass http://127.0.0.1:27701/msync
            ProxyPassReverse http://127.0.0.1:27701/msync
        </Location>
    
        UseCanonicalName off
        SSLEngine on
        SSLProtocol +TLSv1.2
        SSLCertificateFile /path/to/the/cert/cert.pem
        SSLCertificateKeyFile /path/to/the/key/key.pem
        ProxyRequests off
        ProxyPreserveHost on
    </VirtualHost>
    
### Apache2 References

* [mod_proxy](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html)
* [mod_ssl](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html)
