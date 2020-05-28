---
title: Internetbaserad klienthantering
titleSuffix: Configuration Manager
description: Skapa en plan för att hantera Internetbaserade klienter i Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587215"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Planera för internetbaserad klient hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd Internetbaserad klient hantering (IBCM) för att hantera Configuration Manager-klienter när de inte är anslutna till det interna nätverket. Fördelar med att använda IBCM:

- Fullständig kontroll över servrar och roller som tillhandahåller tjänsten
- Inget beroende för moln tjänst
- Kan inte kräva ett virtuellt privat nätverk (VPN)
- Alla kostnader är kopplade till den lokala tjänsten

På grund av de högre säkerhets kraven för att hantera klient datorer i ett offentligt nätverk kräver IBCM att PKI-certifikat används. Den här konfigurationen säkerställer att anslutningarna autentiseras av en oberoende auktoritet. När IBCM-klienter och-plats servrar skickar data är de krypterade och säkra.  

## <a name="client-communications"></a>Klientkommunikation

Följande plats system roller på primära platser stöder anslutningar från klienter som finns på ej betrodda platser:

> [!NOTE]
> Medan IBCM främst fokuserar på det Internetbaserade scenariot gäller samma beteenden för klienter i en skog som inte är betrodd Active Directory. Sekundära platser stöder inte klient anslutningar från ej betrodda platser.

- Certifikat registrerings plats för NDES (Configuration Manager-principmodul)

- Distributionsplats

- Molnbaserad distributionsplats

- Registreringsproxyplats

- Status för återställningsplats

- Hanteringsplats

- Programuppdateringsplats

> [!NOTE]
> Stöd avslutades för program katalog roller med version 1910. Mer information finns i [ta bort program katalogen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). För Configuration Manager version 1906 och tidigare som fortfarande ingår i supporten kan program katalogens webbplats plats godkänna anslutningar från Internetbaserade klienter.

### <a name="about-internet-facing-site-systems"></a>Om plats system som riktas mot Internet

Det finns inget krav på att ha ett förtroende mellan en klients skog och plats system servern. Men när den skog som innehåller ett Internet-riktat plats system litar på den skog som innehåller användar kontona, stöder den här konfigurationen användarbaserade principer för enheter på Internet när du aktiverar klient **princip** klient inställningen **Aktivera användar princip begär Anden från Internet klienter**.

Till exempel illustrerar följande konfigurationer när IBCM stöder användar principer för enheter på Internet:

- Den Internetbaserade hanterings platsen finns i perimeternätverket. Nätverket har också en skrivskyddad domänkontrollant för att autentisera användaren. En brand vägg mellan perimeternätverket och interna nätverk tillåter Active Directory paket.

- Användar kontot finns i den intranätbaserade skogen. Den Internetbaserade hanterings platsen finns i den perimeter-baserade skogen. Perimeter-skogen litar på den interna skogen. En brand vägg mellan perimeternätverket och interna nätverk tillåter autentisering av paket.

- Användar kontot och den Internetbaserade hanterings platsen finns både i den intranätbaserade skogen. Du publicerar hanterings platsen på Internet med en webbproxyserver.

### <a name="use-a-web-proxy-server"></a>Använd en webbproxyserver

Du kan placera Internetbaserade plats system i intranätet när du publicerar dem på Internet med en webbproxyserver. Konfigurera dessa plats system för klient anslutningar från Internet, eller klient anslutningar från Internet och intranätet. När du använder en webbproxyserver kan du konfigurera den för Secure Sockets Layer (SSL) bryggning till SSL eller SSL-tunnlar.

#### <a name="ssl-bridging-to-ssl"></a>SSL-bryggning till SSL

SSL-bryggning till SSL är den rekommenderade och säkrare konfigurationen, eftersom den använder SSL-avslutning med autentisering. Den autentiserar klient datorer med datorautentisering. Mobila enheter som du registrerar med Configuration Manager inte stöder SSL-bryggning.

