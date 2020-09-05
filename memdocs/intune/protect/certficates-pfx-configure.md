---
title: Använda certifikat med privata och offentliga nycklar i Microsoft Intune – Azure | Microsoft Docs
description: Använd PKCS-certifikat (Public Key Cryptography Standards) med Microsoft Intune, arbeta med rotcertifikat och certifikatmallar, installation av Intune Certificate Connector (NDES) och använd enhetskonfigurationsprofiler för ett PKCS-certifikat.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0f360509f456489a321e072c2acfbf26c14bf98
ms.sourcegitcommit: 231e2c3913a1d585310dfab7ffcd5c78c6bc5703
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970506"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Konfigurera och använda PKCS-certifikat med Intune

Intune stöder användning av PKCS-certifikat (privata och offentliga nyckelpar). Den här artikeln kan hjälpa dig att konfigurera den nödvändiga infrastrukturen som lokala certifikatanslutningsappar, exportera ett PKCS-certifikat och sedan lägga till certifikatet i en Intune-enhetskonfigurationsprofil.

Microsoft Intune innehåller inbyggda inställningar för att använda PKCS-certifikat för åtkomst och autentisering till organisationens resurser. Certifikat autentiserar och skyddar åtkomst till dina företagsresurser, till exempel ett VPN- eller Wi-Fi-nätverk. Du distribuerar de här inställningarna till enheter med hjälp av enhetskonfigurationsprofiler i Intune.

Information om användning av importerade PKCS-certifikat finns i [Importerade PFX-certifikat](certificates-imported-pfx-configure.md).


## <a name="requirements"></a>Krav

Om du vill använda PKCS-certifikat med Intune behöver du följande infrastruktur:

- **Active Directory-domän**:  
  Alla servrar i det här avsnittet måste vara anslutna till Active Directory-domänen.

  Mer information om att installera och konfigurera Active Directory Domain Services (AD DS) finns i [Design och planering för AD DS](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning).

- **Certifikatutfärdare**:  
   En utfärdare av företagscertifikat (CA).

  Information om hur du installerar och konfigurerar Active Directory Certificate Services (AD CS) finns i [den stegvisa guiden för Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)).

  > [!WARNING]  
  > Intune kräver att du kör AD CS med en Enterprise-certifikatutfärdare (CA), inte en fristående CA.

- **En klient**:  
  För att ansluta till företags-CA.

- **Rotcertifikat**:  
  En exporterad kopia av ditt rotcertifikat från din Enterprise-CA.

- **Microsoft Intune Certificate Connector** (kallas även *NDES Certificate Connector*):  
  I Intune-portalen går du till **Enhetskonfiguration** > **Certifikatanslutningsappar** > **Lägg till** och följer *stegen för att installera anslutningsappen för PKCS #12*. Använd nedladdningslänken i portalen för att påbörja nedladdningen av installationsprogrammet för certifikatanslutningsappen: **NDESConnectorSetup.exe**.  

  Intune har stöd för upp till 100 instanser av det här anslutningsprogrammet per klientorganisation. Varje instans av anslutningsprogrammet måste finnas på en separat Windows-server. Du kan installera en instans av den här anslutningen på samma server som en instans av PFX-certifikatanslutningsappen för Microsoft Intune. När du använder flera anslutningsprogram stöder kopplingsinfrastrukturen redundans och belastningsutjämning eftersom alla tillgängliga anslutningsinstanser kan bearbeta dina PKCS-certifikatbegäranden. 

  Anslutningsappen bearbetar PKCS-certifikatbegäranden som används för autentisering eller S/MIME-signering för e-post.

  Microsoft Intune Certificate Connector har även stöd för FIPS-läge (Federal Information Processing Standard). FIPS krävs inte, men du kan utfärda och återkalla certifikat när det är aktiverat.

