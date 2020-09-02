---
title: Använda StageNow-loggar på Android Zebra-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Se vanliga problem och lösningar vid användning av StageNow på Android-enheter med Microsoft Intune. Lär dig även hur du hämtar loggar och se exempel på hur du kan läsa loggarna med avseende på framgång eller fel.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8cc44cb614154df1a128ee1f1708a3259f88169
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910051"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Felsök och se potentiella problem på Android Zebra-enheter i Microsoft Intune



I Microsoft Intune kan du använda [Zebra Mobility Extensions (MX) för att hantera Android Zebra-enheter](android-zebra-mx-overview.md). När du använder Zebra-enheter kan du skapa profiler i StageNow för att hantera inställningar och ladda upp dem till Intune. Intune använder StageNow-appen för att tillämpa inställningarna på enheterna. StageNow-appen skapar även en detaljerad loggfil på enheten som används för felsökning.

Den här funktionen gäller för:

- Android

Du kan till exempel skapa en profil i StageNow för att konfigurera en enhet. När du skapar StageNow-profilen genererar det sista steget en fil som du använder för att testa profilen. Sedan använder du den här filen med StageNow-appen på enheten.

I ett annat exempel skapar du en profil i StageNow och testar den. I Intune lägger du till StageNow-profilen och tilldelar den sedan till dina Zebra-enheter. När du kontrollerar status för den tilldelade profilen visar profilen en status på hög nivå.

I båda dessa fall kan du få mer information från StageNow-loggfilen, som sparas på enheten varje gång en StageNow-profil tillämpas.

Vissa problem är inte relaterade till innehållet i StageNow-profilen och återspeglas inte i loggarna.

Den här artikeln visar hur du läser StageNow-loggarna och beskriver några andra potentiella problem med Zebra-enheter som kanske inte återspeglas i loggarna.

[Använda och hantera Zebra-enheter med Zebra Mobility Extensions](android-zebra-mx-overview.md) innehåller mer information om den här funktionen.

## <a name="get-the-logs"></a>Hämta loggarna

### <a name="use-the-stagenow-app-on-the-device"></a>Använda StageNow-appen på enheten
När du testar en profil direkt med hjälp av StageNow på datorn, i stället för att använda [Intune för att distribuera profilen](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow), sparar StageNow-appen på enheten loggarna från testet. Du hämtar loggfilen med hjälp av alternativet **Mer (...)** i StageNow-appen på enheten.

### <a name="get-logs-using-android-debug-bridge"></a>Hämta loggar med hjälp av Android Debug Bridge
Om du vill hämta loggar när profilen redan har distribuerats med Intune ansluter du enheten till en dator med [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (detta öppnar Android-webbplatsen).

På enheten sparas loggar i `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Hämta loggar från e-post
För att hämta loggar efter att profilen redan har distribuerats med Intune kan slutanvändare skicka loggarna till dig via e-post med hjälp av en e-postapp på enheten. På Zebra-enheten öppnar du företagsportalappen och [skickar loggarna](../user-help/send-logs-to-your-it-admin-by-email-android.md). När du använder funktionen för att skicka loggar skapas även ett PowerLift-incident-ID som du kan hänvisa till om du kontaktar Microsoft-supporten.

## <a name="read-the-logs"></a>Läsa loggarna

När du tittar på loggarna uppstår ett fel när du ser taggen `<characteristic-error>`. Information om felet skrivs till taggen `<parm-error>` > egenskapen `desc`.

## <a name="error-types"></a>Feltyper

Zebra-enheter innehåller olika felrapporteringsnivåer:

- CSP:n stöds inte på enheten. Enheten är till exempel inte en mobilenhet och har inte någon mobilhanterare.
- MX- eller OSX-versionen stämmer inte överens. Varje CSP har versionshantering. En fullständig supportmatris finns i [Zebra-dokumentationen](http://techdocs.zebra.com/mx/) (detta öppnar Zebra-webbplatsen).
- Enheten rapporterar ett annat problem eller fel.

## <a name="examples"></a>Exempel

Du har till exempel följande indataprofil:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

I loggen är XML identisk med indata. Dessa matchande utdata innebär att profilen tillämpades på enheten utan fel:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

I ett annat exempel har du följande indata:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

Loggen visar ett fel eftersom den innehåller en `<characteristic-error>`-tagg. I det här scenariot försökte profilen installera ett Android-paket (APK) som inte finns på den angivna sökvägen:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Andra potentiella problem med Zebra-enheter

I det här avsnittet visas andra möjliga problem som kan uppstå vid användning av Zebra-enheter med enhetsadministratör. De här problemen rapporteras inte i StageNow-loggarna.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView är inaktuellt

När äldre enheter loggar in via företagsportalappen ser användarna kanske ett meddelande om att System WebView-komponenten är inaktuell och behöver uppgraderas. Om Google Play är installerat på enheten ansluter du det till Internet och söker efter uppdateringar. Om enheten inte har Google Play installerat hämtar du den uppdaterade versionen av komponenten och tillämpar den på enheterna. Eller så uppdaterar du till enhetens senaste operativsystem som utfärdats av Zebra.

### <a name="management-actions-take-a-long-time"></a>Hanteringsåtgärder tar lång tid

Om Google Play-tjänsterna inte är tillgängliga tar det upp till åtta timmar att slutföra vissa uppgifter. [Begränsningar i Intune-företagsportalappen för Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (öppnar en annan Microsoft-webbplats) kan vara en bra resurs.

### <a name="device-spoofing-suspected-shows-in-intune"></a>”Misstänkt enhetsförfalskning” visas i Intune

Det här felet innebär att Intune misstänker att en icke-Zebra Android-enhet rapporterar sin modell och tillverkare som en zebra-enhet.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>Företagsportalappen är äldre än den minsta version som krävs

Intune uppdaterar kanske den minsta versionen av företagsportalappen som krävs. Om Google Play inte är installerat på enheten kommer företagsportalappen inte att uppdateras automatiskt. Om den minsta version som krävs är nyare än den installerade versionen slutar företagsportalappen att fungera. Uppdatera till den senaste företagsportalappen med hjälp av [separat inläsning på Zebra-enheter](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Nästa steg

[Zebra-diskussionsforum](https://developer.zebra.com/community/home/discussions) (detta öppnar Zebra-webbplatsen)

[Använda och hantera Zebra-enheter med Zebra Mobility Extensions i Intune](android-zebra-mx-overview.md)