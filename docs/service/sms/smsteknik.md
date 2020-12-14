---
# This basic template provides core metadata fields for Markdown articles on docs.superoffice.com.

# Mandatory fields.
title: smsteknik_sms_plugin       # (Required) Very important for SEO. Intent in a unique string of 43-59 chars including spaces.
description: Configuration of SMSTeknik NetServer SMS plugin # (Required) Important for SEO. Recommended character length is 115-145 characters including spaces.
author: {github-id}             # Your GitHub alias.
keywords:
so.topic: howto                 # article, howto, reference, concept, guide

# Optional fields. Don't forget to remove # if you need a field.
# so.envir:              # cloud or onsite
# so.client:                    # online, web, win, pocket, or mobile
---

# Configuration of SMSTeknik NetServer SMS Plugin

This document describes how to set up the SMSTeknik NetServer SMS plugin to use in Customer Service. You need to set up an account with [SMSTeknik][1] to get a username and password to connect to their service.

## Outgoing SMS Configuration from SuperOffice 8.0 SR3

Go to **System - SMS** inside the Service client or **Mailings - Settings** inside Sales & Marketing client. Choose SMS Teknik in the list of available modules

In the **Plugin configuration** you add:

```text
smsteknik_serviceId =
smsteknik_username =
smsteknik_password =
```

![x][2]

Note - do not include the brackets.

## Outgoing SMS Configuration in SR2 or earlier

The file SupeOffice.Messaging.SMSTeknik.dll must be copied manually to the NetServer library folder (bin folder). You may download version 8.0 SR2 [here][3].

### Web.config settings

Under configuration, add and replace username and password with the information you have from SMSTeknik:

```xml
<appSettings>
    <!-- Company name, provided by SMS Teknik  -->
    <add key="smsteknik\serviceId" value="[ServiceID]" />
    <!-- Username, provided by SMS Teknik  -->
    <add key="smsteknik_username" value="[Username]" />
    <!-- Password, provided by SMS Teknik -->
    <add key="smsteknik_password" value="[Password]" />
    <!-- 0=disabled (160 char), 1=enabled (up to 918 chars) -->
    <add key="smsteknik_multisms" value="1" />
    <!-- 0=disabled, 1-6 SMS count (max) -->
    <add key="smsteknik_maxmultisms" value="6"/>
</appSettings>
```

Under configuration -> SuperOffice -> Factory -> DynamicLoad add:

```xml
<add key="SuperOffice.Messaging.SMSTeknik" value="SuperOffice.Messaging.SMSTeknik.dll" />
```

Under configuration -> system.serviceModel add:

```xml
<client>  
      <endpoint address="https://www.smsteknik.se/webservices/SendSMSws1/Service.asmx"  
          binding="basicHttpBinding" bindingConfiguration="SendSMSSoap"
          contract="SMSTeknikGW.SendSMSSoap" name="SendSMSSoap" />
</client>
```
  
Under configuration -> system.serviceModel -> bindings, add:

```xml
<basicHttpBinding>
        <binding name="SendSMSSoap" closeTimeout="00:01:00" openTimeout="00:01:00"
            receiveTimeout="00:10:00" sendTimeout="00:01:00" allowCookies="false"
            bypassProxyOnLocal="false" hostNameComparisonMode="StrongWildcard"
            maxBufferSize="65536" maxBufferPoolSize="524288" maxReceivedMessageSize="65536"
            messageEncoding="Text" textEncoding="utf-8" transferMode="Buffered"
            useDefaultWebProxy="true">
          <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384"
              maxBytesPerRead="4096" maxNameTableCharCount="16384" />
          <security mode="Transport">
            <transport clientCredentialType="None" proxyCredentialType="None"
                realm="" />
            <message clientCredentialType="UserName" algorithmSuite="Default" />
          </security>
        </binding>
        <binding name="SendSMSSoap1" closeTimeout="00:01:00" openTimeout="00:01:00"
            receiveTimeout="00:10:00" sendTimeout="00:01:00" allowCookies="false"
            bypassProxyOnLocal="false" hostNameComparisonMode="StrongWildcard"
            maxBufferSize="65536" maxBufferPoolSize="524288" maxReceivedMessageSize="65536"
            messageEncoding="Text" textEncoding="utf-8" transferMode="Buffered"
            useDefaultWebProxy="true">
          <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384"
              maxBytesPerRead="4096" maxNameTableCharCount="16384" />
          <security mode="None">
            <transport clientCredentialType="None" proxyCredentialType="None"
                realm="" />
            <message clientCredentialType="UserName" algorithmSuite="Default" />
          </security>
        </binding>
</basicHttpBinding>
```

<!-- Referenced links -->
[1]: http://www3.smsteknik.se/tj%C3%A4nster/sms-gateway
[2]: media/smstekniksmssettings.png
[3]: https://community.superoffice.com/globalassets/technical-club/images/service/smsplugin8sr2/superoffice.messaging.smsteknik.dll