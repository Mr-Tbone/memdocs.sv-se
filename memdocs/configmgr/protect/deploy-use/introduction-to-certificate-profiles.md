---
title: Introduktion till certifikatprofiler
titleSuffix: Configuration Manager
description: Lär dig hur certifikat profiler i Configuration Manager fungerar med Active Directory Certificate Services.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3598c95d1431915431d96b16c10c7c913741fe3d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700001"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Introduktion till certifikat profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Certifikat profiler fungerar med Active Directory Certificate Services och rollen för registrerings tjänsten för nätverks enheter (NDES). Skapa och distribuera autentiseringscertifikat för hanterade enheter så att användarna enkelt kan komma åt organisationens resurser. Du kan till exempel skapa och distribuera certifikat profiler för att tillhandahålla nödvändiga certifikat för användare att ansluta till VPN-och trådlösa anslutningar.

Certifikat profiler kan automatiskt konfigurera användar enheter för åtkomst till organisations resurser som Wi-Fi-nätverk och VPN-servrar. Användare kan komma åt dessa resurser utan att manuellt installera certifikat eller använda en out-of-band-process. Certifikat profiler hjälper till att skydda resurser eftersom du kan använda fler säkra inställningar som stöds av din PKI (Public Key Infrastructure). Kräv till exempel serverautentisering för alla Wi-Fi-och VPN-anslutningar eftersom du har distribuerat de nödvändiga certifikaten på de hanterade enheterna.

Certifikatprofiler ger följande hanteringsmöjligheter:  

- Certifikat registrering och förnyelse från en certifikat utfärdare (CA) för enheter som kör olika operativ system typer och versioner. Dessa certifikat kan sedan användas för Wi-Fi-och VPN-anslutningar.  

- Distribution av certifikat från betrodda rot certifikat utfärdare och mellanliggande certifikat utfärdare. Dessa certifikat konfigurerar en förtroende kedja på enheter för VPN-och Wi-Fi-anslutningar när serverautentisering krävs.  

- Övervaka och rapportera om installerade certifikat.  

**Exempel 1**: alla anställda måste ansluta till Wi-Fi-hotspots på flera Office-platser. Om du vill aktivera enkel användar anslutning måste du först distribuera de certifikat som krävs för att ansluta till Wi-Fi. Distribuera sedan Wi-Fi-profiler som hänvisar till certifikatet.  

**Exempel 2**: du har en PKI på plats. Du vill flytta till en mer flexibel, säker metod för att distribuera certifikat. Användare behöver åtkomst till organisations resurser från sina personliga enheter utan att säkerheten äventyras. Konfigurera certifikat profiler med inställningar och protokoll som stöds för den aktuella enhets plattformen. Enheterna kan sedan automatiskt begära dessa certifikat från en Internet-riktad registrerings Server. Konfigurera sedan VPN-profiler för att använda dessa certifikat så att enheten kan komma åt organisationens resurser.  

## <a name="types"></a>Typer

Det finns tre typer av certifikat profiler:  

- **Certifikat för betrodd certifikat utfärdare**: Distribuera en betrodd rot certifikat utfärdare eller mellanliggande CA-certifikat. Dessa certifikat utgör en kedja av förtroende när enheten måste autentisera en server.  

- **Simple Certificate Enrollment Protocol (SCEP)**: begär ett certifikat för en enhet eller användare med hjälp av SCEP-protokollet. Den här typen kräver rollen registrerings tjänst för nätverks enheter (NDES) på en server som kör Windows Server 2012 R2 eller senare.

    Skapa en certifikat profil för en **Simple Certificate Enrollment Protocol (SCEP)** genom att först skapa en certifikat profil för **betrodd certifikat utfärdare** .

