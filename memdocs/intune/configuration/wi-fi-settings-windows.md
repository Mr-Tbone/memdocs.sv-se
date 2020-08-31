---
title: Wi-Fi-inställningar för Windows 10-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa Wi-Fi-konfigurationsprofil med hjälp av Wi-Fi-inställningar för Windows 10-enheter och senare enheter i Microsoft Intune. Du kan konfigurera grundläggande inställningar och inställningar på företagsnivå.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bfa28a6b4df30c6303f75d4a5cf91c20ce4e827
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820637"
---
# <a name="add-wi-fi-settings-for-windows-10-and-later-devices-in-intune"></a>Lägga till Wi-Fi-inställningar för Windows 10-enheter och senare enheter i Microsoft Intune

Du kan skapa en profil med specifika inställningar för WiFi. Distribuera sedan profilen till dina enheter med Windows 10 och senare. Microsoft Intune innehåller många funktioner, inklusive autentisering till ditt nätverk med en i förväg delad nyckel och mycket mer.

Den här artikeln beskriver dessa inställningar.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetsprofil](wi-fi-settings-configure.md).

## <a name="basic-profile"></a>Grundläggande profil

Grundläggande eller personliga profiler använder WPA/WPA2 till att skydda Wi-Fi-anslutningen på enheter. Normalt används WPA/WPA2 i hemnätverk eller personliga nätverk. Du kan också lägga till en i förväg delad nyckel för att autentisera anslutningen.

- **Wi-Fi-typ**: Välj **Basic**. 

- **Namn på Wi-Fi (SSID)** : Förkortning för Service Set Identifier. Det här värdet är det verkliga namnet på det trådlösa nätverk som enheterna ansluter till. Användarna ser dock bara det **anslutningsnamn** som du konfigurerar när de väljer anslutningen.

- **Anslutningens namn**: Ange ett användarvänligt för den här Wi-Fi-anslutningen. Den text som du anger är det namn som användarna ser när de bläddrar i tillgängliga anslutningar på sin enhet.

- **Anslut automatiskt när nätverket kan nås**: När det här är **Ja** ansluter enheter automatiskt när de är inom räckvidden för det här nätverket. När det är **No** (Nej) ansluter enheter inte automatiskt.

  - **Anslut till ett mer prioriterat nätverk om det är tillgängligt**: Om enheterna är inom räckvidden för ett mer prioriterat nätverk väljer du **Ja** för att använda det föredragna nätverket. Välj **No** (Nej) om du vill använda Wi-Fi-nätverket i den här konfigurationsprofilen.

    Exempelvis kan du skapa ett Wi-Fi-nätverk med namnet **ContosoCorp** och använda **ContosoCorp** i konfigurationsprofilen. Du har även ett **ContosoGuest**-Wi-Fi-nätverk inom räckvidd. När företagets enheter är inom räckvidd vill du att de automatiskt ska anslutas till **ContosoCorp**. I det här scenariot ställer du in egenskapen **Connect to more preferred network if available** (Anslut till ett mer prioriterat nätverk om det är tillgängligt) till **No** (Nej).

  - **Anslut till det här nätverket även om det inte sänder sitt SSID**: Välj **Ja** för att konfigurationsprofilen automatiskt ska ansluta till nätverket, även om nätverket är dolt (det vill säga att dess SSID inte sänds offentligt). Välj **No** (Nej) om du inte vill att den här konfigurationsprofilen ska ansluta till ditt dolda nätverk.

- **Gräns för anslutningar med datapriser**: En administratör kan välja hur nätverkstrafiken mäts. Program kan sedan justera sitt nätverkstrafiksbeteende baserat på den här inställningen. Alternativen är:

  - **Obegränsad**: Standard. Anslutningen är inte avgiftsbelagd och det finns inga trafikbegränsningar.
  - **Fast**: Använd det här alternativet om nätverket är konfigurerat med en fast gräns för nätverkstrafik. När den här gränsen har nåtts är nätverksåtkomst förbjuden.
  - **Variabel**: Använd det här alternativet om nätverkstrafiken debiteras per byte (kostnad per byte).

