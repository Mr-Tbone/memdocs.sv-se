---
title: Hantera enheter med lokal MDM
titleSuffix: Configuration Manager
description: Skydda enhets data med fullständig rensning, selektiv rensning, fjärrlåsning eller lösen ords återställning genom att använda Configuration Manager lokal hantering av mobila enheter (MDM).
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721873"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Hantera enheter och skydda data med lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Mobila enheter kan lagra känsliga data och ger enkel åtkomst till många organisations resurser. Använd Configuration Manager för följande enhets hanterings åtgärder för att skydda enheter och data:

- **Fullständig rensning**: Återställ enheten till fabriks inställningarna

- **Selektiv rensning**: ta endast bort organisations data

- **Återställning av lösen ord**: ta bort eller Återställ lösen ordet när en användare glömmer bort det

- **Fjärrlåsning**: skydda en enhet som kan gå förlorad

## <a name="full-wipe"></a>Fullständig rensning  

När du behöver skydda en förlorad enhet eller när du drar tillbaka en enhet från aktiv användning kan du starta en fullständig rensning. Med den här åtgärden återställs enheten till fabriks inställningarna. Alla organisations-och användar data och inställningar tas bort.

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj den enhet som du vill rensa.

1. I menyfliksområdet, i gruppen enhet, väljer du **åtgärder för fjärrenheter**och väljer sedan **dra tillbaka/rensa**.

1. I fönstret **dra tillbaka från Configuration Manager** väljer du alternativet för att **rensa den mobila enheten och dra tillbaka den från Configuration Manager**.

## <a name="selective-wipe"></a>Selektiv rensning

Om du bara vill ta bort organisations data från en enhet startar du en selektiv rensning.

### <a name="behaviors-by-os-version"></a>Beteenden efter OS-version

I följande tabeller beskrivs vilka data som tas bort och vilken inverkan på data som finns kvar på enheten efter en selektiv rensning.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8,1, Windows RT 8,1 och Windows RT

|Innehåll|Beteende för selektiv rensning|  
|-------|--------|
|Appar och associerade data som installeras av Configuration Manager|Apparna avinstalleras och alla nycklar för separat inläsning tas bort. Den återkallar krypterings nyckeln för appar som använder Windows selektiv rensning och data är inte längre tillgängliga.|
|VPN- och Wi-Fi-profiler|Tar bort profiler|
|Certifikat|Tar bort och återkallar certifikaten|
|Inställningar|Tar bort krav|
|E-postprofiler|Tar bort e-post som är EFS-aktiverad, som innehåller e-postappen för e-post och bifogade filer i Windows.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8,0 och Windows Phone 8,1

|Innehåll|Beteende för selektiv rensning|  
|-------|--------|
|Företags program och associerade data som installeras av Configuration Manager|Appen avinstallerar apparna och tar bort organisationens AppData.|
|VPN- och Wi-Fi-profiler|Tar bort profiler för Windows 10 Mobile och Windows Phone 8,1|
|Certifikat|Tar bort certifikaten för Windows Phone 8,1|
|E-postprofiler|Tar bort profiler (utom Windows Phone 8,0)|

Följande inställningar tas också bort från Windows 10 Mobile-och Windows Phone 8,1-enheter:  

- **Kräv lösenord för att låsa upp mobila enheter**  
- **Tillåt enkla lösenord**  
- **Minsta längd på lösenord**  
- **Lösenordstyp krävs**
- **Lösenordets giltighetstid (i dagar)**  
- **Kom ihåg tidigare lösenord**  
- **Antal tillåtna, upprepade felinloggningar innan enheten rensas**  
- **Antal minuters inaktivitet innan lösenord krävs**  
- **Krävd lösenordstyp – minsta antal tecken**  
- **Tillåt kamera**
- **Filkryptering på mobil enhet**  
- **Tillåt flyttbara lagringsenheter**  
- **Tillåt webbläsare**  
- **Tillåt appbutik**  
- **Tillåt skärmbild**  
- **Tillåt geolokalisering**  
- **Tillåt Microsoft-konto**  
- **Tillåt kopiera och klistra in**  
- **Tillåt Wi-Fi -delning**  
- **Tillåt automatisk anslutning till kostnadsfria, trådlösa surfpunkter**  
- **Tillåt rapportering av trådlösa surfpunkter**  
- **Tillåt fabriksåterställning**
- **Tillåt Bluetooth**  
- **Tillåt NFC**
- **Tillåt Wi-Fi**

