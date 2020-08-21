---
title: Förbereda Windows-servrar
titleSuffix: Configuration Manager
description: Se till att en dator uppfyller förutsättningarna för användning som plats Server eller en plats system Server för Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8585f04e6cedf9cb5158dbebc41b00565eabd989
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692731"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Förbereda Windows-servrar för att hantera Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kan använda en Windows-dator som plats system Server för Configuration Manager måste datorn uppfylla kraven för den avsedda användningen som plats Server eller plats Systems server.  

- Dessa krav innehåller ofta en eller flera Windows-funktioner eller-roller, som aktive ras med hjälp av datorerna Serverhanteraren.  

- Eftersom metoden för att aktivera Windows-funktioner och roller skiljer sig mellan olika operativ system versioner finns mer information om hur du konfigurerar det operativ system som du använder i dokumentationen för din OS-version.  

Informationen i den här artikeln ger en översikt över de typer av Windows-konfigurationer som krävs för att stödja Configuration Manager-plats system. Konfigurations information för särskilda plats system roller finns i [krav för plats och plats system](../configs/site-and-site-system-prerequisites.md).

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Windows-funktioner och-roller  
När du konfigurerar Windows-funktioner och-roller på en dator kan du behöva starta om datorn för att slutföra konfigurationen. Därför är det en bra idé att identifiera datorer som ska vara värdar för vissa plats system roller innan du installerar en Configuration Manager plats eller plats system Server.

### <a name="features"></a>Funktioner  
Följande Windows-funktioner krävs på vissa plats system servrar och bör konfigureras innan du installerar en plats system roll på den datorn.  

- **.NET Framework**: Inklusive  

    - ASP.NET  
    - HTTP-aktivering  
    - Icke-HTTP-aktivering  
    - WCF-tjänster (Windows Communication Foundation)  

    Olika plats system roller kräver olika versioner av .NET Framework.  

    Eftersom .NET Framework 4,0 och senare inte är bakåtkompatibel för att ersätta 3,5 och tidigare versioner när olika versioner är listade som obligatoriska, planerar du att aktivera varje version på samma dator.  

- **BITS (Background Intelligent Transfer Services)**: hanterings platser kräver BITS (och automatiskt valda alternativ) för att stödja kommunikation med hanterade enheter.  

- **BranchCache**: distributions platser kan konfigureras med BranchCache för att ge stöd för klienter som använder BranchCache.  

- **Datadeduplicering**: distributions platser kan konfigureras med och dra nytta av datadeduplicering.  

- **RDC (Remote Differential Compression)**: varje dator som är värd för en plats Server eller en distributions plats kräver RDC. RDC används för att generera paketsignaturer och utföra signaturjämförelser.  

### <a name="roles"></a>Roller  
Följande Windows-roller krävs för att stödja vissa funktioner, t. ex. program uppdateringar och distributioner av operativ system, medan IIS krävs av de vanligaste plats system rollerna.  

- **Registrerings tjänsten för nätverks enheter** (under Active Directory certifikat tjänster): den här Windows-rollen är nödvändig för att använda certifikat profiler i Configuration Manager.  

- **Webb server (IIS)**: inklusive:  
    - Vanliga HTTP-funktioner  
          - HTTP-omdirigering  
    - Apputveckling  
          - .NET-utökningsbarhet  
          - ASP.NET  
          - ISAPI-tillägg  
          - ISAPI-filter  
    - Hanteringsverktyg  
          - IIS 6-hanteringskompatibilitet  
          - IIS 6-metabaskompatibilitet  
          - IIS 6 Windows Management Instrumentation (WMI)-kompatibilitet  
    - Säkerhet  
          - Filtrering av förfrågningar  
          - Windows-autentisering  

  Följande plats system roller använder en eller flera av de angivna IIS-konfigurationerna:  
  - Webbservicepunkt för programkatalog  
  - Webbplats för programkatalog  
  - Distributionsplats  
  - Registreringsplats  
  - Registreringsproxyplats  
  - Status för återställningsplats  
  - Hanteringsplats  
  - Programuppdateringsplats  
  - Plats för tillståndsmigrering     

  Den lägsta version av IIS som krävs är den version som medföljer plats serverns operativ system.  

  Förutom dessa IIS-konfigurationer kan du behöva konfigurera [filtrering av IIS-begäranden för distributions platser](#BKMK_IISFiltering).  

- **Windows Deployment Services**: den här rollen används med operativ Systems distribution.  

- **Windows Server Update Services**: den här rollen krävs för program uppdateringar.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtrering av IIS-begäranden för distributions platser  
Som standard använder IIS begärandefiltrering för att blockera flera filnamnstillägg och mapplatser från åtkomst via HTTP- eller HTTPS-kommunikation. På en distributions plats förhindrar detta att klienter hämtar paket som har blockerade tillägg eller mappar.  

När dina paket källfiler har tillägg som blockeras i IIS av din konfiguration för begär ande filtrering, måste du konfigurera begär ande filtrering så att de tillåts. Detta gör du genom [att redigera funktionen för filtrering av begär Anden](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)) i IIS-hanteraren på dina distributions plats datorer.  

Dessutom används följande fil namns tillägg av Configuration Manager för paket och program. Kontrol lera att konfigurationerna för begär ande filtrering inte blockerar följande fil namns tillägg:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Källfiler för en program distribution kan till exempel innehålla en mapp med namnet **bin** eller ha en fil med fil namns tillägget **. mdb** .  

- Filtrering av IIS-begäranden blockerar som standard åtkomst till dessa element (**bin** är blockerat som ett dolt segment och **. mdb** blockeras som ett fil namns tillägg).  

- När du använder standard konfigurationen för IIS på en distributions plats kan klienter som använder BITS inte ladda ned den här program distributionen från distributions platsen och ange att de väntar på innehåll.  

- Om du vill låta klienterna Ladda ned det här innehållet på varje distributions plats redigerar du **begär ande filtrering** i IIS-hanteraren för att tillåta åtkomst till fil namns tilläggen och mapparna som finns i de paket och program som du distribuerar.  

> [!IMPORTANT]  
> Ändringar av filtret för begäran kan öka datorns attack yta.  
> 
> - Ändringar som du gör på server nivå gäller för alla webbplatser på servern.   
>     - Ändringar som du gör på enskilda webbplatser gäller bara för den webbplatsen.  
> 
> Den rekommenderade säkerhets metoden är att köra Configuration Manager på en dedikerad webb server. Om du måste köra andra program på webb servern använder du en anpassad webbplats för Configuration Manager. Mer information finns i [webbplatser för plats system servrar](websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>HTTP-verb
**Hanterings platser:** För att säkerställa att klienter kan kommunicera med en hanterings plats på hanterings plats servern ser du till att följande HTTP-verb tillåts:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Distributions platser:** Distributions platser kräver att följande HTTP-verb tillåts:
- GET
- HEAD
- PROPFIND

Mer information finns i [Konfigurera filtrering av begär anden i IIS](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)#http-verbs).