- **Trådlös säkerhetstyp**: Ange det säkerhetsprotokoll som används för att autentisera enheter i nätverket. Alternativen är:
  - **Öppet (ingen autentisering)** : Använd bara det här alternativet om nätverket är oskyddat.
  - **WPA/WPA2 – Personal**: Ett säkrare alternativ, som ofta används för Wi-Fi-anslutning. För ökad säkerhet kan du också ange lösenordet för en i förväg delad nyckel eller en nätverksnyckel.

    - **I förväg delad nyckel** (PSK): Valfritt. Visas när du väljer **WPA/WPA2-personligt** som säkerhetstyp. När nätverket är konfigurerat, konfigureras också ett lösenord eller en nätverksnyckel. Ange lösenordet eller nätverksnyckeln för PSK-värdet. Ange en sträng på mellan 8 och 64 tecken. Om lösenordet eller nätverksnyckeln är 64 tecken, anger du hexadecimala tecken.

      > [!IMPORTANT]
      > PSK är detsamma för alla enheter som du riktar profilen till. Om nyckeln har komprometterats kan den användas av vilken enhet som helst för att ansluta till Wi-Fi-nätverket. Skydda din PSK:er för att undvika obehörig åtkomst.

- **Företagets proxyinställningar**: Välj att använda proxyinställningarna i din organisation. Alternativen är:
  - **Inga**: Inga proxyinställningar konfigureras.
  - **Konfigurera manuellt**: Ange **proxyserverns IP-adress** och dess **portnummer**.
  - **Konfigurera automatiskt**: Ange URL:en som pekar på ett PAC-skript (Proxy Auto-Configuration). Ange till exempel `http://proxy.contoso.com/proxy.pac`.

## <a name="enterprise-profile"></a>Företagsprofil

Företagsprofiler använder EAP (Extensible Authentication Protocol) för autentisering av Wi-Fi-anslutningar. EAP används ofta av företag eftersom du kan använda certifikat till att autentisera och skydda anslutningar och konfigurera fler säkerhetsalternativ.

- **Wi-Fi-typ**: Välj **Företag**.

- **Namn på Wi-Fi (SSID)** : Förkortning för Service Set Identifier. Det här värdet är det verkliga namnet på det trådlösa nätverk som enheterna ansluter till. Användarna ser dock bara det **anslutningsnamn** som du konfigurerar när de väljer anslutningen.

- **Anslutningens namn**: Ange ett användarvänligt för den här Wi-Fi-anslutningen. Den text som du anger är det namn som användarna ser när de bläddrar i tillgängliga anslutningar på sin enhet.

- **Anslut automatiskt när nätverket kan nås**: När det här är **Ja** ansluter enheter automatiskt när de är inom räckvidden för det här nätverket. När det är **No** (Nej) ansluter enheter inte automatiskt.
  - **Anslut till ett mer prioriterat nätverk om det är tillgängligt**: Om enheterna är inom räckvidden för ett mer prioriterat nätverk väljer du **Ja** för att använda det föredragna nätverket. Välj **No** (Nej) om du vill använda Wi-Fi-nätverket i den här konfigurationsprofilen.

    Exempelvis kan du skapa ett Wi-Fi-nätverk med namnet **ContosoCorp** och använda **ContosoCorp** i konfigurationsprofilen. Du har även ett **ContosoGuest**-Wi-Fi-nätverk inom räckvidd. När företagets enheter är inom räckvidd vill du att de automatiskt ska anslutas till **ContosoCorp**. I det här scenariot ställer du in egenskapen **Connect to more preferred network if available** (Anslut till ett mer prioriterat nätverk om det är tillgängligt) till **No** (Nej).

- **Anslut till det här nätverket även om det inte sänder sitt SSID**: Välj **Ja** för att konfigurationsprofilen automatiskt ska ansluta till nätverket, även om nätverket är dolt (det vill säga att dess SSID inte sänds offentligt). Välj **No** (Nej) om du inte vill att den här konfigurationsprofilen ska ansluta till ditt dolda nätverk.

