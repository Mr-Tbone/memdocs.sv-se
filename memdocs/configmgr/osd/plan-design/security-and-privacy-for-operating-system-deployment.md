---
title: Säkerhet och sekretess för distribution av operativsystem
titleSuffix: Configuration Manager
description: Lär dig mer om säkerhets-och integritets metod tips för operativ Systems distribution i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724428"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Säkerhet och sekretess för operativ system distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller information om säkerhet och sekretess för operativ system distributions funktionen i Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a>Rekommenderade säkerhets metoder för OS-distribution  

Använd följande rekommenderade säkerhets metoder när du distribuerar operativ system med Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementera åtkomstkontroller för att skydda startbara medier

När du skapar startbara medier ska du alltid tilldela ett lösenord för att skydda mediet. Även med ett lösen ord krypterar det bara filer som innehåller känslig information, och alla filer kan skrivas över.  

Skydda mediet fysiskt för att hindra en angripare från att använda kryptografiska angreppsmedel för att skaffa sig tillgång till certifikatet för klientautentisering.  

För att hindra en klient från att installera innehåll eller en klientprincip som har ändrats hashas innehållet och måste användas med den ursprungliga principen. Om innehålls-hashen Miss lyckas eller om kontrollen att innehållet matchar principen, använder klienten inte det startbara mediet. Endast innehållet är hash-kodat. Principen är inte hash-kodad, men den krypteras och skyddas när du anger ett lösen ord. Det här beteendet gör det svårare för en angripare att ändra principen.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Använd en säker plats när du skapar media för OS-avbildningar

Om obehöriga användare har åtkomst till platsen kan de manipulera filerna som du skapar. De kan också använda allt tillgängligt disk utrymme så att det inte går att skapa mediet.  


### <a name="protect-certificate-files"></a>Skydda certifikatfiler 

Skydda certifikatfiler (. pfx) med ett starkt lösen ord. Om du lagrar dem i nätverket ska du skydda nätverks kanalen när du importerar dem till Configuration Manager

När du kräver ett lösen ord för att importera certifikatet för klientautentisering som du använder för startbara medier, hjälper den här konfigurationen dig att skydda certifikatet från en angripare.  

Använd SMB-signering eller IPsec mellan platsen i nätverket och platsservern för att hindra en angripare från att ändra i certifikatfilen.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Blockera eller återkalla eventuella komprometterade certifikat 

Om klient certifikatet komprometteras blockerar du certifikatet från Configuration Manager. Om det är ett PKI-certifikat kan du återkalla det.  

Om du vill distribuera ett operativ system med hjälp av startbara medier och PXE-start, måste du ha ett certifikat för klientautentisering med en privat nyckel. Om certifikatet har hamnat i orätta händer ska du blockera det i noden **Certifikat** på arbetsytan **Administration**, noden **Säkerhet**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Skydda kommunikations kanalen mellan plats servern och SMS-providern

När SMS-providern är fjärran sluten till plats servern skyddar du kommunikations kanalen för att skydda start avbildningar.

När du ändrar Start avbildningar och SMS-providern körs på en server som inte är plats Server är start avbildningarna sårbara för angrepp. Skydda nätverkskanalen mellan dessa datorer genom att använda SMB-signering eller IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Aktivera distributionsplatser för PXE-klientkommunikation endast i säkra nätverkssegment

När en klient skickar en PXE-startbegäran, har du inget sätt att se till att begäran betjänas av en giltig PXE-aktiverad distributions plats. Detta scenario förknippas med följande säkerhetsrisker:  

- En falsk distributionsplats som svarar på PXE-begäranden skulle kunna skicka en ändrad avbildning till klienterna.  

- En angripare kan starta en man-in-the-Middle-attack mot TFTP-protokollet som används av PXE. Detta angrepp kan skicka skadlig kod med OS-filerna. Angriparen kan också skapa en falsk klient för att göra TFTP-begäranden direkt till distributions platsen.  

- Angriparen skulle kunna använda en falsk klient för att göra ett DoS-angrepp mot distributionsplatsen.  

Använd skydd i djupet för att skydda nätverks segmenten där klienterna får åtkomst till PXE-aktiverade distributions platser.  

