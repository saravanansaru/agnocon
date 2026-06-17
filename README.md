nano /usr/local/freeswitch/conf/directory/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/directory/"/>

nano /usr/local/freeswitch/conf/autoload_configs/callcenter.conf.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/skillset/"/>

nano /usr/local/freeswitch/conf/dialplan/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/dialplan/"/>

nano /usr/local/freeswitch/conf/dialplan/public/00_inbound_did.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/didmapping/"/>

sudo sysctl fs.inotify.max_user_instances=1024

cat /proc/sys/fs/inotify/max_user_instances

sudo systemctl restart agnocon.service

curl http://localhost/api/skillset/
curl http://localhost/api/directory/
