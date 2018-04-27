---
title: "Hi everyone"
date: 2018-04-27T10:09:56-07:00
---
# Hi everyone,

In keeping with our philosophy of supporting open source code and greater transparency for security tools, today we are releasing the results of a recent code audit of Umbrella App by iSEC Partners (made possible thanks to the folks at the Open Technology Fund.)

In total, the code audit found three vulnerabilities rated as “low” and seven rated as “informational.” We have described the vulnerabilities found and our response to them below.

Our code is available here: [https://github.com/securityfirst/Umbrella_android](https://github.com/securityfirst/Umbrella_android)

Please compile it, review it, test it, break it, hack it and tell us what you find. We are passionate about what we do and really care for the security of people who use Umbrella. We warmly welcome any advice on other methods of mitigating vulnerabilities.

If you find something please add any issues to the bug tracker or drop a mail to [rory@secfirst.org](rory@secfirst.org) (PGP: 2C1D3B4D). If it is a security vulnerability we ask that you see our responsible disclosure policy.

Thanks,
Rory

#### 1. Insufficient TLS/SSL certificate validation – Low Severity

Response: Two of the sources (ReliefWeb and the Centers for Disease Control) for the security dashboard feed could not be validly retrieved via HTTPS (one had invalid TLS settings and the other didn’t offer content via https at all). In a preliminary discussion with iSEC it was understood that it was better to offer any type of additional security layer then relying on misconfigured or a non-existent SSL connection. For that we needed the client to be more tolerant. Since this was exposed as the biggest risk, we have resorted to proxying requests from 3rd party sources through our servers. For speed and providing a more effective feed we have added basic caching of data drawn from the third party sources, thus adding the security layer of having a correctly configured server. We will be publishing the code that we use for the backend on our GitHub. As mention in our privacy policy, we have configured the server to not store any personally identifiable data. The only data that we are storing is aggregated and non-identifiable information thats tells us what countries are requested on the dashboard the most. The reason to do this is so that in future, if for example we know that Sudan is a very popular feed, then we might try to find more specific and reliable security related feeds for Sudan. At present we think this offers a sensible and useful advantage to our users but we are willing to listen and if they disagree we will change the process.

#### 2. Excessive session timeout – Low Severity

Response: We were aiming to find a middle ground between security and usability and felt what we had in place was a reasonable approach, particularly as logout is an option for the user. We will revisit this and probably enable it as an option in the settings.

#### 3. Weak TLS/SSL ciphers supported Response – Low Severity

Look at response for pt.5

#### 4. SQL Injection in search and password functionality - Informational

Response: We have sanitised the input parameters using ORMLite SelectArg class in both cases. The lines quoted in the report have been changed to:

```java
where.like(Segment.FIELD_BODY, new SelectArg("%"+query+"%"));
getOrmHelper().getWritableDatabase(getOrmHelper().getPassword())
    .rawExecSQL("PRAGMA rekey = '" + new SelectArg(pw) + “‘;"); 
```   
#### 5. SSL enabled and vulnerable to POODLE attack - Informational

Response: The function in question was not able to be executed on account of the functionality being disabled, so the server was in development mode. We have fixed the server config to safer settings, namely:

      SSLProtocol All -SSLv2 -SSLv3 SSLCompression off SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH 
      
The server now receives A for overall rating in Qualys SSL Labs test.

#### 6. Hard-coded encryption key in source code - Informational

Response: While we don’t see a proper attack vector in this case, we have updated the code to now get the default password from the resource files.

#### 7. Verbose debug error messages logged - Informational

Response: We have changed all error logging in multiple places to only be visible in debug configurations, with the like of:

      if (BuildConfig.BUILD_TYPE.equals(“debug")) Log.getStackTraceString(e.getCause());
      
#### 8. Reflected Cross-Site Scripting in search functionality  - Informational

Response: We sanitised html using Jsoup.clean function so the chunk now looks like this:

```java
String queryText = "";
if (mQueries != null && mQueries.size() > 0) { 
    queryText = Jsoup.clean(mQueries.get(0), Whitelist.simpleText()); 
} 
holder.mSearchText.setText(Html.fromHtml("result while searching for: <b>" + queryText + “</ b>")); 
```   
and the queryText gets passed to a method which does the replace as well.
#### 9. Certificate pinning not implemented in mobile application - Informational

Response: As the code to query our server was not executed at all, we didn’t change the settings on that call. Since then, we have reenable that functionality and are using a different client for the calls to Security First API, which is strict and uses SSL pinning to ensure validity of the certificate against CA breaches. The library used for that purpose is [moxie0/AndroidPinning](https://github.com/moxie0/AndroidPinning)

#### 10. Application does not lock when focus is lost - Informational

Response: Again, as with pt. 4, we were aiming for approach that combines user friendliness. We have a timer to lock out the session and we have added a screenshot protection so the content of the app can’t be acquired via screenshot. Code change in BaseActivity: 

```java
getWindow().setFlags(WindowManager.LayoutParams.FLAG_SECURE, WindowManager.LayoutParams.FLAG_SECURE);
if (BuildConfig.BUILD_TYPE.equals("debug")) Log.getStackTraceString(e.getCause()); 
```        

Click [here](https://secfirst.org/150922_iSEC_Security%20First_Umbrella_Final_2015-06-26_v1.1.pdf) to read the download the full code audit paper.