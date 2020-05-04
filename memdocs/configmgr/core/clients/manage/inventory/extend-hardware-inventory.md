---
title: Utöka maskin varu inventering
titleSuffix: Configuration Manager
description: Lär dig hur du utökar maskin varu inventeringen i Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714418"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Så här utökar du maskin varu inventeringen i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Maskin varu inventeringen läser information från Windows-datorer med hjälp av Windows Management Instrumentation (WMI). WMI är Microsofts implementering av webbaserad företags hantering (WBEM), en bransch standard för åtkomst till hanterings information i ett företag. I tidigare versioner av Configuration Manager utökade maskin varu inventeringen genom att ändra filen sms_def. MOF på plats servern. Den här filen innehöll en lista med WMI-klasser som kunde läsas av maskin varu inventering. Genom att redigera den här filen kan du aktivera och inaktivera befintliga klasser och även skapa nya klasser för inventering.  

Filen Configuration. mof används för att definiera data klasser som ska inventeras av maskin varu inventeringen på klienten och har inte ändrats från Configuration Manager 2012. Du kan skapa dataklasser för att inventera befintliga eller anpassade WMI-databasklasser eller registernycklar som finns på klientdatorer.  

 Filen Configuration.mof definierar och registrerar också de WMI-providers som kommer åt enhetsinformation under maskinvaruinventeringen. Registreringen av providers definierar den typ av provider som ska användas och de klasser som providern stöder.  

 När Configuration Manager klienter begär en princip, är Configuration. MOF kopplad till princip innehållet. Den här filen hämtas sedan och kompileras av klienter. När du lägger till, ändrar eller tar bort dataklasser från filen Configuration.mof kompilerar klienterna automatiskt dessa ändringar som görs i inventeringsrelaterade dataklasser. Ingen ytterligare åtgärd krävs för att inventera nya eller ändrade data klasser på Configuration Manager klienter. Den här filen finns i **< CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** på primära platsservrar.  

 I Configuration Manager redigerar du inte längre sms_def. MOF-filen som du gjorde i Configuration Manager 2007. Du kan i stället aktivera och inaktivera WMI-klasser och lägga till nya klasser för insamling vid maskinvaruinventeringen med hjälp av klientinställningar. Configuration Manager tillhandahåller följande metoder för att utöka maskin varu inventeringen.  

