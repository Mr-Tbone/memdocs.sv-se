---
title: Kommunikation mellan slutpunkter
titleSuffix: Configuration Manager
description: Lär dig hur Configuration Manager-plats system och-komponenter kommunicerar i ett nätverk.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587230"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Kommunikation mellan slut punkter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver hur Configuration Manager plats system och klienter kommunicerar över nätverket. Den innehåller följande avsnitt:  

- [Kommunikation mellan platssystem på en plats](#Planning_Intra-site_Com)  
  - [Plats Server till distributions plats](#bkmk_site2dp)  

- [Kommunikation från klienter till platssystem och tjänster](#Planning_Client_to_Site_System)  
  - [Kommunikation mellan klient och hanterings plats](#bkmk_client2mp)  
  - [Kommunikation mellan klient och distributions plats](#bkmk_client2dp)  
  - [Överväganden för klient kommunikation från Internet eller en ej betrodd skog](#BKMK_clientspan)  

- [Kommunikation över Active Directory-skogar](#Plan_Com_X-Forest)  
  - [Stöd för domän datorer i en skog som inte är betrodd av plats serverns skog](#bkmk_noforesttrust)  
  - [Stöd för datorer i en arbets grupp](#bkmk_workgroup)  
  - [Scenarier som stöder en plats eller hierarki som sträcker sig över flera domäner och skogar](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a>Kommunikation mellan plats system på en plats  

När Configuration Manager plats system eller-komponenter kommunicerar via nätverket till andra plats system eller-komponenter på platsen, använder de något av följande protokoll, beroende på hur du konfigurerar platsen:  

- SMB (Server Message Block)  

- HTTP  

- HTTPS  

Med undantag för kommunikation från plats servern till en distributions plats kan server-till-server-kommunikation på en plats ske när som helst. Dessa kommunikationer använder inte mekanismer för att kontrol lera nätverks bandbredden. Eftersom du inte kan styra kommunikationen mellan plats systemen måste du kontrol lera att du installerar plats system servrar på platser som har snabba och väl anslutna nätverk.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a>Plats Server till distributions plats

Använd följande strategier för att hjälpa dig att hantera överföringen av innehåll från plats servern till distributions platser:  

- Konfigurera distributionsplatsen för nätverksbandbreddskontroll och schemaläggning. Dessa kontroller liknar de konfigurationer som används av adresser mellan platser. Använd den här konfigurationen i stället för att installera en annan Configuration Manager plats när överföringen av innehåll till fjärranslutna nätverks platser är din huvudsakliga bandbredd.  

- Du kan installera en distributionsplats som en förinstallerad distributionsplats. Med en förinstallerad distributionsplats kan du använda innehåll som sparas manuellt på distributionsplatsservern, och det undanröjer behovet av att överföra innehållsfiler i nätverket.  

Mer information finns i [Hantera nätverks bandbredd för innehålls hantering](manage-network-bandwidth.md).

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a>Kommunikation från klienter till plats system och tjänster

Klienterna initierar kommunikation till plats system roller, Active Directory Domain Services och onlinetjänster. Om du vill aktivera dessa meddelanden måste brand väggarna tillåta nätverks trafik mellan klienterna och slut punkten för deras kommunikation. Mer information om portar och protokoll som används av klienter när de kommunicerar med dessa slut punkter finns i [portar som används i Configuration Manager](ports.md).  

Innan en klient kan kommunicera med en plats system roll, använder klienten tjänst lokalisering för att hitta en roll som stöder klientens protokoll (HTTP eller HTTPS). Som standard använder klienter den säkraste metoden som är tillgänglig för dem. Mer information finns i [förstå hur klienter hittar plats resurser och tjänster](understand-how-clients-find-site-resources-and-services.md).  

Konfigurera något av följande alternativ om du vill använda HTTPS:  

- Använd en PKI (Public Key Infrastructure) och installera PKI-certifikat på klienter och servrar. Information om hur du använder certifikat finns i [krav för PKI-certifikat](../network/pki-certificate-requirements.md).  

- Från och med version 1806 konfigurerar du platsen så att den **använder Configuration Manager-genererade certifikat för HTTP-platssystem**. Mer information finns i [Enhanced http](enhanced-http.md).  

När du distribuerar en platssystemsroll som använder IIS (Internet Information Services) och stöder kommunikation från klienter, måste du ange om klienterna ansluter till platssystemet via HTTP eller HTTPS. Om du använder HTTP, måste du även fundera på signerings- och krypteringsval. Mer information finns i [Planera för signering och kryptering](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a>Kommunikation mellan klient och hanterings plats

Det finns två steg när en klient kommunicerar med en hanterings plats: autentisering (transport) och auktorisering (meddelande). Den här processen varierar beroende på följande faktorer:

- Plats konfiguration: endast HTTPS, tillåter HTTP eller HTTPS, eller tillåter HTTP eller HTTPS med utökad HTTP aktiverat
- Konfiguration av hanterings plats: HTTPS eller HTTP
- Enhets identitet för enhets drivna scenarier
- Användar identitet för användarbaserade scenarier

Använd följande tabell för att förstå hur den här processen fungerar:  

| MP-typ  | Klientautentisering  | Klient auktorisering<br>Enhetsidentitet  | Klient auktorisering<br>Användar identitet  |
|----------|---------|---------|---------|
| HTTP     | Anonym<br>Med utökad HTTP verifierar-platsen Azure AD- *användare* eller *Device* -token. | Plats begär ande: Anonym<br>Klient paket: anonymt<br>Registrering med någon av följande metoder för att bevisa enhetens identitet:<br> – Anonym (manuellt godkännande)<br> – Windows-integrerad autentisering<br> – Azure AD- *enhets* -token (utökad http)<br>Efter registreringen använder klienten meddelande signering för att bevisa enhetens identitet | För användarbaserade scenarier använder du någon av följande metoder för att bevisa användar identitet:<br> – Windows-integrerad autentisering<br> – *Azure AD-användartoken (* förbättrad http) |
| HTTPS    | Använd någon av följande metoder:<br> – PKI-certifikat<br> – Windows-integrerad autentisering<br> – Azure AD- *användare* eller *enhets* -token | Plats begär ande: Anonym<br>Klient paket: anonymt<br>Registrering med någon av följande metoder för att bevisa enhetens identitet:<br> – Anonym (manuellt godkännande)<br> – Windows-integrerad autentisering<br> – PKI-certifikat<br> – Azure AD- *användare* eller *enhets* -token<br>Efter registreringen använder klienten meddelande signering för att bevisa enhetens identitet | För användarbaserade scenarier använder du någon av följande metoder för att bevisa användar identitet:<br> – Windows-integrerad autentisering<br> – *Azure AD-användartoken* |

> [!Tip]  
> Mer information om konfigurationen av hanterings platsen för olika enhets identitets typer och med Cloud Management Gateway finns i [Aktivera hanterings plats för https](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a>Kommunikation mellan klient och distributions plats

När en klient kommunicerar med en distributions plats behöver den bara autentisera innan innehållet hämtas. Använd följande tabell för att förstå hur den här processen fungerar:

| DP-typ  | Klientautentisering  |
|----------|---------|
| HTTP     | – Anonym, om tillåten<br>– Windows-integrerad autentisering med dator konto eller konto för nätverks åtkomst<br> – Innehålls åtkomst-token (utökad HTTP) |
| HTTPS    | – PKI-certifikat<br> – Windows-integrerad autentisering med dator konto eller konto för nätverks åtkomst<br> – Åtkomsttoken för innehåll |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>Överväganden för klient kommunikation från Internet eller en ej betrodd skog

Mer information finns i följande artiklar:

- [Planera för en molnhanteringsgateway](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [Planera för internetbaserad klienthantering](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a>Kommunikation mellan Active Directory skogar  

Configuration Manager stöder platser och hierarkier som sträcker sig över Active Directory skogar. Det stöder också domän datorer som inte är i samma Active Directory skog som plats servern och datorer som finns i arbets grupper.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a>Stöd för domän datorer i en skog som inte är betrodd av plats serverns skog

- Installera platssystemroller i den ej betrodda skogen, med alternativet att publicera platsinformation till den Active Directory-skogen  

- Hantera dessa datorer som om de är arbets grupps datorer  

När du installerar plats system servrar i en icke-betrodd Active Directory skog, behålls klient-till-Server-kommunikationen från klienter i skogen i skogen och Configuration Manager kan autentisera datorn med hjälp av Kerberos. När du publicerar plats information till klientens skog drar klienterna nytta av att hämta plats information, till exempel en lista över tillgängliga hanterings platser, från sin Active Directory skog, i stället för att hämta den här informationen från den tilldelade hanterings platsen.  

> [!NOTE]  
> Om du vill hantera enheter som finns på Internet kan du installera Internet-baserade plats system roller i perimeternätverket när plats system servrarna finns i en Active Directory skog. Det här scenariot kräver inte dubbelriktat förtroende mellan perimeternätverket och plats serverns skog.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a>Stöd för datorer i en arbets grupp  

- Godkänna arbetsgruppdatorer manuellt när de använder HTTP-klientanslutningar till platssystemroller. Configuration Manager kan inte autentisera de här datorerna med hjälp av Kerberos.  

- Konfigurera arbetsgruppsklienterna för att använda nätverksåtkomstkontot så att dessa datorer kan hämta innehåll från distributionsplatser.  

- Ange en alternativ mekanism för att arbetsgruppsklienter ska hitta hanteringsplatser. Använd DNS-publicering, WINS eller tilldela en hanterings plats direkt. De här klienterna kan inte hämta plats information från Active Directory Domain Services.  

Mer information finns i följande artiklar:  

- [Hantera poster i konflikt](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Konto för nätverks åtkomst](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Så här installerar du Configuration Manager-klienter på arbets grupps datorer](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Scenarier som stödjer en plats eller hierarki som sträcker sig över flera domäner och skogar  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Scenario 1: kommunikation mellan platser i en hierarki som omfattar skogar

Det här scenariot kräver ett dubbelriktat skogs förtroende som stöder Kerberos-autentisering.  Om du inte har ett dubbelriktat skogs förtroende som stöder Kerberos-autentisering så stöder Configuration Manager inte en underordnad plats i den fjärranslutna skogen.  

Configuration Manager stöder installation av en underordnad plats i en fjärran sluten skog som har det nödvändiga dubbelriktade förtroendet för den överordnade platsens skog. Du kan till exempel placera en sekundär plats i en annan skog än dess primära överordnade plats så länge som det nödvändiga förtroendet finns.  

> [!NOTE]  
> En underordnad plats kan vara en primär plats (där den centrala administrations platsen är den överordnade platsen) eller en sekundär plats.  

Kommunikationen mellan platser i Configuration Manager använder databasreplikering och filbaserade överföringar. När du installerar en-plats måste du ange ett konto som platsen ska installeras på på den avsedda servern. Detta konto upprättar och upprätthåller dessutom kommunikationen mellan platserna. När platsen har installerats och initierat filbaserade överföringar och databasreplikering, behöver du inte konfigurera något annat för kommunikation till platsen.  

Om det finns ett dubbelriktat skogs förtroende behöver Configuration Manager inte några ytterligare konfigurations steg.  

Som standard när du installerar en ny underordnad plats, konfigurerar Configuration Manager följande komponenter:  

- Ett filbaserat replikeringsflöde mellan platser på varje plats som använder platsserverns datorkonto. Configuration Manager lägger till dator kontot för varje dator i **SMS_SiteToSiteConnection_&lt;SiteCode\> ** -gruppen på mål datorn.  

- Databasreplikering mellan SQL-servrarna på varje plats.  

Ange även följande konfigurationer:  

- Mellanliggande brand väggar och nätverks enheter måste tillåta att de nätverks paket som Configuration Manager kräver.  

- Namnmatchningen måste fungera mellan skogarna.  

- Om du vill installera en plats eller en platssystemsroll, måste du ange ett konto med lokal administrativ behörighet på den angivna datorn.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Scenario 2: kommunikation på en plats som omfattar skogar

Det här scenariot kräver inte ett dubbelriktat skogs förtroende.  

Primära platser stöder installation av platssystemroller på datorer i fjärranslutna skogar.  

- Webbtjänsten för programkatalogen är det enda undantaget.  Den stöds endast i samma skog som plats servern.  

- När en plats system roll accepterar anslutningar från Internet, som en säkerhets åtgärd, bör du installera plats system rollerna på en plats där skogens gränser tillhandahåller skydd för plats servern (t. ex. i ett perimeternätverk).  

Om du vill installera en platssystemroll på en dator i en ej betrodd skog:  

- Ange ett **installations konto för plats system**som platsen använder för att installera plats system rollen. (Det här kontot måste ha lokal administratörs behörighet för att kunna ansluta till.) Installera sedan plats system roller på den angivna datorn.  

- Välj alternativet plats system **kräver att plats servern initierar anslutningar till plats systemet**. Den här inställningen kräver att plats servern upprättar anslutningar till plats system servern för att överföra data. Den här konfigurationen förhindrar att datorn på den ej betrodda platsen initierar kontakt med den plats server som finns i det betrodda nätverket. Dessa anslutningar använder **installationskontot för platssystem**.  

Om du vill använda en platssystemroll som har installerats i en ej betrodd skog måste brandväggarna tillåta nätverkstrafik även när platsservern initierar överföringen av data.  

Dessutom kräver följande platssystemroller direkt åtkomst till platsdatabasen. Därför måste brand väggarna tillåta tillämplig trafik från den ej betrodda skogen till platsens SQL Server:  

- Plats för synkronisering av tillgångsinformation  

- Plats för slutpunktsskydd  

- Registreringsplats  

- Hanteringsplats  

- Rapporteringstjänstplats  

- Plats för tillståndsmigrering  

Mer information finns i [portar som används i Configuration Manager](ports.md).  

Du kan behöva konfigurera hanterings platsens och registrerings platsens åtkomst till plats databasen.

- Som standard när du installerar dessa roller konfigurerar Configuration Manager dator kontot för den nya plats system servern som anslutnings konto för plats system rollen. Den lägger sedan till kontot i lämplig SQL Server databas roll.  

- När du installerar dessa plats Systems roller i en obetrodd domän konfigurerar du plats system rollens anslutnings konto så att plats system rollen kan hämta information från databasen.  

Om du konfigurerar ett domän användar konto som anslutnings konto för dessa plats system roller ser du till att domän användar kontot har lämplig åtkomst till SQL Server-databasen på den platsen:  

- Hanteringsplats: **Anslutningskonto för hanteringsplatsdatabas**  

- Registreringsplats: **Konto för registreringsplatsanslutning**  

Ha följande ytterligare uppgifter i åtanke när du planerar för platssystemsroller i andra skogar:  

- Om du kör Windows-brandväggen konfigurerar du tillämpliga brand Väggs profiler för att skicka kommunikationen mellan plats databas servern och datorerna som är installerade med fjärrplatsens system roller.

- Användar principer stöds om den Internetbaserade hanterings platsen litar på den skog som innehåller användar kontona. Om det inte finns något förtroende stöds endast datorprinciper.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Scenario 3: kommunikation mellan klienter och plats system roller när klienterna inte är i samma Active Directory skog som sin plats Server

Configuration Manager stöder följande scenarier för klienter som inte är i samma skog som platsens plats Server:  

- Det finns ett dubbelriktat skogs förtroende mellan klientens skog och plats serverns skog.  

- Plats system roll servern finns i samma skog som klienten.  

- Klienten finns på en domän dator som inte har ett dubbelriktat skogs förtroende med plats servern och plats system rollerna är inte installerade i klientens skog.  

- Klienten finns på en arbets grupps dator.  

Klienter på en domänansluten dator kan använda Active Directory Domain Services för tjänst lokalisering när deras plats publiceras i deras Active Directory skog.  

Publicera plats information till en annan Active Directory skog:  

- Ange skogen och sedan aktivera publicering till skogen i noden **Active Directory-skogar** på arbetsytan **Administration** .  

- Konfigurera varje plats så att de publicerar sina data till Active Directory Domain Services. Med den här konfigurationen kan klienter i den skogen hämta platsinformation och lokalisera hanteringsplatser. För klienter som inte kan använda Active Directory Domain Services för tjänst lokalisering kan du använda DNS, WINS eller klientens tilldelade hanterings plats.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a>Scenario 4: sätt Exchange Server-anslutningen i en fjärran sluten skog  

Kontrol lera att namn matchningen fungerar mellan skogarna för att stödja det här scenariot. Konfigurera till exempel DNS-vidarebefordran. När du konfigurerar Exchange Server-anslutningen anger du intranätets FQDN för Exchange Server. Mer information finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="see-also"></a>Se även

- [Planera för säkerhet](../security/plan-for-security.md)  

- [Säkerhet och sekretess för Configuration Manager-klienter](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
