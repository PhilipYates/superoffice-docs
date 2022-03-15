---
title: Services84.PersonAgent.GetConsentInfos SOAP
generated: 1
uid: Services84-Person-GetConsentInfos
---

# Services84 Person GetConsentInfos

SOAP request and response examples **Remote/Services84/Person.svc**
Implemented by the <see cref="M:SuperOffice.Services84.IPersonAgent.GetConsentInfos">SuperOffice.Services84.IPersonAgent.GetConsentInfos</see> method.

## GetConsentInfos

Get all consent information for a given person.

* **personId:** The person id



[WSDL file for Services84/Person](../Services84-Person.md)

Obtain a ticket from the [Services84/SoPrincipal.svc](../SoPrincipal/index.md)

Application tokens must be specified if calling an Online installation. ApplicationTokens are not checked for on-site installations.

## GetConsentInfos Request

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope
 xmlns:SOAP-ENV="http://www.w3.org/2003/05/soap-envelope"
 xmlns:SOAP-ENC="http://www.w3.org/2003/05/soap-encoding"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
 xmlns:NetServerServices842="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
 xmlns:NetServerServices841="http://schemas.microsoft.com/2003/10/Serialization/"
 xmlns:Person="http://www.superoffice.net/ws/crm/NetServer/Services84">
  <Person:ApplicationToken>1234567-1234-9876</Person:ApplicationToken>
  <Person:Credentials>
    <Person:Ticket>7T:1234abcxyzExample==</Person:Ticket>
  </Person:Credentials>
 <SOAP-ENV:Body>
   <Person:GetConsentInfos>
    <Person:PersonId xsi:type="xsd:int">0</Person:PersonId>
   </Person:GetConsentInfos>

 </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```


## GetConsentInfos Response

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope
 xmlns:SOAP-ENV="http://www.w3.org/2003/05/soap-envelope"
 xmlns:SOAP-ENC="http://www.w3.org/2003/05/soap-encoding"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
 xmlns:NetServerServices842="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
 xmlns:NetServerServices841="http://schemas.microsoft.com/2003/10/Serialization/"
 xmlns:Person="http://www.superoffice.net/ws/crm/NetServer/Services84">
 <SOAP-ENV:Body>
  <Person:GetConsentInfosResponse>
   <Person:Response xsi:type="Person:ArrayOfConsentInfo">
    <Person:ConsentInfo xsi:type="Person:ConsentInfo">
     <Person:ConsentPersonId xsi:type="xsd:int">0</Person:ConsentPersonId>
     <Person:Comment xsi:type="xsd:string"></Person:Comment>
     <Person:Registered xsi:type="xsd:dateTime">2021-11-30T13:22:16Z</Person:Registered>
     <Person:RegisteredAssociateId xsi:type="xsd:int">0</Person:RegisteredAssociateId>
     <Person:Updated xsi:type="xsd:dateTime">2021-11-30T13:22:16Z</Person:Updated>
     <Person:UpdatedAssociateId xsi:type="xsd:int">0</Person:UpdatedAssociateId>
     <Person:LegalBaseId xsi:type="xsd:int">0</Person:LegalBaseId>
     <Person:LegalBaseKey xsi:type="xsd:string"></Person:LegalBaseKey>
     <Person:LegalBaseName xsi:type="xsd:string"></Person:LegalBaseName>
     <Person:ConsentPurposeId xsi:type="xsd:int">0</Person:ConsentPurposeId>
     <Person:ConsentPurposeKey xsi:type="xsd:string"></Person:ConsentPurposeKey>
     <Person:ConsentPurposeName xsi:type="xsd:string"></Person:ConsentPurposeName>
     <Person:ConsentSourceId xsi:type="xsd:int">0</Person:ConsentSourceId>
     <Person:ConsentSourceKey xsi:type="xsd:string"></Person:ConsentSourceKey>
     <Person:ConsentSourceName xsi:type="xsd:string"></Person:ConsentSourceName>
    </Person:ConsentInfo>
   </Person:Response>
  </Person:GetConsentInfosResponse>
 </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```