- **PFX-certifikatanslutningsprogram för Microsoft Intune**:  
  Om du planerar att använda S/MIME-kryptering för e-post använder du Intune-portalen för att ladda ned *PFX-anslutningsappen* som stöder import av PFX-certifikat.  Gå till **Enhetskonfiguration** > **Certifikatanslutningsappar** > **Lägg till** och följer *stegen för att installera anslutningsapp för importerade PFX-certifikat*. Använd nedladdningslänken i portalen för att påbörja nedladdningen av installationsprogrammet **PfxCertificateConnectorBootstrapper.exe**.

  Anslutningsappen hanterar begäranden för PFX-filer som importeras till Intune för S/MIME-kryptering av e-post för en specifik användare. Du kan installera den här anslutningen på samma server som en instans av Microsoft Intune Certificate Connector. 

  Den här anslutningsappen kan uppdatera sig automatiskt när nya versioner blir tillgängliga. För att kunna uppdatera kapaciteten behöver du:
  - Installera anslutningsappen för PFX-certifikat för Microsoft Intune på din server.  
  - För att automatiskt få viktiga uppdateringar ser du till att brandväggarna är öppna så att anslutningsappen tillåts kontakta **autoupdate.msappproxy.net** på port **443**.   

  Mer information finns i [Nätverksslutpunkter för Microsoft Intune](../fundamentals/intune-endpoints.md) och [Krav för Intune-nätverkskonfiguration och bandbredd](../fundamentals/network-bandwidth-use.md).

