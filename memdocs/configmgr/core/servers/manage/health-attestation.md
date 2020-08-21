---
title: Hälsoattestering
titleSuffix: Configuration Manager
description: Lär dig mer om Hälsoattestering för enhet funktioner som visas i Configuration Manager-konsolen.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d57be201274c347e5dcd492734b2141c64d579b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700018"
---
# <a name="health-attestation-for-configuration-manager"></a>Hälsoattestering för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Administratörer kan visa statusen för [hälsoattesteringen av Windows 10-enheten](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) i Configuration Manager-konsolen.  Med hälsoattestering för enheten kan administratörer se till att klientdatorer har följande tillförlitliga konfigurationer av BIOS, TPM och startprogram aktiverade:  

-   Tidig start av program mot skadlig kod – Tidig start av program mot skadlig kod (ELAM) skyddar datorn när den startas och innan drivrutiner från tredje part initieras. [Aktivera ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker – Windows BitLocker-diskkryptering är programvara som gör att du kan kryptera alla data som lagras på Windows-operativsystemsvolymen.  [Aktivera BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Säker start – Säker start är en säkerhetsstandard som utvecklats av medlemmar av datorindustrin för att säkerställa att datorn startas med programvara som är betrodd av datortillverkaren. [Mer information om Säker start](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Kodintegritet – Kodintegritet är en funktion som förbättrar säkerheten för operativsystemet genom att verifiera integriteten hos en drivrutin eller systemfil varje gång den läses in i minnet. [Lär dig mer om Kodintegritet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Den här funktionen är tillgänglig för datorer och lokala resurser som hanteras av Configuration Manager och mobila enheter med Microsoft Intune. Administratörer kan ange om rapportering sker via molnet eller lokala infrastrukturer. Med den lokala kontrollen över hälsoattestering av enheter kan administratören övervaka klient datorer utan Internet åtkomst.

## <a name="enable-health-attestation"></a>Aktivera hälsoattestering

 **Signaturkrav**  

-   Klient enheter som kör Windows 10 version 1607 eller Windows Server 2016 version 1607 med [Hälsoattestering för enhet aktiverat](/windows-server/security/device-health-attestation).
-   TPM 1,2 eller TPM 2-aktiverade enheter.
-   När du använder moln hantering, kommunicerar kommunikationen mellan Configuration Manager klient agenten och hanterings platsen med *has.spserv.Microsoft.com* (port 443) tjänsten för hälso tillstånds attestering (Cloud Management). När den är lokalt måste klienten kunna kommunicera med hanterings platsen för enhetens hälsoattestering.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivera kommunikation av hälsoattesteringstjänsten på Configuration Manager-klientdatorer

Använd den här proceduren för att aktivera övervakning av enhetens hälsoattestering för enheter som ansluter till Internet.

1.  I Configuration Manager-konsolen väljer du **Administration**  >  **Översikt**  >  **klient inställningar**.  Välj fliken för **Datoragent** -inställningar.  
2.  I dialogrutan **Standardinställningar** väljer du **Datoragent** och rullar ned till **Aktivera kommunikation med tjänsten för hälsoattestering**.  
3.  Ställ in **Aktivera kommunikation med hälsoattesteringstjänsten** till **Ja**och klicka sedan på **OK**.  
4. Rikta in dig på de enhets samlingar som ska rapportera enhetens hälso tillstånd.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivera lokal kommunikation av hälsoattesteringstjänsten på Configuration Manager-klientdatorer
Använd den här proceduren för att aktivera övervakning av hälsoattestering för enheter för lokala enheter som inte ansluter till Internet.

Från och med Configuration Manager 1702 kan webb adressen för den lokala enhetens hälsoattesterings tjänst konfigureras på hanterings platsen så att den stöder klient enheter utan Internet åtkomst.

1. I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **plats konfiguration**  >  **platser**.
2. Högerklicka på den primära eller sekundära platsen med hanterings platsen som stöder lokala hälsoattesteringar för enheter och välj **Konfigurera plats komponenter**  >  **hanterings plats**. Sidan **Egenskaper för hanterings plats komponent** öppnas.
3. På fliken **Avancerade alternativ** väljer du **Lägg till** och anger en giltig webb adress till tjänst för lokal hälsoattestering för enhet. Du kan lägga till flera URL: er. Om flera lokala webb adresser anges får klienterna den fullständiga uppsättningen och väljer slumpmässigt vilken som ska användas.
4.  I Configuration Manager-konsolen väljer du **Administration**  >  **Översikt**  >  **klient inställningar**.  Välj fliken för **Datoragent** -inställningar.  
5.  Rulla ned för att **Aktivera kommunikation med tjänsten hälsoattestering**och Ställ in på **Ja**.
7.  Klicka på alternativet **Använd lokal Health Attestaion-tjänst** och Ställ in på **Ja**.
8. Rikta in dig på de enheter som ska rapportera enhetens hälso tillstånd med inställningarna för klient agenten för att aktivera rapportering av hälsoattestering för enhet.

Du kan också **redigera** eller **ta bort** webb adresser för tjänsten hälsoattestering för enhet.

> [!NOTE]
> Om du har använt hälsoattestering för enhet innan du uppgraderar till Configuration Manager 1702, fylls de lokala URL: erna som anges i klient agent inställningarna i förväg i hanterings platsens egenskaper under uppgraderingen. Lokala klienter fortsätter att använda den URL som anges i klient agent inställningarna tills de uppgraderas. De växlar sedan till en av de URL: er som anges på hanterings platsen.

## <a name="monitor-device-health-attestation"></a>Övervaka hälsoattestering för enhet

1.  Om du vill visa hälsoattesteringsvyn i Configuration Manager-konsolen, går du till arbetsytan **Övervakning** . Klicka sedan på noden **Säkerhet** och sedan på **Hälsoattestering**.  
2.  Enhetens hälsoattestering visas.  

Configuration Manager-hälsoattesteringen för enheten visar följande:  

-   **Hälsoattesteringsstatus** – Visar status för andelen enheter med kompatibel, inkompatibel och okänd status samt med fel  
-   **Enheter som rapporterar hälsoattestering** – Visar procentandelen enheter som rapporterar hälsoattesteringsstatus  
-   **Inkompatibla enheter efter klienttyp** – Visar andelen mobila enheter och datorer som inte är kompatibla  
-   **Vanliga orsaker till saknad hälsoattestering** – Visar antalet enheter som saknar inställningen för hälsoattestering, enligt inställningen