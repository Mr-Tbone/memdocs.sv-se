---
title: Registrera enheter i Skriv bords analys
titleSuffix: Configuration Manager
description: Lär dig hur du registrerar enheter i Skriv bords analys.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 22b5461df3a560449316009471ea029967118f5d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864917"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Registrera enheter i Skriv bords analys

När du [ansluter Configuration Manager](connect-configmgr.md) till Skriv bords analys konfigurerar du inställningar för registrering av enheter till Skriv bords analys. Du kan ändra inställningarna när du vill. Kontrol lera också att enheterna är uppdaterade.

## <a name="update-devices"></a>Uppdatera enheter

Desktop Analytics använder två huvudsakliga Windows-komponenter:

- **Kompatibilitetsrapport**: komponenten Compatibility Component (**bedömare**) Kör diagnostik på Windows-enheten för att utvärdera dess kompatibilitetsstatus med de senaste versionerna av Windows 10.

- **Tjänsten för anslutna användar upplevelser och telemetri**: när Windows-diagnostikdata är aktiverat samlar**DiagTrack**(Connected User Experience and telemetri service) system-, program-och driv rutins data. Microsoft analyserar dessa data och delar tillbaka dem till dig via Skriv bords analys.

Installera den senaste versionen av dessa komponenter för att få bästa möjliga upplevelse med Desktop Analytics.

I följande tabell visas uppdateringarna för varje komponent i operativ system versioner som stöds:

