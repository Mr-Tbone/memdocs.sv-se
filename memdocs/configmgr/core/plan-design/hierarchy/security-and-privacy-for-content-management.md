---
title: Säkerhet och sekretess för innehålls hantering
titleSuffix: Configuration Manager
description: Optimera säkerhet och sekretess för innehålls hantering i Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720858"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Säkerhet och sekretess för innehålls hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller information om säkerhet och sekretess för innehålls hantering i Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a>Rekommenderade säkerhets metoder för innehålls hantering  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Fördelar och nack delar med HTTPS eller HTTP för intranät distributions platser
För distributions platser i intranätet bör du ta hänsyn till fördelarna och nack delarna med att använda HTTPS och HTTP. I de flesta fall ger HTTP och paket åtkomst konton för auktorisering mer säkerhet än att använda HTTPS med kryptering, men utan auktorisering. Om du dock har känsliga data i ditt innehåll som du vill kryptera under överföringen, använd HTTPS.  

-   **När du använder HTTPS för en distributions plats**använder Configuration Manager inte paket åtkomst konton för att godkänna åtkomst till innehållet, men innehållet krypteras när det överförs i nätverket.  

-   **När du använder http för en distributions plats**kan du använda paket åtkomst konton för auktorisering, men innehållet är inte krypterat när det överförs i nätverket.  

