# Dashboards 

## (Correlation Search Tuning Dashboard)[Dashboards/correlation_search_tuning.xml]

[correlation_search_tuning.xml](Dashboards/correlation_search_tuning.xml) contains a dashboard that could be useful in quickly reviewing dashboards and jumping to incident response to further explore new and existing correlation searches. 

You'll need to change test and 14 to whatever you use for test statuses.

```xml
<input type="radio" token="status">
      <label>Search Status</label>
      <choice value="">All</choice>
      <choice value="default_status IN (test*,14)">Development</choice>
      <choice value="NOT default_status IN (test*,14)">Production</choice>
      <default></default>
    </input>
```

You can use this rest query to find out what your test statuses are. 

```
| rest splunk_server=local count=0 /services/saved/searches 
| where match('action.correlationsearch.enabled', "1|[Tt]|[Tt][Rr][Uu][Ee]") 
| rename eai:acl.app as app, title as csearch_name, action.correlationsearch.label as csearch_label, action.notable.param.security_domain as security_domain, action.notable.param.default_status as default_status 
```

You'll also need to update the `CDATA` URL with your Splunk ES instance name. 
