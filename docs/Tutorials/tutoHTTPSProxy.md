HTTPS Encryption with Apache Proxy
==================================

# Setup Apache2
if you want to use the anki sync server with AnkiDroid you may be faced with an error about unsecured download you may want to set up a https proxy
you may need to install a plugins to allow your self signed certificat.
You need an apache2 server running somewhere.

Here is the detailed procedure for apache2

    sudo apt-get install apache2  # if you don't have it already
    sudo a2enmod proxy
    sudo a2enmod proxy_http
    sudo a2enmod ssl
    sudo systemctl restart apache2

# Generate the certificate  and install them on the phone
now you need to generate a self signed certificate. you can do so with the following command

    openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem

It generate two files. Move them somewhere safe and add the path to these two file in the following config
(DISCLAIMER, the forementioned  command may not be best practice but hey, it works)
Transfer the cert.pem file to the phone where you run AnkiDroid as you need to import is (save it on your phone and go under the correct setting. For android look for biometrics and security -> other security settings -> install from local storage

# add apache2 sites
then you can edit this file ( if you know what this file is or have other site running on the same server, you can do it on another one (beware of using the right port))

    sudo nano /etc/apache2/sites-available/000-default.conf

Here is an example what you should paste inside:

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
    
Nginx can work out too, but it has not been tested.

**Attention**:  you should change the port if you've put anki-sync-server to a non-standard one.

# Troubleshooting

If you encounter some error by following thoses procedures and you find out how to fix it please create a Push request adding how to solve the problem here.