Från och med version 1806 bör du överväga att aktivera **utökad http** för webbplatsen. Med den här funktionen kan klienter använda Azure Active Directory autentisering för att kommunicera säkert med en HTTP-distributions plats. Mer information finns i [Enhanced http](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Skydda certifikat filen för klientautentisering
Om du använder ett PKI-klientautentiseringscertifikat istället för ett självsignerat certifikat för distributionsplatsen, skydda certifikatfilen (.pfx) med ett starkt lösenord. Om du sparar filen i nätverket skyddar du nätverks kanalen när du importerar filen till Configuration Manager.

När du kräver ett lösen ord för att importera certifikatet för klientautentisering som distributions platsen använder för att kommunicera med hanterings platser bidrar den här konfigurationen till att skydda certifikatet från en angripare. Använd SMB-signering (Server Message Block) eller IPsec mellan nätverks platsen och plats servern för att hindra en angripare från att manipulera certifikat filen.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Ta bort distributions plats rollen från plats servern
Som standard installerar Configuration Manager installations programmet en distributions plats på plats servern. Klienterna behöver inte kommunicera direkt med plats servern. Om du vill minska angrepps ytan tilldelar du distributions plats rollen till andra plats system och tar bort den från plats servern.  

#### <a name="secure-content-at-the-package-access-level"></a>Säkert innehåll på paket åtkomst nivå
Distributions plats resursen ger Läs behörighet till alla användare. För att begränsa vilka användare som har tillgång till innehållet kan du använda paketåtkomstkonton när distributionsplatsen konfigureras för HTTP. Den här konfigurationen gäller inte för moln distributions platser, som inte stöder paket åtkomst konton. Mer information finns i [paket åtkomst konton](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Konfigurera IIS på distributions plats rollen
Om Configuration Manager installerar IIS när du lägger till en plats system roll för en distributions plats, tar du bort HTTP-omdirigering eller IIS-hanterings skript och-verktyg när distributions plats installationen är klar. Distributions platsen kräver inte HTTP-omdirigering eller IIS-hanterings skript och-verktyg. Ta bort de här roll tjänsterna för webb Server rollen för att minska angrepps ytan.  Mer information om roll tjänsterna för webb Server rollen för distributions platser finns i krav för [plats och plats system](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Ange paket åtkomst behörighet när du skapar paketet
Eftersom ändringar av åtkomst kontona på paketfilerna endast blir effektiva när du omfördelar paketet, ställer du in paket åtkomst behörigheten noggrant när du först skapar paketet. Den här konfigurationen är viktig när paketet är stort eller distribuerat till många distributions platser och när nätverks bandbredds kapaciteten för innehålls distribution är begränsad.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementera åtkomst kontroller för att skydda media som innehåller förinstallerat innehåll
Förinstallerat innehåll komprimeras men krypteras inte. En angripare kan läsa och ändra filerna som hämtas till enheter. Configuration Manager klienter avvisar innehåll som har manipulerats, men som fortfarande laddar ned det.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importera förinstallerat innehåll med ExtractContent
Importera endast förinstallerat innehåll med hjälp av kommando rads verktyget ExtractContent. exe. Använd endast det auktoriserade kommando rads verktyget som medföljer Configuration Manager för att undvika manipulering och behörighets höjning.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Skydda kommunikations kanalen mellan plats servern och paketets käll plats
Använd IPsec-eller SMB-signering mellan plats servern och paketets käll plats när du skapar program och paket. Den här konfigurationen hjälper till att hindra en angripare från att manipulera källfilerna.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Ta bort standard virtuella kataloger för anpassad webbplats med distributions plats rollen
Om du ändrar plats konfigurations alternativet till att använda en anpassad webbplats istället för standard webbplatsen efter att du har installerat en distributions plats roll, tar du bort de virtuella standard katalogerna. När du växlar från standard webbplatsen till en anpassad webbplats tar Configuration Manager inte bort de gamla virtuella katalogerna. Ta bort följande virtuella kataloger som Configuration Manager ursprungligen skapade under standard webbplatsen:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Skydda dina prenumerations uppgifter och certifikat för Azure för moln distributions platser
När du använder moln distributions platser skyddar du följande höga värde objekt:
- Användar namnet och lösen ordet för din Azure-prenumeration
- Hanterings certifikatet för Azure 
- Moln distributions platsens tjänst certifikat

Lagra certifikaten på ett säkert sätt. Om du bläddrar till dem via nätverket när du konfigurerar distributions platsen för molnet ska du använda IPsec eller SMB-signering mellan plats system servern och käll platsen.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Övervaka förfallo datum för moln distributions platsens certifikat för tjänste kontinuitet
Configuration Manager varnar dig inte när de importerade certifikaten för moln distributions platsen håller på att gå ut. Övervaka förfallo datumen oberoende av Configuration Manager. Se till att du förnyar och sedan importerar de nya certifikaten innan förfallo datumet. Den här åtgärden är viktig om du skaffar ett certifikat för serverautentisering från en extern, offentlig Provider, eftersom du kan behöva ytterligare tid för att skaffa ett förnyat certifikat.  

 Om något av certifikaten går ut genererar Cloud Services Manager status meddelandet ID **9425**. Filen CloudMgr. log innehåller en post som indikerar att certifikatet **har gått ut**, med förfallo datumet även inloggat UTC.  



## <a name="security-considerations-for-content-management"></a>Säkerhetsöverväganden för innehållshantering  

Tänk på följande när du planerar för innehålls hantering:  

-   Klienterna validerar inte innehåll förrän efter att det har laddats ned.  

     Configuration Manager-klienter validerar hashen enbart på innehållet när den har laddats ned till klientens cacheminne. Om en angripare manipulerar listan med filer som ska laddas ned eller med själva innehållet, kan nedladdnings processen ta upp avsevärd nätverks bandbredd, bara för klienten att ignorera innehållet när den påträffar Ogiltig hash.  

-   När du använder moln distributions platser begränsas åtkomsten till innehållet automatiskt till ditt företag. Du kan inte begränsa det ytterligare till valda användare eller grupper.  

-   När du använder moln distributions platser autentiseras klienterna av hanterings platsen och använder sedan en Configuration Manager-token för att få åtkomst till moln distributions platser. Token är giltig i åtta timmar. Det innebär att om du blockerar en klient eftersom den inte längre är betrodd kan den fortsätta att ladda ned innehåll från en moln distributions plats tills giltighets perioden för denna token har upphört att gälla. Vid det här tillfället utfärdar hanterings platsen inte någon annan token för klienten eftersom klienten är blockerad.  

     Stoppa moln tjänsten för att undvika att en blockerad klient laddar ned innehåll i åtta timmar fönstret. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **distributions platser i molnet** .  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Sekretessinformation för innehållshantering  

 Configuration Manager innehåller inte några användar data i innehållsfiler, men en administrativ användare kan välja att utföra den här åtgärden.  



## <a name="see-also"></a>Se även

- [Grundläggande begrepp för innehållshantering](fundamental-concepts-for-content-management.md)  

- [Säkerhet och sekretess för program hantering](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Säkerhet och sekretess för programuppdateringar](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Säkerhet och sekretess för distribution av operativsystem](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
