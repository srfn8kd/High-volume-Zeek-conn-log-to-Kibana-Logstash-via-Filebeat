# High-volume-Zeek-conn-log-to-Kibana-Logstash-via-Filebeat
A method for sending 10gpbs++ Zeek connection logs to Logstash/Kibana - hint, you can't use the Filebeat Zeek Module.
After much testing and debugging, I determined that while the Zeek Filebeat/Logstash/Kibana modules is really nice, it was not coded with high volume data in mind.  
Unfortunately the Zeek module creates JSON events which are virtually 4x larger than the actual data logged in the Zeek connection log, and this has an extremely detrimental effect on shipping the data via Filebeat to the logstash server.  When you are doing up to 10gbps monitoring with Zeek, the conn files are greater than 2.5G in size every 10 minutes, which means when using the Zeek module with Filebeat, Filebeat actually has to send almost 10G of data every 10 minutes.

While it is theoretically possible to ship this much data via Filebeat, you would have to build a very expensive machine in order to do it.  If you have the $$$, then I say go for it for sure, as the Zeek modules does do some nice things in Kibana, like provide GeoIP and other data.  If you don't, then basically don't use the module, and shipping up to 10gbps of data will be no problem and it will only require basic configurations on both ends to work perfectly.

See the example config for how I have configured Filebeat.
