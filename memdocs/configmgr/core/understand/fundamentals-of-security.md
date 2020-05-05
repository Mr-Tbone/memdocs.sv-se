---
title: Grunderna i säkerhet
titleSuffix: Configuration Manager
description: Lär dig mer om säkerhets lagren i Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722839"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Grundläggande säkerhet för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln sammanfattas följande grundläggande säkerhets komponenter i Configuration Managers miljö:
- [Säkerhetslager](#bkmk_layers)
- [Rollbaserad administration](#bkmk_rba)
- [Säkra klientslutpunkter](#bkmk_endpoints)
- [Konton och grupper i Configuration Manager](#bkmk_accounts)
- [Sekretess](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a>Säkerhets lager

Säkerhet för Configuration Manager består av följande skikt: 
- [Windows operativ system och nätverks säkerhet](#bkmk_layer-windows)
- [Nätverks infrastruktur: brand väggar, intrångs identifiering, PKI (Public Key Infrastructure)](#bkmk_layer-network)
- [Configuration Manager säkerhets kontroller](#bkmk_layer-cm)
- [SMS-provider](#bkmk_layer-provider)
- [Behörigheter för plats databas](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a>Windows operativ system och nätverks säkerhet
Det första lagret tillhandahålls av Windows säkerhetsfunktioner för både operativ systemet och nätverket. Det här lagret innehåller följande komponenter:  

-   Fildelning för att överföra filer mellan Configuration Manager-komponenter  

-   Åtkomstkontrollistor för att säkra filer och registernycklar  

-   Internet Protocol säkerhet (IPsec) för att skydda kommunikation  

-   grupprincip att ange säkerhets princip  

-   DCOM-behörigheter (Distributed Component Object Model) för distribuerade program, till exempel Configuration Manager-konsolen  

-   Active Directory Domain Services för lagring av säkerhetsobjekt  

-   Säkerhet för Windows-konto, inklusive vissa grupper som Configuration Manager skapar under installationen  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a>Nätverks infrastruktur

Ytterligare säkerhets komponenter, som brand väggar och intrångs identifiering, hjälper till att ge skydd för hela miljön. Certifikat som utfärdas av PKI-implementeringar (Public Key Infrastructure) som är bransch standard tillhandahåller autentisering, signering och kryptering.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a>Configuration Manager säkerhets kontroller

Utöver den säkerhet som tillhandahålls av Windows Server-och nätverks infrastrukturen, Configuration Manager kontrol lera åtkomsten till konsolen och resurserna på flera olika sätt. Som standard har bara lokala administratörer behörighet till de filer och register nycklar som Configuration Manager-konsolen kräver på datorer där du installerar den.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a>SMS-provider

Nästa säkerhetslager baseras på åtkomst via WMI (Windows Management Instrumentation), specifikt SMS-providern. SMS-providern är en Configuration Manager-komponent som ger en användare behörighet att fråga plats databasen efter information. Åtkomsten till providern är som standard begränsad till medlemmar i den lokala SMS Admins -gruppen. Den här gruppen innehåller först endast den användare som installerade Configuration Manager. Om du vill bevilja andra konton behörighet till CIM-databasen (Common Information Model) och SMS-providern lägger du till de andra kontona i gruppen SMS-administratörer.  

Från och med version 1810 kan du ange den lägsta autentiseringsnivån som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. <!--1357013-->  

Mer information finns i [Planera för SMS-providern](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a>Behörigheter för plats databas

Det sista säkerhetslagret baseras på behörighet till objekt i platsdatabasen. Som standard kan det lokala system kontot och användar kontot som du använde för att installera Configuration Manager administrera alla objekt i plats databasen. Bevilja och begränsa behörigheter till ytterligare administrativa användare i Configuration Manager-konsolen med hjälp av rollbaserad administration.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>Rollbaserad administration  

 Configuration Manager använder rollbaserad administration för att skydda objekt som samlingar, distributioner och platser. Den här administrationsmodellen definierar och hanterar centralt säkerhetsåtkomstinställningar i hela hierarkin för alla platser och platsinställningar. 

 En administratör tilldelar *säkerhets roller* till administrativa användare och grupp behörigheter. Behörigheterna är anslutna till olika Configuration Manager objekt typer, till exempel för att skapa eller ändra klient inställningar. 

 *Säkerhets omfattningar* grupperar specifika instanser av objekt som en administrativ användare ansvarar för att hantera, till exempel ett program som installerar Microsoft Office. 

 Kombinationen av säkerhets roller, säkerhets omfattningar och samlingar definierar de objekt som en administrativ användare kan visa och hantera. Configuration Manager installerar vissa standard säkerhets roller för vanliga hanterings uppgifter. Skapa dina egna säkerhets roller för att stödja dina specifika affärs behov.  

 Mer information finns i [Konfigurera rollbaserad administration](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a>Säkra klient slut punkter  

 Configuration Manager skyddar klient kommunikationen till plats system roller genom att använda antingen självsignerade eller PKI-certifikat eller Azure Active Directory (Azure AD) tokens. Vissa scenarier kräver användning av PKI-certifikat. Till exempel [Internetbaserad klient hantering](../clients/manage/plan-internet-based-client-management.md)och för [mobila enhets klienter](../../mdm/plan-design/plan-on-premises-mdm.md).  

 Du kan konfigurera de plats system roller som klienterna ansluter till för HTTPS-eller HTTP-klient kommunikation. Klient datorer kommunicerar alltid med den säkraste metoden som är tillgänglig. Klient datorer kan bara återgå till att använda mindre säker kommunikations metod om du har plats system roller som tillåter HTTP-kommunikation.  

 Mer information finns i [Planera för säkerhet](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a>Configuration Manager konton och grupper  

 Configuration Manager använder det lokala system kontot för de flesta plats åtgärderna. Vissa hanterings uppgifter kan kräva att du skapar och underhåller ytterligare konton. Configuration Manager skapar flera standard grupper och SQL Server roller under installationen. Du kan behöva manuellt lägga till dator-eller användar konton i standard grupperna och SQL Server roller.  

 Mer information finns i [konton som används i Configuration Manager](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a>Säkerhets  

 Innan du implementerar Configuration Manager bör du tänka igenom dina sekretess krav. Även om företags hanterings produkter erbjuder många fördelar eftersom de effektivt kan hantera många klienter, kan den här program varan påverka sekretessen för användare i din organisation. Configuration Manager innehåller många verktyg för insamling av data och övervakning av enheter. Vissa verktyg kan ge upphov till sekretess problem i din organisation.  

 När du till exempel installerar Configuration Manager-klienten, aktiverar den många hanterings inställningar som standard. Den här konfigurationen gör att klient program varan skickar information till Configuration Manager-platsen. Platsen lagrar klient information i plats databasen. Klient informationen skickas inte direkt till Microsoft. Mer information finns i [diagnostik-och användnings data](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Se även

- [Planera för säkerhet](../plan-design/security/plan-for-security.md)  

- [Säkerhet och sekretess för Configuration Manager-klienter](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurera säkerhet](../plan-design/security/configure-security.md)   

- [Kommunikation mellan slut punkter](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Teknisk referens för kryptografiska kontroller](../plan-design/security/cryptographic-controls-technical-reference.md)  
