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
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427746"
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

## <a name="methods"></a>Metoder

### <a name="enable-or-disable"></a>Aktivera eller inaktivera

Aktivera eller inaktivera vissa av alla attribut för en klass som redan finns på klienten. Den här åtgärden instruerar maskin varu inventerings agenten att samla in den på klienter. Du kan utföra den här åtgärden i standard klient inställningar eller anpassade enhets klient inställningar. Mer information finns i [Aktivera eller inaktivera befintliga inventerings klasser](#BKMK_Enable).

### <a name="add"></a>Lägg till

Om en WMI-klass finns på klienten och är känd för platsen, innehåller den här åtgärden den för en möjlig uppsättning maskin varu lager klasser. Du kan lägga till en ny inventeringsklass från en annan enhets WMI-namnområde. Den här åtgärden är endast på standard klient inställningar. Mer information finns i [lägga till en ny inventerings klass](#BKMK_Add).

### <a name="extend"></a>Utöka

Lägg till en ny WMI-klass till klienten. Om du vill utöka maskin varu inventeringen manuellt redigerar du Configuration. MOF på platsen på den översta nivån.<!-- SCCMDocs#1073 -->

Om WMI-klassen inte redan finns på klienten, måste du utöka WMI-schemat:

1. Redigera Configuration. MOF på platsen på den översta nivån. Granska **Dataldr. log** för att se platsen Lägg till den.

1. Uppdatera principen på en klient och vänta tills den nya klassen kompileras.

1. Använd standard klient inställningar för att [lägga till](#add) den nya klassen i maskin varu inventeringen. Du behöver inte aktivera den här klassen i standard klient inställningarna. Du kan sedan aktivera den i en anpassad enhets klient inställning.

### <a name="import-and-export"></a>Importera och exportera

Använd Configuration Manager-konsolen för att importera och exportera Managed Object Format-filer (MOF) som innehåller lager klasser. Mer information finns i [Importera maskin varu lager klasser](#BKMK_Import) och [Exportera maskin varu lager klasser](#BKMK_Export).

### <a name="create-noidmif-files"></a>Skapa NOIDMIF-filer

Använd NOIDMIF-filer för att samla in information om klient enheter som Configuration Manager inte kan inventera. Du kan till exempel samla in information om enheternas till gångs nummer som endast finns som en etikett på enheten. NOIDMIF-inventeringen associeras automatiskt med klientenheten som den samlats in från. Mer information finns i [skapa NOIDMIF-filer](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>Skapa IDMIF-filer

Använd IDMIF-filer för att samla in information om till gångar i organisationen som inte är associerade med en Configuration Manager-klient. Till exempel projektorer, Foto kopiatorer och nätverks skrivare. Mer information finns i [skapa IDMIF-filer](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Procedurer för att utöka maskinvaruinventeringen

Dessa steg beskriver hur du konfigurerar standardklientinställningarna för maskinvaruinventering. Inställningarna tillämpas på alla klienter i hierarkin. Om du vill att inställningarna bara ska gälla för vissa klienter skapar du en anpassad klienten hets inställning och tilldelar den till en samling med vissa klienter. Mer information finns i [så här konfigurerar du klient inställningar](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Aktivera eller inaktivera befintliga inventerings klasser  

1. I Configuration Manager-konsolen väljer du **Administration**  >  **klient inställningar**  >  **standard klient inställningar**.  

1. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

1. I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

1. I listan **enhets inställningar** väljer du **Ange klasser**.  

1. I dialogrutan **Maskinvarulagerklasser** markerar eller avmarkerar du de klasser och egenskaper som ska samlas in av maskinvaruinventeringen. Du kan expandera klasser om du vill markera eller avmarkera enskilda egenskaper inuti klassen. Använd fältet **Sök efter lagerklasser** om du vill söka efter enskilda klasser.  

    > [!IMPORTANT]  
    >  När du lägger till nya klasser i Configuration Manager maskin varu inventering kommer storleken på inventerings filen som samlas in och skickas till plats servern att öka. Detta kan påverka nätverkets prestanda och Configuration Manager-platsen negativt. Aktivera endast inventeringsklasser som du vill samla in.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Lägg till en ny inventerings klass  

Du kan bara lägga till inventerings klasser från hierarkins översta Server genom att ändra standard klient inställningarna. Det här alternativet är inte tillgängligt när du skapar anpassade enhets inställningar.

1. I Configuration Manager-konsolen väljer du **Administration**  >  **klient inställningar**  >  **standard klient inställningar**.  

1. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

1. I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

1. I listan **enhets inställningar** väljer du **Ange klasser**.  

1. I dialog rutan **maskin varu lager klasser** väljer du **Lägg till**.  

1. I dialog rutan **Lägg till maskin varu inventerings klass** väljer du **Anslut**.  

1. I dialog rutan **Anslut till Windows Management Instrumentation (WMI)** anger du namnet på den dator från vilken du ska hämta WMI-klasserna och WMI-namnrymden som ska användas för att hämta klasserna. Om du vill hämta alla klasser under det WMI-namnområde som du har angett väljer du **rekursivt**. Om datorn som du ansluter till inte är den lokala datorn anger du autentiseringsuppgifter för ett konto som har behörighet att komma åt WMI på fjärrdatorn.

1. Välj **Anslut**.  

1. I dialog rutan **Lägg till maskin varu lager klass** går du till listan **inventerings klasser** och väljer de WMI-klasser som du vill lägga till i Configuration Manager maskin varu inventering.  

1. Om du vill redigera information om den valda WMI-klassen väljer du **Redigera**och anger följande information i dialog rutan **klass kvalificerare** :  

    - **Visnings namn**: det här namnet kommer att visas i Resursläsaren.  

    - **Egenskaper**: Ange de enheter där varje egenskap för WMI-klassen ska visas.  

      Du kan också ange egenskaper som en nyckel egenskap för att unikt identifiera varje instans av klassen. Om ingen nyckel definieras för klassen och flera instanser av klassen rapporteras från klienten lagras endast den senaste instansen som hittas i databasen.  

      När du är klar med att konfigurera egenskaperna väljer du **OK** för att stänga dialog rutan **klass kvalificerare** och andra öppna dialog rutor.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Importera maskin varu lager klasser

Du kan bara importera inventeringsklasser när du ändrar standardklientinställningarna. Du kan dock använda anpassade klient inställningar för att importera information som inte innehåller någon schema ändring, till exempel ändra egenskapen för en befintlig klass från **True** till **false**.  

1. I Configuration Manager-konsolen väljer du **Administration**  >   **klient inställningar**  >  **standard klient inställningar**.

1. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

1. I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

1. I listan **enhets inställningar** väljer du **Ange klasser**.  

1. Välj **Importera**i dialog rutan **maskin varu lager klasser** .  

1. I dialog rutan **Importera** väljer du den Managed Object Format fil (MOF) som du vill importera och väljer sedan **OK**. Granska de objekt som ska importeras och välj sedan **Importera**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Exportera maskin varu lager klasser  

1. I Configuration Manager-konsolen väljer du **Administration**  >  **klient inställningar**  >  **standard klient inställningar**.  

1. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

1. I dialog rutan **Inställningar för standard klient** väljer du **maskin varu inventering**.  

1. I listan **enhets inställningar** väljer du **Ange klasser**.  

1. I dialog rutan **maskin varu lager klasser** väljer du **Exportera**.  

    > [!NOTE]  
    > När du exporterar klasser exporteras alla markerade klasser.  

1. I dialog rutan **Exportera** anger du den Managed Object Format fil (MOF) som du vill exportera klasserna till och väljer sedan **Spara**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Konfigurera maskin varu inventering för att samla in strängar som är större än 255 tecken

Du kan ange längden på strängar som är större än 255 tecken för maskin varu inventerings egenskaper. Den här åtgärden gäller endast nyligen tillagda klasser och för maskin varu inventerings egenskaper som inte är nycklar. <!-- 1357389 -->

1. I arbets ytan **Administration** väljer du **klient inställningar**. Välj en klient enhets inställning som du vill redigera och välj sedan **Egenskaper**.

1. Välj **maskin varu inventering**, sedan **Ange klasser**och **Lägg till**.

1. Välj **Anslut**.

1. Fyll i **dator namn**, **WMI-namnrymd**, Välj **rekursivt** vid behov. Ange autentiseringsuppgifter om det behövs för att ansluta. Välj **Anslut** om du vill visa namn områdes klasserna.

1. Välj en ny klass och välj sedan **Redigera**.

1. Ändra **längden** på din egenskap som är en sträng, förutom nyckeln, som är större än 255. Välj **OK**.

1. Kontrol lera att den redigerade egenskapen har marker ATS för **Lägg till maskin varu inventerings klass**och välj **OK**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Använd MIF-filer för att utöka maskin varu inventeringen

Använd MIF-filer (Management information format) för att utöka maskin varu inventerings information som samlas in från klienter av Configuration Manager. Under maskinvaruinventeringen läggs informationen som lagrats i MIF-filer till i klientinventeringsrapporten och lagras i platsdatabasen, där du kan använda informationen på samma sätt som du använder vanliga klientinventeringsdata. Det finns två typer av MIF-filer: NOIDMIF och IDMIF.

> [!IMPORTANT]  
> Innan du kan lägga till information från MIF-filer i Configuration Manager-databasen måste du skapa eller importera klass information för dem. Mer information finns i avsnitten [lägga till en ny inventerings klass](#BKMK_Add) och [Importera maskin varu lager klasser](#BKMK_Import) i den här artikeln.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>Skapa NOIDMIF-filer

NOIDMIF-filer kan användas för att lägga till information i en klient maskin varu inventering som normalt inte kan samlas in av Configuration Manager och som är kopplad till en viss klient enhet. Många företag etiketterar till exempel varje dator i organisationen med ett till gångs nummer och katalogiserar sedan numren manuellt. När du skapar en NOIDMIF-fil kan den här informationen läggas till i Configuration Manager-databasen och användas för frågor och rapporter. Information om hur du skapar NOIDMIF-filer finns i dokumentationen för Configuration Manager SDK.  

> [!IMPORTANT]  
> När du skapar en NOIDMIF-fil måste den sparas i ANSI-kodat format. Det går inte att läsa NOIDMIF-filer som sparats i UTF-8-kodat format av Configuration Manager.  

När du har skapat en NOIDMIF-fil sparar du den i `%Windir%\CCM\Inventory\Noidmifs` mappen på varje klient. Configuration Manager samlar in information från NODMIF-filer i den här mappen under nästa schemalagda maskin varu inventerings cykel.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a>Skapa IDMIF-filer

IDMIF-filer kan användas för att lägga till information om till gångar som inte kan inventeras av Configuration Manager och som inte är associerade med en viss klient enhet till Configuration Manager-databasen. Du kan till exempel använda IDMIF för att samla in information om projektorer, DVD-spelare, Foto kopiatorer eller annan utrustning som inte har en Configuration Manager-klient. Information om hur du skapar IDMIF-filer finns i dokumentationen för Configuration Manager SDK.  

När du har skapat en IDMIF-fil sparar du den i `%Windir%\CCM\Inventory\Idmifs` mappen på klient datorerna. Configuration Manager samlar in information från den här filen under nästa schemalagda maskin varu inventerings cykel. Deklarera nya klasser för information som finns i filen genom att lägga till eller importera dem.  

> [!NOTE]
> MIF-filer kan innehålla stora mängder data och insamlingen av dessa data kan påverka platsens prestanda negativt. Aktivera endast MIF-samling vid behov och konfigurera alternativet **maximal storlek på anpassad MIF-fil (KB)** i inställningarna för maskin varu inventering. Mer information finns i [Introduktion till maskin varu inventering](introduction-to-hardware-inventory.md).
