Collectd for Joyent SmartOS featuring Giraffi metrics.
----

Setup
====

### clone from repository
<pre><code>
git clone https://github.com/giraffi/collectd-giraffi-smartos.git /opt/collectd-giraffi -b master --depth=1
cp /opt/collectd-giraffi/usr/lib/librabbitmq.so* /opt/local/lib/
</code></pre>

### modify config
<pre><code>
cp /opt/collectd-giraffi/etc/collectd.conf.sample /opt/collectd-giraffi/etc/collectd.conf
</code></pre>

Replace account informations.

<pre><code>
Interval  20
FQDNLookup no
ReadThreads 5
LoadPlugin syslog
<Plugin syslog>
  LogLevel info
</Plugin>
LoadPlugin network
LoadPlugin cpu
LoadPlugin df
LoadPlugin disk
LoadPlugin load
LoadPlugin memory
LoadPlugin swap
LoadPlugin users
LoadPlugin interface
<Plugin interface>
  Interface "eth0"
</Plugin>

LoadPlugin amqp
<Plugin "amqp">
 <Publish "name">
    Host "GIRAFFI_ENDPOINT"
    Port 5672
    VHost "/"
    User "GIRAFFI_USER_ID"
    Password "GIRAFFI_API_KEY"
    Exchange "collectd.json.topic"
    RoutingKey "collectd.GIRAFFI_USER_ID"
    Persistent false
    StoreRates false
    Format "JSON"
  </Publish>
</Plugin>
</code></pre>

### add smf manifest
<pre><code>
svccfg import /opt/collectd-giraffi/share/smf/colelctd-giraffi.xml 
</code></pre>


Start/Stop
====
<pre><code>
svcadm enable colelctd-giraffi
svcadm disable colelctd-giraffi
</code></pre>