- **Personal information Exchange (. pfx)**: begär ett. PFX-certifikat (kallas även PKCS #12) för en enhet eller användare.<!--1321368--> Det finns två metoder för att skapa PFX-certifikat profiler:

  - [Importera autentiseringsuppgifter](../../mdm/deploy-use/import-pfx-certificate-profiles.md) från befintliga certifikat
  - [Definiera en certifikat](../../mdm/deploy-use/create-pfx-certificate-profiles.md) utfärdare att bearbeta begär Anden

  > [!Note]  
  > Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  Du kan använda Microsoft eller entrusted som certifikat utfärdare för **personal information Exchange-certifikat (. pfx)** .

## <a name="requirements"></a>Krav

Om du vill distribuera certifikat profiler som använder SCEP måste du installera certifikat registrerings platsen på en plats system Server. Installera även en principmodul för NDES, Configuration Manager-principmodulen på en server som kör Windows Server 2012 R2 eller senare. Den här servern kräver rollen Active Directory certifikat tjänster. Det kräver också en fungerande NDES som är tillgänglig för de enheter som kräver certifikaten. Om dina enheter behöver registrera sig för certifikat från Internet, måste NDES-servern vara tillgänglig från Internet. Om du till exempel vill aktivera trafik till NDES-servern från Internet kan du använda [Azure Application Proxy](/azure/active-directory/manage-apps/application-proxy).

PFX-certifikat kräver också en certifikat registrerings plats. Ange även certifikat utfärdare (CA) för certifikatet och de relevanta autentiseringsuppgifterna för åtkomst. Du kan ange antingen Microsoft eller entrustet som certifikat utfärdare.  

Mer information om hur NDES stöder en principmodul så att Configuration Manager kan distribuera certifikat finns i [använda en principmodul med registrerings tjänsten för nätverks enheter](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

Beroende på kraven har Configuration Manager stöd för distribution av certifikat till olika certifikat Arkiv på olika enhets typer och operativ system. Följande enheter och operativsystem stöds:  

- Windows 10

- Windows 10 Mobil

- Windows 8,1  

- Windows Phone 8.1  

> [!NOTE]  
> Använd Configuration Manager lokal MDM för att hantera Windows Phone 8,1 och Windows 10 Mobile. Mer information finns i [lokal MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Ett typiskt scenario för Configuration Manager är att installera betrodda certifikat från rot certifikat utfärdare för att autentisera Wi-Fi-och VPN-servrar. Vanliga anslutningar använder följande protokoll:

- Autentiseringsprotokoll: EAP-TLS, EAP-TTLS och PEAP
- Protokoll för VPN-tunnel: IKEv2, L2TP/IPsec och Cisco IPsec

Ett företags certifikat från en rot certifikat utfärdare måste installeras på enheten innan enheten kan begära certifikat med hjälp av en SCEP-certifikat profil.  

Du kan ange inställningar i en SCEP-certifikat profil för att begära anpassade certifikat för olika miljöer eller anslutnings krav. **Guiden Skapa certifikat profil** har två sidor för registrerings parametrar. Den första, **SCEP-registreringen**innehåller inställningar för registreringsbegäran och var certifikatet ska installeras. Den andra, **Certifikategenskaper**, beskriver det begärda certifikatet.  

## <a name="deploy"></a>Distribuera

När du distribuerar en SCEP-certifikat profil bearbetar den Configuration Manager klienten principen. Den begär sedan ett SCEP-utmanings lösen ord från hanterings platsen. Enheten skapar ett offentligt/privat nyckel par och genererar en certifikat signerings förfrågan (CSR). Den skickar denna begäran till NDES-servern. NDES-servern vidarebefordrar begäran till certifikat registrerings platsens plats system via NDES-principmodulen. Certifikat registrerings platsen verifierar begäran, kontrollerar SCEP-utmaningens lösen ord och kontrollerar att begäran inte har ändrats. Den godkänner eller nekar sedan begäran. Om den godkänns skickar NDES-servern signerings förfrågan till den anslutna certifikat utfärdaren (CA) för signering. CA: n signerar begäran och returnerar sedan certifikatet till den begär ande enheten.

Distribuera certifikat profiler till användar-eller enhets samlingar. Du kan ange mål arkivet för varje certifikat. Tillämplighets regler avgör om enheten kan installera certifikatet.

När du distribuerar en certifikat profil till en användar samling avgör [mappningen mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) vilken av användarnas enheter som installerar certifikaten. När du distribuerar en certifikat profil med ett användar certifikat till en enhets samling installerar certifikaten som standard var och en av användarnas primära enheter. Om du vill installera certifikatet på någon av användarnas enheter ändrar du det här beteendet på sidan **SCEP-registrering** i **guiden Skapa certifikat profil**. Om enheterna finns i en arbets grupp kan Configuration Manager inte distribuera användar certifikat.  

## <a name="monitor"></a>Övervaka

Du kan övervaka distributioner av certifikat profiler genom att visa resultat för efterlevnad eller rapporter. Mer information finns i [så här övervakar du certifikat profiler](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Automatisk åter kallelse

Configuration Manager automatiskt återkalla användar-och dator certifikat som har distribuerats med hjälp av certifikat profiler under följande omständigheter:  

- Enheten dras tillbaka från Configuration Manager hantering.  

- Enheten är blockerad från Configuration Manager-hierarkin.  

För att återkalla certifikaten skickar platsservern ett återkallningskommando till certifikatutfärdaren. Orsaken till återkallningen är **Åtgärdsavbrott**.

> [!NOTE]
> Om du vill återkalla ett certifikat korrekt måste dator kontot för platsen på den översta nivån i hierarkin ha behörighet att **utfärda och hantera certifikat** på certifikat utfärdaren.
>
> För ökad säkerhet kan du också begränsa CA-hanterare på CA: n. Ge bara det här kontot behörighet till den angivna certifikat mal len som du använder för SCEP-profilerna på webbplatsen.

## <a name="next-steps"></a>Nästa steg

- [Skapa certifikatprofiler](create-certificate-profiles.md)

- [Konfigurera infrastrukturen för certifikat](certificate-infrastructure.md)