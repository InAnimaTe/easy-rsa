easy-rsa
========

My own clone of easy-rsa with some added enhancements to make it even easier! (eventually)
./vars has been modified for simple basic defaults that are acceptable for an average user.


Instructions
========

There are multiple guides out there for doing this. Here is a quick rundown of what is needed.

1. Edit `./vars` to re-definte the variables for default values of things like CountryName, organizationName, etc.. (optional)
2. `source ./vars`
3. `./clean-all`
4. `./build-ca`, enter through everything if you agree with defaults
5. `./build-dh`
6. `./build-key-server <servername>`, this will create keys for the server, **do not set a challenge password**
7. `./build-key <clientname>`, this will create keys for a client named `<clientname>`, **do not set a challenge password**
    
   **Note** that you *only* need the `ca.[crt|key]` files existent in `./keys` to be able to create more client keys!

8. Copy the keys to the appropriate places. All server keys will need to go to `/etc/openvpn` and `server.conf` will need to have lines defining these files.

   For a client, you will need the `ca.crt` and the `<clientname>.[crt|key]` files.

9. Additionally, for extra security, it is good idea to apply HMAC auth (tls-auth) using a `ta/static.key`. 

    This can be generated via `openvpn --genkey --secret /root/easy-rsa/keys/ta.key` and must exist on both the server and client (and called in the config like `tls-auth ta.key 1`)
    More on this here: https://community.openvpn.net/openvpn/wiki/Hardening#Useof--tls-auth
    
    
Here are official pages on the entire process with a bit more explanation:

http://openvpn.net/index.php/open-source/documentation/miscellaneous/77-rsa-key-management.html
https://wiki.archlinux.org/index.php/Create_a_Public_Key_Infrastructure_Using_the_easy-rsa_Scripts








