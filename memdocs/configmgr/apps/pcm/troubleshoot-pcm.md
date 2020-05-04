---
title: Felsök Package Conversion Manager
titleSuffix: Configuration Manager
description: Lär dig hur du felsöker problem med Package Conversion Manager i Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d2a7d4a16f85e9a5f78dd6251754d86527da87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709896"
---
# <a name="troubleshoot-package-conversion-manager"></a>Felsök Package Conversion Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

Använd informationen i den här artikeln som hjälp för att felsöka problem när du använder Package Conversion Manager.



## <a name="sms-provider"></a>SMS-provider

Paket konverterings hanteraren använder SMS-providern. Mer information finns i [Planera för SMS-providern](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

Om SMS-providern inte fungerar korrekt fungerar inte Configuration Manager-konsolen inklusive paket konverterings hanteraren.



## <a name="package-readiness"></a>Paket beredskap

Innan du konverterar ett paket till ett program analyserar du paketet med hjälp av funktionen Package Conversion Manager- **analys** . Efter analysen lägger du till kolumnen **beredskap** i noden **paket** i Configuration Manager-konsolen. Listan med paket visar något av följande beredskaps tillstånd för det analyserade paketet:

- **Automatiskt**: paketet kan konverteras direkt med funktionen **Convert** .      

  > [!NOTE]  
  > En automatisk konvertering konverterar inte WQL-frågor till program krav. Använd **Fix-och Convert** -processen för att konvertera dessa frågor.  

- **Manuellt**: paketet behöver några tillägg eller ändringar innan du kan konvertera det med hjälp av funktionen **Fix och Convert** .  

- **Inte tillämpligt**: paketet är inte lämpligt för konvertering. Du kan antingen korrigera eventuella problem med paketet eller fortsätta att distribuera det som ett paket.  

- **Fel**: paketet innehåller fel. Korrigera felen manuellt innan du kan analysera och konvertera det.  

I informations fönstret i noden **paket** i Configuration Manager-konsolen visas eventuella beredskaps problem. Välj ett paket och välj sedan fliken **Sammanfattning** i informations fönstret.



## <a name="log-files"></a>Loggfiler

### <a name="enable-logging"></a>Aktivera loggning

När du aktiverar loggning för Package Conversion Manager loggar den alla åtgärder, undantag och fel. 

Om du vill aktivera loggning för den här komponenten i Configuration Manager ändrar du **Microsoft. ConfigurationManagement. exe. config**. Den här konfigurations filen finns som standard i följande sökväg:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

Lägg till följande **växlar** och **spåra** XML-element i elementet **system. Diagnostics** efter det sista elementet **sources** :

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

I det här exemplet används filen **PCMtrace. log**. Den här loggen finns på den dator som kör Configuration Manager-konsolen på följande sökväg:  
`%UserProfile%\AppData\Local\Temp`

Om du vill konfigurera detalj nivån ändrar du inställningen för spårnings växeln **PcmLogging** . Ange det här värdet till fyra detalj nivåer, från minst detaljerad (`1`) till mest detaljerade (`4`).


### <a name="smsprovlog"></a>SMSProv.log

I vissa situationer finns information som är relevant för att felsöka paket konverterings processen i filen **SMSProv. log** . Den här filen fångar information från Configuration Manager SMS-providern.

Som standard finns logg filen på Configuration Manager plats Server på följande sökväg:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Om du ser något av följande fel meddelanden kan filen **SMSProv. log** innehålla relevant felsöknings information:

- `The SMS Provider reported an error`

- `Generic Failure`

Dessa fel meddelanden indikerar vanligt vis att ett fel har inträffat på plats servern och att fel informationen inte skickades till Configuration Manager-konsolen.

Mer information finns i [teknisk referens för fel meddelanden i Package Conversion Manager](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Ändra paketets attribut efter analysen

När du har analyserat ett paket och har ett beredskaps tillstånd för **Automatisk** eller **manuell**, kan konverterings processen Miss klar om du ändrar något av de relevanta attributen.

Du kan till exempel analysera ett paket och dess beredskaps tillstånd är **automatiskt**. Sedan lägger du till ett annat program i paketet. Paket konverteringen kanske inte fungerar.

Om du behöver göra ändringar i ett paket efter analysen kör du om analysen före konverteringen. 



## <a name="see-also"></a>Se även

[Teknisk referens för fel meddelanden i Package Conversion Manager](error-messages.md)
