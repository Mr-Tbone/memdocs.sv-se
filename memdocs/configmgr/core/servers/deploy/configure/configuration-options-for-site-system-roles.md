---
title: Alternativ för plats system roll
titleSuffix: Configuration Manager
description: I den här artikeln finns information om Configuration Manager plats system roller som inte nödvändigt vis är själv för klar Ande.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721089"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Konfigurations alternativ för plats system roller i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

De flesta konfigurations alternativ för Configuration Manager plats system roller är själv för klar ande eller förklaras i guiden eller dialog rutorna när du konfigurerar dem. I följande avsnitt beskrivs plats system roller vars inställningar kan kräva ytterligare information.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a>Plats för program katalog  

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Mer information om hur du konfigurerar webbplatsen för program katalogen finns i [Planera för och konfigurera program hantering](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a>Webb service punkt för program katalog  

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Mer information om hur du konfigurerar Programkatalog webb tjänst punkt finns i [Planera för och konfigurera program hantering](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a>Certifikat registrerings plats  

Mer information om hur du konfigurerar certifikat registrerings platsen finns i [Introduktion till certifikat profiler](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a>Distributions plats  

Mer information om hur du konfigurerar distributions platsen för innehålls distribution finns i [Hantera innehåll och innehålls infrastruktur](manage-content-and-content-infrastructure.md).  

Mer information om hur du konfigurerar distributions platsen för PXE-distributioner finns i [använda PXE för att distribuera Windows via nätverket](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Mer information om hur du konfigurerar distributions platsen för multicast-distributioner finns i [använda multicast för att distribuera Windows via nätverket](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installera och konfigurera IIS om det krävs av Configuration Manager

Välj det här alternativet om du vill låta Configuration Manager installera och konfigurera IIS på plats systemet om det inte redan är installerat. IIS måste vara installerat på alla distributions platser och du måste välja den här inställningen för att fortsätta i guiden.  

### <a name="site-system-installation-account"></a>Konto för installation av plats system

För distributions platser som är installerade på en plats Server stöds endast dator kontot för plats servern för användning som konto för installation av plats system. Mer information finns i [konton](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a>Registrerings plats  

Registrerings platser används för att installera macOS-datorer och registrera enheter som du hanterar med lokal hantering av mobila enheter. Mer information finns i följande artiklar:  

- [Distribuera klienter på Mac-datorer](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Hur användare registrerar enheter med lokal MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Tillåtna anslutningar

HTTPS-inställningen väljs automatiskt och kräver ett PKI-certifikat på servern för serverautentisering till proxyn för registrerings platsen och kryptering av data via SSL. Mer information finns i [krav för PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

Ett exempel på distribution av Server certifikatet och information om hur du konfigurerar det i IIS finns i [distribuera webb Server certifikatet för plats system som kör IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a>Proxy för registrerings plats  

Mer information om hur du konfigurerar en proxy för registrerings plats för mobila enheter finns i [hur användare registrerar enheter med lokal MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### <a name="client-connections"></a>Klientanslutningar

HTTPS-inställningen väljs automatiskt. Det kräver följande PKI-certifikat på servern:

- För serverautentisering till mobila enheter och Mac-datorer som du registrerar med Configuration Manager
- För kryptering av data över Secure Sockets Layer (SSL)

Mer information om certifikat kraven finns i krav för [PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

Ett exempel på distribution av Server certifikatet och information om hur du konfigurerar det i IIS finns i [distribuera webb Server certifikatet för plats system som kör IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a>Återställnings status punkt  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Antal tillstånds meddelanden och begränsnings intervall (i sekunder)

Standardinställningarna för de här alternativen är 10 000 tillstånds meddelanden och 3 600 sekunder för begränsnings intervallet. Även om dessa inställningar är tillräckliga i de flesta fall kan du behöva ändra dem när båda följande villkor uppfylls:  

- Återställnings status punkten accepterar bara anslutningar från intranätet.  

- Du använder återställnings status platsen under en distribution av klient distributioner för många datorer.  

I det här scenariot kan en kontinuerlig ström med tillstånds meddelanden skapa en efter släpning av tillstånds meddelanden som orsakar hög processor användning på plats servern under en varaktig period. Dessutom kanske du inte ser uppdaterad information om klient distributionen i Configuration Manager-konsolen och i klient distributions rapporterna.  

Dessa inställningar för återställnings status punkter är utformade för att konfigureras för tillstånds meddelanden som genereras under klient distributionen. Inställningarna är inte utformade för att ställas in för klient kommunikations problem, t. ex. När klienter på Internet inte kan ansluta till sin internetbaserade hanterings plats. Eftersom återställnings status punkten inte kan tillämpa inställningarna till tillstånds meddelanden som genereras under klient distributionen, ska du inte konfigurera inställningarna när återställnings status punkten accepterar anslutningar från Internet.  

Varje dator som installerar Configuration Manager klienten skickar följande fyra tillstånds meddelanden till återställnings status punkten:  

- Klient distributionen startade  

- Klient distributionen lyckades  

- Klient tilldelningen startade  

- Klient tilldelningen lyckades  

Datorer som inte kan installeras eller som tilldelar Configuration Manager klienten skickar ytterligare tillstånds meddelanden.  

Om du till exempel distribuerar Configuration Manager-klienten till 20 000 datorer, kan distributionen skicka 80 000-tillstånds meddelanden till återställnings status platsen. Eftersom standard begränsnings konfigurationen låter 10 000 tillstånds meddelanden skickas till återställnings status punkten varje 3 600 sekunder (1 timme) kan tillstånds meddelanden bli eftersläpande vid återställnings status platsen. Överväg också den tillgängliga nätverks bandbredden mellan återställnings status platsen och plats servern och plats serverns bearbetnings kraft för att bearbeta många tillstånds meddelanden.  

För att förhindra dessa problem bör du överväga en ökning av antalet tillstånds meddelanden och en minskning av begränsnings intervallet.  

Återställ begränsnings värden för återställnings status punkten om något av följande villkor är uppfyllt:  

- Du beräknar att de aktuella begränsnings värdena är högre än vad som krävs för att bearbeta status meddelanden från återställnings status platsen.  

- Du ser att de aktuella begränsnings inställningarna skapar hög processor användning på plats servern.  

Ändra inte inställningarna för begränsnings inställningarna för återställnings status punkten om du inte förstår konsekvenserna. Om du till exempel ökar begränsnings inställningarna till hög, kan processor användningen på plats servern öka till hög, vilket saktar ned alla plats åtgärder.  