> [!WARNING]  
>  På grund av dessa säkerhets risker ska du inte aktivera en distributions plats för PXE-kommunikation när den finns i ett icke betrott nätverk, till exempel ett perimeternätverk.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Konfigurera PXE-aktiverade distributionsplatser så att de bara svarar på PXE-begäranden på angivna nätverksgränssnitt  

Om du tillåter distributionsplatsen att svara på PXE-begäranden på alla nätverksgränssnitt, kan denna konfiguration göra PXE-tjänsten tillgänglig i icke betrodda nätverk  


### <a name="require-a-password-to-pxe-boot"></a>Kräv lösenord för PXE-start

När du kräver ett lösen ord för PXE-start lägger den här konfigurationen till en extra säkerhets nivå i PXE-startprocessen. Den här konfigurationen hjälper till att skydda falska klienter som ansluter till Configuration Manager hierarkin.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Begränsa innehållet i OS-avbildningar som används för PXE-start eller multicast

Ta inte med branschspecifika program eller program vara som innehåller känsliga data i en avbildning som du använder för PXE-start eller multicast.  

På grund av de inbyggda säkerhets riskerna med PXE-start och multicast kan du minska riskerna om en falsk dator laddar ned OS-avbildningen.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Begränsa innehållet som installeras av variabler för aktivitetssekvens

Ta inte med branschspecifika program eller program vara som innehåller känsliga data i paket med program som du installerar med hjälp av variabler i aktivitetssekvenser.  

När du distribuerar program vara med hjälp av variabler i aktivitetssekvenser kan det vara installerat på datorer och till användare som inte har behörighet att ta emot den program varan.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Skydda nätverks kanalen vid migrering av användar tillstånd

När du migrerar användar tillstånd ska du skydda nätverks kanalen mellan klienten och platsen för tillståndsmigrering genom att använda SMB-signering eller IPsec.  

Efter den inledande HTTP-anslutningen överförs migreringsdata om användartillståndet med SMB. Om du inte skyddar nätverks kanalen kan en angripare läsa och ändra dessa data.  


### <a name="use-the-latest-version-of-usmt"></a>Använd den senaste versionen av USMT

Använd den senaste versionen av User State Migration Tool (USMT) som Configuration Manager stöder.  

Den senaste versionen av Windows Filöverföring innehåller säkerhetsförbättringar och ger mer kontroll när du migrerar användartillståndsdata.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Ta bort mappar manuellt vid tillståndsmigrering när du inaktiverar dem  

När du tar bort en mapp för plats för tillståndsmigrering i Configuration Manager-konsolen på plats egenskaperna för tillståndsmigrering, tar platsen inte bort den fysiska mappen. För att skydda användar tillståndets data från att avslöja informationen, tar du bort nätverks resursen manuellt och tar bort mappen.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Konfigurera inte borttagnings principen så att användar tillstånd tas bort omedelbart  

Om du konfigurerar borttagnings principen på plats för tillståndsmigrering för att omedelbart ta bort data som marker ATS för borttagning, och om en angripare hanterar användar tillstånds data innan den giltiga datorn gör, så tar platsen omedelbart bort användar tillstånds data. Låt intervallet **Ta bort efter** vara tillräckligt långt så att du hinner verifiera att användartillståndsdata har gått att återställa.  


### <a name="manually-delete-computer-associations"></a>Ta bort dator associationer manuellt 

Ta bort dator associationer manuellt när data återställningen av användar tillståndets migrering har slutförts och verifierats.

Configuration Manager tar inte bort dator associationer automatiskt. Skydda identiteten för användar tillstånds data genom att manuellt ta bort dator associationer som inte längre behövs.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Säkerhetskopiera alla data om användartillståndsmigrering på tillståndsmigreringsplatsen  

Configuration Manager säkerhets kopiering innehåller inte data för migrering av användar tillstånd i platsens säkerhets kopia.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementera åtkomstkontroller för att skydda det förinstallerade mediet  

Skydda mediet fysiskt för att hindra en angripare från att använda kryptografiska angreppsmedel för att skaffa sig tillgång till certifikatet för klientautentisering och känsliga data.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementera åtkomstkontroller för att skydda processen för avbildning av referensdatorn  

