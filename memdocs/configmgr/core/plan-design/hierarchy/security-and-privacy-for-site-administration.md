---
title: Säkerhet och sekretess för plats administration
titleSuffix: Configuration Manager
description: Optimera säkerhet och sekretess för plats administration i Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182267"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Säkerhet och sekretess för plats administration i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller information om säkerhet och sekretess för Configuration Manager-platser och hierarkin.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a>Säkerhets vägledning för plats administration

Använd följande vägledning för att skydda Configuration Manager platser och hierarkin.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Kör installations programmet från en betrodd källa och säker kommunikation

Om du vill hindra någon från att manipulera källfilerna kör Configuration Manager-installationen från en betrodd källa. Skydda nätverksplatsen om du lagrar filerna i nätverket.  

Om du kör installations programmet från en nätverks plats, för att hindra en angripare från att manipulera filerna när de överförs via nätverket, använder du IPsec eller SMB-signering mellan käll platsen för installationsfilerna och plats servern.  

Om du använder installations hämtaren för att ladda ned de filer som krävs av installations programmet, se till att du skyddar platsen där filerna lagras. Skydda även kommunikations kanalen för den här platsen när du kör installations programmet.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Utöka Active Directory schema och publicera webbplatser i domänen  

Schema utökningar krävs inte för att köra Configuration Manager, men de skapar en säkrare miljö. -Klienter och-plats servrar kan hämta information från en betrodd källa.  

Om klienterna finns i en obetrodd domän distribuerar du följande plats system roller i klienternas domäner:  

- Hanteringsplats  

- Distributionsplats  

> [!NOTE]  
> En betrodd domän för Configuration Manager kräver Kerberos-autentisering. Om klienterna finns i en annan skog som inte har ett dubbelriktat skogs förtroende för plats serverns skog, anses dessa klienter vara i en domän som inte är betrodd. Ett externt förtroende räcker inte för detta ändamål.  

### <a name="use-ipsec-to-secure-communications"></a>Skydda kommunikation med IPsec

Även om Configuration Manager skyddar kommunikationen mellan plats servern och datorn som kör SQL Server, kan Configuration Manager inte säkra kommunikationen mellan plats system roller och SQL Server. Du kan bara konfigurera vissa plats system med HTTPS för kommunikation mellan platser.  

Om du inte använder ytterligare kontroller för att skydda dessa server-till-Server-kanaler kan angripare använda olika förfalskningar och man-in-the-middle-attacker mot plats system. Använd SMB-signering när du inte kan använda IPsec.  

> [!Important]  
> Skydda kommunikations kanalen mellan plats servern och paket käll servern. Vid sådan kommunikation används SMB. Om du inte kan använda IPsec för att skydda den här kommunikationen ska du använda SMB-signering för att se till att filerna inte har manipulerats innan klienterna laddar ned och kör dem.  

### <a name="dont-change-the-default-security-groups"></a>Ändra inte standard säkerhets grupper

Ändra inte följande säkerhets grupper som Configuration Manager skapar och hanterar för plats system kommunikation:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager skapar och hanterar dessa säkerhets grupper automatiskt. Det här beteendet inkluderar att ta bort dator konton när en plats system roll tas bort.  

För att se till att tjänste kontinuiteten och lägsta behörigheten används kan du inte redigera dessa grupper manuellt.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Hantera etablerings processen för betrodda rot nycklar

Om klienterna inte kan skicka frågor till den globala katalogen för Configuration Manager information måste de förlita sig på den betrodda rot nyckeln för att autentisera giltiga hanterings platser. Den betrodda rot nyckeln lagras i klient registret. Den kan anges med hjälp av en grup princip eller manuell konfiguration.  

