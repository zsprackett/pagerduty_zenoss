pagerduty_zenoss
================

A Zenoss command for notification to PagerDuty via their rest API


In Zenoss, Events -> Event Manager -> Event Commands -> Add

Command:
/usr/local/bin/pagerduty_zenoss --action trigger --apikey 7116b41059b8012f7f4c123139146e6c --description "${evt/device}: ${evt/summary}" --incidentkey "${evt/evid}"

Clear Command:
pagerduty_zenoss --action resolve --apikey PAGERDUTYAPIKEY --incidentkey "${evt/evid}"
