---
title: Konfigurera proxyinställningar för Intune-anslutningsappen för Active Directory
description: Beskriver hur du konfigurerar Intune-anslutningsappen för Active Directory till att fungera med befintliga lokala proxyservrar.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: b26bf4910e6745a60634a2b313a37beeb33192d3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986896"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Arbeta med befintliga lokala proxyservrar

Den här artikeln förklarar hur du konfigurerar Intune-anslutningsappen för Active Directory till att fungera med utgående proxyservrar. Den är avsedd för kunder med nätverksmiljöer som har befintliga proxyservrar.

Som standard försöker Intune Connector för Active Directory automatiskt hitta en proxyserver i nätverket med WPAD (Web Proxy Auto-Discovery). Om detta har konfigurerats i ditt nätverk kanske ytterligare konfiguration inte krävs.  Om ändringar krävs kan du använda följande avsnitt för att åsidosätta standardinställningarna, och samtidigt använda [standardfunktionerna för .NET Framework för att konfigurera proxyinställningar](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  Ytterligare alternativ beskrivs i dokumentationen.

Mer information om hur anslutningsappar fungerar finns i avsnittet om att [förstå anslutningsappar för Azure AD-programproxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Kringgå helt utgående proxyservrar

Du kan konfigurera anslutningsappen till att kringgå den lokala proxyn för att säkerställa att den använder direktanslutning till Azure-tjänsterna. Vi rekommenderar den här metoden förutsatt att din nätverksprincip tillåter det, eftersom det innebär att det blir en färre konfiguration att underhålla.

Om du vill inaktivera utgående proxyanvändning för anslutningsappen redigerar du filen :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config och lägger till proxyadressen och proxyporten i det avsnitt som visas i det här kodexemplet:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

För att säkerställa att Connector Updater-tjänsten kringgår proxyn gör du en liknande ändring i C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Se till att göra kopior av originalfilerna i fall du behöver återställa till de standardmässiga .config-filerna.

När konfigurationsfilerna har ändrats behöver du starta om Intune-anslutningsapptjänsten. 

1. Öppna **services.msc**.
2. Leta upp och välj **Intune ODJConnector-tjänsten**.
3. Välj **Starta om**.

![Skärmbild av omstart av tjänsten](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Ange en alternativ proxyserver

Om en annan proxyserver (till exempel en som kringgår autentisering) måste användas med Intune Connector för Active Directory kan det anges på liknande sätt. Om du vill göra det redigerar du filen :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config och lägger till proxyadressen och proxyporten i det avsnitt som visas i det här kodexemplet:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

För att säkerställa att Connector Updater-tjänsten kringgår proxyn gör du en liknande ändring i C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Se till att göra kopior av originalfilerna i fall du behöver återställa till de standardmässiga .config-filerna.

När konfigurationsfilerna har ändrats behöver du starta om Intune-anslutningsapptjänsten. 

1. Öppna **services.msc**.
2. Leta upp och välj **Intune ODJConnector-tjänsten**.
3. Välj **Starta om**.

![Skärmbild av omstart av tjänsten](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Nästa steg

[Hantera dina enheter](../remote-actions/device-management.md)
