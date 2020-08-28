---
title: Arbets belastningar för samhantering
titleSuffix: Configuration Manager
description: Lär dig mer om arbets belastningarna som du kan växla från Configuration Manager till Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 0425b937062acd96b8df66df38ec53a04e91b4de
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995236"
---
# <a name="co-management-workloads"></a>Arbets belastningar för samhantering

Du behöver inte byta arbets belastningar eller så kan du göra dem individuellt när du är klar. Configuration Manager fortsätter att hantera alla andra arbets belastningar, inklusive de arbets belastningar som du inte växlar till Intune, och alla andra funktioner i Configuration Manager den samhanteringen inte stöder.

Om du växlar en arbets belastning till Intune, men ändrar dig senare, kan du växla tillbaka till Configuration Manager.

Samhantering har stöd för följande arbets belastningar:

- [Efterlevnadspolicyer](#compliance-policies)  

- [Windows Update principer](#windows-update-policies)  

- [Resurs åtkomst principer](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Enhetskonfiguration](#device-configuration)  

- [Office Klicka-och-kör-appar](#office-click-to-run-apps)  

- [Klient program](#client-apps)  

## <a name="compliance-policies"></a>Efterlevnadsprinciper

Efterlevnadsprinciper definierar de regler och inställningar som en enhet måste följa för att anses vara kompatibla med principer för villkorlig åtkomst. Du kan också använda efterlevnadsprinciper för att övervaka och åtgärda kompatibilitetsproblem med enheter oberoende av villkorlig åtkomst. Från och med Configuration Manager version 1910 kan du lägga till utvärdering av anpassade konfigurations bas linjer som en bedömnings regel för efterlevnadsprinciper. Mer information finns i [Inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Mer information om Intune-funktionen finns i [efterlevnadsprinciper för enheter](/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Windows Update principer

Med Windows Update för affärs principer kan du konfigurera regler för avstängning för Windows 10-funktions uppdateringar eller kvalitets uppdateringar för Windows 10-enheter som hanteras direkt av Windows Update för företag.

Mer information om Intune-funktionen finns i [Konfigurera principer för avstängning av Windows Update för företag](/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Resurs åtkomst principer

Resurs åtkomst principer konfigurera VPN, Wi-Fi, e-post och certifikat inställningar på enheter.

Mer information om Intune-funktionen finns i [distribuera resurs åtkomst profiler](/intune/device-profiles).

> [!Note]  
> Resurs åtkomst arbets belastningen ingår också i enhets konfigurationen. Dessa principer hanteras av Intune när du växlar arbets belastningen för [enhets konfigurationen](#device-configuration) .

## <a name="endpoint-protection"></a>Slutpunktsskydd

<!--1357365-->

Endpoint Protection arbets belastningen omfattar Windows Defender Suite för skydd mot skadlig kod:

- Windows Defender program mot skadlig kod
- Windows Defender Application Guard  
- Windows Defender-brandvägg  
- Windows Defender SmartScreen  
- Windows-kryptering
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender Säkerhetscenter  
- Windows Defender Avancerat skydd (nu kallat Microsoft Defender Threat Protection)

Mer information om Intune-funktionen finns i [Endpoint Protection för Microsoft Intune](/intune/endpoint-protection-windows-10).

> [!Note]  
> När du växlar den här arbets belastningen finns Configuration Manager-principerna kvar på enheten tills Intune-principerna skriver över dem. Det här beteendet ser till att enheten fortfarande har skydds principer under över gången.
>
> Endpoint Protection arbets belastningen ingår också i enhets konfigurationen. Samma sak gäller när du växlar arbets belastningen för [enhets konfigurationen](#device-configuration) .<!-- SCCMDocs.nl-nl issue #4 --> När du växlar arbets belastningen för enhets konfigurationen innehåller den också principer för Windows Information Protection-funktionen, som inte ingår i arbets belastningen för Endpoint Protection.<!-- 4184095 -->
>
> De inställningar för Microsoft Defender Antivirus som är en del av profil typen enhets begränsningar för enhets konfiguration i Intune ingår inte i omfattningen för skjutreglaget för slut punkts skydd. Om du vill hantera Microsoft Defender Antivirus för samhanterade enheter med skjutreglaget för Endpoint Protection aktiverat, använder du de nya antivirus principerna i **Microsoft Endpoint Manager administrations Center**  >  **Endpoint Security**  >  **Antivirus**. Den nya princip typen har nya och förbättrade alternativ och har stöd för alla samma inställningar som är tillgängliga i profilen enhets begränsningar. <!--6609171-->
>
> Windows-krypterings funktionen innehåller BitLocker-hantering. Mer information om beteendet för den här funktionen med samhantering finns i [distribuera BitLocker-hantering](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Enhetskonfiguration

<!--1357903-->

Arbets belastningen enhets konfiguration innehåller inställningar som du hanterar för enheter i din organisation. När du växlar den här arbets belastningen flyttas även **resurs åtkomsten** och **Endpoint Protection** arbets belastningar.

Du kan fortfarande distribuera inställningar från Configuration Manager till samhanterade enheter även om Intune är enhets konfigurations utfärdaren. Detta undantag kan användas för att konfigurera inställningar som din organisation kräver men som ännu inte är tillgängliga i Intune. Ange detta undantag i en [Configuration Manager konfigurations bas linje](../compliance/deploy-use/create-configuration-baselines.md). Aktivera alternativet att **alltid tillämpa den här bas linjen även för samhanterade klienter** när du skapar bas linjen. Du kan ändra den senare på fliken **Allmänt** i egenskaperna för en befintlig bas linje.  

Mer information om Intune-funktionen finns [i skapa en enhets profil i Microsoft Intune](/intune/device-profile-create).  

> [!NOTE]
> När du växlar arbets belastningen för enhets konfigurationen innehåller den också principer för Windows Information Protection-funktionen, som inte ingår i arbets belastningen för Endpoint Protection.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Office Klicka-och-kör-appar

<!--1357841-->

Den här arbets belastningen hanterar Microsoft 365 appar på samhanterade enheter.

- När arbets belastningen har flyttats visas appen i **företagsportal** på enheten  

- Office-uppdateringar kan ta cirka 24 timmar innan de visas på klienten om inte enheterna startas om  

- Det finns ett nytt globalt villkor, **Office 365-program som hanteras av Intune på enheten**. Det här villkoret läggs till som standard som ett krav på nya Microsoft 365-program. När du flyttar den här arbets belastningen uppfyller inte samhanterade klienter kraven på programmet. Sedan installerar de inte Microsoft 365 som distribueras via Configuration Manager.  

Mer information om Intune-funktionen finns i [tilldela Microsoft 365 appar till Windows 10-enheter med Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

## <a name="client-apps"></a>Klientappar

<!--1357892-->

Använd Intune för att hantera klient program och PowerShell-skript på samhanterade Windows 10-enheter. När du har övergått till den här arbets belastningen är alla tillgängliga appar som distribueras från Intune tillgängliga i Företagsportal. Appar som du distribuerar från Configuration Manager är tillgängliga i Software Center.

Mer information om Intune-funktionen finns i [Vad är Microsoft Intune App Management?](/intune/app-management).

> [!Tip]  
> Den här funktionen introducerades först i version 1806 som en [för hands versions funktion](../core/servers/manage/pre-release-features.md). Från och med version 2002 är det inte längre en för hands versions funktion.  
>
> Den här funktionen kan visas i listan med funktioner som **mobilappar för samhanterade enheter**.<!-- 5849669 -->

Från och med version 1910 kan de nu hantera Microsoft Intune Win32-appar till samhanterade klienter när du aktiverar Microsoft Connected cache på dina Configuration Manager distributions platser. Mer information finns [i Microsoft Connected cache i Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagram över app-arbetsbelastningar

:::image type="content" source="media/co-management-apps.svg" alt-text="Diagram över arbets belastningar för samhantering av appar" lightbox="media/co-management-apps.svg":::

> [!TIP]
> Från och med version 2006 kan du konfigurera Företagsportal så att du även kan visa Configuration Manager appar. Om du ändrar den här app Portal-upplevelsen ändras de beteenden som beskrivs i diagrammet ovan. Mer information finns i [Använd Företagsportalappen på samhanterade enheter](company-portal.md).<!--CMADO-3601237,INADO-4297660-->

## <a name="known-issues"></a>Kända problem

När Endpoint Protection arbets belastningen flyttas över till Intune kanske klienten fortfarande följer principer som angetts av Configuration Manager och Microsoft Defender. <!--5024559-->

Undvik det här problemet genom att använda CleanUpPolicy.xml med ConfigSecurityPolicy.exe när Intune-principerna har tagits emot av klienten med hjälp av stegen nedan:

1. Kopiera och spara texten nedan som `CleanUpPolicy.xml` .

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```

1. Öppna en upphöjd kommando tolk för `ConfigSecurityPolicy.exe` . Den här körbara filen är vanligt vis i någon av följande kataloger:
   - C:\Program\Windows Defender
   - C:\Program\Microsoft säkerhets klient

1. I kommando tolken skickar du i XML-filen för att rensa principen. Till exempel `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Nästa steg

[Så här växlar du arbets belastningar](how-to-switch-workloads.md)
