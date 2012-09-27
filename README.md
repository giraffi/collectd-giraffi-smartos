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

