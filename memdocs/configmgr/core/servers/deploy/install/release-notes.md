---
title: Viktig information
titleSuffix: Configuration Manager
description: Läs om brådskande problem som ännu inte har åtgärd ATS i produkten eller som omfattas av en Microsoft Support kunskaps bas artikel.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da0b9fc5600a957680ad22e54edc176c892527a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718135"
---
# <a name="release-notes-for-configuration-manager"></a>Viktig information för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager är produkt versions anteckningar begränsade till brådskande problem. De här problemen har ännu inte åtgärd ATS i produkten eller beskrivs i en Microsoft Support kunskaps bas artikel.  

Användarspecifik dokumentation innehåller information om kända problem som påverkar kärn scenarier.  

Den här artikeln innehåller viktig information om den aktuella grenen av Configuration Manager. Information om den tekniska för hands versionen finns i [teknisk för hands version](../../../get-started/technical-preview.md)  

Information om de nya funktionerna som introducerades med olika versioner finns i följande artiklar:

- [Nyheter i version 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Nyheter i version 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Nyheter i version 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [Nyheter i version 1902](../../../plan-design/changes/whats-new-in-version-1902.md)

> [!Tip]  
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare:`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Konfigurera och uppgradera  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>Klientens automatiska uppgradering sker omedelbart för alla klienter

<!-- 6040412 -->

*Gäller för version 1910*

Om din webbplats använder [Automatisk klient uppgradering](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), uppgraderas alla klienter omedelbart efter att platsen har uppdaterats när platsen uppdateras till version 1910. Den enda slump bara är när klienter tar emot principen, vilket som standard är varje timme. För en stor webbplats med många klienter kan det här beteendet förbruka en stor mängd nätverks trafik och stress distributions platser.

Mer information om berörda versioner finns i [klient uppdatering för Configuration Manager aktuella grenen, version 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Plats server i passivt läge uppdaterar inte Configuration. MOF

<!-- 5787848 -->

*Gäller för version 1910*

Om platsen innehåller en [plats server i passivt läge](../configure/site-server-high-availability.md)kan du förlora inventerings anpassningar när du uppdaterar platsen. Platsen synkroniserar för närvarande inte Configuration. MOF när du växlar över plats servrarna.

Undvik det här problemet genom att manuellt säkerhetskopiera och återställa platsens Configuration. mof.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Varnings krav varning på domänens funktions nivå på Server 2019

<!-- 4904376 -->

*Gäller för version 1906*

När du installerar uppdateringen för version 1906 i en miljö med domänkontrollanter som kör Windows Server 2019, returnerar krav kontrollen för domän funktions nivån följande varning:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Undvik problemet genom att ignorera varningen.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>Synkronisering av Azure AD-användare och samlings grupp fungerar inte efter plats expansionen

<!-- 4797313 -->
*Gäller för version 1906*

När du har konfigurerat någon av följande funktioner:

- Azure Active Directory användar grupp identifiering
- Synkronisera samlings medlemskaps resultat till Azure Active Directory grupper

Om du expanderar en fristående primär plats till en hierarki med en central administrations plats visas följande fel meddelande i SMS_AZUREAD_DISCOVERY_AGENT. log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Undvik det här problemet genom att förnya nyckeln som är kopplad till appens registrering i Azure AD. Mer information finns i [förnya hemlig nyckel](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Rollbaserad administration

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Säkerhets omfattningar för vissa mappar replikeras inte från CAS till primära platser
<!--6306759-->
*Gäller för version 1910*

Efter uppgraderingen till version 1910 replikeras inte [säkerhets omfattningar för mappar](../configure/configure-role-based-administration.md#bkmk_config-folder) i användar samlingar och enhets samlingar från CAS till primära platser.

## <a name="application-management"></a>Programhantering

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Det går inte att hämta certifikat för PowerShell-fel vid distribution av Microsoft Edge, version 77 och senare
<!--5769384-->
*Gäller för: Configuration Manager version 1910*

Om du kör Configuration Manager-konsolen på ett operativ system där språket är svenska, ungerska eller japanska får du följande fel meddelande när du distribuerar Microsoft Edge, version 77 och senare:

`Unable to get certificate for Powershell`

Felet beror på att en `scripts` mapp inte finns under `AdminConsole\bin` katalogen för svenska, ungerska eller japanska språk. Mappen skript är lokaliserad på dessa OS-språk.

Undvik det här problemet genom att skapa en mapp som `scripts` heter i `AdminConsole\bin` katalogen. Kopiera filerna från din lokaliserade mapp till den nya `scripts` mappen. Distribuera Microsoft Edge, version 77 och senare när filerna har kopierats.

## <a name="os-deployment"></a>Distribution av operativsystem

### <a name="task-sequences-cant-run-over-cmg"></a>Aktivitetssekvenser kan inte köras över CMG

*Gäller för: Configuration Manager version 2002*

Det finns två instanser där aktivitetssekvenser inte kan köras på en enhet som kommunicerar via en Cloud Management Gateway (CMG):

- Du konfigurerar platsen för utökad HTTP och hanterings platsen är HTTP.<!-- 6358851 -->

    Undvik det här problemet genom att konfigurera hanterings platsen för HTTPS.

- Du har installerat och registrerat klienten med en Mass registrerings-token för autentisering.<!-- 6377921 -->

    Undvik det här problemet genom att använda någon av följande autentiseringsmetoder:

  - Registrera enheten i det interna nätverket i förväg
  - Konfigurera enheten med ett certifikat för klientautentisering
  - Anslut enheten till Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>När passiv plats Server har uppgraderats har standard start avbildnings paketen fortfarande paket källa på den tidigare aktiva servern

<!--3453224, SCCMDocs-pr issue 3097-->
*Gäller för: Configuration Manager version 1810*

Om du har en plats server i passivt läge (Server B) och du befordrar den till aktiv, fortsätter innehålls platsen för standard start avbildningarna att referera till den tidigare aktiva servern (Server A). Om Server A har ett maskin varu problem kan du inte uppdatera eller ändra standard start avbildningarna.

Det finns ingen lösning för det här problemet.

## <a name="software-updates"></a>Programuppdateringar

### <a name="security-roles-are-missing-for-phased-deployments"></a>Säkerhets roller saknas för stegvisa distributioner

<!--3479337, SCCMDocs-pr issue 3095-->
*Gäller för: Configuration Manager version 1810, 1902*

Den inbyggda säkerhets rollen **OS Deployment Manager** har behörighet till stegvisa [distributioner](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). Följande roller saknar följande behörigheter:  

- **Programadministratör**  
- **Programdistributionsansvarig**  
- **Program uppdaterings hanteraren**  

**Appens författar** roll kan se ut att ha vissa behörigheter för stegvisa distributioner, men kan inte skapa distributioner.

En användare med en av dessa roller kan starta guiden skapa stegvis distribution och kan se stegvisa distributioner för ett program eller en program uppdatering. De kan inte slutföra guiden eller göra ändringar i en befintlig distribution.

Undvik det här problemet genom att skapa en anpassad säkerhets roll. Kopiera en befintlig säkerhets roll och Lägg till följande behörigheter för den stegvisa **distributions** objekt klassen:

- Skapa  
- Ta bort  
- Ändra  
- Läsa  

Mer information finns i [skapa anpassade säkerhets roller](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Om du använder maskin varu inventering för distribuerade vyer kan du inte publicera till Skriv bords analys

<!-- 4950335 -->
*Gäller för: Configuration Manager version 1902 med Samlad uppdatering och version 1906*

Om du har en hierarki och aktiverar **maskin varu inventering** plats data för [distribuerade vyer](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) på alla platser för replikering av Skriv Configuration Manager bordet, visas följande fel meddelande i M365UploadWorker. log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Undvik det här problemet genom att inaktivera plats data för **maskin varu inventering** för distribuerade vyer på varje plats replikeringslänk.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>Konsolen stängs oväntat när samlingar tas bort

<!-- 4749443 -->
*Gäller för: Configuration Manager version 1902 med Samlad uppdatering*

När du har anslutit platsen till [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md)kan du **välja vissa samlingar som ska synkroniseras med Desktop Analytics**. Om du tar bort en samling och tillämpar ändringarna, orsakar ett ohanterat undantag om du lägger till en ny samling direkt. Konsolen stängs oväntat.

Undvik problemet genom att välja **OK** för att stänga fönstret Egenskaper när du tar bort en samling. Öppna sedan egenskaperna igen för att lägga till en ny samling på fliken **stationär Analytics-anslutning** .

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Panelen pilot status visar vissa enheter som "odefinierade"

<!-- 4547783 -->
*Gäller för: Configuration Manager version 1902 med Samlad uppdatering*

När du använder Configuration Manager-konsolen för att övervaka status för pilot distribution visas pilot enheter som är uppdaterade på mål versionen av Windows för den distributions planen som **odefinierat** i panelen pilot status.  

Dessa **odefinierade** enheter är **uppdaterade** med operativ systemets mål version för distributions planen. Ingen ytterligare åtgärd krävs.

## <a name="cloud-services"></a>Molntjänster

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>Azure-tjänsten för amerikanska myndigheter visar som offentligt moln

<!-- 6036748 -->

*Gäller för version 1910*

Om du skapar en anslutning till en Azure-tjänst och ställer in **Azure-miljön** på det offentliga molnet visar egenskaperna för anslutningen miljön som det offentliga Azure-molnet. Det här problemet är bara ett visnings problem i-konsolen, tjänsten är i det offentliga molnet. Bekräfta konfigurationen genom att köra följande SQL-fråga på plats databasen:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

För det offentliga molnet är `2` resultatet av den här frågan för den angivna innehavaren.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Det går inte att ladda ned innehåll från en moln hanterings-Gateway 1,2 som är aktive rad

<!-- 5771680 -->

*Gäller för version 1906, 1910 tidig uppdaterings ring*

Om du aktiverar en Cloud Management Gateway (CMG) för att **fungera som en moln distributions plats och hanterar innehåll från Azure Storage** och **tillämpar TLS 1,2**, kan det hända att innehålls hämtningen Miss lyckas.

Följande fel visas i DataTransferService. log på klienten:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Följande fel visas i CMGContentService. log på servern:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Så här kan du lösa problemet:

- Uppdatera platsen till den globalt tillgängliga versionen av 1910, som gavs ut den 20 december 2019. (Om du tidigare har uppdaterat till 1910 tidig uppdaterings ring måste du uppdatera till den här versionen när den är tillgänglig.)

- Du kan också använda en traditionell [moln distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Rollen upprätthåller inte TLS 1,2, men är kompatibel med klienter som kräver TLS 1,2.

## <a name="protection"></a>Skydd

### <a name="bitlocker-management-appears-in-version-1906"></a>BitLocker-hantering visas i version 1906

*Gäller för version 1906*

<!-- 5984688 -->

Efter den 21 november 2019, om du uppdaterar till version 1906 från version 1902 eller tidigare, aktive ras funktionen för BitLocker-hanteringen och är tillgänglig. Den här funktionen är en valfri funktion som börjar i version 1910. Den stöds inte i version 1906. Om du försöker använda det i version 1906 kan det uppstå oväntade resultat. Om du inte använder funktionen påverkas ingen påverkan.

Om du vill använda [funktionen BitLocker-hantering](../../../../protect/plan-design/bitlocker-management.md)uppdaterar du till version 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
