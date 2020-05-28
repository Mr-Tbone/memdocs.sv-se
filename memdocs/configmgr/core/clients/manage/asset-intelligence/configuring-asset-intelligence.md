---
title: Konfigurera Tillgångsinformation
titleSuffix: Configuration Manager
description: Konfigurera Tillgångsinformation i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1a5c89d3fdd82bfa654f806c6931bde2621e714b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906618"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Konfigurera Tillgångsinformation i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Tillgångsinformation inventeringar och hanterar användning av program varu licenser.   

## <a name="steps-to-configure-asset-intelligence"></a>Steg för att konfigurera Tillgångsinformation  
   

- **Steg 1**: om du vill samla in de inventerings data som krävs för tillgångsinformation rapporter måste du aktivera klient agenten för maskin varu inventering enligt beskrivningen i [så här utökar du maskin varu inventeringen](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Steg 2**: [aktivera tillgångsinformation rapporterings klasser för maskin varu inventering](#BKMK_EnableAssetIntelligence).  
- **Steg 3**: [installera en tillgångsinformation plats för synkronisering](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Steg 4**: [aktivera granskning av lyckade inloggnings händelser](#BKMK_EnableSuccessLogonEvents)  
- **Steg 5**: [Importera licens information för program vara](#BKMK_ImportSoftwareLicenseInformation)  
- **Steg 6**: [Konfigurera tillgångsinformation underhålls aktiviteter](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Om du vill aktivera Tillgångsinformation på Configuration Manager platser måste du aktivera en eller Tillgångsinformation flera rapporterings klasser för maskin varu inventering. Du kan aktivera klasserna på startsidan för **Tillgångsinformation** eller i egenskaperna för klientinställningar på arbetsytan **Administration** på noden **Klientinställningar** . Använd någon av följande procedurer.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Så här aktiverar du rapportklasser för maskinvaruinventering i Tillgångsinformation från startsidan för Tillgångsinformation  

1.  I Configuration Manager-konsolen väljer du **till gång och efterlevnad**  >  **tillgångsinformation**.  

3.  På fliken **Start** går du till gruppen **tillgångsinformation** och väljer **Redigera lager klasser**.   

4.  Aktivera Tillgångsinformation rapportering genom att välja **Aktivera alla tillgångsinformation rapporterings klasser** eller **bara aktivera de valda tillgångsinformation rapporterings**klasserna och välja minst en rapport klass från de klasser som visas.  

    > [!NOTE]  
    >  Tillgångsinformationsrapporter som är beroende av maskinvarulagerklasser som du aktiverar genom att följa dessa steg visar inga data förrän klienterna har genomsökts och returnerat maskinvaruinventeringen.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Så här aktiverar du rapportklasser för maskinvaruinventering i Tillgångsinformation från egenskaperna för klientinställningar  

1.  I Configuration Manager-konsolen väljer du **Administration**  >   **klient inställningar**  >  **standard klient agent inställningar**. Om du har skapat anpassade klient inställningar kan du välja dem i stället.  

3.  På fliken **start** > **egenskaps** grupp väljer du **Egenskaper**.   

4.  Välj klasser för **maskin varu inventerings**  >  **uppsättning**. .  

5.  Välj **Filtrera efter kategori**  >  **tillgångsinformation rapporterings klasser**. Listan med klasser uppdateras med endast rapportklasserna för maskinvaruinventering i Tillgångsinformation.  

6.  Välj minst en rapport klass från listan.  

    > [!NOTE]  
    >  Tillgångsinformationsrapporter som är beroende av maskinvarulagerklasser som du aktiverar genom att följa dessa steg visar inga data förrän klienterna har genomsökts och returnerat maskinvaruinventeringen.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Plats system rollen för Tillgångsinformation-platsen används för att ansluta Configuration Manager platser till System Center Online för att synkronisera Tillgångsinformation katalog information. Tillgångsinformation-platsen för synkronisering kan bara installeras på ett plats system på den översta nivån i hierarkin Configuration Manager och kräver Internet åtkomst för att synkroniseras med System Center Online genom att använda TCP-port 443.

Förutom att hämta ny information för tillgångsinformationskatalogen kan platsen för synkronisering av tillgångsinformation överföra anpassad information om programvarutitlar till System Center Online för kategorisering. Microsoft behandlar alla överförda program varu titlar som offentlig information. Se till att dina anpassade program varu titlar inte innehåller konfidentiell eller patentskyddad information. Mer information om hur du begär kategorisering av programvarutitlar finns i [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Så här installerar du en platssystemroll för en plats för synkronisering av tillgångsinformation  

1.  I Configuration Manager-konsolen väljer du **Administration** >  **plats konfigurations**  >  **servrar och plats system roller**.  

3.  Lägg till plats system rollen för Tillgångsinformation-platsen till en ny eller befintlig plats system Server:  

    -  För en **ny plats system Server**: Klicka på **skapa plats system Server** i gruppen **skapa** på fliken **Start** sida för att starta guiden.   

        > [!NOTE]  
        >  När Configuration Manager installerar en plats system roll installeras installationsfilerna som standard på den första tillgängliga NTFS-formaterade hård disken som har mest ledigt hårddisk utrymme. Om du vill förhindra Configuration Manager att installera på vissa enheter skapar du en tom fil med namnet No_sms_on_drive. SMS och kopierar den till enhetens rotmapp innan du installerar plats system servern.  

    -  För en **befintlig plats system Server**: Välj den server där du vill installera plats system rollen för tillgångsinformation-platsen. När du väljer en server visas en lista över de plats system roller som redan är installerade på servern i informations fönstret.  

         På fliken **Start** går du till gruppen **Server** och väljer **Lägg till plats system roll** för att starta guiden.  

4.  Slutför sidan **Allmänt** . Om du lägger till platsen för synkronisering av tillgångsinformation på en befintlig platssystemserver kontrollerar du de tidigare angivna värdena.  

5.  På sidan **urval för system roll** väljer du **tillgångsinformation plats för synkronisering** i listan över tillgängliga roller.  

6.  På sidan **anslutnings inställningar för tillgångsinformation-synkronisering** väljer du **Nästa**.  

     Inställningen **Använd denna plats för synkronisering av tillgångsinformation** är vald som standard och kan inte konfigureras på den här sidan. System Center Online accepterar endast nätverkstrafik via TCP-port 443. Därför kan inställningen **SSL-portnummer** inte konfigureras på den här sidan i guiden.  

7.  Alternativt kan du ange en sökväg till System Center Online Authentication Certificate-filen (. pfx). Normalt anger du inte en sökväg för certifikatet eftersom anslutningscertifikatet etableras automatiskt när platsrollen installeras.  

8.  På sidan **Inställningar för proxyserver** anger du om den tillgångsinformation platsen ska använda en proxyserver vid anslutning till System Center Online för att synkronisera katalogen och om du vill använda autentiseringsuppgifter för att ansluta till proxyservern.  

    > [!WARNING]  
    >  Om en proxyserver krävs för att ansluta till System Center Online kan anslutningscertifikatet också tas bort om användarens lösenord upphör att gälla för det konto som har konfigurerats för autentisering av proxyservern.  

9. På sidan **Synkroniseringsschema** anger du om du vill synkronisera tillgångsinformationskatalogen baserat på ett schema. När du aktiverar synkroniseringsschemat anger du ett enkelt eller anpassat synkroniseringsschema. Vid en schemalagd synkronisering ansluter platsen för synkronisering av tillgångsinformation till System Center Online för att hämta den senaste tillgångsinformationskatalogen. Du kan synkronisera Tillgångsinformation-katalogen manuellt från noden Tillgångsinformation i Configuration Manager-konsolen. Anvisningar för hur du synkroniserar Tillgångsinformation-katalogen manuellt finns i avsnittet [om att synkronisera tillgångsinformation katalog manuellt](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) i [operationerna för tillgångsinformation](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Slutför guiden 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Fyra tillgångsinformationsrapporter visar information som samlats in från händelseloggarna för Windows-säkerhet på klientdatorer. Så här konfigurerar du inloggnings inställningar för datorns säkerhets princip för att aktivera granskning av lyckade inloggnings händelser.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Så här aktiverar du loggning av lyckade inloggningshändelser med hjälp av en lokal säkerhetsprincip  

1.  På en Configuration Manager klient dator väljer du **Starta**  >  **administrations verktyg**  >  **lokal säkerhets princip**.  

2.  I dialog rutan **lokal säkerhets princip** , under **säkerhets inställningar**, expanderar du **lokala principer**och väljer sedan **gransknings princip**.  

3.  Dubbelklicka på **Granska inloggnings händelser**i resultat fönstret, kontrol lera att kryss rutan **lyckades** är markerad och välj sedan **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Så här aktiverar du loggning av lyckade inloggningshändelser med hjälp av en säkerhetsprincip för Active Directory-domäner  

1.  På en domänkontrollant dator väljer du **Start**, pekar på **administrations verktyg**och väljer sedan **säkerhets princip för domän**.  

2.  I dialog rutan **lokal säkerhets princip** , under **säkerhets inställningar**, expanderar du **lokala principer**och väljer sedan **gransknings princip**.  

3.  Dubbelklicka på **Granska inloggnings händelser**i resultat fönstret, kontrol lera att kryss rutan **lyckades** är markerad och välj sedan **OK**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 I följande avsnitt beskrivs de procedurer som krävs för att importera både Microsoft och allmän information om program varu licensiering till Configuration Manager plats databasen med hjälp av guiden Importera program varu licenser. När du importerar informationen om programvarulicenser till platsdatabasen från licensöversiktsfiler kräver platsserverns datorkonto **Fullständig behörighet** för NTFS-filsystemet till filresursen som används för att importera informationen om programvarulicenser.  

> [!IMPORTANT]  
>  När informationen om programvarulicenser importeras till platsdatabasen skrivs befintlig information om programvarulicenser över. Kontrollera att filen med information om programvarulicenser som du använder med guiden Importera programvarulicenser innehåller en komplett lista med all nödvändig information om programvarulicenserna.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Så här importerar du information om programvarulicenser till tillgångsinformationskatalogen  

1.  På arbets ytan **till gångar och efterlevnad** väljer du **tillgångsinformation**.  

2.  På fliken **Start** går du till gruppen **tillgångsinformation** och väljer **importera program varu licenser**.   

4.  På sidan **Importera** anger du om du importerar en MVLS-fil (Microsoft Volume Licensing) (.xml eller .csv) eller en allmän licensöversikt (.csv). Mer information om hur du skapar en allmänt licensöversiktsfil finns i [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) senare i det här avsnittet.  

    > [!WARNING]  
    >  Information om hur du hämtar en MVLS-fil i CSV-format som du kan importera till tillgångsinformationskatalogen finns i [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Du måste ha ett registrerat konto på webbplatsen för att komma åt den här informationen. Du måste kontakta din Microsoft-kontorepresentant för information om hur du får tag på en MVLS-fil i XML-format.  

5.  Ange UNC-sökvägen till licens översikts filen eller Välj **Bläddra** för att välja en delad nätverksmapp och en fil.  

    > [!NOTE]  
    >  Den delade mappen bör vara skyddad så att obehöriga inte har åtkomst till licensinformationsfilen, och datorkontot för den dator som guiden körs på måste ha fullständig behörighet till resursen som innehåller licensimportfilen.  

6. Slutför guiden.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Du kan också importera en allmän licensöversikt till tillgångsinformationskatalogen med hjälp av en manuellt skapad licensimportfil med kommaavgränsat filformat (.csv).  

> [!NOTE]  
>  Endast fälten **Name**, **Publisher**, **Version**och **EffectiveQuantity** måste innehålla data, men alla fält måste läggas till på den första raden i licensimportfilen. Datumfält måste ha följande format: år-månad-dag, t.ex. 2008-04-08.  

Tillgångsinformation matchar de produkter som du anger i den allmänna licensöversikten genom att använda produktnamnet och produktversionen, men inte utgivarens namn. Du måste använda ett produktnamn i den allmänna licensöversikten som är identiskt med produktnamnet som lagras i platsdatabasen. Tillgångsinformation tar det **EffectiveQuantity** -nummer som ges i den allmänna licens översikten och jämför antalet med antalet installerade produkter som finns i Configuration Manager inventering.  

> [!TIP]  
>  Om du vill få en fullständig lista över de produkt namn som lagras i Configuration Manager plats databasen kan du köra följande fråga på plats databasen: Välj Productname0 from från v_GS_INSTALLED_SOFTWARE.  

 Du kan ange exakta versioner för en produkt eller ange en del av versionen, till exempel endast huvudversionen. Följande exempel visar versionsmatchningarna för den allmänna licensöversiktsversion som anges för en bestämd produkt.  

|Post i allmän licensöversikt|Matchande poster i platsdatabasen|  
|-------------------------------------|------------------------------------|  
|Namn: "program vara", ProductVersion0: "2"|Productname0 from: "program vara", ProductVersion0: "2.01.1234"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.02.5678"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.05.1234"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.05.5678"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.05.3579.000"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.10.1234"|  
|Namn: "program vara", version "2,05"|Productname0 from: "program vara", ProductVersion0: "2.05.1234"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.05.5678"<br /><br /> Productname0 from: "program vara", ProductVersion0: "2.05.3579.000"|  
|Namn: "program vara", version "2"<br /><br /> Namn: "program vara", version "2,05"|Fel vid import. Importen misslyckas om mer än en post matchar samma produktversion.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Så här skapar du en importfil för en allmän licensöversikt i Microsoft Excel  

1.  Öppna Microsoft Excel och skapa ett nytt kalkylblad.  

2.  Ange alla namn på fälten med information om programvarulicenser på den första raden i det nya kalkylbladet.  

3.  Ange nödvändig programlicensinformation på den andra och efterföljande rader i det nya kalkylbladet. Kontrollera att åtminstone alla obligatoriska fält för information om programvarulicenserna har angetts på efterföljande rader för varje programvarulicens som ska importeras. Namnet på programvarutitlarna som anges i kalkylbladet måste vara samma som programvarutiteln som visas i Resursläsaren för en klientdator när maskinvaruinventeringen har körts.  

4.  Spara filen i CSV-format.  

5.  Kopiera CSV-filen till den filresurs som används för att importera informationen om programvarulicenserna till tillgångsinformationskatalogen.  

6.  I Configuration Manager-konsolen använder du guiden Importera program varu licenser för att importera den nyss skapade. csv-filen.  

7.  Kör rapporten Tillgångsinformation **licens 15a-Third Party Software avstämning** för att kontrol lera att licens informationen har importer ats till tillgångsinformation katalogen.  

> [!NOTE]  
>  Ett exempel på en allmän program varu licens fil som du kan använda i test syfte finns i [exempel tillgångsinformation allmän licens import fil](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Exempeltabell för att beskriva programvarulicenser  
 När du skapar en importfil för en allmän licensöversikt kan du använda följande tabell för att beskriva programlicenser som ska importeras till tillgångsinformationskatalogen.  

|Kolumnnamn|Datatyp|Obligatorisk|Exempel|  
|-----------------|---------------|--------------|-------------|  
|Name|Högst 255 tecken|Ja|Programvarutitel|  
|Utgivare|Högst 255 tecken|Ja|Programvaruutgivare|  
|Version|Högst 255 tecken|Ja|Programvaruversion|  
|Språk|Högst 255 tecken|Ja|Programvarans språk|  
|EffectiveQuantity|Heltal|Ja|Antal köpta licenser|  
|PONumber|Högst 255 tecken|Nej|Information om inköpsordern|  
|ResellerName (Återförsäljarnamn)|Högst 255 tecken|Nej|Information om återförsäljaren|  
|DateOfPurchase|Datumvärde i följande format: ÅÅÅÅ-MM-DD|Nej|Datum för licensköpet|  
|SupportPurchased|Bitvärde|Nej|0 eller 1: Ange 0 för Ja och 1 för Nej|  
|SupportExpirationDate|Datumvärde i följande format: ÅÅÅÅ-MM-DD|Nej|Slutdatum för köpt support|  
|Kommentarer|Högst 255 tecken|Nej|Valfria kommentarer|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Följande underhållsaktiviteter är tillgängliga för Tillgångsinformation:  

-   **Kontrol lera program titel med inventerings information**: kontrollerar att program varu titeln som rapporteras i program varu inventeringen har stämts av mot program varu titeln i Tillgångsinformation katalogen. Som standard är den här aktiviteten aktive rad och schemalagd att köras på lördag efter 12:00 A.M. och före 5:00 Den här underhålls åtgärden är bara tillgänglig på platsen på den översta nivån i Configuration Manager hierarkin.  

-   **Sammanfatta installerade program varu data**: innehåller den information som visas i arbets ytan **till gångar och efterlevnad** , i noden **Inventerad program vara** under noden **tillgångsinformation** . När aktiviteten körs samlar Configuration Manager in ett antal för alla inventerade program varu titlar på den primära platsen. Som standard är den här aktiviteten aktive rad och schemalagd att köras varje dag efter 12:00 A.M. och före 5:00 Den här underhålls aktiviteten är endast tillgänglig på primära platser.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Så här konfigurerar du underhållsaktiviteter för Tillgångsinformation  

1.  I Configuration Manager-konsolen väljer du **Administration**  >  **plats konfiguration**  >  **platser**.  

3.  Välj den plats där du vill konfigurera underhållsaktiviteten för Tillgångsinformation.  

4.  Välj **plats underhåll**i gruppen **Inställningar** på fliken **Start** . Välj en aktivitet och välj **Redigera** för att ändra inställningarna. 

    Vi rekommenderar att du ställer in tids perioden på låg belastnings tid för platsen. Tidsperioden är tidsintervallet då aktiviteten kan köras. Den definieras av **Starta efter** och **Senaste starttid** som anges i dialogrutan **Aktivitetsegenskaper** .  

    Du kan starta aktiviteten direkt genom att välja dagens datum och ange **Starta efter** till ett par minuter efter den aktuella tiden.  

7.  Spara inställningarna genom att klicka på **OK** . Nu körs aktiviteten enligt sitt schema.  

    > [!NOTE]  
    >  Om en aktivitet inte kan köras vid det första försöket, Configuration Manager försöker att köra aktiviteten igen tills aktiviteten körs eller tills den tids period som aktiviteten kan köras i har slutförts.  
