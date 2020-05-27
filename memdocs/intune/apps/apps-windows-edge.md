---
title: Lägga till Microsoft Edge för Windows 10 till Microsoft Intune
titleSuffix: ''
description: Lär dig hur du lägger till Microsoft Edge för Windows till Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71b6468975012f41b0c34bbfbe5921bc8a60cb57
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985803"
---
# <a name="add-microsoft-edge-for-windows-10-to-microsoft-intune"></a>Lägga till Microsoft Edge för Windows 10 till Microsoft Intune

Innan du kan distribuera, konfigurera, övervaka eller skydda appar måste du lägga till dem till Intune. En av de tillgängliga [apptyperna](apps-add.md#app-types-in-microsoft-intune) är Microsoft Edge *version 77 och senare*. Genom att välja den här apptypen i Intune kan du tilldela och installera Microsoft Edge *version 77 och senare* till enheter som du hanterar och som kör Windows 10.

> [!IMPORTANT]
> Den här typen av app erbjuder en stabil kanal, betakanal och utvecklarkanal för Windows 10. Distributionen är bara på engelska (EN), men slutanvändarna kan ändra visningsspråket i webbläsaren under **Inställningar** > **Språk**. Microsoft Edge är en Win32-app som installeras i systemkontext och på samma arkitektur (x86-appen i x86-operativsystem och x64-appen i x64-operativsystem). Intune identifierar alla befintliga Microsoft Edge-installationer. Om installationen görs i användarkontexten skrivs den över av en systeminstallation. Om installationen görs i systemkontexten rapporteras installationen som lyckad. Dessutom är automatiska uppdateringar av Microsoft Edge **På** som standard.

> [!NOTE]
> Microsoft Edge *version 77 och senare* är även tillgängligt för macOS.
>
> Du kan inte använda den inbyggda programdistributionen för Microsoft Edge för Workplace Join-datorer. Inbyggd programdistribution kräver Intune-hanteringstillägget, som endast finns för AAD-anslutna enheter. Du kan fortfarande distribuera Microsoft Edge *version 77 och senare* med hjälp av en *.msi* som laddats upp till **Appar**. Mer information finns i [Lägga till en verksamhetsspecifik Windows-app till Microsoft Intune](lob-apps-windows.md).

## <a name="prerequisites"></a>Krav

- Windows 10 version 1709 eller senare.
- En Edge-installation i systemkontexten skriver över förinstallerade versioner av Microsoft Edge *version 77 och senare* för alla kanaler som gjorts i användarkontexten.

## <a name="configure-the-app-in-intune"></a>Konfigurera appen i Intune

Du kan lägga till en Microsoft Edge version 77 och senare till Intune med hjälp av följande steg:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Alla appar** > **Lägg till**.
3. I listan **Apptyp**, under **Microsoft Edge, version 77 och senare**, väljer du **Windows 10**.

## <a name="configure-app-information"></a>Konfigurera appinformation

I det här steget anger du information om den här appdistributionen. Den här informationen hjälper dig att identifiera appen i Intune och hjälper användarna att hitta appen i företagsportalen.

1. Visa fönstret **Appinformation** genom att klicka på **Appinformation**.
2. Ange information om den här appdistributionen i fönstret **Appinformation**. Den här informationen hjälper dig att identifiera appen i Intune och hjälper användarna att hitta appen i företagsportalen.
    - **Namn**: Ange namnet på appen så som det ska visas i företagsportalen. Kontrollera att alla namn är unika. Om samma appnamn förekommer två gånger visas endast en av apparna för användarna på företagsportalen.
    - **Beskrivning**: Ange en beskrivning för appen. Du kan till exempel ange målanvändarna i beskrivningen.
    - **Utgivare**: Microsoft visas som utgivare.
    - **Kategori**: Välj en eller flera av de inbyggda appkategorierna, eller en kategori som du har skapat. Inställningen gör det enklare för användarna att hitta appen när de söker på företagsportalen.
    - **Visa denna som en aktuell app i företagsportalen**: Välj det här alternativet för att tydligt visa appen på företagsportalens huvudsida när användarna söker efter appar.
    - **Webbadress till information**: Du kan välja att ange en webbadress till en webbplats som innehåller information om den här appen. Webbadressen visas för användarna på företagsportalen.
    - **Sekretesswebbadress**: Du kan välja att ange en webbadress till en webbplats som innehåller sekretessinformation för den här appen. Webbadressen visas för användarna på företagsportalen.
    - **Utvecklare**: Microsoft visas som utvecklare.
    - **Ägare**: Microsoft visas som ägare.
    - **Kommentarer**: Alternativt kanske du vill ange kommentarer till appen.
3. Välj **OK**.

## <a name="configure-app-settings"></a>Konfigurera appinställningar
I det här steget konfigurerar du installationsalternativ för appen.

1. Välj **Appinställningar** i fönstret **Lägg till app**.
2. Bestäm vilken Edge-kanal du ska distribuera appen från genom att gå till fönstret **Appinställningar** och välja **Stabil**, **Beta** eller **Dev** i listan **Kanal**.
    - Kanalen **Stabil** är den rekommenderade kanalen för bredare distributioner i företagsmiljöer. Den uppdateras var sjätte vecka, och varje utgåva innehåller förbättringar från betakanalen.
    - Kanalen **Beta** är den mest stabila Microsoft Edge-förhandsupplevelsen och det bästa valet för en fullständig pilotlansering i din organisation. Större uppdateringar sker var sjätte vecka, och i varje ny version ingår lärdomar och förbättringar från Dev-kanalen.
    - **Dev**-kanalen är redo för företagsfeedback för Windows, Windows Server och macOS. Den uppdateras varje vecka och innehåller de senaste förbättringarna och korrigeringarna.

    > [!NOTE]
    > Microsoft Edge-webbläsarens logotyp visas med appen när användare söker på företagsportalen.

3.    Välj **OK**.

## <a name="select-scope-tags-optional"></a>Välj omfångstaggar (valfritt)
Du kan använda omfångstaggar för att bestämma vem som kan se klientappsinformation i Intune. Fullständig information om omfångstaggar finns i Använda RBAC och omfångstaggar för distribuerad IT.
1.    Välj **Omfång (taggar)**  > **Lägg till**.
2.    Använd rutan **Välj** för att söka efter omfångstaggar.
3.    Markera kryssrutan bredvid de omfångstaggar som du vill tilldela till den här appen.
4.    Klicka på **Välj** > **OK**.

## <a name="add-the-app"></a>Lägg till appen
När du har slutfört konfigurationen av appen väljer du **Lägg till** i fönstret **Lägg till en app**. 

Appen som du har skapat visas i applistan där du kan tilldela den till de grupper du väljer. 

> [!NOTE]
> För närvarande gäller att om du tar bort tilldelningen av Microsoft Edge-distributionen så blir den kvar på enheten.

## <a name="uninstall-the-app"></a>Avinstallera appen

Använd följande steg när du behöver avinstallera Microsoft Edge från användarnas enheter.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Alla appar** > *Microsoft Edge* app > **Tilldelningar** > **Lägg till grupp**.
3. I fönstret **Lägg till grupp** väljer du **Avinstallera**.

    > [!NOTE]
    > Appen avinstalleras från enheter i de valda grupperna om Intune tidigare har installerat programmet på enheten via tilldelningen **Tillgänglig för registrerade enheter** eller **Obligatorisk** med hjälp av samma distribution.
4. Välj **Inkluderade grupper** för att välja vilka grupper av användare som ska påverkas av apptilldelningen.
5. Välj de grupper som du vill tillämpa avinstallationen på.
6. Klicka på **Välj** i fönstret **Välj grupper**.
7. Klicka på **OK** i fönstret **Tilldela** för att ange tilldelningen.
8. Välj **Exkludera grupper** om du vill undanta grupper av användare så att de inte påverkas av den här apptilldelningen.
9. Om du har valt att undanta grupper i **Välj grupper**, klicka på **Välj**.
10. Välj **OK** i fönstret **Lägg till grupp**.
11. Välj **Spara** i appfönstret **Tilldelningar**.

> [!IMPORTANT]
> Om du vill avinstallera appen måste du ta bort medlemmarna eller grupptilldelningen för installationen innan du tilldelar en avinstallation. Om en grupp är tilldelad att både installera en app och avinstallera en app, förblir appen kvar och tas inte bort.

## <a name="troubleshooting"></a>Felsökning
**Microsoft Edge version 77 och senare för Windows 10:**<br>
Intune använder Intune-hanteringstillägget för att ladda ned och distribuera Microsoft Edge-installationsprogrammet till tilldelade Windows 10-enheter. Därefter kommunicerar det distributionsinställningarna till Microsoft Edge-installationsprogrammet, som laddar ned och installerar webbläsaren Microsoft Edge direkt från CDN. Läs [kraven för Intune-hanteringstillägget](intune-management-extension.md#prerequisites) och den bästa praxis som beskrivs i åtkomsten till Azure Update Service och CDN för att säkerställa att din nätverkskonfiguration tillåter att Windows 10-enheter kommer åt dessa platser. För att kunna ge åtkomst till installationsfiler från ett CDN för att installera webbläsaren, måste du dessutom tillåta åtkomst till Windows Updates slutpunkter. Mer information finns i [Hantera anslutningsslutpunkter för Windows 10, version 1809 – Windows Update](https://docs.microsoft.com/windows/privacy/manage-windows-1809-endpoints#windows-update) och [Nätverksslutpunkter för Microsoft Intune](../fundamentals/intune-endpoints.md).

## <a name="next-steps"></a>Nästa steg
- [Tilldela appar till grupper](apps-deploy.md)