Se till att referens datorn som du använder för att avbilda OS-avbildningar finns i en säker miljö. Använd lämpliga åtkomst kontroller så att oväntade eller skadliga program inte kan installeras och oavsiktligt tas med i avbildningen. När du skapar avbildningen ser du till att mål nätverks platsen är säker. Den här processen ser till att det inte går att manipulera avbildningen när du har samlat in den.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Installera alltid de senaste säkerhetsuppdateringarna på referensdatorn  

Om referensdatorn har de senaste säkerhetsuppdateringarna blir de nya datorerna mindre sårbara första gången de startas.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementera åtkomst kontroller när du distribuerar ett operativ system till en okänd dator

Om du måste distribuera ett operativ system till en okänd dator ska du implementera åtkomst kontroller för att förhindra att obehöriga datorer ansluter till nätverket.  

Att tillhandahålla okända datorer är en praktisk metod för att distribuera nya datorer på begäran. Men det kan också göra det möjligt för en angripare att effektivt bli en betrodd klient i nätverket. Begränsa den fysiska tillgången till nätverket, och övervaka klienterna så att du upptäcker obehöriga datorer. 

Datorer som svarar på en PXE-initierad operativ Systems distribution kan ha alla data som förstörts under processen. Det här beteendet kan leda till att system som oavsiktligt omformateras är tillgängliga.  


### <a name="enable-encryption-for-multicast-packages"></a>Aktivera kryptering av multicast-paket  

För varje operativ Systems distributions paket kan du aktivera kryptering när Configuration Manager överför paketet med hjälp av multicast. Den här konfigurationen hjälper till att förhindra att falska datorer ansluter till multicast-sessionen. Det hjälper också till att förhindra angripare från att manipulera överföringen.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Håll ett vakande öga på obehöriga, multicast-aktiverade distributionsplatser  

Om angripare kan få åtkomst till nätverket kan de konfigurera falska multicast-servrar till förfalskning OS-distribution.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>När du exporterar aktivitetssekvenser till en nätverksplats måste platsen och nätverkskanalen skyddas

Begränsa vilka som har tillgång till nätverksmappen.  

Använd SMB-signering eller IPsec mellan platsen i nätverket och platsservern för att hindra en angripare från att ändra den exporterade aktivitetssekvensen.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Om du använder kör som-kontot för aktivitetssekvens bör du vidta ytterligare säkerhets åtgärder

Om du använder [Kör som-kontot för aktivitetssekvens](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)bör du vidta följande försiktighets steg:  

- Använd ett konto med minsta möjliga behörigheter.  

- Använd inte kontot för nätverks åtkomst för det här kontot.  

- Gör aldrig kontot till domänadministratör.  

- Konfigurera aldrig centrala profiler för detta konto. När aktivitetssekvensen körs laddar den nätverks växlings profilen för kontot, vilket lämnar profilen sårbar för åtkomst på den lokala datorn.  

- Begränsa kontots omfattning. Skapa exempelvis andra kör som-konton för aktivitetssekvens för varje aktivitetssekvens. Om ett konto har komprometterats komprometteras bara de klient datorer som det kontot har åtkomst till. Om kommando raden kräver administrativ åtkomst på datorn kan du överväga att endast skapa ett lokalt administratörs konto för aktivitetssekvensen kör som-konto. Skapa det här lokala kontot på alla datorer som kör aktivitetssekvensen och ta bort kontot så fort det inte längre behövs.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Begränsa och övervaka de administrativa användare som har tilldelats säkerhets rollen OS Deployment Manager

Administrativa användare som tilldelas säkerhets rollen **operativ system distributions hanteraren** kan skapa självsignerade certifikat. Dessa certifikat kan sedan användas för att personifiera en klient och hämta klient principer från Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Använd utökad HTTP för att minska behovet av ett konto för nätverks åtkomst

