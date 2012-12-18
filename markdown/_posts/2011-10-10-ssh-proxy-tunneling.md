Found yourself in a foreign country which restricts access to social media or streaming sites?  Frustrated by an error page when trying to watch the latest Walking Dead episode on the <a href="http://www.amctv.com/">AMC website</a>?  Feel wrong to connect through VPN just to check your crush's Facebook wall?   Foreign censorship sucks.  Here's how to regain access to those sites we have all grown so fond of.

<!--more-->Mentioned above, one obvious and popular way of skirting around this censorship nightmare is through a VPN, or <a href="http://en.wikipedia.org/wiki/Virtual_private_network" target="_blank">Virtual Private Network</a>.  VPNs have been around forever to offer secure remote access to a central network, typically a school or corporate network.  There are free, personal VPN solutions out there (notably <a href="http://openvpn.net/" target="_blank">OpenVPN</a>) which can connect you to your always-on home PC for transferring files, checking email, etc.  However, a VPN solution can have its downsides.  Firstly, all internet services utilize this encrypted connection, which can hog CPU and isn't necessary when you just need to stream Bruce Springsteen from Pandora.  Also, a VPN connection requires the service to be running on your remote client, which many US-based hosts do not allow without a SSL certificate.

Another option is <a title="Tor Project" href="https://www.torproject.org/" target="_blank">Tor</a>, a free client which connects to your browser and encrypts &amp; routes traffic through a random path of other Tor users.  Essentially Tor is a P2P connection to the net, meaning that the source and destination of connection requests are untraceable.  Interesting and powerful technology, and supposedly safe, but I personally didn't feel very comfortable opening my computer ports to a circuit of strangers.  I'm not fond of what I can't fully understand.

The last solution worth mentioning is probably the easiest and most flexible, making it my favorite.  A <a href="http://en.wikipedia.org/wiki/Proxy_server" target="_blank">web proxy server</a> simply acts as a gateway between your local client and the internet for common http connections.  Ahh, just what we want.

The only requirements for setup are:
<ul>
    <li>A Unix-based terminal or ssh client on the computer you have with you</li>
    <li>A running server with uncensored web-connectivity and ssh access - this can be a PC at home or a <a href="http://en.wikipedia.org/wiki/Web_hosting_service">web host</a>.  While the server does not need to have a static IP address, in the case of a home PC you must know this IP or have set up a static locator such as <a href="http://dyn.com/dns/">DynDNS.org</a>.</li>
</ul>
I will not get into too much detail here since there are plenty of guides already online.  But to prevent snoopers from eavesdropping on the weird stuff you watch on YouTube, you will want to encrypt your connection to the remote proxy server using <a href="http://en.wikipedia.org/wiki/Secure_Shell" target="_blank">ssh</a>.  This requires ssh access to your server as well as an ssh client.  As always with standard versions of Windows, these features aren't available out-of-the-box and require ssh protocol support from client and server.  For a client Windows box, see  <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/">PuTTY</a>,  and for a server Windows box, see <a href="http://cygwin.com/" target="_blank">Cygwin</a>.

Running the following command from your terminal client and authenticating yields the encrypted, interactive network tunnel you are looking for.
<pre lang="shell"> ssh -ND 8888 username@yourdomain.com</pre>
Or for a home PC running a ssh server on port 22,  this would look like:
<pre lang="shell"> ssh -p 22 -ND 8888 username@SERVER_IP_ADDRESS</pre>
This shell should now be running on your client port 8888 (although no confirmation should appear after authenticating due to the -N parameter).  Now all you have to do is configure your browser of choice's proxy settings for SOCKS through the server port number we defined above.  Note that the hostname should be 'localhost' since we are already connected via ssh.

Tips:
<ul>
    <li>To configure which sites will automatically use this proxy (so the blocked or censored sites), I recommend the Firefox add-on <a href="https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/">FoxyProxy</a>.</li>
    <li>If your connection is crappy, which is often the case when traveling abroad, add -C to the shell command for compression.</li>
    <li>If your proxy server is running Linux, I recommend installing <a href="http://www.squid-cache.org/">Squid</a> for caching and security.  It can be installed with
<pre lang="shell">apt-get install squid</pre>
or
<pre lang="shell">yum install squid</pre>
</li>
    <li>Also note that a proxy connection can be tracked to its source through the host's log file.  So no funny business.</li>
</ul>
Hit the comments (or just google it) if you have questions.

EDIT:  Apparently certain video streaming sites such as Hulu are starting to block access from proxy servers.  Best to give Tor a shot for these tricksters.