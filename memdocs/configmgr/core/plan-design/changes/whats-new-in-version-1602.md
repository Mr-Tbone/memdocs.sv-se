---
title: Nytt i version 1602
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1602 av Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 334397cfa52c90694823107c2144bfbbcbd509ac
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993632"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>Vad&#39;s nya i version 1602 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Uppdatering 1602 för Configuration Manager är bara tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1511. Version 1511 är den första, bas linje version som du använder för att installera nya Configuration Manager-platser.  


> [!TIP]  
> Läs mer om:  
>   
> - [Installera nya platser](../../servers/deploy/install/prepare-to-install-sites.md) (med en bas linje version som 1511)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md) (t. ex. uppdatering 1602)  

 Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1602 av Configuration Manager.  

## <a name="site-infrastructure"></a>Plats infrastruktur  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a> Uppgradering på plats av operativ systemet för plats servrar som kör Windows Server 2008 R2  
 Configuration Manager-platser som kör version 1602 eller senare har stöd för uppgradering på plats av operativ systemet för plats servrar från Windows Server 2008 R2 till Windows Server 2012 R2.  

> [!WARNING]  
>  Innan du uppgraderar till Windows Server 2012 R2 måste du avinstallera WSUS 3.2 från servern.  
>   
>  Mer information om det här viktiga steget finns i avsnittet "nya och ändrade funktioner" i [Windows Server Update Services översikt](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

 Om du vill uppgradera en server använder du uppgraderings procedurerna för Windows Server 2012 R2. Du behöver inte köra en återställning av Configuration Manager plats Server efter uppgraderingen. Information om uppgraderingsprocesser finns i [Uppgraderingsalternativ för Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) i dokumentationen för Windows Server.  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> SQL Server AlwaysOn-tillgänglighetsgrupper  
 Använd SQL Server AlwaysOn-tillgänglighetsgrupper för att vara värd för plats databasen på primära platser och den centrala administrations platsen som en lösning för hög tillgänglighet och katastrof återställning.  

 Mer information finns i [SQL Server AlwaysOn för en plats databas med hög tillgänglighet för Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Distribution av operativsystem  

### <a name="windows-10-servicing"></a>Windows 10-underhåll  
 Följande förbättringar för service i Windows 10 har lagts till i Configuration Manager version 1602:  

-   Nya filter alternativ är tillgängliga för Service planer som gör att du kan filtrera efter **språk**, **obligatorisk**och **rubrik**. Det är enbart uppgraderingar som uppfyller de angivna kriterierna som läggs till i den associerade distributionen.  

-   När du väljer klassificeringen **uppgraderingar** för synkronisering av program uppdateringar visas en varning. Med den här varningen kan du se att [snabb korrigering 3095113](https://support.microsoft.com/kb/3095113) för Windows Server Update Services (WSUS) 4,0 krävs innan du kan synkronisera program uppdateringar och för att Windows 10-underhållet ska fungera korrekt. Från varnings meddelandet kan du gå till den associerade kunskaps bas artikeln.  

-   Tillgängliga Windows 10-uppgraderingar visas nu bara i noden **Windows 10**-  \  **uppdateringar för alla Windows 10-uppdateringar** i Configuration Manager-konsolen. De här uppdateringarna visas inte längre i noden **program**uppdateringar  \  **alla program uppdateringar** i-konsolen.  

-   En service plan anses vara en distribution med hög risk och i fönstret **Välj samling** visas endast de anpassade samlingar som uppfyller de verifierings inställningar för distribution som kon figurer ATS i platsens egenskaper. Mer information finns i [Inställningar för att hantera högrisk distributioner för Configuration Manager](../../servers/manage/settings-to-manage-high-risk-deployments.md).  

-   Användare som startar ett uppgraderings paket för Windows 10 får nu ett meddelande om att de kommer att uppgradera sitt operativ system.  

## <a name="application-management"></a>Programhantering  

### <a name="ios-app-configuration-policies"></a>Konfigurationsprinciper för iOS-appar  
 Använd Configuration Manager konfigurations principer för appar för att tillhandahålla inställningar som kan krävas när användaren kör en iOS-app. En app kan till exempel kräva att användaren anger ett anpassat port nummer, språk, säkerhets inställningar eller anpassnings inställningar (t. ex. en företags logo typ). Om de här inställningarna har angetts felaktigt kan detta öka belastningen på supportavdelningen och även sakta in nya appar.  

 Med konfigurations principer för appar kan du undvika dessa problem genom att låta dig distribuera de här inställningarna till användare i en princip innan de kör appen. Inställningarna anges sedan automatiskt och användaren behöver inte vidta några åtgärder.

### <a name="manage-volume-purchased-ios-apps"></a>Hantera iOS-appar som köpts i volym  
 Configuration Manager kan hjälpa dig att distribuera och hantera appar som du har köpt i volym från Apples volym köps program (VPP). Configuration Manager importerar licens informationen från App Store och spårar hur många av de licenser som du har använt.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Automatisk generering av Office-mobilappar  
 När du uppdaterar till version 1602 från 1511 skapar Configuration Manager automatiskt följande Microsoft Office mobilappar för Android och iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (endast iOS)  

-   Microsoft Outlook  

De här apparna finns i noden **program** i Configuration Manager-konsolen.  

 Mer information om hur du distribuerar program finns i [distribuera program med Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Programuppdateringar  

### <a name="manage-microsoft-365-client-updates"></a>Hantera Microsoft 365 klient uppdateringar  
 Configuration Manager kan hantera Microsoft 365 klient uppdateringar med hjälp av arbets flödet för program uppdaterings hantering. Mer information finns i [Hantera uppdateringar för Office 365-appar med Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).  

## <a name="compliance-settings"></a>Kompatibilitetsinställningar  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Kompatibilitetsinställningar för enheter som kör Windows 10 team  
 Nya inställningar har lagts till i konfigurationsobjektet **windows 8,1 och Windows 10** . De här inställningarna hjälper dig att styra enheter som kör Windows 10 team, till exempel en Surface Hub enhet.  

 Mer information finns i [så här skapar du konfigurations objekt för windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Inställningar för hel skärms läge för Android Samsung KNOX Standard-enheter  
 Med hel skärms läget kan du låsa en enhet så att bara vissa funktioner fungerar. Du kan t.ex. tillåta att enheten ska kunna köra endast en hanterad app som du anger, eller så kan du inaktivera volymknapparna på en enhet. De här inställningarna kan användas på en demonstrationsmodell av en enhet, eller en enhet som bara används för att utföra en enda funktion, till exempel i en butikskassa. I Configuration Manager kan du nu ange inställningar för hel skärms läge för Samsung KNOX Standard-enheter.  


## <a name="conditional-access"></a>Villkorsstyrd åtkomst  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Villkorlig åtkomst för datorer som hanteras av Configuration Manager  
 Före den här versionen, för att konfigurera villkorlig åtkomst för en dator, måste datorn antingen vara registrerad i Intune eller vara en domänansluten dator. Från och med 1602-uppdateringen stöds villkorlig åtkomst för datorer som hanteras av Configuration Manager. För datorer som hanteras av Configuration Manager kan du begränsa åtkomsten till Exchange Online och SharePoint Online enbart till enheter som är kompatibla med de efterlevnadsprinciper som du har angett.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Begränsa åtkomst baserat på enheternas hälsa  
 Du kan nu begränsa åtkomsten till e-post och Microsoft 365 tjänster baserat på enhetens hälso tillstånd, enligt rapporter från tjänsten hälsoattestering. Enheter som hanteras av Intune ingår dessutom i enhetens hälso rapporter.  

 Configuration Manager-konsolen innehåller en ny efterlevnadsprincip som gör att du kan ange om enheterna ska tillåtas eller blockeras för att få åtkomst baserat på deras hälso status. Information om tjänsten hälsoattestering och hur hälsan för enheter rapporteras i Intune finns i [hälsoattestering för Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nya regler för efterlevnadsprinciper  
 Nya regler för efterlevnadsprinciper, som automatiska uppdateringar och kräver lösen ord för att låsa upp enheter, har lagts till för att stödja bättre säkerhets krav.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Se till att registrerade och kompatibla enheter alltid har åtkomst till Exchange On-premises  
 När du markerar följande alternativ tillåts enheter som är registrerade i Intune och som är kompatibla med efterlevnadsprinciper åtkomst till Exchange On-premises: **Åsidosätt standard regel – Tillåt alltid att Intune-registrerade och kompatibla enheter får åtkomst till Exchange lokalt:**. Den här regeln finns på  **sidan Allmänt** i **guiden Konfigurera princip för villkorlig åtkomst** för Exchange lokalt.

 Den här regeln åsidosätter standard regeln, vilket innebär att även om du ställer in standard regeln för karantän eller blockera åtkomst, kommer registrerade och kompatibla enheter fortfarande att kunna komma åt Exchange lokalt. Använd den här inställningen när du vill att registrerade och kompatibla enheter alltid ska ha åtkomst till e-post via Exchange lokalt.   

 Detaljerad genom gång finns i [Hantera e-poståtkomst](../../../mdm/understand/what-happened-to-hybrid.md).  

## <a name="client-management"></a>Klienthantering  

### <a name="client-online-status"></a>Klientens onlinestatus  
 En ny status för klienter är tillgänglig för övervakning om en dator är online eller inte. En dator anses vara online om den är ansluten till den tilldelade hanterings platsen. För att indikera att datorn är online skickar klienten ping-liknande meddelanden till hanterings platsen. Om hanterings platsen inte får ett meddelande efter 5 minuter anses klienten vara offline.  

 Mer information finns i [övervaka klienter](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Uppdatera dator-och användar princip från Software Center  
 Ett nytt alternativ, **Sync-princip**, har lagts till på sidan **alternativ**  >  **dator underhåll** i Software Center som gör att datorn uppdaterar sin Configuration Manager dator och användar princip.  

### <a name="software-center-branding-changes"></a>Ändringar i Software Center-anpassning  
 Du kan ändra färg, organisations namn och ikon som visas i Software Center. De här inställningarna tillämpas enligt följande regler:  

- Om plats Server rollen Programkatalog webbplats plats inte är installerad visar Software Center det organisations namn som anges i klient inställningen för **dator agent** som heter **organisations namn som visas i Software Center**.  

- Om plats Server rollen Programkatalog webbplats plats är installerad visar Software Center det organisations namn och den färg som anges i egenskaperna för plats Server rollen Programkatalog för webbplats platser.  

- Om en Microsoft Intune-prenumeration har kon figurer ATS och är ansluten till Configuration Managers miljön visar Software Center organisationens namn, färg och företags logo typ som anges i prenumerations egenskaperna för Intune.  

### <a name="health-attestation"></a>Hälsoattestering  
 Administratörer kan visa statusen för hälsoattesteringen av Windows 10-enheten i Configuration Manager-konsolen. Detta är tillgängligt för Configuration Manager, samt Configuration Manager med Microsoft Intune. Med hälsoattestering för enheten kan administratörer se till att klientdatorer har följande tillförlitliga konfigurationer av BIOS, TPM och startprogram aktiverade:  

-   Tidig lansering av program mot skadlig kod  

-   BitLocker  

-   Säker start  

-   Kodintegritet  

Mer information finns i [hälsoattestering för Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Förbättringar av Endpoint Protection inställningar för program mot skadlig kod  
 1602 lägger till följande nya inställningar i Endpoint Protection princip för program mot skadlig kod för Windows Defender:  

-   Real tids skydd: blockera potentiellt oönskade program vid nedladdning innan installationen.  

-   Genomsöknings inställningar: Genomsök mappade nätverks enheter under en fullständig genomsökning.  

-   Inställningar för automatisk sändning av exempel fil:  

     Motorn för program mot skadlig kod kan begära att fil exempel skickas till Microsoft för ytterligare analys. Som standard får du alltid en fråga innan sådana exempelfiler skickas. Administratörer kan nu hantera följande inställningar för att konfigurera den här funktionen:  

    -   Avancerat: Aktivera automatisk sändning av exempel fil för att hjälpa Microsoft att fastställa om vissa hittade objekt är skadliga.  

    -   Avancerat: Tillåt användare att ändra inställningar för automatisk sändning av exempel fil.  

    I avsnittet "undantags inställningar" i Endpoint Protection-principen för program mot skadlig kod kan dessutom den befintliga inställningen **undanta filer och mappar** nu tillåta enhets undantag.  

Mer information finns i [skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Hantering av mobila enheter  

### <a name="ios-activation-lock"></a>iOS-Aktiveringslås  
 Configuration Manager kan hjälpa dig att hantera iOS Aktiveringslås, en funktion i Hitta min iPhone-appen för enheter med iOS 7,1 och senare. Aktiveringslås aktiveras automatiskt när Hitta Min iPhone appen används på en enhet. När den har aktiverats måste användarens Apple-ID och lösenord anges innan någon kan:  

-   Inaktivera Hitta min iPhone.  

-   Radera enheten.  

-   Återaktivera enheten.  

Configuration Manager kan begära Aktiveringslås status för både övervakade och oövervakade enheter som kör iOS 7,1 och senare. För övervakade enheter kan Configuration Manager hämta koden för att kringgå Aktiveringslås och skicka den direkt till enheten.  

### <a name="monitor-terms-and-conditions-deployments"></a>Övervaka distributioner av allmänna villkor  
 Du kan övervaka distributioner av allmänna villkor i Configuration Manager-konsolen.  

 Välj distributionen av allmänna villkor i listan över distributioner. I sammanfattnings delen visas följande statistik:  

-   **Kompatibel**: användarna har godkänt den senaste versionen av de allmänna villkoren.  

-   **Fel**  

-   **Inkompatibel**: användare har godkänt en version av de allmänna villkoren, men inte den senaste versionen.  

-   **Okänd**: användare har aldrig godkänt villkoren, inklusive de som saknar en registrerad enhet.