- **Gräns för anslutningar med datapriser**: En administratör kan välja hur nätverkstrafiken mäts. Program kan sedan justera sitt nätverkstrafiksbeteende baserat på den här inställningen. Alternativen är:

  - **Obegränsad**: Standard. Anslutningen är inte avgiftsbelagd och det finns inga trafikbegränsningar.
  - **Fast**: Använd det här alternativet om nätverket är konfigurerat med en fast gräns för nätverkstrafik. När den här gränsen har nåtts är nätverksåtkomst förbjuden.
  - **Variabel**: Använd det här alternativet om nätverkstrafiken debiteras per byte.

- **Enkel inloggning (SSO)** : Gör att du kan konfigurera enkel inloggning (SSO), där autentiseringsuppgifter delas för nätverksinloggning med dator och Wi-Fi. Alternativen är:
  - **Inaktivera**: Inaktiverar SSO-beteende. Användaren måste autentisera till nätverket separat.
  - **Aktivera innan användaren loggar in på enheten**: Använd enkel inloggning för att autentisera till nätverket precis före användarens inloggningsprocess.
  - **Aktivera när användaren har loggat in på en enhet**: Använd enkel inloggning för att autentisera till nätverket omedelbart efter användarens inloggningsprocess är klar.
  - **Längsta tid att autentisera före timeout**: Ange det maximala antalet sekunder att vänta före autentisering till nätverket, 1–120 sekunder.
  - **Tillåt Windows att fråga användaren om ytterligare autentiseringsuppgifter**: Om du väljer **Ja** tillåts Windows-systemet att fråga användaren om ytterligare autentiseringsuppgifter om autentiseringsmetoden som kräver det. Välj **Nej** för att dölja dessa frågor.

- **Aktivera cachelagring av Pairwise Master Key (PMK)** : Välj **Ja** för att cachelagra PMK:n som användes vid autentiseringen. Den här cachelagringen gör vanligtvis att autentisering till nätverket slutförs snabbare. Välj **Nej** för att framtvinga autentiseringshandskakningen vid anslutning till Wi-Fi-nätverket varje gång. Om du vill använda inställningen **Aktivera förautentisering** väljer du **Ja**.

  - **Längsta tid som en PMK lagras i cacheminnet**: Ange hur många minuter som en Pairwise Master Key (PMK) lagras i cacheminnet, 5–1440 minuter.
  - **Högsta antal PMK-nycklar lagrade i cachen**: Ange antalet nycklar som lagrade i cachen, från 1–255.

- **Aktivera förautentisering**: Förautentisering gör att profilen kan autentisera till alla åtkomstpunkter för nätverket i profilen före anslutning. Vid flyttning mellan åtkomstpunkter återansluter förautentisering användaren eller enheter snabbare. Välj **Ja** för att profilen ska autentisera till alla åtkomstpunkter för det här nätverket som ligger inom räckvidd. Välj **Nej** om du vill kräva att användaren eller enheten autentiserar till varje åtkomstpunkt separat.

  Om du vill använda den här inställningen väljer du **Ja** för **Aktivera cachelagring av Pairwise Master Key (PMK)** .

  - **Högsta antal förautentiseringsförsök**: Ange antalet försök för att förautentisera, från 1–16.