Från och med version 1806, när du aktiverar [utökat http](../../core/plan-design/hierarchy/enhanced-http.md), kräver flera distributions scenarier för operativ system inget konto för nätverks åtkomst för att ladda ned innehåll från en distributions plats. Mer information finns i [aktivitetssekvenser och kontot för nätverks åtkomst](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Säkerhets problem för operativ Systems distribution  

Även om distribution av operativ system kan vara ett bekvämt sätt att distribuera de säkraste operativ systemen och konfigurationerna för datorer i nätverket, har det följande säkerhets risker:  


### <a name="information-disclosure-and-denial-of-service"></a>Information som avslöjas och utelåsning från tjänster  

Om en angripare kan få kontroll över din Configuration Manager-infrastruktur kan de köra alla aktivitetssekvenser. Den här processen kan omfatta formatering av hård diskarna på alla klient datorer. Det går att konfigurera aktivitetssekvenser med känslig information, t.ex. konton som har behörighet att ansluta till domänen och volymlicensnycklar.  


### <a name="impersonation-and-elevation-of-privileges"></a>Personifiering och ökade behörigheter  

Aktivitetssekvenser kan göra att en dator ansluts till en domän. Det kan ge en obehörig dator autentiserad tillgång till nätverket. 

Skydda certifikatet för klientautentisering som används för startbara aktivitetssekvenser och för PXE-startdistribution. När du fångar ett certifikat för klientautentisering ger den här processen en angripare möjlighet att hämta den privata nyckeln i certifikatet. Med det här certifikatet kan de personifiera en giltig klient i nätverket. I så fall kan bedragarens dator ladda ned principer som kan innehålla känsliga data.  

Om klienter använder nätverks åtkomst kontot för att komma åt data som lagras på platsen för tillståndsmigrering, delar dessa klienter effektivt samma identitet. De kan komma åt data för tillståndsmigrering från en annan klient som använder nätverks åtkomst kontot. Informationen är krypterad, så det är bara ursprungsklienten som kan läsa den, men den kan manipuleras eller raderas.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Klientautentisering till platsen för tillståndsmigrering uppnås med hjälp av en Configuration Manager token som utfärdas av hanterings platsen.  

Configuration Manager begränsar eller hanterar inte mängden data som lagras på platsen för tillståndsmigrering. En angripare kan fylla i det tillgängliga disk utrymmet och orsaka en denial of service.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Om du använder samlingsvariabler kan lokala administratörer läsa information som kan vara känslig  

Även om Collection-variabler erbjuder en flexibel metod för att distribuera operativ system, kan den här funktionen leda till att information lämnas ut.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a>Sekretess information för OS-distribution  

Förutom att distribuera ett operativ system till datorer utan ett, kan Configuration Manager användas för att migrera användarnas filer och inställningar från en dator till en annan. Administratören anger vilken information som ska överföras, till exempel personliga datafiler, konfigurationer och inställningar samt webbläsarcookies.  

Configuration Manager lagrar informationen på en plats för tillståndsmigrering och krypterar den under överföring och lagring. Endast den nya dator som är associerad med tillståndsinformation kan hämta den lagrade informationen. Om den nya datorn förlorar nyckeln för att hämta informationen, kan en Configuration Manager administratör med behörigheten **Visa återställnings information** på instans objekt för dator associationer komma åt informationen och associera den med en ny dator. När den nya datorn har återställt tillståndsinformationen tas data bort efter en dag, som standard. Du kan ställa in när tillståndsmigreringsplatsen ska ta bort data som markerats för borttagning. Configuration Manager lagrar inte information om tillståndsmigrering i plats databasen och skickar den inte till Microsoft.  

Om du använder start medier för att distribuera OS-avbildningar ska du alltid använda standard alternativet för att skydda start mediet. Lösenordet krypterar alla variabler som lagrats i aktivitetssekvensen, men information som inte lagrats i en variabel riskerar att röjas.  

OS-distribution kan använda aktivitetssekvenser för att utföra många olika aktiviteter under distributions processen, vilket innefattar installation av program och program uppdateringar. När du konfigurerar aktivitetssekvenser bör du också vara medveten om vilka följder för den personliga integriteten det kan ha när man installerar program.  

Configuration Manager implementerar inte operativ Systems distribution som standard. Det krävs flera konfigurations steg innan du samlar in information om användar tillstånd eller skapar aktivitetssekvenser eller start avbildningar.  

Innan du konfigurerar operativ system distribution bör du tänka igenom dina sekretess krav.  



## <a name="see-also"></a>Se även

[Diagnostik och användningsdata](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Säkerhet och sekretess för Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
