
Stop DDoS Attacks

To stop DDoS (distributed denial of service) attack, one needs to have a clear understanding of what happens when an attack takes place. In short, a DDoS attack can be accomplished by exploiting vulnerability in the server or by consuming server resources (for example, memory, hard disk, and so forth).There are two broad types of DDoS attacks: bandwidth depletion attacks and resources depletion attacks. In order to halt both types of attacks, you can follow the steps given below:

If only a few computers are the source of the attack and you have identified the source of those IP, you can put an ACL (access control list) in your firewall blocking those IPs. Change the IP address of the web server for a while, if possible, but it will not be affective when the attacker will start resolving your new IP by querying your DNS servers.
When you identify that attacks originating from a specific country, you think block that country’ IP block, at least for a while.
Create an inbound traffic profile. This way you will know who is regularly visiting your site. In case you discover an unexpected number of new visitors, you can further investigate the logs and source IPs. Before large scale attacks, you might experience a small-scale DDOS attack that the attacker may use to estimate the strength of your network resilience.
The easiest, although a costly, way to defend your network from bandwidth consumption attack is to buy more bandwidth.
You may deploy more servers, spread around various datacenters, and you may use good load balancing software.
Make sure your DNS is protected behind the same type of load balancer that you used to protect your web and other resources.
Optimize your webserver to handle more visitors without exhausting all resources. If you are using Apache server, you can use Apachebooster plugin, which was designed by integration of varnish and nginx. Apachebooseter can cope with sudden spike with traffic and memory usages.
Fast DNS-Protect against DNS-based DDoS attacks with a highly scalable DNS infrastructure. You can think about buying CloudFlair business or enterprise plan, which provides protection to DNS and layer 3, 4 and 7 based DDoS attacks.
Enable anti IP spoofing features in your firewall and routers. It is much easier to implement anti-spoofing in Cisco ASA firewall than in the routers. To enable anti-spoof with ASDM, click on configuration from firewalls and then click on anti-spoofing. You can prevent spoofing in router using ACL. Create an access control list for your internal IP subnets, and apply that ACL in your Internet facing interface.
Hire third party DDoS service to protect your site. There are a number of service providers with robust network who can help your website survive during denial of service attack. You can subscribe to such service for a monthly cost of few hundred dollars only.
Pay attention to your server’s security configuration in order to prevent resource depletion type of DDoS attack.
Consult a DDoS expert, and make an action plan to carry out when you actually face the attack.
Monitor your network and web traffic. If possible you can set up multiple analytics such as Statcounter and Google analytics in order to understand and gather more data of your traffic patterns.
Secure you DNS server against recursive DNS query attacks.
Block ICMP in your router. Enable it when you need it for troubleshooting purpose only. Also you can do the following things with your router: rate limit, filtering packets, timeout half-open connections, drop junk and spoofed packets, set low threshold for TCP SYN, ICMP and UDP flood drop.
Finally study more about DDoS attacks and be familiar with the types of DDoS attacks and make action plan to defend against each type of DDoS attack.

- See more at: http://securitywing.com/15-ways-to-stop-ddos-attacks-in-network/#sthash.hGp2Eoe6.dpuf
