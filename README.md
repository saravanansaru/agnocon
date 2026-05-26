nano /usr/local/freeswitch/conf/directory/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/directory/"/>

/usr/local/freeswitch/conf/autoload_configs/callcenter.conf.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/skillset/"/>


curl http://localhost/api/directory/

nano /usr/local/freeswitch/conf/dialplan/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/dialplan/"/>

nano /usr/local/freeswitch/conf/dialplan/public/00_inbound_did.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/didmapping/"/>