> [!NOTE]  
>  Om du har ändrat filen Configuration. MOF manuellt för att lägga till anpassade lager klasser kommer dessa ändringar att skrivas över när du uppdaterar till version 1602. Om du vill fortsätta att använda anpassade klasser efter att du har uppdaterat måste du lägga till dem i avsnittet tillägg i filen Configuration. MOF när du har uppdaterat till 1602.  
> Men du får inte ändra något ovanför det här avsnittet eftersom dessa avsnitt är reserverade för ändringar av Configuration Manager. En säkerhetskopia av din anpassade Configuration.mof finns i:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Metod|Mer information|  
|------------|----------------------|  
|Aktivera eller inaktivera befintliga inventeringsklasser|Aktivera eller inaktivera standard inventerings klasserna eller skapa anpassade klient inställningar som gör att du kan samla in olika maskin varu lager klasser från angivna klient samlingar. Se proceduren [för att aktivera eller inaktivera befintliga inventerings klasser](#BKMK_Enable) i den här artikeln.|  
|Lägga till en ny inventeringsklass|Lägg till en ny inventerings klass från WMI-namnrymden för en annan enhet. Se proceduren [för att lägga till en ny inventerings klass](#BKMK_Add) i den här artikeln.|  
|Importera och exportera maskinvarulagerklasser|Importera och exportera Managed Object Format-filer (MOF) som innehåller inventerings klasser från Configuration Manager-konsolen. Se [Importera maskin varu lager klasser](#BKMK_Import) och exportera procedurer för [maskin varu lager klasser](#BKMK_Export) i den här artikeln.|  
|Skapa NOIDMIF-filer|Använd NOIDMIF-filer för att samla in information om klient enheter som inte kan inventeras av Configuration Manager. Du kanske till exempel vill samla in information om enheternas tillgångsnummer som endast förekommer som en etikett på enheten. NOIDMIF-inventeringen associeras automatiskt med klientenheten som den samlats in från. Se [för att skapa NOIDMIF-filer](#BKMK_NOIDMIF) i den här artikeln.|  
|Skapa IDMIF-filer|Använd IDMIF-filer för att samla in information om till gångar i organisationen som inte är associerade med en Configuration Manager-klient, till exempel projektorer, Foto kopiatorer och nätverks skrivare. Se [för att skapa IDMIF-filer](#BKMK_IDMIF) i den här artikeln.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedurer för att utöka maskinvaruinventeringen  
Dessa steg beskriver hur du konfigurerar standardklientinställningarna för maskinvaruinventering. Inställningarna tillämpas på alla klienter i hierarkin. Om du vill att inställningarna bara ska gälla för vissa klienter skapar du en anpassad klienten hets inställning och tilldelar den till en samling med vissa klienter. Se [Konfigurera klient inställningar](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Så här aktiverar eller inaktiverar du befintliga inventerings klasser  

1.  I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

4.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

5.  I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

6.  I listan **Enhetsinställningar** klickar du på **Ange klasser**.  

7.  I dialogrutan **Maskinvarulagerklasser** markerar eller avmarkerar du de klasser och egenskaper som ska samlas in av maskinvaruinventeringen. Du kan expandera klasser om du vill markera eller avmarkera enskilda egenskaper inuti klassen. Använd fältet **Sök efter lagerklasser** om du vill söka efter enskilda klasser.  

    > [!IMPORTANT]  
    >  När du lägger till nya klasser i Configuration Manager maskin varu inventering kommer storleken på inventerings filen som samlas in och skickas till plats servern att öka. Detta kan påverka nätverkets prestanda och Configuration Manager-platsen negativt. Aktivera endast inventeringsklasser som du vill samla in.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Lägga till en ny inventerings klass  

Du kan bara lägga till lager klasser från hierarkins toppnivå Server genom att ändra standard klient inställningarna. Det här alternativet är inte tillgängligt när du skapar anpassade enhetsinställningar.

1. I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

2. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

3. I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

4. I listan **enhets inställningar** väljer du **Ange klasser**.  

5. I dialog rutan **maskin varu lager klasser** väljer du **Lägg till**.  

6. I dialogrutan **Lägg till maskinvaruinventeringsklass** klickar du på **Anslut**.  

7. I dialogrutan **Anslut till WMI (Windows Management Instrumentation)** anger du namnet på den dator som du ska hämta WMI-klasserna från och det WMI-namnområde som ska användas för att hämta klasserna. Om du vill hämta alla klasser under det WMI-namnområde som du har angett klickar du på **Rekursivt**. Om den dator som du ansluter till inte är den lokala datorn anger du inloggningsuppgifterna för ett konto som har behörighet att komma åt WMI på fjärrdatorn.  

8. Välj **Anslut**.  

9. I dialog rutan **Lägg till maskin varu lager klass** går du till listan **inventerings klasser** och väljer de WMI-klasser som du vill lägga till i Configuration Manager maskin varu inventering.  

10. Om du vill redigera information om den valda WMI-klassen väljer du **Redigera**och anger följande information i dialog rutan **klass kvalificerare** :  

    - **Visnings namn** – det här namnet kommer att visas i Resursläsaren.  

    - **Egenskaper** – ange i vilken enhet som varje egenskap för WMI-klassen ska visas.  

      Du kan också ange egenskaper som en nyckelegenskap om du vill identifiera varje instans av klassen unikt. Om ingen nyckel definieras för klassen och flera instanser av klassen rapporteras från klienten lagras endast den senaste instansen som hittas i databasen.  

      När du är klar med att konfigurera egenskaperna klickar du på **OK** för att stänga dialog rutan **klass kvalificerare** och andra öppna dialog rutor. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Så här importerar du maskin varu lager klasser  

Du kan bara importera inventeringsklasser när du ändrar standardklientinställningarna. Du kan dock använda anpassade klient inställningar för att importera information som inte innehåller någon schema ändring, till exempel ändra egenskapen för en befintlig klass från **True** till **false**.  

1.  I Configuration Manager-konsolen väljer du **Administration** >  **klient inställningar** > **standard klient inställningar**.  

4.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

5.  I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

6.  I listan **enhets inställningar** väljer du **Ange klasser**.  

7.  Välj **Importera**i dialog rutan **maskin varu lager klasser** .  

8.  I dialog rutan **Importera** väljer du den Managed Object Format fil (MOF) som du vill importera och väljer sedan **OK**. Granska de objekt som ska importeras och klicka sedan på **Importera**.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Så här exporterar du maskin varu lager klasser  

1.  I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

4.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

5.  I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

6.  I listan **enhets inställningar** väljer du **Ange klasser**.  

7.  I dialog rutan **maskin varu lager klasser** väljer du **Exportera**.  

    > [!NOTE]  
    >  När du exporterar klasser exporteras alla markerade klasser.  

8.  I dialog rutan **Exportera** anger du den Managed Object Format fil (MOF) som du vill exportera klasserna till och väljer sedan **Spara**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Konfigurera maskin varu inventering för att samla in strängar som är större än 255 tecken
Från och med Configuration Manager 1802 kan du ange längden på strängar som är större än 255 tecken för maskin varu inventerings egenskaper. Den här ändringen gäller endast nyligen tillagda klasser och för maskin varu inventerings egenskaper som inte är nycklar. <!-- 1357389 -->

1. I arbets ytan **Administration** klickar du på **klient inställningar** Markera en klient enhets inställning som du vill redigera, högerklickar och väljer sedan **Egenskaper**.

2. Välj **maskin varu inventering**, sedan **Ange klasser**och **Lägg till**.

3. Klicka på knappen **Anslut** .

4. Fyll i **dator namn**, **WMI-namnrymd**, Välj **rekursivt** vid behov. Ange autentiseringsuppgifter om det behövs för att ansluta. Klicka på **Anslut** om du vill visa namn områdets klasser.

5. Välj en ny klass och klicka sedan på **Redigera**.

6. Ändra **längden** på din egenskap som är en sträng, förutom nyckeln, som är större än 255. Klicka på **OK**. 

7. Se till att den redigerade egenskapen har marker ATS för **Lägg till maskin varu inventerings klass** och klicka på **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Så här utökar du maskinvaruinventeringen med hjälp av MIF-filer (Management Information Format)  
 Använd MIF-filer (Management information format) för att utöka maskin varu inventerings information som samlas in från klienter av Configuration Manager. Under maskinvaruinventeringen läggs informationen som lagrats i MIF-filer till i klientinventeringsrapporten och lagras i platsdatabasen, där du kan använda informationen på samma sätt som du använder vanliga klientinventeringsdata. Det finns två typer av MIF-filer, NOIDMIF och IDMIF.

> [!IMPORTANT]  
>  Innan du kan lägga till information från MIF-filer i Configuration Manager-databasen måste du skapa eller importera klass information för dem. Mer information finns i avsnitten [lägga till en ny inventerings klass](#BKMK_Add) och [Importera maskin varu lager klasser](#BKMK_Import) i den här artikeln.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>Så här skapar du NOIDMIF-filer  
 NOIDMIF-filer kan användas för att lägga till information i en klient maskin varu inventering som normalt inte kan samlas in av Configuration Manager och som är kopplad till en viss klient enhet. Många företag etiketterar till exempel varje dator i organisationen med ett till gångs nummer och katalogiserar sedan numren manuellt. När du skapar en NOIDMIF-fil kan den här informationen läggas till i Configuration Manager-databasen och användas för frågor och rapporter. Information om hur du skapar NOIDMIF-filer finns i dokumentationen för Configuration Manager SDK.  

> [!IMPORTANT]  
>  När du skapar en NOIDMIF-fil måste den sparas i ANSI-kodat format. Det går inte att läsa NOIDMIF-filer som sparats i UTF-8-kodat format av Configuration Manager.  

 När du har skapat en NOIDMIF-fil sparar du den i mappen _% windir%_**\CCM\Inventory\Noidmifs** på varje klient. Configuration Manager samlar in information från NODMIF-filer i den här mappen under nästa schemalagda maskin varu inventerings cykel.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a>Så här skapar du IDMIF-filer  
 IDMIF-filer kan användas för att lägga till information om till gångar som inte kan inventeras av Configuration Manager och som inte är associerade med en viss klient enhet till Configuration Manager-databasen. Du kan till exempel använda IDMIF för att samla in information om projektorer, DVD-spelare, Foto kopiatorer eller annan utrustning som inte har en Configuration Manager-klient. Information om hur du skapar IDMIF-filer finns i dokumentationen för Configuration Manager SDK.  

 När du har skapat en IDMIF-fil sparar du den i mappen _% windir%_**\CCM\Inventory\Idmifs** på klient datorer. Configuration Manager samlar in information från den här filen under nästa schemalagda maskin varu inventerings cykel. Du måste deklarera nya klasser för information som finns i filen genom att lägga till eller importera dem.  

> [!NOTE]
> MIF-filer kan innehålla stora mängder data och insamlingen av dessa data kan påverka platsens prestanda negativt. Aktivera endast MIF-samling vid behov och konfigurera alternativet **maximal storlek på anpassad MIF-fil (KB)** i inställningarna för maskin varu inventering. Mer information finns i [Introduktion till maskin varu inventering](introduction-to-hardware-inventory.md).