### <a name="start-a-selective-wipe"></a>Starta en selektiv rensning

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj den enhet som du vill rensa.

1. I menyfliksområdet, i gruppen enhet, väljer du **åtgärder för fjärrenheter**och väljer sedan **dra tillbaka/rensa**.

1. I fönstret **dra från Configuration Manager** väljer du följande alternativ: **Rensa företags innehåll och dra tillbaka den mobila enheten från Configuration Manager**.

### <a name="recommendations-for-selective-wipe"></a>Rekommendationer för selektiv rensning

- För en lyckad rensning av e-post kan du konfigurera e-postprofiler till Windows Phone 8,1-enheter.

- Om du har en lyckad rensning av appar, se till att apparna distribueras via hantering av mobila enhets appar.

## <a name="passcode-reset"></a>Återställning av lösenord

Om en användare glömmer sitt lösen ord använder du den här åtgärden för att tvinga ett nytt tillfälligt lösen ord på enheten. Du kan också ta bort lösen ordet helt och hållet. Följande tabell visar hur lösenordsåterställning fungerar på olika mobilplattformar.

| OS-version | Återställning av lösenord |
|------------|----------------|
| Windows 10 | Stöds inte |
| Windows 10 Mobile | Stöds, exklusive Azure Active Directory anslutna enheter |
| Windows Phone 8 och Windows Phone 8.1 | Stöds |
| Windows RT 8.1 | Stöds inte |
| Windows 8,1 | Stöds inte |

> [!Note]
> Starta åtgärden för lösen ords återställning från platsen på den översta nivån. Om du till exempel använder en central administrations plats kan du bara utföra åtgärden på den platsen. Om du använder en fristående primär plats kan du bara utföra åtgärden från den platsen.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Återställa lösen ordet på en mobil enhet via fjärr anslutning

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj de enheter du vill återställa lösenordet på.

1. I menyfliksområdet i gruppen enhet väljer du åtgärder för **fjärrenheter**och väljer sedan **Återställ lösen ord**.  

### <a name="show-the-state-of-the-passcode-reset"></a>Visa status för lösen ords återställning  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj de enheter vars återställningsstatus du vill visa.

1. I menyfliksområdet i gruppen enhet väljer du åtgärder för **fjärrenheter**och väljer sedan **Visa lösen ords tillstånd**.  

## <a name="remote-lock"></a>Fjärrlåsning

Om en användare förlorar sin enhet kan du låsa enheten via fjärr anslutning. Följande tabell visar hur fjärrlåsning fungerar på olika mobilplattformar.  

|OS-version|Fjärrlåsning|
|----------|-----------|
|Windows 10|Stöds inte|
|Windows Phone 8 och Windows Phone 8.1|Stöds|
|Windows RT 8.1|Stöds om den aktuella användaren av enheten är samma användare som registrerade enheten.|
|Windows 8,1|Stöds om den aktuella användaren av enheten är samma användare som registrerade enheten.|

> [!Note]
> Starta åtgärden fjärrlåsning från platsen på den översta nivån. Om du till exempel använder en central administrations plats kan du bara utföra åtgärden på den platsen. Om du använder en fristående primär plats ska du utföra åtgärden från den platsen.

### <a name="remotely-lock-a-mobile-device"></a>Fjärrlåsa en mobil enhet

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj de enheter du vill låsa.

1. Välj **fjär renhets åtgärder**i enhets gruppen i menyfliksområdet och välj sedan **fjärrlåsning**. Bekräfta åtgärden.

### <a name="show-the-state-of-the-remote-lock"></a>Visa status för fjärrlåsningen

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja **enhets samlingar** och välja en samling där enheten är medlem.

1. Välj de enheter vars fjärrlåsningsstatus du vill visa.

1. I menyfliksområdet i gruppen enhet väljer du åtgärder för **fjärrenheter**och väljer sedan **Visa tillstånd för fjärrlåsning**.
