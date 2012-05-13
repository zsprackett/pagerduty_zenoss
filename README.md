pagerduty_zenoss
================

A Zenoss command for notification to PagerDuty via their rest API


In Zenoss, Events -> Event Manager -> Event Commands -> Add

Command:
pagerduty_zenoss --action trigger --apikey PAGERDUTYAPIKEY --description "${evt/message}" --incidentkey "${evt/evid}"

Clear Command:
pagerduty_zenoss --action resolve --apikey PAGERDUTYAPIKEY --incidentkey "${evt/evid}"
