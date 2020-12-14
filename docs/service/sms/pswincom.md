---
# This basic template provides core metadata fields for Markdown articles on docs.superoffice.com.

# Mandatory fields.
title: pswincom_sms_plugin       # (Required) Very important for SEO. Intent in a unique string of 43-59 chars including spaces.
description: PSWinCom NetServer SMS plugin # (Required) Important for SEO. Recommended character length is 115-145 characters including spaces.
author: {github-id}             # Your GitHub alias.
keywords:
so.topic: howto                 # article, howto, reference, concept, guide

# Optional fields. Don't forget to remove # if you need a field.
# so.envir:              # cloud or onsite
# so.client:                    # online, web, win, pocket, or mobile
---

# PSWinCom

This document describes how to set up the PSWinCom NetServer SMS plugin to use in Customer Service. You need to set up an account with [PSWinCom][1] to get a username and password to connect to their service.

## Outgoing SMS Configuration from SuperOffice 8.0 SR3

Go to **System - SMS** inside the Service client or **Mailings - Settings** inside Sales & Marketing client. Choose PSWinCom SMS in the list of available modules

In the **Plugin configuration** you add:
```text
pswin_username =
pswin_password =
```

![x][2]

Note - do not include the brackets.

## Outgoing SMS Configuration in SR2 or earlier

From version 7.1 SR1 of NetServer, the SupeOffice.Messaging.PSWinCom.dll is included in the NetServer release. The plugin can also be used in 7.1, but the .dll must be copied manually to the NetServer library folder (bin folder).

### Web.config settings

Under configuration, add and replace username and password with the information you have from PSWinCom:

```xml
 <appSettings>  
    <add key="pswin_username" value=""/>
    <add key="pswin_password" value=""/>
    <add key="pswin_seriesStart" value=""/>
    <add key="pswin_seriesEnd" value=""/>
    <add key="pswin_noStatusReport" value=""/>
    <add key="pswin_NoSmsSession" value=""/>
 </appSettings>
```

Under configuration -> SuperOffice -> Factory -> DynamicLoad add:

```xml
 <add key="PSWinCom" value="SuperOffice.Messaging.PSWinCom.dll" />
```

Under configuration -> system.serviceModel add:

```xml
  <client>
     <endpoint address="http://sms.pswin.com/SOAP/SMS.asmx" binding="basicHttpBinding" bindingConfiguration="SMSServiceSoap" contract="PsWinComGW.SMSServiceSoap" name="SMSServiceSoap" />
  </client>
```

Under configuration -> system.serviceModel -> bindings, add:

```xml
<basicHttpBinding>
  <binding name="SMSServiceSoap" closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" allowCookies="false"
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
[1]: https://www.linkmobility.com/products/link-sms-gateway/
[2]: media/pswincomsmssettings.png