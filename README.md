pagerduty_zenoss
================

Summary
-------

A Zenoss command for triggering and resolving incidents within PagerDuty via their rest API.

Within PagerDuty:
-----------------

Create a “Generic API system” service:

1.  In your account, under the Services tab, click "Add New Service".
2.  Enter a name for the service and select an escalation policy. Then, select “Generic API system” for the Service Type.
3.  Click the "Add Service" button.
4.  Once the service is created, you’ll be taken to the service page. On this page, you’ll see the “Service key”, which will be needed when you configure your Zenoss to send events to PagerDuty. 

Within Zenoss:
--------------

1.  Run the following commands:
2.  
```
cd /usr/local/bin
wget https://raw.github.com/ryanhoskin/pagerduty_zenoss/master/pagerduty_zenoss
chmod 755 pagerduty_zenoss
```

3.  Go to Events > Event Manager > Event Commands > Add.
4.  Enter the following for the command information:

Command:
```
/usr/local/bin/pagerduty_zenoss --action trigger --apikey PAGERDUTY_API_KEY --description "${evt/device}: ${evt/summary}" --incidentkey "${evt/evid}"
```
Clear Command:
```
pagerduty_zenoss --action resolve --apikey PAGERDUTY_API_KEY --incidentkey "${evt/evid}"
```

Make sure to set enabled to True and replace PAGERDUTY_API_KEY with your PagerDuty Service key.  Your PagerDuty service key can be found under services > &lt;service name&gt; > Integration Settings > Service API key.  

<strong>Note:</strong>  This has been tested with Zenoss 3.1.0 on CentOS 5x64.

Troubleshooting:
----------------

If you're having trouble with getting Zenoss to trigger new incidents, check to make sure that the command is getting triggered by running the following:

```
grep pagerduty /opt/zenoss/log/zenactions.log
```

You should see an event like the following:

2013-03-29 17:30:03,413 INFO zen.ZenActions: Queueing /usr/local/bin/pagerduty_zenoss --action trigger --apikey PAGERDUTY_API_KEY --description "localhost: SNMP agent down" --incidentkey "f8e7c752-be86-4286-9503-7f7778f17bed"

