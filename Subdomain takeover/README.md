### Description

Subdomain takeover vulnerabilities occur when a subdomain is pointing to a service (e.g. GitHub pages, Heroku, AWS/S3) that has been removed or deleted. 
This is a summary of EdOverflow's ["can-i-take-over-xyz"](https://github.com/EdOverflow/can-i-take-over-xyz).

### Content
Always look out for a custom `404 not found ` page pointing to a service.   
I will only describe the most important and common cases here (e.g. there is no public subdomain-takeover regarding "Cargo Collective" but it's "vulnerable" too).   

**Github**  
Optical indicators: 404 not found page. Own it by re-registering the username.
```
A: 192.30.252.153 [ or ] 192.30.252.154
CNAME: username.github.io
```
**Amazon S3 (cloud computing)**  
Optical indicators: "NoSuchBucket". Own it by creating an AWS account e.g. using the free tier (aws.amazon.com/free)
```
CNAME: *.s3.amazonaws.com
```
**Microsoft Azure**  
Azure can host various services: Web Apps (*.azurewebsites.net), Cloud Services (*.cloudapp.net), Traffic Manager profiles (*.trafficmanager.net) or Blob Storages (*.blob.core.windows.net). Once a service is removed it's address will become available to others.

**Heroku**  
Optical indicators: "No such app". Own it by creating a new app on Heroku named like the missing entry.
```
CNAME: *.herokuapp.com
```
**Tumblr**    
Optical indicators: "Not found" or "There's nothing here".
```
A: 66.6.44.4
```
**WordPress**  
Optical indicators: "Domain mapping upgrade for this domain not found". Register the required WordPress account.

**Feedpress**  
Optical indicators: "The feed has not been found".
```
CNAME: redirect.feedpress.me
```
**Zendesk**  
Optical indicators: "Oops, this help center no longer exists".

**Surge.sh**  
To own the affected subdomain edit your account-settings to the following (which also indicates)
```
A: 45.55.110.124
CNAME: na-west1.surge.sh
```

**Ghost**  
Costs 20$. Indiciators:
```
CNAME: *.ghost.io
```

**BitBucket**  
```
CNAME: *.bitbucket.io
```

**Desk**  
Indicators: A rediection will be made to the following page: support.desk.com/system/site_not_found
```
CNAME: *.desk.com
```

**JetBrains**  
Indicators: A rediection will be made to the following page: jetbrains.com/youtrack/youtrack-hosted-master/instanceIsNotRegistered/*
```
CNAME: *.myjetbrains.com
```