- **Windows Server**:  
  Använd Windows Server som värd för:

  - Microsoft Intune-certifikatanslutningsapp – för scenarier med autentisering och S/MIME-signering av e-post
  - PFX-certifikatanslutningsapp för Microsoft Intune – för scenarier med S/MIME-kryptering av e-post.

  Anslutningsappar måste ha åtkomst till samma portar som för hanterade enheter. Dessa beskrivs i vår [information om slutpunkter för enheter](/intune/fundamentals/intune-endpoints#access-for-managed-devices).

  Intune stöder installation av *PFX-certifikatanslutningsappen* på samma server som *Microsoft Intune Certificate Connector*.
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Exportera rotcertifikatet från Enterprise-CA:n

För en enhet ska autentiseras med VPN, Wi-Fi eller andra resurser behöver enheten ett rot-CA-certifikat eller ett mellanliggande CA-certifikat. Följande steg förklarar hur du hämtar nödvändiga certifikat från din Enterprise CA.

**Använda en kommandorad**:  
1. Logga in på servern för rotcertifikatutfärdare med ett administratörskonto.
 
2. Gå till **Start** > **Kör** och ange **Cmd** för att öppna kommandotolken. 
    
3. Ange **certutil -ca.cert ca_name.cer** för att exportera rotcertifikatet som en fil med namnet *ca_name.cer*.



## <a name="configure-certificate-templates-on-the-ca"></a>Konfigurera certifikatmallar på CA

1. Logga in på din Enterprise CA med ett konto som har administratörsbehörighet.
2. Öppna konsolen **Certifikatutfärdare**, högerklicka på **Certifikatmallar** och välj **Hantera**.
3. Leta upp certifikatmallen **Användare**, högerklicka på den och välj **Duplicera mall** för att öppna **Egenskaper för ny mall**.

    > [!NOTE]
    > För scenarier med S/MIME-signering och kryptering av e-post använder många administratörer separata certifikat för signering och kryptering. Om du använder Microsoft Active Directory-certifikattjänster kan du använda mallen **Exchange Signature Only** (Endast Exchange-signatur) för certifikat för S/MIME-e-postsignering och mallen **Exchange User** (Exchange-användare) för S/MIME-krypteringscertifikat.  Om du använder en tredje parts certifikatutfärdare rekommenderas det att du granskar deras vägledning för att konfigurera mallar för signering och kryptering.

4. På fliken **Kompatibilitet**:

    - Ställ in **certifikatutfärdare** till **Windows Server 2008 R2**
    - Ställ in **certifikatmottagare** till **Windows 7 / Server 2008 R2**

5. På fliken **Allmänt** ställer du in **Mallens visningsnamn** till något som betyder något för dig.

    > [!WARNING]
    > **Mallnamnet** är som standard samma som **mallens visningsnamn** med *inga blanksteg*. Anteckna mallens namn. Du behöver det senare.

6. I **Hantering av begäranden** väljer du **Tillåt att den privata nyckeln exporteras**.
    
    > [!NOTE]
    > I motsats till SCEP genereras den privata certifikatnyckeln med PKCS på den server där anslutningsprogrammet är installerat och inte på enheten. Det krävs att certifikatmallen tillåter att den privata nyckeln exporteras, så att certifikatanslutningsprogrammet kan exportera PFX-certifikatet och skicka det till enheten. 
    >
    > Observera dock att certifikaten installeras på själva enheten med den privata nyckeln markerad som ej exporterbar.
    
7. I **kryptografi** bekräftar du att den **minsta nyckelstorleken** är inställd på 2048.
8. I **Ämnesnamn** väljer du **Anges i begäran**.
9. I **Tillägg**, bekräftar du att du ser krypterar filsystem, säker e-post och klientautentisering under **användningsprinciper**.

    > [!IMPORTANT]
    > För iOS/iPadOS-certifikatmallar: uppdatera **Nyckelanvändning** på fliken **Tillägg** och kontrollera att **Signaturen är bevis för ursprung** inte har markerats.

10. I **säkerhet** lägger du till datorkontot för den server där du installerar Microsoft Intune Certificate Connector. Ge det här kontot **läs-** och **registrera**-behörigheter.
11. Välj **Tillämpa** > **OK** för att spara certifikatmallen. Stäng **konsolen för certfikatmallar**.
12. I konsolen **Certifikatutfärdare** högerklickar du på **Certifikatmallar** > **Ny** > **Certifikatmall som ska utfärdas**. Välj den mall som du skapade i föregående steg. Välj **OK**.
13. Använd följande steg för att servern ska hantera certifikat för registrerade enheter och användare:

    1. Högerklicka på certifikatutfärdaren och välj **egenskaper**.
    2. På fliken för säkerhet lägger du till datorkontot för den server där du kör anslutningsapparna (**Microsoft Intune-certifikatanslutningsapp** eller **PFX-certifikatanslutningsapp för Microsoft Intune**). 
    3. Bevilja behörigheterna **utfärda och hantera certifikat** och **begära certifikat** till datorkontot.

14. Logga ut från Enterprise-CA:n.

## <a name="download-install-and-configure-the-microsoft-intune-certificate-connector"></a>Ladda ned, installera och konfigurera Microsoft Intune Certificate Connector

> [!IMPORTANT]  
> Microsoft Intune-certifikatanslutningsappen kan inte installeras på den utfärdande certifikatutfärdaren (CA) och måste i stället installeras på en separat Windows-server.  

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Administration av klientorganisation** > **Anslutning och token** > **Certifikatanslutningsprogram** >  **+ Lägg till**.

3. Klicka på *Ladda ned programvara för certifikatanslutningsapp* för anslutningsprogrammet för PKCS #12 och spara filen på en plats som du kan komma åt från servern där du ska installera anslutningsprogrammet.

   ![Microsoft Intune Certificate Connector nedladdning](./media/certficates-pfx-configure/download-ndes-connector.png)

4. När nedladdningen är klar loggar du in på servern. Efter det:

    1. Se till att .NET 4.5 Framework eller senare är installerat, eftersom det krävs av NDES-certifikatanslutningsappen. .NET 4.5 framework ingår automatiskt i Windows Server 2012 R2 och senare versioner.
    2. Kör installationsprogrammet (NDESConnectorSetup.exe) och godkänn standardplatsen. Anslutningsprogrammet installeras då till `\Program Files\Microsoft Intune\NDESConnectorUI`. Bland installationsalternativen väljer du **PFX-distribution**. Fortsätt och slutför installationen.
    3. Som standard körs anslutningsapptjänsten under det lokala systemkontot. Om en proxy krävs för att få åtkomst till Internet kontrollerar du att det lokala tjänstkontot kan komma åt proxyinställningarna på servern.

5. Microsoft Intune-certifikatanslutningsappen öppnar fliken **Registrering**. Om du vill aktivera anslutningen till Intune **Loggar du in** och anger ett konto med globala administratörsbehörigheter.
6. Vi rekommenderar att du på fliken **Avancerat** låter **Använd den här datorns systemkonto (standard)** vara markerat.
7. **Tillämpa** > **Stäng**
8. Gå tillbaka till Intune-portalen (**Intune** > **Enhetskonfiguration** > **Certifikatanslutningsappar**). Efter en stund visas en grön bockmarkering och **Anslutningsstatus** är **Aktiv**. Anslutningsservern kan nu kommunicera med Intune.
9. Om du har en webbproxy i nätverksmiljön kan du behöva ytterligare konfigurationer för att anslutningsappen ska fungera. Mer information finns i [Arbeta med befintliga lokala proxyservrar](/azure/active-directory/manage-apps/application-proxy-configure-connectors-with-proxy-servers) i Azure Active Directory-dokumentationen.
    - Android Enterprise (*Arbetsprofil*)
    - iOS
    - macOS
    - Windows 10 och senare

> [!NOTE]
> Microsoft Intune-certifikatanslutningsappen har stöd för TLS 1.2. Om TLS 1.2 installeras på den server som är värd för anslutningsappen använder anslutningsappen TLS 1.2. I annat fall används TLS 1.1. För närvarande används TLS 1.1 för autentisering mellan enheter och servern.

## <a name="create-a-trusted-certificate-profile"></a>Skapa en betrodd certifikatprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj och gå till **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande egenskaper:
   - **Plattform**: Välj plattform för de enheter som ska få den här profilen.
   - **Profil**: Välj **Betrott certifikat**.
  
4. Välj **Skapa**.

5. Ange följande egenskaper i **Grundinställningar**:
   - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett exempel på ett bra profilnamn är *Trusted certificate profile for entire company* (Betrodd certifikatprofil för hela företaget).
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Välj **Konfigurationsinställningar** och ange .CER-filen för certifikatutfärdarens rotcertifikat som du exporterade tidigare.

   > [!NOTE]
   > Beroende på vilken plattform du valde i **steg 3** kan du få alternativet att välja **målarkiv** för certifikatet.

   ![Skapa en profil och ladda upp ett betrott certifikat](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

   Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Planera för att distribuera den här certifikatprofilen till samma grupper som tar emot PKCS-certifikatets profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

    Välj **Nästa**.

11. (*Gäller endast Windows 10*) I **Tillämplighetsregler** anger du tillämplighetsregler för att förfina tilldelningen av profilen. Du kan välja att tilldela eller inte tilldela profilen baserat på operativsystemversionen eller enhetsversionen.

  Mer information finns i [Tillämplighetsregler](../configuration/device-profile-create.md#applicability-rules) i *Skapa en enhetsprofil i Microsoft Intune*.

12. Granska inställningarna under **Granska + skapa**. När du väljer Skapa sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="create-a-pkcs-certificate-profile"></a>Skapa en PKCS-certifikatprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj och gå till **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande egenskaper:
   - **Plattform**: Välj plattform för dina enheter. Alternativen är:
     - Android-enhetsadministratör
     - Android Enterprise > Fullständigt hanterad och dedikerad Android Enterprise och företagsägd arbetsprofil
     - Android Enterprise > Endast arbetsprofil
     - iOS/iPadOS
     - macOS
     - Windows 10 och senare
   - **Profil**: Välj **PKCS-certifikat**

   > [!NOTE]
   > På enheter med en Android Enterprise-profil syns inte certifikat som har installerats med en PKCS-certifikatprofil på enheten. Kontrollera statusen för profilen i Intune-konsolen för att bekräfta lyckad certifikatdistribution.
4. Välj **Skapa**.

5. Ange följande egenskaper i **Grundinställningar**:
   - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett bra profilnamn är t.ex. *PKCS-profil för hela företaget*.
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar: – Android-enhetsadministratör – Android Enterprise – iOS/iPad – Windows 10
   
   |Inställningen     | Plattform     | Information   |
   |------------|------------|------------|
   |**Tröskelvärde för förnyelse (%)**        |<ul><li>Alla         |20 % rekommenderas  | 
   |**Certifikatets giltighetsperiod**  |<ul><li>Alla         |Om du inte har ändrat certifikatmallen kan det här alternativet anges till ett år. |
   |**Nyckellagringsprovider (KSP)**   |<ul><li>Windows 10  |För Windows väljer du var du vill lagra nycklarna på enheten. |
   |**Certifikatutfärdare**      |<ul><li>Alla         |Visar det interna fullständiga domännamnet (FQDN) för din Enterprise-CA.  |
   |**Namn på certifikatutfärdare** |<ul><li>Alla         |Anger namnet på din Enterprise-CA, till exempel ”Contoso Certification Authority”. |
   |**Certifikatmallens namn**    |<ul><li>Alla         |Visar namnet på certifikatmallen. |
   |**Certifikattyp**             |<ul><li>Android Enterprise (*Arbetsprofil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 och senare|Välj en typ: <ul><li> **Användarcertifikat** kan innehålla både användarattribut och enhetsattribut i certifikatets ämne och SAN. </il><li>**Enhetscertifikat** kan endast innehålla enhetsattribut i certifikatets ämne och SAN. Använd Enhet för scenarier såsom användarlösa enheter, till exempel kiosker eller andra delade enheter.  <br><br> Det här valet påverkar ämnesnamnets format. |
   |**Ämnesnamnets format**          |<ul><li>Alla         |Mer information om hur du konfigurerar ämnesnamnets format finns i [Ämnesnamnets format](#subject-name-format) längre fram i den här artikeln.  <br><br> För de flesta plattformar använder du alternativet **Eget namn** om inget annat krävs. <br><br>För följande plattformar bestäms ämnesnamnets format av certifikattypen: <ul><li>Android Enterprise (*Arbetsprofil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 och senare</li></ul>  <p>  |
   |**Alternativt namn för certifikatmottagare**     |<ul><li>Alla         |Välj **Användarens huvudnamn** som *attribut* (om inget annat krävs), konfigurera ett motsvarande *värde* och klicka sedan på **Lägg till**. <br><br>Mer information finns i [Ämnesnamnets format](#subject-name-format) senare i den här artikeln.|
   |**Förbättrad nyckelanvändning**           |<ul><li> Android-enhetsadministratör </li><li>Android Enterprise (*Enhetsägare*, *Arbetsprofil*) </li><li>Windows 10 |Certifikat kräver vanligtvis *Klientautentisering* så att användaren eller enheten kan autentisera till en server. |
   |**Tillåt alla appar att komma åt privat nyckel** |<ul><li>macOS  |Ange till **Aktivera** för att ge appar som är konfigurerade för den associerade Mac-enheten åtkomst till den privata nyckeln för PKCS-certifikat. <br><br> Mer information om den här inställningen finns i *AllowAllAppsAccess* avsnittet Certifikatnyttolast i [referensen för konfigurationsprofil](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) i Apple-utvecklardokumentationen. |
   |**Rotcertifikat**             |<ul><li>Android-enhetsadministratör </li><li>Android Enterprise (*Enhetsägare*, *Arbetsprofil*) |Välj en certifikatprofil för en rotcertifikatutfärdare som tidigare har tilldelats. |

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

   Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Planera för att distribuera den här certifikatprofilen till samma grupper som tar emot det betrodda certifikatets profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer Skapa sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.


### <a name="subject-name-format"></a>Format för namn på certifikatmottagare

När du skapar en PKCS-certifikatprofil för följande plattformar beror alternativen för ämnesnamnets format på den certifikattyp du väljer, antingen **Användare** eller **Enhet**.  

Plattformar:

- Android Enterprise (*Arbetsprofil*)
- iOS
- macOS
- Windows 10 och senare

> [!NOTE]
> Det finns ett känt problem med användning av PKCS för att hämta certifikat; detta är [samma problem som för SCEP](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters) när ämnesnamnet i den resulterande certifikatsigneringsförfrågan (CSR) innehåller något av följande tecken som undantaget tecken (med ett omvänt snedstreck \\):
> - \+
> - ;
> - ,
> - =

- **Certifikattypen Användare**  
  Formatalternativ för *Format för namn på certifikatmottagare* omfattar två variabler: **Eget namn (CN)** och **E-postadress (E)** . **Eget namn (cn)** kan ställas in till någon av följande variabler:

  - **CN={{UserName}}** : Användarens huvudnamn, till exempel janedoe@contoso.com.
  - **CN={{AAD_Device_ID}}** : Ett ID som tilldelas när du registrerar en enhet i Azure Active Directory (AD). Detta ID används vanligtvis för att autentisera med Azure AD.
  - **CN={{SERIALNUMBER}}** : Det unika serienummer (SN) som vanligtvis används av tillverkaren för att identifiera en enhet.
  - **CN={{IMEINumber}}** : Det unika IMEI-nummer (International Mobile Equipment Identity) som används för att identifiera en mobiltelefon.
  - **CN={{OnPrem_Distinguished_Name}}** : En sekvens med relativa unika namn avgränsade med kommatecken, till exempel *CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com*.

    Om du vill använda variabeln *{{OnPrem_Distinguished_Name}}* ska du synkronisera användarattributet *onpremisesdistinguishedname* med hjälp av [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) till din Azure AD.

  - **CN={{onPremisesSamAccountName}}** : Administratörer kan synkronisera attributet samAccountName från Active Directory till Azure AD med hjälp av Azure AD Connect till ett attribut som heter *onPremisesSamAccountName*. Intune kan ersätta denna variabel som en del av en begäran om certifikatutfärdande i ämnet på ett certifikat. Attributet samAccountName är användarens inloggningsnamn som används för att stödja klienter och servrar från en tidigare version av Windows (före Windows 2000). Formatet på användarens inloggningsnamn är: *Domännamn\testUser* eller bara *testUser*.

    Om du vill använda variabeln *{{onPremisesSamAccountName}}* ska du synkronisera användarattributet *onPremisesSamAccountName* med hjälp av [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) till din Azure AD.

  Genom att kombinera en eller flera av dessa variabler och statiska strängar kan du skapa ett anpassat format för ämnesnamnet, till exempel:  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  Det exemplet omfattar ett format för ämnesnamnet som använder variablerna CN och E samt strängar för värdena för organisationsenhet, organisation, plats, tillstånd och land/region. [CertStrToName-funktionen](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) beskriver den här funktionen och dess strängar som stöds.

- **Certifikattypen Enhet**  
  Formatalternativ för Format för namn på certifikatmottagare omfattar följande variabler: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{DeviceName}}**
  - **{{FullyQualifiedDomainName}}** *(Gäller endast för Windows och domänanslutna enheter)*
  - **{{MEID}}**

  Du kan ange de här variablerna följt av texten för variabeln i textrutan. Till exempel kan det egna namnet för en enhet som heter *Device1* läggas till som **CN={{DeviceName}}Device1**.

  > [!IMPORTANT]  
  > - När du anger en variabel omger du variabelnamnet inom klammerparenteser { } som det visas i exemplet, för att undvika ett fel.  
  > - Enhetsegenskaper som används i *ämnet* eller *SAN* för ett enhetscertifikat, till exempel **IMEI**, **SerialNumber** och **FullyQualifiedDomainName**, är egenskaper som kan förfalskas av en person med åtkomst till enheten.
  > - En enhet måste ha stöd för alla variabler som anges i en certifikatprofil för att den profilen ska installeras på den enheten.  Om till exempel **{{IMEI}}** används i ämnesnamnet för en SCEP-profil och tilldelas till en enhet som inte har något IMEI-nummer kommer profilen inte att installeras.  
 
## <a name="whats-new-for-connectors"></a>Nyheter för anslutningsappar

Uppdateringar för de två certifikatanslutningsapparna släpps regelbundet. När vi uppdaterar en anslutningsapp kan du läsa om ändringarna här.

*PFX-certifikatanslutningsappen för Microsoft Intune* [har stöd för automatiska uppdateringar](#requirements), medan *Intune-certifikatanslutningsappen* uppdateras manuellt.

### <a name="may-17-2019"></a>17 maj 2019

- **PFX-certifikatanslutningsprogram för Microsoft Intune – version 6.1905.0.404**  
  Ändringar i den här versionen:  
  - Åtgärdade ett problem där befintliga PFX-certifikat fortsätter att bearbetas, vilket gör att anslutningsappen slutar att bearbeta nya begäranden. 

### <a name="may-6-2019"></a>Den 6 maj 2019

- **PFX-certifikatanslutningsprogram för Microsoft Intune – version 6.1905.0.402**  
  Ändringar i den här versionen:  
  - Avsökningsintervallet för anslutningsappen har minskats från 5 minuter till 30 sekunder.

### <a name="april-2-2019"></a>2 april 2019

- **Intune-certifikatanslutningsapp – version 6.1904.1.0**  
  Ändringar i den här versionen:  
  - Åtgärdade ett problem där anslutningsappen kunde misslyckas med att registrera till Intune efter inloggning till anslutningsappen med ett konto för global administratör.  
  - Innehåller tillförlitlighetsåtgärder för certifikatåterkallande.  
  - Innehåller prestandaåtgärder som ökar hastigheten för bearbetning av PKCS-certifikatbegäranden.  

- **PFX-certifikatanslutningsprogram för Microsoft Intune – version 6.1904.0.401**
  > [!NOTE]  
  > Automatisk uppdatering för den här versionen av PFX-anslutningsappen är inte tillgänglig förrän den 11 april 2019.  

  Ändringar i den här versionen:  
  - Åtgärdade ett problem där anslutningsappen kunde misslyckas med att registrera till Intune efter inloggning till anslutningsappen med ett konto för global administratör.  


## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](../configuration/device-profile-assign.md) och [övervaka dess status](../configuration/device-profile-monitor.md).

[Använda SCEP för certifikat](certificates-scep-configure.md) eller [utfärda PKCS-certifikat från en Symantec PKI Manager-webbtjänst](certificates-digicert-configure.md).

[Felsök PKCS-certifikatprofiler](../protect/troubleshoot-pkcs-certificate-profiles.md)
