# cnwrt
ip tables and domain tables used by dd-wrt to bypass gfw

===How to Setup R6300V2===

1. Flash dd-wrt

refer to http://www.dd-wrt.com/wiki/index.php/Netgear_R6300v2

2. Install shadowsocks

refer to https://haoutil.com/topic/install-shadowsocks-on-ddwrt

3. Add startup command
cp firewall.sh and cn.sh to /opt/etc
{{{
mount -o bind /jffs/opt /opt
/jffs/opt/bin/ss-redir -c /jffs/opt/etc/shadowsocks.json -f /var/run/ss-redir.pid
/opt/etc/firewall.sh
}}}

4. Setup dnsmasq
DNSMasq Enable
Local DNS Enable
No DNS Rebind Enable
Query DNS in Strict Order Enable
Add Requestor MAC to DNS Query Disable
Additional DNSMasq Options
conf-dir=/jffs/opt/etc/dnsmasq.d
copy gfw.conf to /jffs/opt/etc/dnsmasq.d

5. Add cron jobs
copy cron_wrapper to /opt/etc
0 5 * * * root /opt/etc/cron_wrapper