| OS-version | Bedömning | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | <sup> [Anmärkning 1](#bkmk_note1) ingår</sup> | [Senaste kumulativa uppdateringen](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | <sup> [Anmärkning 1](#bkmk_note1) ingår</sup> | [Senaste kumulativa uppdateringen](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | <sup> [Anmärkning 1](#bkmk_note1) ingår</sup> | [Senaste kumulativa uppdateringen](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | <sup> [Anmärkning 1](#bkmk_note1) ingår</sup> | [Senaste kumulativa uppdateringen](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | <sup> [Anmärkning 1](#bkmk_note1) ingår</sup> | [Senaste kumulativa uppdateringen](https://support.microsoft.com/help/4043454) |
| Windows 8,1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup> [Anmärkning 2](#bkmk_note2)</sup> | [Senaste månatliga sammanställning](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup> [Anmärkning 3](#bkmk_note3)</sup> | [Senaste månatliga sammanställning](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Använd Configuration Manager för att automatiskt installera dessa uppdateringar. Mer information finns i [distribuera program uppdateringar](../sum/deploy-use/deploy-software-updates.md).
>
> Starta om enheter när du har installerat kompatibilitetsinställningarna för första gången.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a>Anmärkning 1: Windows 10

Även om Windows 10 innehåller dessa komponenter som standard kräver Windows 10-enheter den senaste kumulativa uppdateringen för att få alla funktioner i Skriv bords analys som att utvärdera enheten för kompatibilitet mot den senaste versionen av operativ systemet.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a>Anmärkning 2: Windows 8,1

Microsoft ökar regelbundet uppdateringarna för den här komponenten, men det tillhör ande KB-numret ändras inte. Kontrol lera att du alltid har den senaste versionen av uppdateringen.

Den här komponenten kör diagnostik på Windows 8,1-system som ingår i Windows-Customer Experience Improvement Program. Den här diagnostiken hjälper till att avgöra om det kan uppstå kompatibilitetsproblem vid uppgradering till Windows 10.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a>Anmärkning 3: Windows 7

Om din organisation inte använder uppdaterings uppdateringar av månads kvalitet på Windows 7-enheter, och endast använder "endast säkerhets uppdateringar", hittar du några "endast säkerhets uppdateringar" i [listan över uppdateringar som ersätter KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). Du kan installera dessa nyare uppdateringar i stället för i KB 2952664.

> [!NOTE]
> För Windows 8,1 ändrar Microsoft bara KB 2976978 som en del av uppdaterings uppdateringar för månads kvalitet.

## <a name="device-enrollment"></a>Enhetsregistrering

Skriv bords analys tjänsten har inga agenter att installera. Enhets registreringen kräver att du konfigurerar inställningar på de enheter som du vill övervaka. Dessa inställningar styr vilken Desktop Analytics-instans enheten ska skicka data till och andra konfigurations alternativ.

> [!Note]  
> Om du tidigare använde Windows Analytics använder du samma arbets yta för Skriv bords analys. Du måste registrera om enheter till Skriv bords analys som du tidigare har registrerat i Windows Analytics.
>
> Du kan bara ha en Desktop Analytics-arbetsyta per Azure AD-klient. Enheter kan bara skicka diagnostikdata till en arbets yta.  

Configuration Manager ger en integrerad upplevelse för att hantera och distribuera dessa inställningar till klienter. Använd Configuration Manager för bästa möjliga upplevelse.

När du ansluter Configuration Manager till Skriv bords analys konfigurerar du inställningarna för att registrera enheter. Mer information finns i [så här ansluter du Configuration Manager med Desktop Analytics](connect-configmgr.md#bkmk_connect).

Använd följande procedur om du vill ändra inställningarna:

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Välj anslutningen till Skriv bords analys och välj **Egenskaper** i menyfliksområdet.

2. På sidan **diagnostikdata** gör du nödvändiga ändringar i följande inställningar:  

    - **Kommersiellt ID**: det här värdet ska automatiskt fyllas i med organisationens ID. Om den inte gör det kontrollerar du att proxyservern har kon figurer ATS för att tillåta alla nödvändiga [slut punkter](enable-data-sharing.md#endpoints) innan du fortsätter. Du kan också hämta ditt kommersiella ID manuellt från [Skriv bords analys portalen](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Windows 10-diagnostisk data nivå**: Mer information finns i [nivåer för diagnostikdata](enable-data-sharing.md#diagnostic-data-levels).  

    - **Tillåt enhets namn i diagnostikdata**: Mer information finns i [enhets namn](#device-name).  

    När du gör ändringar på den här sidan, visar sidan **tillgängliga funktioner** en förhands granskning av funktionerna för Skriv bords analys med de valda inställningarna för diagnostikdata.  

3. På sidan **anslutning till Skriv bords analys** gör du nödvändiga ändringar i följande inställningar:

    - **Visnings namn**: Skriv bords analys portalen visar den här Configuration Manager anslutningen med det här namnet.  

    - **Mål samling**: den här samlingen innehåller alla enheter som Configuration Manager konfigurerar med inställningarna för ditt handels-ID och diagnostikdata. Det är en fullständig uppsättning enheter som Configuration Manager ansluter till Skriv bords analys tjänsten.  

    - **Enheter i mål samlingen använder en användar autentiserad proxy för utgående kommunikation**: som standard är det här värdet **Nej**. Ange till **Ja**om det behövs i din miljö. Mer information finns i [Proxy Server-autentisering](enable-data-sharing.md#proxy-server-authentication).

    - **Välj specifika samlingar som ska synkroniseras med Desktop Analytics**: Välj **Lägg till** om du vill inkludera ytterligare samlingar från **mål samlingens** hierarki. Dessa samlingar är tillgängliga i Skriv bords analys portalen för gruppering med distributions planer. Se till att inkludera samlingar av pilot-och pilot undantags samlingar.  <!-- 4097528 -->

        > [!IMPORTANT]
        > De här samlingarna fortsätter att synkroniseras när deras medlemskap ändras. Din distributions plan använder till exempel en samling med en regel för Windows 7-medlemskap. När enheterna uppgraderar till Windows 10 och Configuration Manager utvärderar samlings medlemskapet, släpps dessa enheter ut ur samlingen och distributions planen.

### <a name="windows-settings"></a>Windows-inställningar

När Configuration Manager registrerar enheter i Desktop Analytics, ställer den in Windows-principer för att konfigurera enheten för Skriv bords analys. I de flesta fall använder du endast Configuration Manager för att konfigurera de här inställningarna. Använd inte heller de här inställningarna i domänens grup princip objekt.

Mer information finns i [grup princip inställningar för Desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Enhetsnamn

Från och med Windows 10, version 1803, samlas enhets namnet inte längre in som standard. Att samla in enhets namnet med diagnostikdata kräver ett separat deltagande. Utan enhets namnet är det svårare för dig att identifiera vilka enheter som kräver uppmärksamhet vid utvärdering av en uppgradering till en ny version av Windows.

Om du inte skickar enhets namnet visas det i Skriv bords analys som "okänt":

![Enhets lista för Skriv bords analys med "okända" namn](media/unknown-device-name.png)

Det finns ett alternativ i Configuration Manager inställningarna för Skriv bords analys för att konfigurera det här alternativet: **Tillåt enhets namn i diagnostikdata**. Configuration Manager den här inställningen styr [inställningen för Windows-principen](group-policy-settings.md) **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Konfliktlösning

I allmänhet använder du Configuration Manager samlingar för att ange inställningar för Skriv bords analys och registrering. Använd direkt medlemskap eller frågor för att ta med eller undanta enheter från samlingen. Mer information finns i [så här skapar du samlingar](../core/clients/manage/collections/create-collections.md).

Configuration Manager konfigurerar bara Windows-inställningarna om ett värde inte redan finns. Om du behöver konfigurera olika inställningar för en unik enhets grupp kan du använda [grup princip](group-policy-settings.md). Inställningar som riktas mot grup princip har företräde framför Configuration Manager inställningar. Enheter som omfattas av grup principen kanske inte korrekt reflekterar status på instrument panelen för [anslutnings hälsa](monitor-connection-health.md) .

När du konfigurerar den diagnostiska data nivån ställer du in den övre gräns värdet för enheten. Som standard i Windows 10, version 1803 och senare kan användare välja att ange en lägre nivå. Du kan styra det här beteendet med hjälp av grup princip inställningen **Konfigurera telemetri välja användar gränssnitt**. Mer information finns i [grup princip inställningar för Desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Proxyinställningar

Om din organisation använder autentisering av proxyserver för Internet åtkomst, måste du konfigurera den korrekt eller enheterna. Mer information finns i [Proxy Server-autentisering](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Nästa steg

Fortsätt till nästa artikel för att skapa distributions planer i Desktop Analytics.
> [!div class="nextstepaction"]
> [Skapa distributionsplaner](create-deployment-plans.md)
