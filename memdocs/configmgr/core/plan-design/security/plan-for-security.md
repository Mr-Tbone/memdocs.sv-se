---
title: Planera för säkerhet
titleSuffix: Configuration Manager
description: Få metod tips och annan information om säkerhet i Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b15b3017dd49c75f4281a3c0bfd1c8a695ab8bae
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526006"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planera för säkerhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln beskrivs de koncept som du bör tänka på när du planerar säkerheten med din Configuration Manager implementering. Den innehåller följande avsnitt:  

- [Planera för certifikat (självsignerade och PKI)](#BKMK_PlanningForCertificates)  
  - [Kryptografi: CNG-certifikat (Next Generation)](#bkmk_plan-cng)  
  - [Förbättrad HTTP](#bkmk_plan-ehttp)  
  - [Certifikat för CMG och CDP](#bkmk_plan-cmgcdp)  
  - [Plats serverns signerings certifikat (självsignerat)](#bkmk_plansitesign)  
  - [Åter kallelse av PKI-certifikat](#BKMK_PlanningForCRLs)  
  - [PKI betrodda rot certifikat och certifikat utfärdare](#BKMK_PlanningForRootCAs)  
  - [Val av PKI-klientcertifikat](#BKMK_PlanningForClientCertificateSelection)  
  - [En över gångs strategi för PKI-certifikat och Internetbaserad klient hantering](#BKMK_PlanningForPKITransition)  

- [Planera för den betrodda rot nyckeln](#BKMK_PlanningForRTK)  

- [Planera för signering och kryptering](#BKMK_PlanningForSigningEncryption)  

- [Planera för rollbaserad administration](#BKMK_PlanningForRBA)  

- [Planera för Azure Active Directory](#bkmk_planazuread)  

- [Planera för autentisering av SMS-provider](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a>Planera för certifikat (självsignerade och PKI)  

Configuration Manager använder en kombination av självsignerade certifikat och PKI-certifikat (Public Key Infrastructure).  

Använd PKI-certifikat närhelst det är möjligt. Mer information finns i [krav för PKI-certifikat](../network/pki-certificate-requirements.md). När Configuration Manager begär PKI-certifikat vid registrering för mobila enheter måste du använda Active Directory Domain Services och en utfärdare av företags certifikat. För alla andra PKI-certifikat distribuerar och hanterar du dem oberoende av Configuration Manager. 

PKI-certifikat krävs när klient datorer ansluter till Internetbaserade plats system. Vissa scenarier med Cloud Management Gateway och moln distributions platsen kräver också PKI-certifikat. Mer information finns i [Hantera klienter på Internet](../../clients/manage/manage-clients-internet.md).

När du använder en PKI kan du också använda IPsec för att skydda server-till-Server-kommunikationen mellan plats system på en plats, mellan platser och för annan data överföring mellan datorer. Implementering av IPsec är oberoende av Configuration Manager.  

När PKI-certifikat inte är tillgängliga genererar Configuration Manager automatiskt självsignerade certifikat. Vissa certifikat i Configuration Manager är alltid självsignerade. I de flesta fall hanterar Configuration Manager automatiskt de självsignerade certifikaten och du behöver inte vidta ytterligare åtgärder. Ett exempel är signerings certifikatet för plats servern. Det här certifikatet är alltid egensignerat. Det säkerställer att principerna som klienterna laddar ned från hanterings platsen skickades från plats servern och inte har manipulerats.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a>Kryptografi: CNG-certifikat (Next Generation)  

Configuration Manager stöder kryptografi: CNG-certifikat (Next Generation). Configuration Manager klienter kan använda certifikat för PKI-klientautentisering med privat nyckel i CNG Key Storage Provider (KSP). Med KSP-stöd har Configuration Manager-klienter stöd för maskinvarubaserad privat nyckel, t. ex. TPM-KSP för certifikat för PKI-klientautentisering. Mer information finns i [Översikt över CNG-certifikat](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a>Förbättrad HTTP  

Att använda HTTPS-kommunikation rekommenderas för alla Configuration Manager kommunikations vägar, men är utmanande för vissa kunder på grund av omkostnader för hantering av PKI-certifikat. Införandet av Azure Active Directory (Azure AD)-integration minskar vissa, men inte alla certifikat krav. Från och med version 1806 kan du aktivera platsen för att använda **utökad http**. Den här konfigurationen har stöd för HTTPS på plats system med hjälp av en kombination av självsignerade certifikat och Azure AD. Det kräver inte PKI. Mer information finns i [Enhanced http](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a>Certifikat för CMG och CDP

Att hantera klienter på Internet via Cloud Management Gateway (CMG) och Cloud distribution Point (CDP) kräver att certifikat används. Antalet och typen av certifikat varierar beroende på dina speciella scenarier. Mer information finns i följande artiklar:
- [Certifikat för Cloud Management Gateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certifikat för moln distributions platsen](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a>Planera för plats serverns signerings certifikat (självsignerat)  

Klienter kan få en kopia av plats serverns signerings certifikat på ett säkert sätt från Active Directory Domain Services och från push-installation av klienter. Om klienterna inte kan hämta en kopia av det här certifikatet med någon av dessa metoder installerar du det när du installerar-klienten. Den här processen är särskilt viktig om klientens första kommunikation med platsen är baserad på en Internetbaserad hanterings plats. Eftersom den här servern är ansluten till ett ej betrott nätverk är det mer sårbart för angrepp. Om du inte gör detta ytterligare steg, laddar klienterna automatiskt ned en kopia av plats serverns signerings certifikat från hanterings platsen.  

Klienterna kan inte säkert få en kopia av plats Server certifikatet i följande scenarier:  

- Du installerar inte klienten genom att använda push-installation av klienter och:  

  - Du har inte utökat Active Directorys schema för Configuration Manager.  

  - Du har inte publicerat klientens plats på Active Directory Domain Services.  

  - Klienten kommer från en obetrodd skog eller arbetsgrupp.  

- Du använder Internetbaserad klient hantering och installerar klienten när den är på Internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Installera klienter med ett exemplar av platsserverns signeringscertifikat  

1.  Leta upp plats serverns signerings certifikat på den primära plats servern. Certifikatet lagras i **SMS** -certifikat arkivet i Windows. Det har ämnes namnet **plats Server** och eget namn, **signerings certifikat för plats Server**.  

2.  Exportera certifikatet utan den privata nyckeln, lagra filen på ett säkert sätt och få åtkomst till den från en säker kanal.  

3.  Installera klienten med hjälp av följande client.msi-egenskap:`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a>Planera för åter kallelse av PKI-certifikat  

När du använder PKI-certifikat med Configuration Manager planera du för användning av en lista över återkallade certifikat (CRL). Enheter använder CRL: en för att verifiera certifikatet på den anslutande datorn. CRL är en fil som en certifikat utfärdare (CA) skapar och signerar. Den innehåller en lista över certifikat som certifikat utfärdaren har utfärdat men som har återkallats. När en certifikat administratör återkallar certifikat läggs dess tumavtryck till i listan över återkallade certifikat. Om ett utfärdat certifikat till exempel är känt eller misstänks vara komprometterat.

> [!IMPORTANT]  
> Eftersom platsen för listan över återkallade certifikat läggs till i ett certifikat när en CA utfärdar den, bör du se till att du planerar för CRL innan du distribuerar några PKI-certifikat som Configuration Manager använder.  

IIS kontrollerar alltid CRL för klient certifikat och du kan inte ändra den här konfigurationen i Configuration Manager. Som standard kontrollerar Configuration Manager klienter alltid CRL för plats system. Inaktivera den här inställningen genom att ange en plats egenskap och genom att ange en CCMSetup-egenskap.  

Datorer som använder återkallnings kontroll av certifikat men inte kan hitta listan över återkallade certifikat fungerar som om alla certifikat i certifikat kedjan har återkallats. Detta beror på att de inte kan verifiera om certifikaten finns i listan över återkallade certifikat. I det här scenariot fungerar inte alla anslutningar som kräver certifikat och inkluderar CRL-kontroll. När du verifierar att listan över återkallade certifikat är tillgänglig genom att bläddra till dess http-plats är det viktigt att Observera att Configuration Manager-klienten körs som lokalt SYSTEM. Därför kan testning av CRL-tillgänglighet med en webbläsare som körs under användar kontexten lyckas, men dator kontot kan vara blockerat vid försök att upprätta en HTTP-anslutning till samma CRL-URL på grund av den interna webb filtrerings lösningen. Vit listning för CRL-URL: en för webb filtrerings lösningar kan vara nödvändigt i den här situationen.

Genom att kontrol lera listan över återkallade certifikat varje gång ett certifikat används får du mer säkerhet än att använda ett certifikat som har återkallats. Även om den introducerar en anslutnings fördröjning och ytterligare bearbetning på klienten. Din organisation kan kräva denna ytterligare säkerhets kontroll för klienter på Internet eller i ett ej betrott nätverk.  

Kontakta PKI-administratörerna innan du bestämmer om Configuration Manager klienter måste kontrol lera listan över återkallade certifikat. Överväg att behålla det här alternativet i Configuration Manager när båda följande villkor är uppfyllda:  

- PKI-infrastrukturen stöder en lista över återkallade certifikat och publiceras där alla Configuration Manager-klienter kan hitta den. Dessa klienter kan omfatta enheter på Internet och de ingår i obetrodda skogar.  

- Kravet på att kontrol lera listan över återkallade certifikat för varje anslutning till ett plats system som är konfigurerat att använda ett PKI-certifikat är större än följande krav:  
  - Snabbare anslutningar  
  - Effektiv bearbetning av klienten  
  - Risken för att klienterna inte kan ansluta till servrar om det inte går att hitta listan  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a>Planera för betrodda PKI-rotcertifikat och listan certifikat utfärdare  

Om dina IIS-platssystem använder PKI-klientcertifikat för klientautentisering över HTTP, eller för klientautentisering och kryptering över HTTPS, kan du behöva importera certifikat från rot certifikat utfärdaren som en plats egenskap. Här är de två scenarierna:  

- Du distribuerar operativ system med hjälp av Configuration Manager och hanterings platserna accepterar bara HTTPS-klientanslutningar.  

- Du använder PKI-klientcertifikat som inte är kedja till ett rot certifikat som hanterings platserna litar på.  

  > [!NOTE]  
  > När du utfärdar klient-PKI-certifikat från samma CA-hierarki som utfärdar Server certifikat som du använder för hanterings platser behöver du inte ange detta rot certifikat för certifikat utfärdare. Men om du använder flera CA-hierarkier och du inte är säker på om de har förtroende för varandra importerar du rot certifikat utfärdaren för klienternas CA-hierarki.  

Om du måste importera rot certifikat utfärdarens certifikat för Configuration Manager exporterar du dem från den utfärdande certifikat utfärdaren eller från klient datorn. Om du exporterar certifikatet från den utfärdande certifikat utfärdaren som också är rot certifikat utfärdare, ser du till att du inte exporterar den privata nyckeln. Lagra den exporterade certifikat filen på en säker plats för att förhindra manipulering. Du behöver åtkomst till filen när du konfigurerar platsen. Om du kommer åt filen via nätverket kontrollerar du att kommunikationen skyddas från manipulering genom att använda IPsec.  

Om ett rot certifikat för certifikat utfärdare som du importerar förnyas, måste du importera det förnyade certifikatet.  

De här importerade rot certifikat utfärdarens certifikat och rot certifikat UTFÄRDARens certifikat för varje hanterings plats skapar listan med certifikat utfärdare som Configuration Manager datorer använder på följande sätt:  

- När klienter ansluter till hanterings platser verifierar hanterings platsen att klient certifikatet är kopplat till ett betrott rot certifikat i platsens lista över certifikat utfärdare. Om den inte gör det avvisas certifikatet och PKI-anslutningen Miss lyckas.  

- När klienter väljer ett PKI-certifikat och har en lista med certifikat utfärdare, väljer de ett certifikat som är kopplat till ett betrott rot certifikat i listan med certifikat utfärdare. Om det inte finns någon matchning väljer klienten inget PKI-certifikat. Mer information finns i [Planera för val av PKI-klientcertifikat](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a>Planera för val av PKI-klientcertifikat  

Om dina IIS-platssystem använder PKI-klientcertifikat för klientautentisering över HTTP eller för klientautentisering och kryptering över HTTPS, bör du planera för hur Windows-klienter väljer det certifikat som ska användas för Configuration Manager.  

> [!NOTE]  
> Vissa enheter stöder inte någon certifikat urvals metod. I stället väljer de automatiskt det första certifikatet som uppfyller certifikat kraven. Till exempel har klienter på Mac-datorer och mobila enheter inte stöd för certifikat urvals metod.  

I många fall räcker standard konfigurationen och beteendet. Configuration Manager-klienten på Windows-datorer filtrerar flera certifikat med hjälp av dessa kriterier i följande ordning:  

1.  Listan med certifikat utfärdare: certifikatet är kopplat till en rot certifikat utfärdare som hanterings platsen litar på.  

2.  Certifikatet finns i standardcertifikatarkivet **Personligt**.  

3.  Certifikatet är giltigt, inte återkallat och har inte upphört att gälla. Giltighets kontrollen verifierar också att den privata nyckeln är tillgänglig.  

4.  Certifikatet har funktioner för klientautentisering.

5.  Certifikatets ämnes namn innehåller namnet på den lokala datorn som en under sträng.  

6.  Certifikatet har den längsta giltighetsperioden.  

Konfigurera klienterna så att de använder listan med certifikat utfärdare med hjälp av följande mekanismer:  

- Publicera den med Configuration Manager plats information som ska Active Directory Domain Services.  

- Installera klienter med push-installation av klienter.  

- Klienterna hämtar den från hanterings platsen efter att de har tilldelats sin plats.  

- Ange det under klient installationen som en CCMSetup client.msi-egenskap för CCMCERTISSUERS.  

Klienter som inte har listan med certifikat utfärdare när de installeras och ännu inte har tilldelats till platsen, hoppar över den här kontrollen. När klienterna har listan med certifikat utfärdare och inte har ett PKI-certifikat som är kopplat till ett betrott rot certifikat i listan med certifikat utfärdare, Miss lyckas certifikat urvalet. Klienterna fortsätter inte med de andra urvalskriterierna för certifikat.  

I de flesta fall identifierar Configuration Manager-klienten ett unikt och lämpligt PKI-certifikat korrekt. Men när det här beteendet inte är fallet kan du konfigurera två alternativa urvals metoder i stället för att välja certifikatet baserat på funktionen för klientautentisering:  

- En partiell sträng matchning av klient certifikatets ämnes namn. Den här metoden är Skift läges känslig. Det är lämpligt om du använder det fullständigt kvalificerade domän namnet (FQDN) för en dator i fältet ämne och vill att certifikatet ska väljas utifrån domänsuffixet, till exempel **contoso.com**. Du kan dock använda denna urvals metod för att identifiera en sträng med sekventiella tecken i certifikatets ämnes namn som särskiljer certifikatet från andra i klient certifikat arkivet.  

  > [!NOTE]
  > Du kan inte använda den partiella sträng matchningen med certifikat mottagarens alternativa namn som plats inställning. Även om du kan ange en delvis sträng matchning för SAN med hjälp av CCMSetup, skrivs den över av plats egenskaperna i följande scenarier:  
  > 
  > - Klienterna hämtar plats information som publiceras till Active Directory Domain Services.  
  >   - Klienterna har installerats via push-installation.  
  > 
  >   Använd en delvis sträng matchning i SAN-nätverket endast när du installerar klienter manuellt och när de inte hämtar plats information från Active Directory Domain Services. Dessa villkor gäller exempelvis endast Internet klienter.  

- En matchning på attributvärdena för klient certifikatets ämnes namn eller attribut för certifikat mottagarens alternativa namn. Den här metoden är Skift läges känslig matchning. Det är lämpligt om du använder ett unikt X500-namn eller motsvarande objekt identifierare (OID) i enlighet med RFC 3280 och du vill att certifikat urvalet ska baseras på attributvärdena. Du kan välja att bara ange de attribut och värden som du vill ska identifieras unikt eller verifiera certifikatet och särskilja det certifikatet från andra i certifikatarkivet.  

I följande tabell visas de attributvärden som Configuration Manager stöder för urvalskriterier för klient certifikat.  

|Objektidentifierarattribut|Attribut för unikt namn|Attributdefinition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domänkomponent|  
|1.2.840.113549.1.9.1|E eller E-mail|E-postadress|  
|2.5.4.3|CN|Allmänt namn|  
|2.5.4.4|SN|Mottagarnamn|  
|2.5.4.5|SERIALNUMBER|Serienummer|  
|2.5.4.6|C|Landskod|  
|2.5.4.7|L|Plats|  
|2.5.4.8|S eller ST|Namn på region|  
|2.5.4.9|STREET|Gatuadress|  
|2.5.4.10|O|Organisationsnamn|  
|2.5.4.11|OU|Organisationsenhet|  
|2.5.4.12|T eller Title|Rubrik|  
|2.5.4.42|G eller GN eller GivenName|Tilltalsnamn|  
|2.5.4.43|I eller Initials|Initialer|  
|2.5.29.17|(inget värde)|Alternativt namn för certifikatmottagare| 

  > [!NOTE]
  > Om du konfigurerar någon av ovanstående metoder för val av certifikat behöver certifikat mottagar namnet inte innehålla namnet på den lokala datorn.

Om fler än ett lämpligt certifikat hittas när urvals villkoren har tillämpats kan du åsidosätta standard konfigurationen för att välja det certifikat som har den längsta giltighets perioden och i stället ange att inget certifikat har valts. I det här scenariot kommer klienten inte att kunna kommunicera med IIS-plats system med ett PKI-certifikat. Klienten skickar ett fel meddelande till den tilldelade återställnings status platsen för att varna dig om att certifikat urvalet Miss lyckas, så att du kan ändra eller förfina urvalskriterierna för certifikat. Klientens funktionssätt därefter beror på om den felande anslutningen skedde över HTTPS eller HTTP:  

- Om den misslyckade anslutningen skedde över HTTPS: klienten försöker ansluta via HTTP och använder det självsignerade klient certifikatet.  

- Om den misslyckade anslutningen skedde över HTTP: klienten försöker ansluta igen via HTTP genom att använda det självsignerade klient certifikatet.  

För att hjälpa till att identifiera ett unikt PKI-klientcertifikat kan du också ange ett eget Arkiv förutom standard alternativet **personligt** i **dator** arkivet. Du måste dock skapa den här butiken oberoende av Configuration Manager. Du måste kunna distribuera certifikat till det här anpassade arkivet och förnya dem innan giltighets perioden går ut.  

Mer information finns i [Konfigurera inställningar för klient-PKI-certifikat](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a>Planera en över gångs strategi för PKI-certifikat och Internetbaserad klient hantering  

Med de flexibla konfigurations alternativen i Configuration Manager kan du gradvis överföra klienter och platsen till att använda PKI-certifikat för att skydda klient slut punkter. PKI-certifikat ger bättre säkerhet och gör att du kan hantera Internet-klienter.  

På grund av antalet konfigurations alternativ och alternativ i Configuration Manager finns det inget enkelt sätt att överföra en plats så att alla klienter använder HTTPS-anslutningar. De här stegen är avsedda som vägledning:  

1. Installera Configuration Manager-platsen och konfigurera den så att plats systemen godkänner klient anslutningar över HTTPS och HTTP.  

2. Konfigurera fliken **kommunikation på klient datorn** i plats egenskaperna så att **plats system inställningarna** är **http eller https**och välj **Använd PKI-klientcertifikat (funktion för klientautentisering) när det är tillgängligt**.  Mer information finns i [Konfigurera inställningar för klient-PKI-certifikat](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

3. Gör en testkörning av PKI-certifikat för klienter. Ett exempel på distribution finns i [distribuera klient certifikatet för Windows-datorer](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Installera klienter via push-installationsmetoden. Mer information finns i [så här installerar du Configuration Manager-klienter med push-installation](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)av klienter.  

5. Övervaka klient distribution och status med hjälp av rapporter och information i Configuration Manager-konsolen.  

6. Spåra hur många klienter som använder ett PKI-klientcertifikat genom att titta i kolumnen **Klientcertifikat** i arbetsytan **Tillgångar och efterlevnad** , noden **Enheter** .  

    Du kan också distribuera Configuration Manager HTTPS readiness Assessment-verktyget (**cmHttpsReadiness.exe**) till datorer. Använd sedan rapporterna för att se hur många datorer som kan använda ett PKI-klientcertifikat med Configuration Manager.  

   > [!NOTE]
   >  När du installerar Configuration Manager-klienten installeras **CMHttpsReadiness.exe** -verktyget i `%windir%\CCM` mappen. Följande kommando rads alternativ är tillgängliga när du kör det här verktyget:  
   > 
   > - `/Store:<name>`: Det här alternativet är samma som egenskapen **CCMCERTSTORE** client.msi  
   > - `/Issuers:<list>`: Det här alternativet är samma som egenskapen **CCMCERTISSUERS** client.msi    
   > - `/Criteria:<criteria>`: Det här alternativet är samma som egenskapen **CCMCERTSEL** client.msi    
   > - `/SelectFirstCert`: Det här alternativet är samma som egenskapen **CCMFIRSTCERT** client.msi    
   > 
   >   Mer information finns i [om klient installations egenskaper](../../clients/deploy/about-client-installation-properties.md).  

7. Följ dessa steg när du är säker på att tillräckligt många klienter använder sina PKI-klientcertifikat för autentisering över HTTP:  

   1.  Distribuera ett webb server certifikat för PKI till en medlems server som kör en ytterligare hanterings plats för platsen och konfigurera certifikatet i IIS. Mer information finns i [distribuera webb Server certifikatet för plats system som kör IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Installera hanteringsplatsrollen på den här servern och konfigurera alternativet **Klientanslutningar** i hanteringsplatsegenskaperna för **HTTPS**.  

8. Övervaka och kontrollera att klienterna som har ett PKI-certifikat använder den nya hanteringsplatsen via HTTPS. Du kan verifiera genom att använda IIS-loggning eller prestanda räknare.  

9. Konfigurera om andra platssystemroller för användning av HTTPS-klientanslutningar. Om du vill hantera klienter på Internet måste du se till att plats systemen har ett fullständigt domän namn för Internet. Konfigurera enskilda hanterings platser och distributions platser för att godkänna klient anslutningar från Internet.  

    > [!IMPORTANT]  
    > Innan du konfigurerar plats system roller för att godkänna anslutningar från Internet granskar du planerings informationen och kraven för internetbaserad klient hantering. Mer information finns i [kommunikation mellan slut punkter](../hierarchy/communications-between-endpoints.md).  

10. Utöka distributionen av PKI-certifikat för klienter och för plats system som kör IIS. Konfigurera plats system rollerna för HTTPS-klientanslutningar och Internet anslutningar efter behov.  

11. För högsta möjliga säkerhet: när du är säker på att alla klienter använder ett PKI-klientcertifikat för autentisering och kryptering, ändrar du plats egenskaperna till att endast använda HTTPS.  

    Den här planen introducerar först PKI-certifikat för autentisering över HTTP och sedan för autentisering och kryptering över HTTPS. När du följer den här planen för att gradvis införa dessa certifikat minskar risken för att klienterna blir ohanterade. Du kan också dra nytta av den högsta säkerhet som Configuration Manager stöder.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a>Planera för den betrodda rot nyckeln  

Den Configuration Manager betrodda rot nyckeln ger en mekanism för Configuration Manager klienter för att kontrol lera att plats system tillhör deras hierarki. Varje platsserver genererar en platsutbytesnyckel för kommunikation med andra platser. Platsutbytesnyckeln på den översta platsen i hierarkin kallas den betrodda rotnyckeln.  

Funktionen för den betrodda rot nyckeln i Configuration Manager liknar ett rot certifikat i en infrastruktur för offentliga nycklar. Allt som signeras av den privata nyckeln för den betrodda rot nyckeln är betrott ytterligare nedåt i hierarkin. Klienterna lagrar en kopia av platsens betrodda rot nyckel i **Root\ccm\locationservices** WMI-namnrymden. 

Platsen utfärdar till exempel ett certifikat till hanterings platsen, som den signerar med den privata nyckeln för den betrodda rot nyckeln. Platsen delas med klienterna som den offentliga nyckeln till den betrodda rot nyckeln. Klienterna kan sedan skilja mellan hanterings platser som finns i deras hierarki och hanterings platser som inte finns i deras hierarki.   

Klienterna hämtar automatiskt den offentliga kopian av den betrodda rot nyckeln genom att använda två mekanismer:  

- Du utökar Active Directory-schemat för Configuration Manager och publicerar platsen till Active Directory Domain Services. Sedan hämtar klienter den här plats informationen från en global katalog server. Mer information finns i [förbereda Active Directory för webbplats publicering](../network/extend-the-active-directory-schema.md).  

- När du installerar klienter med push-installation av klienter. Mer information finns i [push-installation av klienter](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

Om klienterna inte kan hämta den betrodda rot nyckeln genom att använda någon av dessa metoder, litar de på den betrodda rot nyckel som tillhandahålls av den första hanterings plats som de kommunicerar med. I det här scenariot kan en klient vara feldirigerad till en angripares hanterings plats där den tar emot principer från den falska hanterings platsen. Den här åtgärden kräver en avancerad angripare. Den här angreppen är begränsad till kort tid innan klienten hämtar den betrodda rot nyckeln från en giltig hanterings plats. För att minska risken för att en angripare feldirigerar klienter till en falsk hanterings plats kan du Företablera klienterna med den betrodda rot nyckeln.  

Använd följande procedurer för att företablera och kontrol lera den betrodda rot nyckeln för en Configuration Manager-klient:  

- [Företablera en klient med den betrodda rot nyckeln med hjälp av en fil](#bkmk_trk-provision-file)  

- [Företablera en klient med den betrodda rot nyckeln utan att använda en fil](#bkmk_trk-provision-nofile)  

- [Verifiera den betrodda rot nyckeln på en klient](#bkmk_trk-verify)  

- [Ta bort eller Ersätt den betrodda rot nyckeln](#bkmk_trk-reset)  

  > [!NOTE]  
  > Om klienterna kan hämta den betrodda rot nyckeln från Active Directory Domain Services eller klient-push behöver du inte Företablera den. 
  > 
  > När klienter använder HTTPS-kommunikation till hanterings platser behöver du inte Företablera den betrodda rot nyckeln. De upprättar förtroende av PKI-certifikaten.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a>Företablera en klient med den betrodda rot nyckeln med hjälp av en fil  

1.  Öppna följande fil på plats servern i en text redigerare:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Leta upp posten **SMSPublicRootKey =**. Kopiera nyckeln från den raden och Stäng filen utan några ändringar.  

3.  Skapa en ny textfil och klistra in den nyckelinformation som du kopierade från filen filen mobileclient. TCF.  

4.  Spara filen på en plats där alla datorer har åtkomst till den, men var filen är säker mot manipulering.  

5.  Installera klienten med hjälp av en installations metod som godkänner client.msi egenskaper. Ange följande egenskap:`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > När du anger den betrodda rot nyckeln under klient installationen anger du även plats koden. Använd följande client.msi egenskap:`SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a>Företablera en klient med den betrodda rot nyckeln utan att använda en fil  

1.  Öppna följande fil på plats servern i en text redigerare:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Leta upp posten **SMSPublicRootKey =**. Kopiera nyckeln från den raden och Stäng filen utan några ändringar.  

3.  Installera klienten med hjälp av en installations metod som godkänner client.msi egenskaper. Ange följande client.msi egenskap: `SMSPublicRootKey=<key>` där `<key>` är strängen som du kopierade från filen mobileclient. TCF.  

    > [!IMPORTANT]  
    >  När du anger den betrodda rot nyckeln under klient installationen anger du även plats koden. Använd följande client.msi egenskap:`SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a>Verifiera den betrodda rot nyckeln på en klient  

1. Öppna en Windows PowerShell-konsol som administratör.  

2. Kör följande kommando:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

Den returnerade strängen är den betrodda rot nyckeln. Kontrol lera att den matchar **SMSPublicRootKey** -värdet i filen filen mobileclient. TCF på plats servern.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a>Ta bort eller Ersätt den betrodda rot nyckeln  

Ta bort den betrodda rot nyckeln från en klient med hjälp av egenskapen client.msi **RESETKEYINFORMATION = True**. 

Om du vill ersätta den betrodda rot nyckeln installerar du om klienten tillsammans med den nya betrodda rot nyckeln. Använd till exempel klient-push eller ange client.msi egenskapen **SMSPublicRootKey**.  

Mer information om dessa installations egenskaper finns i [om klient installations parametrar och egenskaper](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a>Planera för signering och kryptering  
 
När du använder PKI-certifikat för all klient kommunikation behöver du inte planera för signering och kryptering för att skydda kommunikationen mellan klienterna. Om du konfigurerar ett plats system som kör IIS för att tillåta HTTP-klientanslutningar, bestämmer du hur du ska skydda klient kommunikationen för platsen.  

För att skydda data som klienter skickar till hanterings platser kan du kräva att klienter signerar data. Du kan också kräva SHA-256-algoritmen för signering. Den här konfigurationen är säkrare, men kräver inte SHA-256 om inte alla klienter har stöd för det. Många operativ system har inbyggt stöd för den här algoritmen, men äldre operativ system kan kräva en uppdatering eller snabb korrigering. 

När signering bidrar till att skydda data från manipulering skyddar krypteringen data från att avslöja information. Du kan aktivera 3DES-kryptering för inventeringsdata och tillståndsmeddelanden som klienter skickar till hanteringsplatser i platsen. Du behöver inte installera några uppdateringar på klienter för att kunna använda det här alternativet. Klienter och hanterings platser kräver ytterligare CPU-användning för kryptering och dekryptering.  

Mer information om hur du konfigurerar inställningarna för signering och kryptering finns i [Konfigurera signering och kryptering](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a>Planera för rollbaserad administration  

Mer information finns i [grunderna i rollbaserad administration](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a>Planera för Azure Active Directory

Configuration Manager integreras med Azure Active Directory (Azure AD) för att låta platsen och klienterna använda modern autentisering. Att publicera din webbplats med Azure AD har stöd för följande Configuration Manager scenarier:

**Klient**  

- [Hantera klienter på Internet via Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Hantera domänanslutna enheter i molnet](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Samhantering](../../../comanage/overview.md)  

- [Distribuera användar tillgängliga appar](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Microsoft Store for Business Online-appar](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Minska infrastruktur kraven. Till exempel [Software Center som använder hanterings platsen](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) i stället för program katalogen  

- [Hantera Microsoft 365 appar för företag](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Community-hubb](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Moln distributions plats](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Användar identifiering](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Mer information om hur du ansluter din webbplats till Azure AD finns i [Konfigurera Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md).


Mer information om Azure AD finns i [Azure Active Directory-dokumentationen](https://docs.microsoft.com/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a>Planera för autentisering av SMS-provider
<!--1357013--> 

Från och med version 1810 kan du ange den lägsta autentiseringsnivån som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. Den gäller för alla komponenter som har åtkomst till SMS-providern. Till exempel Configuration Manager-konsolen, SDK-metoder och Windows PowerShell-cmdletar. 

Den här konfigurationen är en inställning för hela hierarkin. Innan du ändrar den här inställningen ser du till att alla Configuration Manager administratörer kan logga in i Windows med den autentiseringsnivå som krävs. 

Följande nivåer är tillgängliga:

- **Windows-autentisering**: Kräv autentisering med Active Directory domänautentiseringsuppgifter.   

- **Certifikatautentisering**: Kräv autentisering med ett giltigt certifikat som har utfärdats av en betrodd PKI-certifikatutfärdare.  

- **Windows Hello för företag-autentisering**: Kräv autentisering med stark tvåfaktorautentisering som är knutet till en enhet och använder biometrik eller en PIN-kod.  

Mer information finns i [Planera för SMS-providern](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Se även
- [Säkerhet och sekretess för Configuration Manager-klienter](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurera säkerhet](configure-security.md)  

- [Kommunikation mellan slut punkter](../hierarchy/communications-between-endpoints.md)  

- [Teknisk referens för kryptografiska kontroller](cryptographic-controls-technical-reference.md)  

- [Certifikatkrav för PKI](../network/pki-certificate-requirements.md)  

