---
title: Klient säkerhet och sekretess
titleSuffix: Configuration Manager
description: Lär dig mer om säkerhet och sekretess för Configuration Manager-klienter.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84ef4e37ddf756f04101c9cdec0ec7a4ed91688d
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270845"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Säkerhet och sekretess för Configuration Manager-klienter

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln beskrivs säkerhets-och sekretess information för Configuration Manager-klienter. Den innehåller också information för mobila enheter som hanteras av [Exchange Server-anslutningen](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a>Rekommenderade säkerhets metoder för klienter  

Configuration Manager-platsen accepterar data från enheter som kör Configuration Manager-klienten. Det här beteendet medför risk för att klienterna angriper platsen. De kan exempelvis skicka felaktig inventeringsinformation eller försöka överbelasta platssystemen. Distribuera endast Configuration Manager-klienten till enheter som du litar på. Använd också följande rekommenderade säkerhetsmetoder för att skydda platsen från icke-registrerade eller manipulerade enheter:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Använd PKI-certifikat (Public Key Infrastructure) för klient kommunikation med plats system som kör IIS  

- Som platsegenskap ställer du in **Inställningar för platssystem** på **Endast HTTPS**.  

- Installera klienter med `UsePKICert` egenskapen CCMSetup.  

- Använd en lista över återkallade certifikat och se till att klienter och kommunicerande servrar alltid har åtkomst till den.  

Mobila enhets klienter och vissa Internetbaserade klienter kräver dessa certifikat. Microsoft rekommenderar dessa certifikat för alla klient anslutningar på intranätet.  

Mer information om kraven för PKI-certifikat och hur de används för att skydda Configuration Manager finns i [krav för PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Godkänn automatiskt klientdatorer från betrodda domäner och kontrollera och godkänn andra datorer manuellt  

Om du inte kan använda PKI-autentisering identifierar godkännandet en dator som du litar på att hanteras av Configuration Manager. Hierarkin har följande alternativ för att konfigurera klient godkännande:  

- Manuell
- Automatiskt för datorer i betrodda domäner
- Automatisk för alla datorer  

Den säkraste metoden för godkännande är att automatiskt godkänna klienter som är medlemmar i betrodda domäner. Det här alternativet inkluderar moln domänanslutna klienter från anslutna Azure Active Directory (Azure AD)-klient organisationer.<!-- MEMDocs#318 --> Kontrol lera sedan manuellt och godkänn alla andra datorer. Att automatiskt godkänna alla klienter rekommenderas inte om du inte har andra åtkomst kontroller för att förhindra att otillförlitliga datorer får åtkomst till nätverket.  

Mer information om hur du godkänner datorer manuellt finns i [Hantera klienter från noden enheter](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Förlita dig inte på blockering för att förhindra att klienter kommer åt Configuration Manager hierarkin  

Blockerade klienter avvisas av Configuration Manager-infrastrukturen. Om klienterna blockeras kan de inte kommunicera med plats system för att ladda ned principer, ladda upp inventerings data eller skicka tillstånds-eller status meddelanden.

Blockering är utformat för följande scenarier:

- Blockera borttappade eller komprometterade start medier när du distribuerar ett operativ system till klienter
- När alla plats system godkänner HTTPS-klientanslutningar

När plats systemen godkänner HTTP-klientanslutningar ska du inte förlita dig på att blockera för att skydda Configuration Manager-hierarkin från ej betrodda datorer. I det här scenariot kan en blockerad klient ansluta till platsen igen med ett nytt självsignerat certifikat och maskinvaru-ID.

Återkallning av certifikat är den primära försvars linjen mot potentiellt komprometterade certifikat. En lista över återkallade certifikat (CRL) är endast tillgänglig från en PKI (Public Key Infrastructure) som stöds. Att blockera klienter i Configuration Manager ger en extra försvars linje för att skydda din hierarki.  

Mer information finns i [avgöra om klienter ska blockeras](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Använd de säkraste klient installations metoderna som är praktiska för din miljö  

- För domändatorer är metoderna grupprincipklientinstallation och programuppdateringsbaserad klientinstallation säkrare än push-installation av klient.  

- Använd avbildning och manuella installations metoder om du använder åtkomst kontroller och ändrings kontroller.  

- I version 1806 eller senare kan du använda Kerberos ömsesidig autentisering med push-installation av klienter.  

Av alla klient installations metoder är push-installation av klienter den minst säkra på grund av de många beroenden som finns. Dessa beroenden inkluderar lokal administratörs behörighet, admin $-resursen och brand Väggs undantag. Antalet och typen av dessa beroenden ökar risken för angrepp.  

Från och med version 1806, när klient-push används, kan platsen kräva ömsesidig Kerberos-autentisering genom att inte tillåta återställning till NTLM innan anslutningen upprättas. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten. Mer information finns i [så här installerar du klienter med klient-push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Mer information om olika klient installations metoder finns i [klient installations metoder](client-installation-methods.md).  

När det är möjligt väljer du en klient installations metod som kräver minst säkerhets behörighet i Configuration Manager. Begränsa de administrativa användare som har tilldelats säkerhets roller med behörigheter som kan användas för andra funktioner än klient distribution. Om du till exempel vill konfigurera automatisk klient uppgradering krävs säkerhets rollen **Fullständig administratör** , vilket ger en administrativ användare alla säkerhets behörigheter.  

Mer information om beroenden och vilka säkerhets behörigheter som krävs för varje klient installations metod finns i avsnittet "installations metodens beroenden" i [förutsättningar för dator klienter](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Om du måste använda push-installation av klienter bör du vidta ytterligare åtgärder för att skydda kontot för push-installation av klienter  

Detta konto måste vara medlem i den lokala gruppen **Administratörer** på varje dator som installerar Configuration Manager-klienten. Lägg aldrig till kontot för push-installation av klienter i gruppen **domän administratörer** . Skapa i stället en global grupp och Lägg sedan till den globala gruppen i den lokala gruppen **Administratörer** på dina klienter. Skapa ett grup princip objekt för att lägga till en begränsad grupp inställning för att lägga till kontot för push-installation av klienter i den lokala gruppen **Administratörer** .  

För ytterligare säkerhet kan du skapa flera konton för push-installation av klienter, var och en med administrativ åtkomst till ett begränsat antal datorer. Om ett konto har komprometterats komprometteras bara de klient datorer som det kontot har åtkomst till.  

### <a name="remove-certificates-before-imaging-clients"></a>Ta bort certifikat innan avbildnings klienter  

När du distribuerar klienter med hjälp av OS-avbildningar ska du alltid ta bort certifikat innan du fångar avbildningen. Dessa certifikat inkluderar PKI-certifikat för klientautentisering och självsignerade certifikat. Om du inte tar bort certifikaten kan klienterna personifiera varandra. Du kan inte verifiera data för varje klient.  

Mer information finns i [skapa en aktivitetssekvens för att avbilda ett operativ system](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Kontrol lera att de Configuration Manager dator klienterna får en auktoriserad kopia av dessa certifikat  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Det Configuration Manager betrodda rot nyckel certifikatet  

När båda dessa påståenden stämmer förlitar sig klienterna på Configuration Manager betrodda rot nyckeln för att autentisera giltiga hanterings platser:  

- Du har inte utökat Active Directory schema för Configuration Manager
- Klienter använder inte PKI-certifikat när de kommunicerar med hanterings platser  

I det här scenariot har klienter inget sätt att kontrol lera att hanterings platsen är betrodd för hierarkin om de inte använder den betrodda rot nyckeln. Om klienter saknar den betrodda rotnyckeln kan en skicklig angripare dirigera dem till en falsk hanteringsplats.  

Om klienterna inte kan hämta Configuration Manager betrodda rot nyckeln från den globala katalogen eller med PKI-certifikat, företablerar du klienterna med den betrodda rot nyckeln. Den här åtgärden säkerställer att de inte kan dirigeras till en falsk hanterings plats. Mer information finns i [Planera för den betrodda rot nyckeln](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>Signeringscertifikat för platsserver  

Klienter använder det här certifikatet för att verifiera att plats servern har signerat den princip som hämtats från en hanterings plats. Det här certifikatet självsigneras av platsservern och publiceras på Active Directory Domain Services.  

Om klienterna inte kan ladda ned signerings certifikatet för plats servern från den globala katalogen, hämtas de från hanterings platsen som standard. Om hanterings platsen är exponerad för ett ej betrott nätverk som Internet installerar du plats serverns signerings certifikat manuellt på klienterna. Den här åtgärden säkerställer att de inte kan hämta manipulerade klient principer från en komprometterad hanterings plats.  

Använd CCMSetup client.msi-egenskapen **SMSSIGNCERT** för att installera signeringscertifikatet för platsservern manuellt. Mer information finns i [om klient installations egenskaper](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Använd inte automatisk platstilldelning om klienten laddar ned den betrodda rot nyckeln från den första hanterings plats den kontaktar  

Undvik risken för att en ny klient laddar ned den betrodda rot nyckeln från en falsk hanterings plats genom att endast använda automatisk platstilldelning i följande scenarier:  

- Klienten kan komma åt Configuration Manager plats information som publiceras till Active Directory Domain Services.  

- Du företablerar klienten med den betrodda rotnyckeln.  

- Du använder PKI-certifikat från en företagscertifikatutfärdare för att upprätta förtroende mellan klienten och hanteringsplatsen.  

Mer information om den betrodda rot nyckeln finns i [Planera för den betrodda rot nyckeln](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Installera klientdatorer med CCMSetup Client.msi-alternativet SMSDIRECTORYLOOKUP=NoWINS  

Den säkraste tjänstplatsmetoden för klienter för att hitta platser och hanteringsplatser är att använda Active Directory Domain Services. Ibland går det inte att utföra den här metoden i vissa miljöer. Till exempel, eftersom du inte kan utöka Active Directory-schemat för Configuration Manager eller eftersom klienterna finns i en skog som inte är betrodd eller en arbets grupp. Om den här metoden inte är möjlig använder du DNS-publicering som en alternativ tjänst plats metod. Om båda metoderna inte fungerar, och om hanterings platsen inte har kon figurer ATS för HTTPS-klientanslutningar, kan klienterna återgå till att använda WINS.  

Publicering till WINS är mindre säkert än andra publicerings metoder. Konfigurera klient datorer så att de inte återgår till att använda WINS genom att ange **SMSDIRECTORYLOOKUP = NoWINS**. Om du måste använda WINS för service location använder du **SMSDIRECTORYLOOKUP = WINSSECURE**. Den här inställningen är standardinställningen. Den använder den betrodda rot nyckeln Configuration Manager för att verifiera det självsignerade certifikatet för hanterings platsen.  

> [!NOTE]  
> När du konfigurerar-klienten för **SMSDIRECTORYLOOKUP = WINSSECURE** och den hittar en hanterings plats från WINS, kontrollerar klienten sin kopia av den Configuration Manager betrodda rot nyckeln i WMI.  
>
> Om signaturen på hanterings platsens certifikat matchar klientens kopia av den betrodda rot nyckeln verifieras certifikatet. När certifikatet har verifierats börjar klienten kommunicera med den hanterings plats som hittades med hjälp av WINS.  
>
> Om signaturen på hanterings platsens certifikat inte matchar klientens kopia av den betrodda rot nyckeln är certifikatet inte giltigt. I det här scenariot kommunicerar klienten inte med den hanterings plats som den hittade med hjälp av WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Se till att underhållsperioderna är tillräckligt långa för att distribuera kritiska programuppdateringar  

Underhålls fönster för enhets samlingar begränsar de tider som Configuration Manager kan installera program vara på dessa enheter. Om du konfigurerar underhålls perioden så att den är för liten, kanske inte klienten installerar kritiska program uppdateringar. Det här beteendet gör att klienten är sårbar för angrepp som program uppdateringen minskar.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Vidta ytterligare säkerhets åtgärder för att minska angrepps ytan på Windows Embedded-enheter med Skriv filter  

När du aktiverar Skriv filter på Windows Embedded-enheter görs alla program varu installationer eller ändringar i överlägget. Ändringarna sparas inte när enheten har startats om. Om du använder Configuration Manager för att inaktivera Skriv filtren under den här perioden är den inbäddade enheten sårbar för ändringar i alla volymer. Dessa volymer omfattar delade mappar.  

Configuration Manager låser datorn under denna tid så att bara lokala administratörer kan logga in. När det är möjligt bör du vidta ytterligare säkerhets åtgärder för att skydda datorn. Du kan till exempel aktivera ytterligare begränsningar i brand väggen.  

Om du använder underhålls perioder för att bevara ändringar bör du planera dessa Windows noggrant. Minimera tiden som Skriv filtren är inaktiverade, men gör dem tillräckligt långa för att tillåta programinstallationer och omstarter för att slutföras.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Använd den senaste klient versionen med klient installation baserad på program uppdatering

Om du använder klient installation baserad på program uppdatering och installerar en senare version av klienten på platsen uppdaterar du den publicerade program uppdateringen. Klienterna får sedan den senaste versionen från program uppdaterings platsen.  

När du uppdaterar platsen uppdateras inte program uppdateringen för klient distributioner som publiceras till program uppdaterings platsen automatiskt. Publicera om Configuration Manager-klienten på program uppdaterings platsen och uppdatera versions numret.  

Mer information finns i [så här installerar du Configuration Manager-klienter med hjälp av installation baserad på program uppdatering](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Pausa bara PIN-koden för BitLocker på betrodda och begränsade åtkomst enheter  

Konfigurera bara klient inställningen för att **Inaktivera PIN-koden för BitLocker vid omstart** till **alltid** för datorer som du litar på och har begränsad fysisk åtkomst.

När du anger den här klient inställningen till **Always**kan Configuration Manager slutföra installationen av program varan. Det här beteendet hjälper till att installera kritiska program uppdateringar och återuppta tjänster. Om en angripare fångar upp omstarts processen kan de ta kontroll över datorn. Använd endast den här inställningen när du litar på datorn och när fysisk åtkomst till datorn är begränsad. Den här inställningen kan till exempel vara lämplig för servrar i ett Data Center.  

Mer information om den här klient inställningen finns i [om klient inställningar](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>Kringgå inte princip för körning av PowerShell

Om du konfigurerar Configuration Manager klient inställningen för **körnings principen för PowerShell** att **kringgå**, tillåter Windows osignerade PowerShell-skript att köras. Den här funktionen kan tillåta att skadlig kod körs på klient datorer. Använd en anpassad klient inställning när din organisation kräver det här alternativet. Tilldela bara de klient datorer som måste köra osignerade PowerShell-skript.  

Mer information om den här klient inställningen finns i [om klient inställningar](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a>Rekommenderade säkerhets metoder för mobila enheter  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Installera proxyn för registrerings platsen i ett perimeternätverk och registrerings platsen i intranätet  

För Internetbaserade mobila enheter som du registrerar med Configuration Manager installerar du proxyn för registrerings platsen i ett perimeternätverk och registrerings platsen i intranätet. Den här rolldelningen hjälper till att skydda registreringsplatsen från attacker. Om en angripare komprometterar registrerings platsen kan de Hämta certifikat för autentisering. De kan också stjäla autentiseringsuppgifterna för användare som registrerar sina mobila enheter.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Konfigurera lösen ords inställningarna för att skydda mobila enheter från obehörig åtkomst  

*För mobila enheter som har registrerats av Configuration Manager*: Använd ett konfigurations objekt för mobila enheter för att konfigurera lösen ords komplexiteten som PIN-kod. Ange minst den minsta standard längden för lösen ord.  

*För mobila enheter som inte har Configuration Manager-klienten installerad men som hanteras av Exchange Server-anslutningen*: konfigurera **lösen ords inställningar** för Exchange Server-anslutningen så att lösen ords komplexiteten är PIN-koden. Ange minst den minsta standard längden för lösen ord.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Tillåt endast att program körs som är signerade av företag som du litar på  

Hjälp till att förhindra manipulering av inventerings information och statusinformation genom att tillåta att program körs endast när de har signerats av företag som du litar på. Tillåt inte att enheter installerar osignerade filer.  

*För mobila enheter som har registrerats av Configuration Manager*: Använd ett konfigurations objekt för mobila enheter för att konfigurera säkerhets inställningen **osignerade program** som **förbjudna**. Konfigurera **osignerade fil installationer** som en betrodd källa.  

*För mobila enheter som inte har Configuration Manager-klienten installerad men som hanteras av Exchange Server-anslutningen*: konfigurera **program inställningar** för Exchange Server-anslutningen så att **osignerad fil installation** och **osignerade program** inte är **tillåtna**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Lås mobila enheter när de inte används  

Hjälp till att förhindra höjning av behörighets attacker genom att låsa den mobila enheten när den inte används.

*För mobila enheter som har registrerats av Configuration Manager*: Använd ett konfigurations objekt för mobila enheter för att konfigurera lösen ords inställningen **vilo tid i minuter innan den mobila enheten låses**.  

*För mobila enheter som inte har Configuration Manager-klienten installerad men som hanteras av Exchange Server-anslutningen*: konfigurera **lösen ords inställningar** för Exchange Server-anslutningen för att ange **inaktiv tid i minuter innan den mobila enheten låses**.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Begränsa vilka användare som kan registrera sina mobila enheter  

Hjälp till att förhindra behörighets höjning genom att begränsa vilka användare som kan registrera sina mobila enheter. Använd en anpassad klientinställning snarare än standardklientinställningar så att endast auktoriserade användare kan registrera sina mobila enheter.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Vägledning för mappning mellan användare och enhet för mobila enheter  

Distribuera inte program till användare som har mobila enheter som har registrerats med Configuration Manager eller Microsoft Intune i följande scenarier:  

- Den mobila enheten används av mer än en person.  

- Enheten registreras av en administratör å en användares vägnar.  

- Enheten överförs till en annan person utan att ta bort den och sedan registrera enheten på nytt.  

Enhets registrering skapar en mappning mellan användare och enhet. Den här relationen mappar användaren som utför registreringen till den mobila enheten. Om en annan användare använder den mobila enheten kan de köra de program som distribueras till den ursprungliga användaren, vilket kan resultera i en höjning av privilegier. Om en administratör registrerar den mobila enheten för en användare installeras inte heller program som distribueras till användaren på den mobila enheten. I stället kan program som distribueras till administratören installeras.  

Till skillnad från mappning mellan användare och enhet för Windows-datorer kan du inte definiera mappnings information mellan användare och enhet manuellt för mobila enheter som har registrerats med Microsoft Intune.  

Om du överför ägarskapet för en mobil enhet som har registrerats av Intune måste du först dra tillbaka den mobila enheten från Intune. Den här åtgärden tar bort mappningen mellan användare och enhet. Be den aktuella användaren att registrera enheten igen.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Se till att användarna registrerar sina egna mobila enheter för Microsoft Intune  

En mappning mellan användare och enhet skapas under registreringen. Den här åtgärden mappar den användare som utför registreringen till den mobila enheten. Om en administratör registrerar den mobila enheten för en användare installeras inte program som distribueras till användaren på den mobila enheten. I stället kan program som distribueras till administratören installeras.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Skydda anslutningen mellan Configuration Manager plats Server och Exchange Server

Om Exchange-servern är lokalt använder du IPsec. Värdbaserad Exchange skyddar anslutningen automatiskt med hjälp av SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Använd principen minst privilegier för anslutningen  

En lista över de minsta cmdlets som krävs för Exchange Server-anslutningen finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a>Rekommenderade säkerhets metoder för Mac  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Lagra och få åtkomst till klientens källfiler från en skyddad plats  

Innan du installerar eller registrerar klienten på Mac-datorn, kontrollerar Configuration Manager inte om källfilerna för dessa klienter har ändrats. Ladda ned dessa filer från en betrodd källa. Lagra och få åtkomst till dem på ett säkert sätt.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Övervaka och spåra giltighets perioden för certifikatet  

För att garantera kontinuitet i verksamheten bör du övervaka och spåra validitetsperioden för de certifikat som du använder för Mac-användare. Configuration Manager stöder inte automatisk förnyelse av det här certifikatet eller varnar dig om att certifikatet håller på att gå ut. En typisk giltighets period är ett år.  

Mer information om hur du förnyar certifikatet finns i [förnya Mac-klientcertifikatet manuellt](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Konfigurera det betrodda rot certifikatet endast för SSL  

Konfigurera certifikatet för den betrodda rot certifikat utfärdaren så att den endast är betrodd för SSL-protokollet för att skydda dig mot behörighets höjning.

När du registrerar Mac-datorer installeras ett användar certifikat för att hantera Configuration Manager klienten automatiskt. Detta användar certifikat innehåller de betrodda rot certifikaten i dess förtroende kedja. Använd följande procedur om du vill begränsa förtroendet för det här rot certifikatet endast till SSL-protokollet:  

1. Öppna ett terminalfönster på Mac-datorn.  

2. Ange följande kommando:`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. I dialog rutan **nyckel hanterare** går du till avsnittet nyckel **ringar** och klickar på **system**. Klicka sedan på **certifikat**i avsnittet **kategori** .  

4. Leta upp och dubbelklicka på certifikatet för rot certifikat utfärdaren för Mac-klientcertifikatet.  

5. I dialogrutan för certifikatet för rotcertifikatutfärdaren expanderar du avsnittet **Förtroende** och gör sedan följande ändringar:  

    1. **När du använder det här certifikatet**: ändra inställningen för **alltid förtroende** till **Använd systemets standardinställningar**.  

    2. **Secure Sockets Layer (SSL)**: ändra **inget värde har angetts** till **Lita alltid**på.  

6. Stäng dialogrutan. När du uppmanas till det anger du administratörens lösen ord och klickar sedan på **Uppdatera inställningar**.  

När du har slutfört den här proceduren är rot certifikatet endast betrott för att verifiera SSL-protokollet. Andra protokoll som nu inte är betrodda med detta rot certifikat är säker e-post (S/MIME), utöknings bar autentisering (EAP) eller kod signering.  

> [!NOTE]  
> Använd även den här proceduren om du har installerat klient certifikatet oberoende av Configuration Manager.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a>Säkerhets problem för Configuration Manager klienter  

Följande säkerhetsfrågor har ingen minskning:  

### <a name="status-messages-arent-authenticated"></a>Status meddelanden är inte autentiserade

Ingen autentisering utförs på statusmeddelanden. När HTTP-klientanslutningar accepteras för en hanteringsplats kan alla enheter skicka statusmeddelanden till hanteringsplatsen. Om hanterings platsen bara accepterar HTTPS-klientanslutningar måste en enhet ha ett giltigt certifikat för klientautentisering, men kan också skicka alla status meddelanden. Hanterings platsen tar bort alla ogiltiga status meddelanden från en klient.  

Det finns några möjliga attacker mot denna sårbarhet:

- En angripare kan skicka ett felaktigt status meddelande för att få medlemskap i en samling som baseras på status meddelande frågor.
- Alla klienter kan neka en tjänst mot hanteringspunkten genom att låta den översvämmas av statusmeddelanden.
- Om statusmeddelanden utlöser åtgärder i filterregler för statusmeddelanden kan en angripare utlösa filterregeln för statusmeddelande.
- En angripare kan skicka status meddelande som återger rapporterings information felaktigt.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>Principer kan ge nya mål till klienter som inte har något mål  

Det finns flera metoder som angripare kan använda för att göra så att en princip som är mål för en klient tillämpas på en helt annan klient. En angripare på en betrodd klient kan till exempel skicka falsk inventering eller identifierings information till att datorn har lagts till i en samling som den inte ska tillhöra. Klienten tar sedan emot alla distributioner till den samlingen.

Det finns kontroller för att förhindra att angripare kan ändra principen direkt. Angripare kan dock ta en befintlig princip som formaterar om och distribuerar om ett operativ system och skickar det till en annan dator. Den här omdirigerade principen kan skapa en denial of service. De här typerna av attacker skulle kräva exakt tids inställning och omfattande kunskaper om Configuration Manager-infrastrukturen.  

### <a name="client-logs-allow-user-access"></a>Med klientloggar ges användaråtkomst  

Alla klient loggfiler tillåter gruppen **användare** med *Läs* behörighet och den speciella **interaktiva** användaren med *Skriv* behörighet. Om du aktiverar utförlig loggning kan inkräktare läsa loggfiler för att leta efter information om kompatibilitet eller säkerhetsrisker i systemet. Processer som-program vara som klienten installerar i en användares kontext måste skriva till loggar med ett användar konto med låg behörighet. Detta innebär att en angripare också kan skriva till loggarna med ett konto med låg behörighet.  

Den mest allvarliga risken är att en angripare kan ta bort information i loggfilerna. En administratör kan behöva den här informationen för granskning och intrångs identifiering.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>En dator kan användas för att hämta ett certifikat som har utformats för registrering av mobila enheter  

När Configuration Manager bearbetar en registreringsbegäran kan den inte verifiera att begäran kommer från en mobil enhet i stället för från en dator. Om begäran kommer från en dator kan den installera ett PKI-certifikat som sedan gör det möjligt att registrera med Configuration Manager.

Om du vill förhindra en höjning av behörighets angreppet i det här scenariot tillåter du bara att betrodda användare registrerar sina mobila enheter. Övervaka enhets registrerings aktiviteter på platsen noggrant.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>En blockerad klient kan fortfarande skicka meddelanden till hanterings platsen

När du blockerar en klient som du inte längre litar på, men som upprättar en nätverks anslutning för klient aviseringen, kommer Configuration Manager inte att koppla från sessionen. den blockerade klienten kan fortsätta att skicka paket till hanteringsplatsen tills klienten kopplas från nätverket. Dessa paket är bara små och Keep-Alive-paket. Den här klienten kan inte hanteras av Configuration Manager förrän den har avblockerats.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Automatisk klient uppgradering verifierar inte hanterings platsen

När du använder automatisk klient uppgradering kan klienten dirigeras till en hanterings plats för att hämta klientens källfiler. I det här scenariot verifierar klienten inte hanterings platsen som en betrodd källa.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>När användare först registrerar Mac-datorer är de utsatta för DNS-förfalskning  

När Mac-datorn ansluter till proxyn för registrerings platsen under registreringen är det osannolikt att Mac-datorn redan har certifikatet för den betrodda rot certifikat utfärdaren. I det här läget är Mac-datorn inte betrodd för servern och användaren ombeds att fortsätta. Om en falsk DNS-Server matchar det fullständigt kvalificerade domän namnet (FQDN) för proxyn för registrerings platsen, kan den dirigera Mac-datorn till en otillåten proxy för registrerings plats för att installera certifikat från en ej betrodd källa. Du reducerar den här risken genom att följa de bästa metoderna för att undvika DNS-förfalskning i din miljö.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac-registrering begränsar inte certifikat begär Anden  

Användare kan registrera sina Mac-datorer på nytt och begära ett nytt klientcertifikat varje gång. Configuration Manager söker inte efter flera begär Anden eller begränsar antalet certifikat som begärs från en enda dator. En falsk användare kan köra ett skript som upprepar begäran om registrering av kommando tolken. Detta angrepp kan orsaka en DOS-attack på nätverket eller på den utfärdande certifikat utfärdaren (CA). Om du vill reducera den här risken övervakar du certifikatutfärdaren noggrant vid den här typen av misstänkt beteende. Omedelbart blockera från Configuration Manager hierarkin alla datorer som visar det här mönstret.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>En rensnings bekräftelse verifierar inte att enheten har rensats  

När du startar en rensnings åtgärd för en mobil enhet och Configuration Manager bekräftar rensningen, är verifieringen att Configuration Manager har *skickat* meddelandet. Den verifierar inte att enheten har *handlat* på begäran.

För mobila enheter som hanteras av Exchange Server-anslutningen kontrollerar en rensnings bekräftelse att kommandot har tagits emot av Exchange, inte av enheten.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Om du använder alternativen för att genomföra ändringar på Windows Embedded-enheter kan kontona låsas upp tidigare än förväntat  

Om Windows Embedded-enheten kör en operativ system version före Windows 7, och en användare försöker logga in medan Skriv filtren har inaktiverats av Configuration Manager, tillåter Windows bara hälften av det konfigurerade antalet felaktiga försök innan kontot låses.

Du kan till exempel konfigurera domän principen för **tröskelvärdet för konto utelåsning** till sex försök. En användare anger sitt lösen ord tre gånger och kontot är utelåst. Det här beteendet skapar en DOS-attack effektivt. Om användarna måste logga in på inbäddade enheter i det här scenariot, bör du känna till dem om potentialen för ett minskat utelåsnings tröskelvärde.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a>Sekretess information för Configuration Manager-klienter  

När du distribuerar Configuration Manager-klienten aktiverar du klient inställningar för Configuration Manager funktioner. Inställningarna som du använder för att konfigurera funktionerna kan tillämpas på alla klienter i hierarkin Configuration Manager. Det här beteendet är detsamma oavsett om de är direkt anslutna till det interna nätverket, är anslutna via en fjärrsession eller anslutna till Internet.  

Klient information lagras i Configuration Manager-databasen på din SQL Server och skickas inte till Microsoft. Informationen sparas i databasen tills den raderas av plats underhålls aktiviteterna **ta bort föråldrade identifierings data** var 90: e dag. Du kan konfigurera borttagningsintervallet. 

Vissa sammanfattande eller aggregerade diagnostik-och användnings data skickas till Microsoft. Mer information finns i [diagnostik-och användnings data](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Innan du konfigurerar Configuration Manager-klienten bör du tänka igenom dina sekretess krav.  

Du kan lära dig mer om Microsofts data insamling och användning i [Microsofts sekretess policy](https://privacy.microsoft.com/privacystatement).

### <a name="client-status"></a>Klientstatus  

Configuration Manager övervakar klienternas aktivitet. Den utvärderar regelbundet Configuration Manager klienten och kan åtgärda problem med klienten och dess beroenden. Klient status är aktive rad som standard. Den använder mått på Server sidan för klient aktivitets kontrollerna. Klient status använder åtgärder på klient sidan för självkontroller, reparation och för att skicka klient status information till platsen. Klienten kör själv kontrollerna enligt ett schema som du konfigurerar. Klienten skickar resultaten från kontrollerna till Configuration Managers platsen. Informationen är krypterad under överföringen.  

Information om klient status lagras i Configuration Manager-databasen i SQL Server och skickas inte till Microsoft. Informationen lagras inte i krypterat format i plats databasen. Den här informationen sparas i databasen tills den raderas enligt det värde som har kon figurer ATS för inställningen **Behåll klient status historik för följande antal dagar:** klient status inställning. Standardvärdet är 31 dagar.  

Innan du installerar Configuration Manager klienten med klient status kontroll bör du tänka igenom dina sekretess krav.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a>Sekretess information för mobila enheter som hanteras med Exchange Server-anslutningen  

Exchange Server-anslutningen hittar och hanterar enheter som ansluter till en lokal eller värdbaserad Exchange-Server med hjälp av ActiveSync-protokollet. Posterna som hittas av Exchange Server-anslutningen lagras i Configuration Manager-databasen på SQL-servern. Informationen samlas in från Exchange-servern. Den innehåller ingen ytterligare information från vad de mobila enheterna skickar till Exchange Server.  

Den mobila enhets informationen skickas inte till Microsoft. Informationen om mobila enheter lagras i Configuration Manager-databasen på SQL-servern. Informationen sparas i databasen tills den raderas av plats underhålls aktiviteten **ta bort föråldrade identifierings data** var 90: e dag. Du konfigurerar borttagnings intervallet.  

Innan du installerar och konfigurerar Exchange Server-anslutningen bör du tänka igenom dina sekretesskrav.  

Du kan lära dig mer om Microsofts data insamling och användning i [Microsofts sekretess policy](https://privacy.microsoft.com/privacystatement).