Med SSL-avslutning på proxyn kontrollerar den om det finns paket från Internet innan de vidarebefordras till det interna nätverket. Proxyservern autentiserar anslutningen från klienten, avslutar den och öppnar sedan en ny autentiserad anslutning till de Internetbaserade plats systemen. När Configuration Manager klienter använder en proxyserver, innehåller klienten en säker identitet (GUID) i paketets nytto Last. Hanterings platsen betraktar inte proxyservern som klient. Configuration Manager stöder inte bryggning med HTTP till HTTPS, eller från HTTPS till HTTP.

> [!NOTE]
> Configuration Manager stöder inte konfiguration av konfigurationer för SSL-bryggning från tredje part. Till exempel Citrix NetScaler eller F5 BIG-IP. Arbeta med enhets leverantören och konfigurera den för användning med Configuration Manager.

#### <a name="tunneling"></a>Tunneltrafik

Om din proxyserver inte stöder kraven för SSL-bryggning Configuration Manager även stöd för SSL-tunnlar. Du kan också använda SSL-tunnlar för att stödja mobila enheter som du registrerar med Configuration Manager. Det är ett mindre säkert alternativ eftersom proxyn vidarebefordrar SSL-paketen från Internet till plats systemen utan SSL-avslutning. Proxyn kontrollerar inte paketen för skadligt innehåll. När du använder SSL-tunneltrafik finns det inga certifikatkrav för proxywebbservern.

## <a name="plan-for-internet-based-clients"></a>Planera för Internetbaserade klienter

Bestäm om du vill konfigurera Internetbaserade klienter för hantering både på intranätet och på Internet, eller för klient hantering enbart för Internet. Du kan bara konfigurera hanterings alternativet under klient installationen. Installera om klienten om du vill ändra den senare.

> [!NOTE]
> Om du konfigurerar en hanterings plats så att den stöder Internetbaserade klienter, kommer klienter som ansluter till den här hanterings platsen att bli Internet-kompatibla när de uppdaterar listan över tillgängliga hanterings platser nästa gång.
>
> Du behöver inte begränsa konfigurationen av klient hantering enbart via Internet till Internet. Du kan också använda den i intranätet.

Klienter som du konfigurerar för endast Internet-hantering kommunicerar endast med de plats system som du konfigurerar för klient anslutningar från Internet. Använd den här konfigurationen i följande scenarier:

- För datorer som du vet aldrig kommer att ansluta till intranätet. Till exempel en plats för försäljnings datorer på fjärrplatser.
- Begränsa klient kommunikation till endast HTTPS. Till exempel för att stödja brand vägg och begränsade säkerhets principer.
- När du installerar Internetbaserade plats system i ett perimeternätverk och du vill hantera dessa servrar som Configuration Manager klienter.

> [!NOTE]
> När du vill hantera arbets grupps klienter på Internet måste du installera dem som enbart för Internet.
>
> När du konfigurerar en mobil enhet för att använda en Internetbaserad hanterings plats konfigureras den automatiskt som endast Internet.

Du kan konfigurera andra klienter för både Internet-och intranäts klient hantering. När de identifierar en nätverks förändring växlar de automatiskt mellan IBCM-och intranäts klient hantering. Om dessa klienter kan hitta och ansluta till en hanterings plats som har stöd för klient anslutningar på intranätet hanteras dessa klienter som intranäts klienter. Intranäts klienter har fullständig Configuration Manager funktion. Om klienterna inte kan hitta eller ansluta till en hanterings plats som har stöd för klient anslutningar på intranätet, försöker de ansluta till en Internetbaserad hanterings plats. Om den här åtgärden lyckas hanteras dessa klienter sedan av de Internetbaserade plats systemen på den tilldelade platsen.

Fördelen med automatisk växling är att klienter kan använda alla funktioner när de ansluter till intranätet och få viktig hantering när de är på Internet. Innehålls hämtning som börjar på Internet kan återupptas sömlöst i intranätet och på det andra sättet.

## <a name="prerequisites"></a>Förutsättningar

IBCM i Configuration Manager har följande beroenden:

- Klienter kräver en Internet anslutning. Configuration Manager använder enhetens befintliga Internet anslutning. Mobila enheter måste ha en direkt Internet anslutning. Fullständiga klient datorer kan ha antingen en direkt Internet anslutning eller ansluta med hjälp av en webb server för proxy.