Om klienten inte har en kopia av den betrodda rot nyckeln innan den kontaktar en hanterings plats för första gången, litar den på den första hanterings platsen som den kommunicerar med. För att minska risken för att en angripare dirigerar klienter till en falsk hanteringsplats kan du etablera den betrodda rotnyckeln på klienterna på förhand. Mer information finns i [Planera för den betrodda rot nyckeln](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Använd port nummer som inte är standard

Om du använder port nummer som inte är standard kan du ge ytterligare säkerhet. De gör det svårare för angripare att utforska miljön i förberedelser inför ett angrepp. Om du bestämmer dig för att använda portar som inte är standard måste du planera för dem innan du installerar Configuration Manager. Använd dem konsekvent på alla platser i hierarkin. Portarna för klient förfrågningar och Wake On LAN är exempel där du kan använda port nummer som inte är standard.  

### <a name="use-role-separation-on-site-systems"></a>Använd rollseparering på plats system

Även om du kan installera alla plats system roller på en enda dator, används den här metoden sällan i produktions nätverk. Den skapar en enskild felpunkt.  

### <a name="reduce-the-attack-profile"></a>Minska angrepps profilen

Att isolera varje plats system roll på en annan server minskar risken för att ett angrepp mot sårbarheter på ett plats system kan användas mot ett annat plats system. Många roller kräver installation av Internet Information Services (IIS) på plats systemet, och detta måste öka angrepps ytan. Om du måste kombinera roller för att minska kostnaderna för maskin vara, ska du bara kombinera IIS-roller med andra roller som kräver IIS.  

> [!IMPORTANT]  
> Rollen återställnings status plats är ett undantag. Eftersom den här plats system rollen accepterar data som inte har autentiserats från klienter tilldelar du inte rollen återställnings status plats till någon annan Configuration Manager plats system roll.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Konfigurera statiska IP-adresser för plats system

Statiska IP-adresser är lättare att skydda från namnmatchningsangrepp.  

Statiska IP-adresser gör det också enklare att konfigurera IPsec. Att använda IPsec är en säker säkerhets metod för att skydda kommunikationen mellan plats system i Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Installera inte andra program på plats system servrar

När du installerar andra program på plats system servrar ökar du angrepps ytan för Configuration Manager. Du drabbas också av problem med inkompatibilitet.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Kräv signering och aktivera kryptering som plats alternativ

Aktivera platsens signerings- och krypteringsalternativ. Se till att alla klienter har stöd för SHA-256-hashalgoritmen och aktivera sedan alternativet för att **kräva SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Begränsa och övervaka administrativa användare

Ge administrativ åtkomst enbart till Configuration Manager till användare som du litar på. Ge dem sedan lägsta behörighet genom att använda de inbyggda säkerhets rollerna eller genom att anpassa säkerhets rollerna. Administrativa användare som kan skapa, ändra och distribuera program och konfigurationer kan potentiellt styra enheter i Configuration Manager hierarkin.  

Granska tilldelningen av administrativa användare regelbundet och deras behörighetsnivåer och verifiera nödvändiga ändringar.  

Mer information finns i [Konfigurera rollbaserad administration](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Säkra Configuration Manager säkerhets kopieringar

När du säkerhetskopierar Configuration Manager innehåller den här informationen certifikat och andra känsliga data som kan användas av en angripare för personifiering.  

Använd SMB-signering eller IPsec när du överför dessa data i nätverket, och skydda säkerhetskopieringsplatsen.  

### <a name="secure-locations-for-exported-objects"></a>Säkra platser för exporterade objekt

När du exporterar eller importerar objekt från Configuration Manager-konsolen till en nätverks plats skyddar du platsen och skyddar nätverks kanalen.

Begränsa vilka som har tillgång till nätverksmappen.  

Använd SMB-signering eller IPsec mellan nätverks platsen och plats servern för att hindra en angripare från att manipulera exporterade data. Skydda även kommunikationen mellan datorn som kör Configuration Manager-konsolen och plats servern. Kryptera alla data i nätverket med IPsec för att förhindra att information röjs.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Ta bort certifikat från misslyckade servrar manuellt

Om ett plats system inte avinstalleras korrekt eller slutar fungera och inte kan återställas manuellt tar du bort Configuration Manager-certifikat för den här servern från andra Configuration Manager-servrar.

Ta bort det peer-förtroende som ursprungligen etablerades med plats systemet och plats system rollerna genom att manuellt ta bort Configuration Manager certifikat för den felande servern i certifikat arkivet **Betrodda personer** på andra plats system servrar. Den här åtgärden är viktig om du återanvänder servern utan att formatera om den.  

Mer information finns i [kryptografiska kontroller för server kommunikation](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Konfigurera inte Internet-baserade plats system för att överbrygga perimeternätverket

Konfigurera inte plats system servrar så att de får flera hem så att de ansluter till perimeternätverket och intranätet. Även om den här konfigurationen tillåter att Internet-baserade plats system accepterar klient anslutningar från Internet och intranätet, eliminerar den en säkerhets gräns mellan perimeternätverket och intranätet.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Konfigurera plats servern för att initiera anslutningar till perimeternätverk

Om ett plats system finns i ett icke betrott nätverk, till exempel ett perimeternätverk, konfigurerar du plats servern så att den initierar anslutningar till plats systemet.

Plats system initierar som standard anslutningar till plats servern för att överföra data. Den här konfigurationen kan vara en säkerhets risk när anslutningen initieras från ett ej betrott nätverk till det betrodda nätverket. När plats systemen accepterar anslutningar från Internet eller finns i en obetrodd skog, konfigurerar du alternativet plats system så att **plats servern kan initiera anslutningar till plats systemet**. Efter installationen av plats systemet och alla roller initieras alla anslutningar av plats servern från det betrodda nätverket.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Använd SSL-bryggning och avslutning med autentisering

Om du använder en webbproxyserver för internetbaserad klient hantering ska du använda SSL-bryggning till SSL genom att använda avslutning med autentisering.

När du konfigurerar SSL-avslutning på webb servern för proxyservern kan paket från Internet kontrol leras innan de vidarebefordras till det interna nätverket. Proxy-webbservern autentiserar anslutningen från klienten, avslutar den och öppnar sedan en ny autentiserad anslutning till de Internetbaserade plats systemen.  

När Configuration Manager klient datorer använder en proxyserver för att ansluta till Internetbaserade plats system, finns klient identiteten (GUID) på ett säkert sätt i paketets nytto Last. Sedan betraktar hanterings platsen inte webb servern för proxy som klienten.

Om din proxyserver inte stöder kraven för SSL-bryggning, stöds även SSL-tunnlar. Det här alternativet är mindre säkert. SSL-paketen från Internet vidarebefordras till plats systemen utan Termination. Sedan kan de inte inspekteras för skadligt innehåll.  

> [!WARNING]  
> Mobila enheter som har registrerats av Configuration Manager kan inte använda SSL-bryggning. De måste endast använda SSL-tunnlar.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Konfigurationer som ska användas om du konfigurerar platsen så att den aktiverar datorer för att installera program vara

- Om du använder traditionella väcknings paket ska du använda unicast i stället för undernät-dirigerade sändningar.  

- Om du måste använda undernät-dirigerad sändning kan du konfigurera routrar att tillåta IP-dirigerad broadcast enbart från plats servern och endast på ett port nummer som inte är standard.  

Mer information om de olika Wake On LAN teknikerna finns i [Planera aktivering av klienter](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Om du använder e-postavisering konfigurerar du autentiserad åtkomst till SMTP-e-postservern

Använd närhelst det är möjligt en e-postserver som har stöd för autentiserad åtkomst. Använd dator kontot för plats servern för autentisering. Om du måste ange ett användarkonto för autentisering bör du välja ett konto med minst uppsättning privilegier. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>Framtvinga LDAP-kanals bindning och LDAP-signering

Säkerheten för Active Directory domänkontrollanter kan förbättras genom att konfigurera servern för att avvisa Simple Authentication and Security Layer (SASL) LDAP-bindningar som inte begär signering eller för att avvisa enkla LDAP-bindningar som utförs på en klar text anslutning. Från och med version 1910 stöder Configuration Manager tvingande av LDAP-kanalig bindning och LDAP-signering. Mer information finns i [2020 LDAP-kanal bindning och LDAP-signerings krav för Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a>Säkerhets vägledning för plats servern

Använd följande vägledning för att skydda Configuration Manager plats servern.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Installera Configuration Manager på en medlems server i stället för en domänkontrollant

Configuration Manager plats Server och plats system behöver inte installeras på en domänkontrollant. Domänkontrollanter har ingen annan lokal databas för säkerhets konto hantering än domän databasen. När du installerar Configuration Manager på en medlems Server kan du underhålla Configuration Manager-konton i den lokala SAM-databasen i stället för i domän databasen.  

Den här metoden minskar också risken för angrepp på domänkontrollanterna.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Installera sekundära platser utan att kopiera filerna över nätverket

När du kör installations programmet och skapar en sekundär plats ska du inte välja alternativet för att kopiera filerna från den överordnade platsen till den sekundära platsen. Använd inte heller en nätverks käll plats. När du kopierar filer över nätverket kan en utbildad angripare kapa installations paketet för den sekundära platsen och manipulera filerna innan de installeras. Tids inställningen för den här attacken skulle vara svår. Om du använder IPsec eller SMB när du överför filerna kan du minimera risken för det här angreppet.  

I stället för att kopiera filerna över nätverket kopierar du källfilerna från Media-mappen till en lokal mapp på den sekundära plats servern. När du sedan kör installations programmet för att skapa en sekundär plats väljer du **Använd källfilerna på följande plats på den sekundära platsens dator (säkrast)** på sidan källfiler för **installation** och anger den här mappen.  

Mer information finns i [installera en sekundär plats](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>Installation av plats roll ärver behörigheter från enhets roten

<!-- SCCMDocs#1380 -->
Se till att konfigurera system enhetens behörigheter korrekt innan du installerar den första plats system rollen på en server. `C:\SMS_CCM` Ärver till exempel behörigheter från `C:\`. Om roten på enheten inte är korrekt skyddad kan användarna få åtkomst till eller ändra innehållet i mappen Configuration Manager.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a>Säkerhets rikt linjer för SQL Server

Configuration Manager använder SQL Server som backend-databas. Om databasen komprometteras kan angripare kringgå Configuration Manager. Om de kommer åt SQL Server direkt kan de starta attacker via Configuration Manager. Tänk på att attacker mot SQL Server är höga risker och minimerar lämpligt.  

Använd följande säkerhets anvisningar för att skydda SQL Server för Configuration Manager.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Använd inte Configuration Manager plats databas servern för att köra andra SQL Server program

När du ökar åtkomsten till Configuration Manager plats databas servern, ökar den här åtgärden risken för Configuration Manager data. Om den Configuration Manager plats databasen komprometteras, kan andra program på samma SQL Server dator också utgöra en risk.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Konfigurera SQL Server att använda Windows-autentisering

Även om Configuration Manager har åtkomst till plats databasen med hjälp av ett Windows-konto och Windows-autentisering, är det fortfarande möjligt att konfigurera SQL Server att använda SQL Server blandat läge. Med SQL Server blandat läge kan ytterligare SQL-inloggningar få åtkomst till databasen. Den här konfigurationen är inte obligatorisk och ökar angrepps ytan.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Uppdatera SQL Server Express på sekundära platser

När du installerar en primär plats Configuration Manager hämtningar SQL Server Express från Microsoft Download Center. Sedan kopieras filerna till den primära plats servern. När du installerar en sekundär plats och väljer alternativet som installerar SQL Server Express, installerar Configuration Manager den tidigare nedladdade versionen. Den kontrollerar inte om det finns nya versioner. Gör något av följande för att se till att den sekundära platsen har de senaste versionerna:  

- När du har installerat den sekundära platsen kör du Windows Update på den sekundära plats servern.  

- Innan du installerar den sekundära platsen installerar du SQL Server Express manuellt på den sekundära plats servern. Se till att du installerar den senaste versionen och eventuella program uppdateringar. Installera sedan den sekundära platsen och välj alternativet för att använda en befintlig SQL Server instans.  

Kör regelbundet Windows Update för alla installerade versioner av SQL Server. Den här metoden ser till att de har de senaste program uppdateringarna.  

### <a name="follow-general-guidance-for-sql-server"></a>Följ allmänna rikt linjer för SQL Server

Identifiera och följ den allmänna vägledningen för din version av SQL Server. Beakta dock följande krav för Configuration Manager:  

- Platsserverns datorkonto måste vara medlem i gruppen Administratörer på den dator som kör SQL Server. Om du följer SQL Server rekommendationen "etablera administratörs principer uttryckligen" måste det konto som du använder för att köra installations programmet på plats servern vara medlem i gruppen SQL-användare.  

- Om du installerar SQL Server med ett domän användar konto måste du kontrol lera att plats serverns dator konto har kon figurer ATS för ett SPN-namn (Service Principal Name) som publiceras till Active Directory Domain Services. Utan SPN Miss lyckas Kerberos-autentiseringen och Configuration Manager installationen Miss lyckas.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a>Säkerhets rikt linjer för plats system som kör IIS

Flera plats system roller i Configuration Manager kräver IIS. Processen för att skydda IIS gör att Configuration Manager fungerar korrekt och minskar risken för säkerhets attacker. Minimera i praktiken antalet servrar som kräver IIS. Du kan till exempel bara köra antalet hanterings platser som du behöver för att stödja klient basen, med hänsyn till hög tillgänglighet och nätverks isolering för internetbaserad klient hantering.  

Använd följande vägledning för att skydda de plats system som kör IIS.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Inaktivera IIS-funktioner som du inte behöver

Installera så få IIS-funktioner som möjligt för den platssystemroll du installerar. Mer information finns i [krav för plats och plats system](../configs/site-and-site-system-prerequisites.md).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Konfigurera plats system rollerna att kräva HTTPS

När klienter ansluter till ett plats system genom att använda HTTP istället för att använda HTTPS, använder de Windows-autentisering. Det här beteendet kan gå tillbaka till att använda NTLM-autentisering i stället för Kerberos-autentisering. När NTLM-autentisering används kan klienterna ansluta till en icke-registrerad server.  

Undantaget till den här vägledningen kan vara distributions platser. Paket åtkomst konton fungerar inte när distributions platsen har kon figurer ATS för HTTPS. Paketåtkomstkonton ger behörighet till innehållet så att du kan bestämma vilka användare som får åtkomst till innehållet. Mer information finns i [rekommenderade säkerhets metoder för innehålls hantering](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Konfigurera en lista över betrodda certifikat (CTL) i IIS för plats system roller

Platssystemroller:  

- En distributions plats som du konfigurerar för HTTPS  

- En hanterings plats som du konfigurerar för HTTPS och möjliggör stöd för mobila enheter

En CTL är en definierad lista över betrodda rot certifikat utfärdare (ca). När du använder en CTL med grup princip och en PKI-distribution (Public Key Infrastructure) kan du använda en CTL för att komplettera de befintliga betrodda rot certifikat utfärdarna som är konfigurerade i nätverket. Till exempel certifikat utfärdare som installeras automatiskt med Microsoft Windows eller som lagts till via Windows Enterprise rot certifikat utfärdare. När en lista över betrodda certifikat konfigureras i IIS definierar den en delmängd av dessa betrodda rot certifikat utfärdare.  

Med den här del mängden får du större kontroll över säkerheten. Listan över BETRODDA certifikat begränsar klient certifikaten som endast godkänns till de certifikat som utfärdas från listan över certifikat utfärdare i listan över BETRODDA certifikat. Windows levereras till exempel med ett antal välkända certifikat från tredje part, till exempel VeriSign och Thawte.

Som standard har den dator som kör IIS förtroende för certifikat som går med i kedjan till dessa välkända certifikat utfärdare. När du inte konfigurerar IIS med en CTL för de listade plats system rollerna, accepterar platsen som giltig klient alla enheter som har ett certifikat utfärdat av dessa certifikat utfärdare. Om du konfigurerar IIS med en lista över betrodda certifikat som inte innehåller de här certifikat utfärdarna, vägrar-platsen klient anslutningar, om certifikatet är kopplat till dessa certifikat utfärdare. Om Configuration Manager-klienter ska godkännas för plats system rollerna i listan måste du konfigurera IIS med en CTL som anger de certifikat utfärdare som används av Configuration Manager-klienter.  

> [!NOTE]  
> Endast de angivna plats system rollerna kräver att du konfigurerar en lista över betrodda certifikat i IIS. Listan med certifikat utfärdare som Configuration Manager används för hanterings platser ger samma funktioner för klient datorer när de ansluter till HTTPS-hanterings platser.  

Mer information om hur du konfigurerar en lista över betrodda certifikat utfärdare i IIS finns i IIS-dokumentationen.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Lägg inte till plats servern på en dator med IIS

Rolldelningen minskar risken för angrepp och ökar möjligheten till återställning. Plats serverns dator konto har vanligt vis administratörs behörighet för alla plats system roller. Den kan också ha de här behörigheterna på Configuration Manager klienter om du använder push-installation av klienter.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Använd dedikerade IIS-servrar för Configuration Manager

Även om du kan vara värd för flera webbaserade program på de IIS-servrar som också används av Configuration Manager, kan den här metoden öka risken för angrepp markant. Ett dåligt konfigurerat program kan göra det möjligt för en angripare att få kontroll över ett Configuration Manager plats system. Detta brott kan göra det möjligt för en angripare att få kontroll över hierarkin.  

Om du måste köra andra webbaserade program på Configuration Manager-plats system skapar du en anpassad webbplats för Configuration Manager plats system.  

### <a name="use-a-custom-website"></a>Använda en anpassad webbplats

För plats system som kör IIS konfigurerar du Configuration Manager att använda en anpassad webbplats i stället för standard webbplatsen. Om du behöver köra andra webb program på plats systemet måste du använda en anpassad webbplats. Den här inställningen är en inställning för hela platsen i stället för en inställning för ett enskilt plats system.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>När du använder anpassade webbplatser ska du ta bort de virtuella standard katalogerna

När du byter från att använda standard webbplatsen till att använda en anpassad webbplats, kan Configuration Manager inte ta bort de gamla virtuella katalogerna. Ta bort de virtuella kataloger som Configuration Manager ursprungligen skapade under standard webbplatsen.  

Ta till exempel bort följande virtuella kataloger för en distributions plats:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Följ säkerhets vägledning för IIS-server

Identifiera och följ den allmänna vägledningen för din version av IIS-servern. Ta hänsyn till eventuella krav som Configuration Manager har för särskilda plats system roller. Mer information finns i [krav för plats och plats system](../configs/site-and-site-system-prerequisites.md).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a>Säkerhets vägledning för hanterings platsen

Hanterings platser är det primära gränssnittet mellan enheter och Configuration Manager. Överväg angrepp mot hanterings platsen och servern som den körs på för att kunna vara hög risk och minimera den på lämpligt sätt. Använd alla lämpliga säkerhets guider och Övervakare för ovanlig aktivitet.  

Använd följande vägledning för att skydda en hanterings plats i Configuration Manager.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Tilldela klienten på en hanterings plats till samma plats

Undvik scenariot där du tilldelar Configuration Manager-klienten på en hanterings plats till en annan plats än hanterings platsens plats.  

Om du migrerar från en tidigare version till Configuration Manager aktuella grenen migrerar du klienten på hanterings platsen till den nya platsen så snart som möjligt.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a>Säkerhets rikt linjer för återställnings status platsen

Om du installerar en återställnings status plats i Configuration Manager använder du följande säkerhets guider:

Mer information om säkerhets överväganden när du installerar en återställnings status punkt finns i [avgöra om du behöver en återställnings status plats](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Kör inga andra roller på samma plats system

Återställnings status punkten är utformad för att acceptera oautentiserad kommunikation från vilken dator som helst. Om du kör den här plats system rollen med andra roller eller en domänkontrollant ökar risken för servern avsevärt.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Installera återställnings status punkten innan du installerar klienter med PKI-certifikat

Om Configuration Manager-plats system inte accepterar HTTP-klient kommunikation kanske du inte vet att klienterna inte hanteras på grund av PKI-relaterade certifikat problem. Om du tilldelar klienter till en återställnings status punkt rapporteras dessa certifikat problem via återställnings status platsen.  

Av säkerhets skäl kan du inte tilldela en återställnings status plats till klienter när de har installerats. Du kan bara tilldela den här rollen under klient installationen.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Undvik att använda återställnings status punkten i perimeternätverket

Återställningsstatuspunkten är utformad att acceptera data från vilken klient som helst. Även om en återställnings status punkt i perimeternätverket kan hjälpa dig att felsöka internetbaserade klienter, balansera fel söknings fördelarna med risken för ett plats system som accepterar oautentiserade data i ett offentligt tillgängligt nätverk.  

Om du installerar återställnings status punkten i perimeternätverket eller ett ej betrott nätverk konfigurerar du plats servern för att initiera data överföringar. Använd inte standardinställningen som tillåter återställnings status platsen att initiera en anslutning till plats servern.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>Säkerhets problem för plats administration

Läs följande säkerhets problem för Configuration Manager:  

- Configuration Manager har inget skydd mot en behörig administrativ användare som använder Configuration Manager för att attackera nätverket. Obehöriga administrativa användare är en hög säkerhets risk. De kan starta många attacker, bland annat följande strategier:  

    - Använd program varu distribution för att automatiskt installera och köra skadlig program vara på varje Configuration Manager klient dator i organisationen.  

    - Fjärr styrning av en Configuration Manager-klient utan klient behörighet.  

    - Konfigurera snabba avsöknings intervall och extrema inventerings mängder. Den här åtgärden skapar denial of Service-attacker mot klienter och servrar.  

    - Använda en plats i hierarkin till att skriva data till en annan plats Active Directory-data.  

    Platshierarki är säkerhets gränser. Betrakta bara platser som hanterings gränser.  

    Granska all aktivitet som rör administrativa användare och kontrollera regelbundet granskningsloggarna. Kräv att alla Configuration Manager administrativa användare måste genomgå en bakgrunds kontroll innan de anställs. Kräv periodiska omkontroller som ett villkor för anställningen.  

- Om registrerings platsen komprometteras kan en angripare erhålla certifikat för autentisering. De kan stjäla autentiseringsuppgifterna för användare som registrerar sina mobila enheter.  

    Registrerings platsen kommunicerar med en certifikat utfärdare. Den kan skapa, ändra och ta bort Active Directory objekt. Installera aldrig registrerings platsen i perimeternätverket. Övervaka alltid för ovanlig aktivitet.  

- Om du tillåter användar principer för internetbaserad klient hantering ökar du din attack profil.  

    Förutom att använda PKI-certifikat för klient-till-Server-anslutningar kräver de här konfigurationerna Windows-autentisering. De kan återgå till att använda NTLM-autentisering i stället för Kerberos. NTLM-autentisering är sårbar för personifierings- och repetitionsattacker. För att kunna autentisera en användare på Internet måste du tillåta en anslutning från det Internetbaserade plats systemet till en domänkontrollant.  

- **Admin $** -resursen krävs på plats system servrar.  

    Den Configuration Manager plats servern använder admin $-resursen för att ansluta till och utföra tjänst åtgärder på plats system. Inaktivera eller ta inte bort den här resursen.  

- Configuration Manager använder namn matchnings tjänster för att ansluta till andra datorer. Dessa tjänster är svåra att säkra mot följande säkerhets attacker:
    - Förfalskning
    - Manipulation
    - Avvislighet
    - Avslöjande av information
    - Denial of Service (nekad tjänst)
    - Behörighets höjning

    Identifiera och följ eventuella säkerhets anvisningar för den version av DNS som du använder för namn matchning.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a>Sekretess information för identifiering

Identifiering skapar poster för nätverks resurser och lagrar dem i Configuration Manager databasen. Identifierings data poster innehåller dator information, till exempel IP-adresser, OS-versioner och dator namn. Du kan också konfigurera Active Directory identifierings metoder för att returnera information som din organisation lagrar i Active Directory Domain Services.  

Den enda identifierings metod som Configuration Manager aktiverar som standard är pulsslags identifiering. Den här metoden identifierar bara datorer som redan har Configuration Manager-klient program varan installerad.  

Identifierings informationen skickas inte direkt till Microsoft. Den lagras i Configuration Manager-databasen. Configuration Manager behåller informationen i databasen tills data tas bort. Den här processen sker var 90: e dag av plats underhålls aktiviteten **ta bort föråldrade identifierings data**.  