- **EAP-typ**: Välj EAP-typ (Extensible Authentication Protocol) för autentisering av skyddade trådlösa anslutningar. Alternativen är:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **Skyddad PEAP** (PEAP)

    **Ytterligare inställningar för EAP-TLS, EAP-TTLS och PEAP**:

    > [!NOTE]
    > Certifikatprofilerna SCEP och PKCS stöds när du använder en EAP-typ.

    **SERVERFÖRTROENDE**  

    - **Certifikatservernamn**: Använd med EAP-typerna **EAP-TLS**, **EAP-TTLS** eller **PEAP**. Ange ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). Om du anger den här informationen kan du hoppa över dialogrutan för dynamiskt förtroende som visas på användarenheter när de ansluter till Wi-Fi-nätverket.  

    - **Rotcertifikat för serververifiering**: Använd med EAP-typerna **EAP-TLS**, **EAP-TTLS** eller **PEAP**. Välj den betrodda rotcertifikatsprofil som ska användas för att autentisera anslutningen.  

    - **Identitetssekretess (yttre identitet)** : Använd med EAP-typen **PEAP**. Ange den text som ska skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.  

    - **Utför serververifiering i PEAP fas 1**: När värdet är **Ja** i PEAP-förhandlingsfas 1 validerar enheterna certifikatet och verifierar servern. Välj **Nej** för att blockera eller förhindra den här verifieringen. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

      Om du väljer **Ja** konfigurerar du även:

      **Inaktivera användaruppmaningar om att verifiera servern i PEAP fas 1**: När detta är **Ja** i PEAP-förhandlingsfas 1 visas inte uppmaningar som ber användare att auktorisera nya PEAP-servrar för betrodda certifikatutfärdare. Välj **Nej** för att visa uppmaningarna. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

    - **Kräv kryptografisk bindning**: **Ja** förhindrar anslutningar till PEAP-servrar som inte använder krypteringsbindning under PEAP-förhandlingen. **Nej** kräver inte kryptografibindning. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

    **KLIENTAUTENTISERING**

    - **Klientcertifikat för klientautentisering (identitetscertifikat)** : Använd med EAP-typen **EAP-TLS**. Välj den certifikatprofil som ska användas för att autentisera anslutningen.

    - **Autentiseringsmetod**: Använd med EAP-typen **EAP-TTLS**. Välj autentiseringsmetod för anslutningen:  

      - **Certifikat**: Välj det klientcertifikat som är det identitetscertifikat som presenteras för servern.
      - **Användarnamn och lösenord**: Ange en **Annan metod än EAP (inre identitet)** för autentisering. Alternativen är:

        - **Okrypterat lösenord (PAP)**
        - **Utmaningshandskakning (CHAP)**
        - **Microsoft CHAP (MS-CHAP)**
        - **Microsoft CHAP Version 2 (MS-CHAP v2)**

    - **Identitetssekretess (yttre identitet)** : Använd med EAP-typen **EAP-TTLS**. Ange den text som ska skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

- **Företagets proxyinställningar**: Välj att använda proxyinställningarna i din organisation. Alternativen är:
  - **Inga**: Inga proxyinställningar konfigureras.
  - **Konfigurera manuellt**: Ange **proxyserverns IP-adress** och dess **portnummer**.
  - **Konfigurera automatiskt**: Ange den URL som pekar till ett PAC-skript. Ange till exempel `http://proxy.contoso.com/proxy.pac`.

- **Tvinga Wi-Fi-profilen att följa FIPS-standarden (Federal Information Processing Standard)** : Välj **Ja** när du verifierar mot FIPS 140-2-standarden. Den här standarden krävs för alla amerikanska federala myndigheter som använder kryptografibaserade säkerhetssystem för att skydda känslig men ej klassificerad information som lagras digitalt. Välj **Nej** för att inte vara FIPS-kompatibel.

## <a name="use-an-imported-settings-file"></a>Använd en importerad inställningsfil

För alla inställningar som inte är tillgängliga i Intune kan du exportera Wi-Fi-inställningar från en annan Windows-enhet. Den här exporten skapar en XML-fil med alla inställningarna. Importera sedan den här filen i Intune och använd den som Wi-Fi-profilen. Se [Exportera och importera Wi-Fi-inställningar för Windows-enheter](wi-fi-settings-import-windows-8-1.md).

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör någonting. Kom ihåg att [tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

## <a name="more-resources"></a>Fler resurser

- [Windows 8.1 Wi-Fi-inställningar](wi-fi-settings-import-windows-8-1.md)
- [Översikt över Wi-Fi-inställningar](wi-fi-settings-configure.md), inklusive andra plattformar
