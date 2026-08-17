nano /usr/local/freeswitch/conf/directory/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/directory/"/>

nano /usr/local/freeswitch/conf/autoload_configs/callcenter.conf.xml
<param name="odbc-dsn" value="$${dbconnection}"/>
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/skillset/"/>

nano /usr/local/freeswitch/conf/dialplan/default.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/dialplan/"/>
	<X-PRE-PROCESS cmd="exec" data="curl -k http://localhost/api/dialplan/"/>
	<extension name="outbound_Jio">
    <condition field="destination_number" expression="^(((\+*)((0[ -]*)*|((91 )*))((\d{12})+|(\d{10})+))|\d{5}([- ]*)\d{6})$">		
		<action application="log" data="X-Company-ID is ${sip_h_X-Company-ID}"/>
		<action application="log" data="X-Company-ID is ${sip_h_X-User-ID}"/>
		<action application="set" data="company_id=${sip_h_X-Company-ID}"/>
		<action application="set" data="cc_agent=${sip_h_X-User-ID}"/>
		<action application="set" data="call_type=Outbound"/>
    <action application="record_session" data="E:/recordings/${strftime(%Y)}/${strftime(%m)}/${strftime(%d)}/${uuid}.wav"/>
    <action application="bridge" data="{sip_from_uri=sip:+914435052611@100.64.24.4<sip:+914435052611@100.64.24.4>}sofia/gateway/JioSip/$1"/>
    </condition>
    </extension>

nano /usr/local/freeswitch/conf/dialplan/public/00_inbound_did.xml
<X-PRE-PROCESS cmd="exec" data="curl http://localhost/api/didmapping/"/>

sudo sysctl fs.inotify.max_user_instances=1024

cat /proc/sys/fs/inotify/max_user_instances

sudo systemctl restart agnocon.service

curl http://localhost/api/skillset/
curl http://localhost/api/directory/
vars.xml
<X-PRE-PROCESS cmd="set" data="default_password=Admin@123"/>
  <X-PRE-PROCESS cmd="set" data="dbconnection=pgsql://hostaddr=192.168.240.47 dbname=agnocon user=postgres password='Tasmac@2026'  connect_timeout=30"/>
  <X-PRE-PROCESS cmd="set" data="dbconnectioncdr=host=192.168.240.47  dbname=agnocon  user=postgres password=Tasmac@2026 connect_timeout=30"/>