- Plats system som stöder IBCM kräver en Internet anslutning och måste finnas i en Active Directory domän. De Internetbaserade plats systemen kräver ingen förtroende relation med Active Directory-skogen på plats servern. Om den Internetbaserade hanterings platsen kan autentisera användaren med hjälp av Windows-autentisering, stöder den dock användar principer. Om Windows-autentiseringen Miss lyckas stöder den endast enhets principer.

    > [!NOTE]
    > Om du vill ha stöd för användar principer aktiverar du även följande klient inställningar i **klient princip** gruppen:
    >
    > - **Aktivera avsökning av användarprinciper på klienter**
    > - **Aktivera användarprincipsbegäranden från Internetklienter**  

- En PKI (Public Key Infrastructure) för att distribuera och hantera de certifikat som krävs för Internetbaserade klienter och plats system servrar. Mer information finns i [krav för PKI-certifikat](../../plan-design/network/pki-certificate-requirements.md).

- Registrera offentliga DNS-värdnamn för Internet fullständigt kvalificerade domän namn (FQDN) för plats system som stöder IBCM.

### <a name="client-communication-requirements"></a>Krav för klient kommunikation

Mellanliggande brand väggar eller proxyservrar måste tillåta klient kommunikation för Internetbaserade plats system:

- Stöd för HTTP 1.1  

- Tillåt HTTP-innehållstypen för MIME-multipartsbilaga (multipart/blandad och program/oktett-ström)  

#### <a name="verbs"></a>Verb

Tillåt följande verb för de Internetbaserade plats system Server rollerna:

| Roll | Verb |
|------|-------|
| Hanteringsplats | -HEAD<br>-CCM_POST<br>-BITS_POST<br>- GET<br>-PROPFIND |
| Distributionsplats | -HEAD<br>- GET<br>-PROPFIND |
| Status för återställningsplats | POST |
| Plats för program katalog | -POST<br>– Hämta |

#### <a name="http-headers"></a>HTTP-rubriker

Tillåt följande HTTP-huvuden för den Internet-baserade plats system Server rollerna:

| Roll | HTTP-rubriker |
|------|--------------|
| Hanteringsplats | Intervall<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Distributionsplats | Intervall: |

Information om liknande kommunikations krav när du använder program uppdaterings platsen för klient anslutningar från Internet finns i dokumentationen för Windows Server Update Services (WSUS).

## <a name="unsupported-features"></a>Funktioner som inte stöds

Alla klient hanterings funktioner är inte lämpliga för Internet. Configuration Manager stöder inte vissa funktioner för klienter på Internet. Dessa funktioner som inte stöds förlitar sig vanligt vis på Active Directory Domain Services eller är inte lämpliga för ett offentligt nätverk.

Följande funktioner stöds inte när du hanterar klienter på Internet med IBCM:

- Klient distribution via Internet, t. ex. push-installation av klienter och klient distribution på program uppdatering. Använd manuell klient installation.

- Automatisk platstilldelning

- Wake-on-LAN

- OS-distribution. Du kan dock distribuera aktivitetssekvenser som inte distribuerar ett operativ system.

- Fjärrstyrning

- Program distribution till användare. Den här funktionen förlitar sig på program katalogen, som är föråldrad.

- Klient nätverks växling. Med nätverksväxling kan klienterna alltid lokalisera de närmaste distributionsplatserna för att hämta innehåll. Klienter som inte deterministiskt väljer ett av de Internetbaserade plats systemen, oavsett bandbredd eller fysisk plats.

När du konfigurerar en program uppdaterings plats för att godkänna anslutningar från Internet genomsöks alltid Internetbaserade klienter mot den här program uppdaterings platsen för att avgöra vilka program uppdateringar som krävs. När de här klienterna är på Internet försöker de först ladda ned program uppdateringarna från Microsoft Update, i stället för från en Internetbaserad distributions plats. Om det här beteendet Miss lyckas försöker de Ladda ned de nödvändiga program uppdateringarna från en Internetbaserad distributions plats.

> [!TIP]
> Configuration Manager klienten avgör automatiskt om den finns på intranätet eller Internet. Om klienten kan kontakta en domänkontrollant eller en lokal hanterings plats, anger den anslutnings typen till "för närvarande *intranät*". Annars växlar den till " *Internet*" och kommunicerar med de plats system som har tilldelats till platsen.
