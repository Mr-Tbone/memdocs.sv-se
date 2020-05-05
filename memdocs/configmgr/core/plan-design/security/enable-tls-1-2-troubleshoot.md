---
title: Vanliga problem när du aktiverar Transport Layer Security (TLS) 1,2
titleSuffix: Configuration Manager
description: Beskriver vanliga problem när du aktiverar Transport Layer Security (TLS) 1,2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720529"
---
# <a name="common-issues-when-enabling-tls-12"></a>Vanliga problem vid aktivering av TLS 1.2

Den här artikeln innehåller råd om vanliga problem som uppstår när du aktiverar TLS 1,2-stöd i Configuration Manager.

## <a name="unsupported-platforms"></a>Plattformar som inte stöds

Följande klient plattformar stöds av Configuration Manager, men stöds inte i en TLS 1,2-miljö:

- Windows CE
- Apple OS X
- Windows 10-enheter som hanteras med lokal MDM

## <a name="reports-dont-show-in-the-console"></a>Rapporter visas inte i-konsolen

Om rapporter inte visas i Configuration Manager-konsolen, måste du uppdatera den dator där du kör-konsolen. [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)och aktivera stark kryptering.

## <a name="fips-security-policy-enabled"></a>Princip för FIPS-säkerhet aktive rad

Om du aktiverar princip inställningen FIPS-säkerhet för antingen klienten eller en server kan du använda TLS-1,0 för att kunna använda TLS. Det här beteendet inträffar även om du inaktiverar protokollet i registret.

Om du vill undersöka aktiverar du händelse loggning för säker kanal och granskar sedan Schannel-händelser i system loggen. Mer information finns i [så här begränsar du användningen av vissa kryptografiska algoritmer och protokoll i Schannel. dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>SQL Server kommunikations problem

Om SQL Server kommunikation Miss lyckas och returnerar ett **SslSecurityError** -fel kontrollerar du följande inställningar:

- [Uppdatera .NET Framework](enable-tls-1-2-server.md#bkmk_net)och aktivera stark kryptering på varje dator
- [Uppdatera SQL Server](enable-tls-1-2-server.md#bkmk_sql) på värd servern
- [Uppdatera SQL-klientens komponenter](enable-tls-1-2-server.md#bkmk_sql-client) på alla system som kommunicerar med SQL. Till exempel plats servrar, SMS-provider och plats roll servrar.

## <a name="configuration-manager-client-communication-failures"></a>Configuration Manager klient kommunikations problem

Om Configuration Manager klienten inte kommunicerar med plats roller kontrollerar du att du har [uppdaterat Windows](enable-tls-1-2-client.md#bkmk_winhttp) för att stödja TLS 1,2 för klient-server-kommunikation med hjälp av WinHTTP. Vanliga plats roller är distributions platser, hanterings platser och platser för tillståndsmigrering.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Repor ting Services-platsen Miss lyckas och returnerar ett förväntat fel

Om repor ting Services-platsen inte konfigurerar rapporter kontrollerar du **SRSRP. log** efter följande fel post:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Följ dessa anvisningar för att lösa problemet:

1. [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)och aktivera stark kryptografi på alla relevanta datorer.

1. När du har installerat uppdateringar startar du om SMS_Executive tjänsten.

## <a name="application-catalog-doesnt-initialize"></a>Program katalogen är inte initierad

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [borttagna och föråldrade funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Om program katalogen inte initieras kontrollerar du **ServicePortalWebSite. svclog** -filen för följande felpost:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Följ dessa anvisningar för att lösa problemet:

1. [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)och aktivera stark kryptografi på alla relevanta datorer.

1. I `%WinDir%\System32\InetSrv` mappen på program katalog servern skapar du en **W2SP. exe. config** -fil med följande innehåll:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Den här filen är den standard fil som skapas om programmet skapades med hjälp av .NET Framework 4.6.3.

1. Använd HTTPS Transport Security för program katalog roller.

    > [!Important]
    > När du använder HTTP-meddelandets säkerhet för program katalog roller hårdkodas WCF för att endast använda SSL 3,0 och TLS 1,0. Detta förhindrar användning av TLS 1,2.

1. Om du har gjort några ändringar startar du om datorn.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Software Center eller webbläsare kommunicerar inte med program katalogen

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [borttagna och föråldrade funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Den bästa metoden för att göra Software Center att fungera med användare tillgängliga appar på en TLS 1,2-aktiverad plats, tar du bort rollen program katalog. Låt sedan Software Center kommunicera direkt med en hanterings plats. Mer information finns i [ta bort program katalogen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Om du behöver lösa kommunikations fel mellan program katalogen och Software Center kontrollerar du följande villkor:

- [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)och aktivera stark kryptering på varje dator.

- När du har gjort ändringarna startar du om alla berörda datorer.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Överförings problem med tjänst anslutnings punkt

Om tjänst anslutnings punkten inte överför data till SCCMConnectedService [uppdaterar du .NET Framework](enable-tls-1-2-server.md#bkmk_net)och aktiverar stark kryptering på varje dator. Kom ihåg att starta om datorerna när du har gjort ändringarna.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager-konsolen visar dialog rutan Intune Onboarding

Om dialog rutan Intune Onboarding visas när konsolen försöker ansluta till Intune-portalen [uppdaterar du .NET Framework](enable-tls-1-2-client.md#bkmk_net)och aktiverar stark kryptografi på varje dator. Kom ihåg att starta om datorerna när du har gjort ändringarna.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager-konsolen visar att det inte går att logga in på Azure

När du försöker skapa program i Azure Active Directory (Azure AD) kan du, om dialog rutan Azure-tjänster onboarding omedelbart Miss lyckas när du har valt **Logga in**, [Uppdatera .NET Framework](enable-tls-1-2-server.md#bkmk_net)och aktivera stark kryptering. Kom ihåg att starta om datorerna när du har gjort ändringarna.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager Cloud Services och TLS 1,2

Azure virtuella datorer som används av Cloud Management Gateway och moln distributions platser stöder TLS 1,2. Klient versioner som stöds använder automatiskt TLS 1,2.

**SMSAdminui. log** kan innehålla ett fel som liknar följande exempel:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

I systemets händelse logg kan SChannel EventID 36874 loggas med följande beskrivning:`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Ytterligare resurser

- [Metod tips för TLS (Transport Layer Security) med .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1,2 stöd för Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Teknisk referens för kryptografiska kontroller](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Nästa steg

- [Aktivera TLS 1.2 på klienter](enable-tls-1-2-client.md)
- [Aktivera TLS 1,2 på plats servrarna och fjärrplatsens system](enable-tls-1-2-server.md)

