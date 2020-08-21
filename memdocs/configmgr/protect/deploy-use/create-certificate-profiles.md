---
title: Skapa SCEP-certifikatprofiler, eller
titleSuffix: Configuration Manager
description: Lär dig hur du använder certifikat profiler för att etablera hanterade enheter med de certifikat som de behöver
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f1ea48887f89cf06ed4b41d0de0dfc24e9d508
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697134"
---
# <a name="create-certificate-profiles"></a>Skapa certifikatprofiler

*Gäller för: Configuration Manager (aktuell gren)*

Använd certifikat profiler i Configuration Manager för att etablera hanterade enheter med de certifikat som de behöver för att få åtkomst till företagets resurser. Innan du skapar certifikat profiler konfigurerar du certifikat infrastrukturen enligt beskrivningen i [Konfigurera certifikat infrastruktur](certificate-infrastructure.md).  

> [!TIP]
> Överväg att flytta [arbets belastningen för **resurs åtkomst principer** ](../../comanage/workloads.md#resource-access-policies) till Intune för samhanterade enheter. Använd sedan Intune-principer för att hantera dessa certifikat. Mer information finns i [så här växlar du arbets belastningar](../../comanage/how-to-switch-workloads.md).

Den här artikeln beskriver hur du skapar certifikat profiler för betrodda rot-och Simple Certificate Enrollment Protocol (SCEP). Om du vill skapa PFX-certifikat profiler, se [skapa profiler för PFX-certifikat](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

Så här skapar du en certifikat profil:

1. Starta guiden Skapa certifikat profil.
1. Ange allmän information om certifikatet.
1. Konfigurera ett certifikat för betrodd certifikat utfärdare (CA).  
1. Konfigurera SCEP-certifikat information.  
1. Ange plattformar som stöds för certifikat profilen.

## <a name="start-the-wizard"></a>Starta guiden  

Så här startar du skapa certifikat profil:

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj sedan noden **certifikat profiler** .  

1. På fliken **Start** i menyfliksområdet väljer du **Skapa certifikat profil**i gruppen **skapa** .  

## <a name="general"></a>Allmänt

Gå till sidan **Allmänt** i guiden Skapa certifikatprofil och ange följande:  

- **Namn**: Ange ett unikt namn för certifikatprofilen. Använd högst 256 tecken.  

- **Beskrivning**: Ange en beskrivning som ger en översikt över certifikat profilen. Inkludera även annan relevant information som hjälper dig att identifiera den i Configuration Manager-konsolen. Använd högst 256 tecken.  

- Ange vilken typ av certifikat profil du vill skapa:

  - **Certifikat för betrodd certifikat utfärdare**: Välj den här typen om du vill distribuera en betrodd rot certifikat utfärdare (ca) eller ett mellanliggande CA-certifikat för att bilda en certifikat kedja när användaren eller enheten måste autentisera en annan enhet. Enheten kan exempelvis vara en RADIUS-server (Remote Authentication Dial-In User Service) eller en server för virtuellt privat nätverk (VPN).
  
    Du kan också konfigurera en certifikat profil för en betrodd certifikat utfärdare innan du kan skapa en SCEP-certifikatutfärdare. I det här fallet måste certifikatet från betrodd certifikat utfärdare för den certifikat utfärdare som utfärdar certifikatet till användaren eller enheten.  

  - **Simple Certificate Enrollment Protocol inställningar (SCEP)**: Välj den här typen om du vill begära ett certifikat för en användare eller enhet Simple Certificate Enrollment Protocol med roll tjänsten för registrerings tjänsten för nätverks enheter (NDES).

  - **Personal information Exchange PKCS #12 (pfx) inställningar – importera**: Välj det här alternativet om du vill importera ett PFX-certifikat. Mer information finns i [Importera PFX-certifikat profiler](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Personal information Exchange PKCS #12 (pfx) inställningar – skapa**: Välj det här alternativet om du vill bearbeta PFX-certifikat med en certifikat utfärdare. Mer information finns i [Skapa PFX-certifikat profiler](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Certifikat för betrodd certifikat utfärdare  

> [!IMPORTANT]  
> Innan du skapar en SCEP-certifikat profil konfigurerar du minst en certifikat profil för betrodd certifikat utfärdare.
>
> Om du ändrar något av dessa värden efter det att certifikatet har distribuerats, så begärs ett nytt certifikat:
>
> - Nyckel lagrings leverantör
> - Certifikatmallens namn
> - Certifikattyp
> - Format för namn på certifikatmottagare
> - Alternativt namn för certifikatmottagare
> - Certifikatets giltighetsperiod
> - Nyckel användning
> - Nyckel storlek
> - Förbättrad nyckel användning
> - Rot certifikat utfärdarens certifikat

1. Gå till sidan **Certifikat för betrodd certifikatutfärdare** i guiden Skapa certifikatprofil och ange följande:  

    - **Certifikat fil**: Välj **Importera**och bläddra sedan till certifikat filen.  

    - **Målarkiv**: För enheter som har flera certifikatarkiv väljer du i vilket arkiv certifikatet ska lagras. För enheter som bara har ett arkiv ignoreras den här inställningen.  

2. Använd **certifikatets tumavtryck** -värde för att kontrol lera att du har importerat rätt certifikat.  

## <a name="scep-certificates"></a>SCEP-certifikat

### <a name="1-scep-servers"></a>1. SCEP-servrar

På sidan **SCEP-servrar** anger du webbadresserna för NDES-servrarna som ska utfärda certifikat via SCEP. Du kan tilldela en NDES-URL automatiskt baserat på konfigurationen av certifikat registrerings platsen eller lägga till webb adresser manuellt.  

### <a name="2-scep-enrollment"></a>2. SCEP-registrering

Slutför sidan **SCEP-registrering** i guiden Skapa certifikat profil.

- **Återförsök**: Ange hur många gånger enheten automatiskt ska försöka skicka CERTIFIKATBEGÄRAN till NDES-servern. Den här inställningen stöder scenariot där en certifikats hanterare måste godkänna en certifikatbegäran innan den accepteras. Inställningen används vanligtvis i miljöer med hög säkerhet eller om du använder en fristående certifikatutfärdare i stället för en företagscertifikatutfärdare. Du kan också använda alternativet i testsyfte om du vill granska alternativen för certifikatförfrågan innan certifikatutfärdaren behandlar certifikatförfrågan. Använd det här alternativet med inställningen **Tid innan nytt försök (minuter)** .  

- **Tid innan nytt försök (minuter)**: Ange intervallet, i minuter, mellan varje registreringsförsök när du använder certifikatutfärdargodkännande innan certifikatutfärdaren behandlar certifikatförfrågan. Om du använder godkännande för hantering i testnings syfte anger du ett lågt värde. Sedan väntar du inte längre på att enheten ska försöka utföra certifikatbegäran igen efter att du godkänt begäran.

    Om du använder godkännande för hantering i ett produktions nätverk anger du ett högre värde. Detta gör att CA-administratören får tillräckligt med tid för att godkänna eller neka väntande godkännanden.  

- **Tröskelvärde för förnyelse (%)**: Ange i procent hur mycket av certifikatets giltighetstid som får återstå innan förfrågningar om förnyat certifikat görs.  

- **Nyckel lagrings leverantör (KSP)**: Ange var nyckeln till certifikatet ska lagras. Välj något av följande värden:  

  - **Installera till TPM (Trusted Platform Module) om tillgänglig**: Installerar nyckeln till TPM. Om TPM: en inte finns installeras nyckeln på lagringsprovidern för program varu nyckeln.  

  - **Installera till TPM (Trusted Platform Module), rapportera annars ett fel**: Installerar nyckeln till TPM. Om TPM-modulen inte finns går det inte att installera.  

  - **Installera på Windows Hello för företag, rapportera annars**ett problem: det här alternativet är tillgängligt för Windows 10-enheter. Det gör att du kan lagra certifikatet i Windows Hello för företag-butiken som skyddas av Multi-Factor Authentication. Mer information finns i [Windows Hello för företag](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Det här alternativet stöder inte smartkortsinloggning för den förbättrade nyckel användningen på sidan certifikat egenskaper.

  - **Installera till programvaruprovidern för nyckellagring**: Installerar nyckeln till programvaruprovidern för nyckellagring  

- **Enheter för certifikat registrering**: om du distribuerar certifikat profilen till en användar samling kan du bara tillåta certifikat registrering på användarens primära enhet eller på någon annan enhet som användaren loggar in på.

    Om du distribuerar certifikat profilen till en enhets samling kan du tillåta certifikat registrering enbart för enhetens primära användare eller för alla användare som loggar in på enheten.  

### <a name="3-certificate-properties"></a>3. certifikat egenskaper

Gå till sidan **Certifikategenskaper** i guiden Skapa certifikatprofil och ange följande:  

- **Certifikatmallens namn**: Välj namnet på en certifikatmall som du konfigurerade i NDES och lagt till i en utfärdande certifikat utfärdare. För att kunna bläddra till certifikatmallar måste ditt användar konto ha **Läs** behörighet för certifikat mal len. Om du inte kan **söka** efter certifikatet skriver du dess namn.  

  > [!IMPORTANT]
  > Om certifikatmallens namn innehåller icke-ASCII-tecken distribueras certifikatet inte. (Ett exempel på dessa tecken är från det kinesiska alfabetet.) För att kontrol lera att certifikatet har distribuerats måste du först skapa en kopia av certifikat mal len på certifikat utfärdaren. Byt sedan namn på kopian med ASCII-tecken.  

  - Om du *bläddrar* för att välja namnet på certifikat mal len fylls vissa fält på sidan automatiskt från certifikat mal len. I vissa fall kan du inte ändra dessa värden om du inte väljer en annan certifikatmall.  

  - Om du *skriver* in namnet på certifikat mal len kontrollerar du att namnet matchar exakt en av certifikatmallarna. Den måste matcha namnen som anges i registret på NDES-servern. Se till att du anger namnet på certifikat mal len och inte visnings namnet på certifikat mal len.  

    Bläddra till följande register nyckel för att hitta namnen på certifikatmallarna: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP` . Den listar certifikatmallarna som värden för **EncryptionTemplate**, **GeneralPurposeTemplate**och **SignatureTemplate**. Värdet för alla tre certifikatmallar är som standard **IPSECIntermediateOffline**vilket mappar till mallvisningsnamnet **IPSec (Offline request)**.  

    > [!WARNING]  
    > När du skriver in namnet på certifikat mal len kan Configuration Manager inte verifiera innehållet i certifikat mal len. Du kanske kan välja alternativ som certifikat mal len inte stöder, vilket kan resultera i en misslyckad certifikatbegäran. När detta inträffar visas ett fel meddelande för w3wp.exe i filen CPR. log att mallnamnet i certifikat signerings förfrågan (CSR) och utmaningen inte matchar.  
    >
    > När du skriver namnet på den certifikatmall som har angetts för **GeneralPurposeTemplate** -värdet väljer du alternativet **nyckelchiffrering** och den **digitala signaturen** för den här certifikat profilen. Om du bara vill aktivera alternativet **nyckelchiffrering** i den här certifikat profilen, anger du namnet på certifikat mal len för **EncryptionTemplate** -nyckeln. Och om du bara vill aktivera alternativet **Digital signatur** i den här certifikatprofilen, anger du certifikatmallnamnet för nyckeln **SignatureTemplate** .  

- **Certifikat typ**: Välj om du vill distribuera certifikatet till en enhet eller en användare.  

- **Ämnes namnets format**: välj hur Configuration Manager automatiskt skapar ämnes namnet i certifikat förfrågan. Om certifikatet avser en användare kan du ange användarens e-postadress i mottagarnamnet.

    > [!NOTE]  
    > Om du väljer **IMEI-nummer** eller **serie nummer**kan du skilja mellan olika enheter som ägs av samma användare. Dessa enheter kan till exempel dela ett eget namn, men inte ett IMEI-nummer eller serie nummer. Om enheten inte rapporterar ett IMEI-eller serie nummer utfärdas certifikatet med det egna namnet.

- **Alternativt namn**för certifikat mottagare: ange hur Configuration Manager automatiskt ska skapa värden för det alternativa certifikat mottagar namnet (San) i certifikat förfrågan. Om du exempelvis valde en användarcertifikattyp kan du ange användarens huvudnamn (UPN) i det alternativa certifikatmottagarnamnet. Om klient certifikatet ska autentiseras till en nätverks princip server anger du UPN som alternativt namn på certifikat mottagare.  

- **Certifikatets giltighets period**: om du anger en anpassad giltighets period för den utfärdande certifikat utfärdaren anger du hur lång tid som ska gå innan certifikatet upphör att gälla.

    > [!TIP]
    > Ange en anpassad giltighets period med följande kommando rad: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Mer information om det här kommandot finns i [certifikat infrastruktur](certificate-infrastructure.md).  

    Du kan ange ett värde som är lägre än giltighets perioden i den angivna certifikat mal len, men inte högre. Om certifikatets giltighets period i certifikat mal len till exempel är två år, kan du ange ett värde på ett år, men inte ett värde på fem år. Värdet måste också vara lägre än den återstående giltighetsperioden för certifikatutfärdaren.  

- **Nyckelanvändning**: Ange alternativ för nyckelanvändning för certifikatet. Välj bland följande alternativ:  

  - **Nyckelchiffrering**: Tillåt nyckelutbyte endast när nyckeln är krypterad.  

  - **Digital signatur**: Tillåt nyckelutbyte endast när en digital signatur skyddar nyckeln.  

  Om du har bläddrat till en certifikatmall kan du inte ändra inställningarna, såvida du inte väljer en annan certifikatmall.  

  Konfigurera den valda certifikat mal len med en eller båda av de två nyckel användnings alternativen ovan. Annars visas följande meddelande i logg filen för certifikat registrerings platsen, **CRP. log**: **nyckel användningen i CSR och Challenge matchar inte**  

- **Nyckelstorlek (bitar)**: Välj storleken på nyckeln i bitar.  

- **Utökad nyckel användning**: Lägg till värden för certifikatets avsedda syfte. I de flesta fall kräver certifikatet **klientautentisering** så att användaren eller enheten kan autentisera till en server. Du kan lägga till andra nyckel användningar efter behov.  

- **Hash-algoritm**: Välj en av de tillgängliga typerna av hash-algoritmer som ska användas med det här certifikatet. Välj den högsta säkerhetsnivå som de anslutande enheterna har stöd för.  

  > [!NOTE]  
  > **SHA-2** stöder SHA-256, SHA-384 och SHA-512. **SHA-3** stöder endast SHA-3.  

- **Rot certifikat för certifikat utfärdare**: Välj en certifikat profil för certifikat utfärdare som du tidigare har konfigurerat och distribuerat till användaren eller enheten. Detta CA-certifikat måste vara rot certifikatet för den certifikat utfärdare som kommer att utfärda det certifikat som du konfigurerar i den här certifikat profilen.  

  > [!IMPORTANT]  
  > Om du anger ett certifikat från en rot certifikat utfärdare som inte har distribuerats till användaren eller enheten, initierar Configuration Manager inte den certifikat förfrågan som du konfigurerar i den här certifikat profilen.  

## <a name="supported-platforms"></a>Plattformar som stöds  

På sidan **plattformar som stöds** i guiden Skapa certifikat profil väljer du de operativ system versioner där du vill installera certifikat profilen. Välj **Välj alla** om du vill installera certifikat profilen på alla tillgängliga operativ system.

## <a name="next-steps"></a>Nästa steg

Den nya certifikat profilen visas i noden **certifikat profiler** på arbets ytan **till gångar och efterlevnad** . Det är redo för dig att distribuera till användare eller enheter. Mer information finns i [så här distribuerar du profiler](deploy-wifi-vpn-email-cert-profiles.md).