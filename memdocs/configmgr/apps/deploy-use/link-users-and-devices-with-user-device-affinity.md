---
title: Länka användare och enheter med mappning mellan användare och enhet
titleSuffix: Configuration Manager
description: Länka användare och enheter med mappning mellan användare och enhet och distribuera appar automatiskt till alla enheter som är associerade med en användare.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710099"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Länka användare och enheter med mappning mellan användare och enhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Mappning mellan användare och enhet i Configuration Manager kopplar en användare till en eller flera enheter. Det här beteendet kan eliminera behovet av att känna till namnen på användarens enheter för att distribuera ett program till användaren. I stället för att distribuera programmet till var och en av användarens enheter distribuerar du programmet till användaren. Därefter ser mappning mellan användare och enhet automatiskt till att programmet installeras på alla enheter som är associerade med den användaren.  

Definiera primära enheter som användarna använder varje dag för sitt arbete. När du skapar en mappning mellan en användare och en enhet får du tillgång till fler alternativ för appdistribution. Om en användare till exempel kräver Microsoft Visio kan du installera det på användarens primära enhet med hjälp av en Windows Installer distribution. Men på en enhet som inte är en primär enhet kan du distribuera Visio som ett virtuellt program. Du kan också använda mappning mellan användare och enhet för att Fördistribuera program vara på en användares enhet när användaren inte är inloggad. När användaren loggar in är appen redan installerad och redo att köras.  

Du hanterar bara mappnings information för användare och enheter för datorer. Configuration Manager hanterar automatiskt mappningar mellan användare och enheter för de mobila enheter som den registrerar.  

## <a name="manually-set-up-user-device-affinity"></a>Konfigurera mappning mellan användare och enhet manuellt  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** .  

1. Välj en enhet. Välj **Redigera primära användare**i gruppen **enhet** på fliken **Start** i menyfliksområdet.  

1. I dialog rutan **Redigera primära användare** söker du efter och väljer de användare som ska läggas till som primära användare för den valda enheten. Välj **Lägg till**.  

    > [!NOTE]  
    > Listan med **primära användare** visar användare som redan är primära användare av enheten och den metod som varje användares enhets relation tilldelats.  

## <a name="set-up-primary-devices-for-a-user"></a>Konfigurera primära enheter för en användare  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **användare** .  

1. Välj en användare. På fliken **enhet** i menyfliksområdet väljer du **Redigera primära enheter**.  

1. I dialog rutan **Redigera primära enheter** söker du efter och väljer sedan de enheter som ska läggas till som primära enheter för den valda användaren. Välj **Lägg till**.  

    > [!NOTE]  
    > I listan med **primära enheter** visas enheter som redan har kon figurer ATS som primära enheter för den här användaren och den metod som varje användares enhets relation tilldelats.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Skapa mappningar mellan användare och enheter automatiskt (endast Windows-datorer)

Configuration Manager läser data om användar inloggnings händelser från händelse loggen i Windows. Om du vill skapa mappningar mellan användare och enheter automatiskt aktiverar du de här två alternativen i den lokala säkerhets principen på klient datorerna för att lagra inloggnings händelser i händelse loggen i Windows:  

- **Granska kontoinloggningshändelser**  
- **Granska inloggningshändelser**  

Använd Windows grupprincip om du vill konfigurera dessa inställningar.  

> [!IMPORTANT]  
> Om ett fel gör att Windows-händelseloggen genererar ett stort antal poster kan det skapa en ny händelse logg. Om detta inträffar kanske befintliga inloggnings händelser inte är tillgängliga för Configuration Manager.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Konfigurera platsen för att skapa mappningar mellan användare och enheter automatiskt  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **klient inställningar** .  

1. Om du vill ändra standard klient inställningarna väljer du **standard klient inställningar**. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.

    Om du vill skapa anpassade klient agent inställningar går du till gruppen **skapa** på fliken **Start** i menyfliksområdet och väljer **skapa anpassade klient enhets inställningar**.

    > [!NOTE]  
    > Om du ändrar standard klient inställningarna distribuerar-platsen dem till alla datorer i hierarkin. Mer information finns i [så här konfigurerar du klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

1. I gruppen **mappning mellan användare och enhet** anger du följande inställningar:  

    - **Tröskel för tillhörighet mellan användare och enhet (minuter)**: Ange antal minuter av enhets användning innan platsen skapar en mappning mellan användare och enhet.  

    - **Tröskel för tillhörighet mellan användare och enhet (dagar)**: Ange det antal dagar under vilka platsen mäter den användnings tillhörighets tröskeln.  

    - **Konfigurera automatiskt mappning mellan användare och enhet från användnings data**: Välj **Sant** om du vill att platsen automatiskt ska skapa mappningar mellan användare och enheter. Om du väljer **falskt**måste du godkänna alla mappningar mellan användare och enheter manuellt.  

    > [!TIP]  
    > Om du till exempel anger **tröskelvärdet för tillhörighet mellan användare och enhet (minuter)** till **60** minuter och anger värdet **5** dagar för **tillhörighet mellan användare och enhet (dagar)** , måste användaren använda enheten under minst 60 minuter under en period på fem dagar för att automatiskt skapa en mappning mellan användare och enhet.  

När Configuration Manager skapar en automatisk mappning mellan användare och enhet fortsätter den att övervaka tröskelvärden för tillhörighet mellan användare och enhet. Om användarens aktivitet för enheten hamnar under tröskelvärdena som du har angett tar platsen bort mappningen mellan användare och enhet. Ange **tröskelvärdet för tillhörighet mellan användare och enhet (dagar)** till ett värde på minst sju dagar. Den här konfigurationen förhindrar situationer där en automatiskt konfigurerad mappning mellan användare och enhet kan försvinna när användaren inte är inloggad, till exempel under helgen.  


## <a name="import-user-device-affinities-from-a-file"></a>Importera mappningar mellan användare och enheter från en fil

Om du vill skapa flera relationer samtidigt importerar du en fil som innehåller information om flera mappningar mellan användare och enheter. Kontrol lera att mål enheterna redan har identifierats av platsen och att de finns som resurser i den Configuration Manager databasen.  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer antingen noden **användare** eller **enheter** .  

1. Välj **Importera mappning mellan användare och enhet**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

1. På sidan **Välj mappning** i guiden Importera mappning mellan användare och enhet anger du följande information:  

    - **Fil namn**. Ange en fil med kommaavgränsade värden (CSV) som innehåller en lista över användare och enheter som du vill skapa en tillhörighet mellan. I den här filen måste varje användar-och enhets par finnas på en egen rad, med värden avgränsade med kommatecken. Använd det här formatet:`<domain>\<username>,<device NetBIOS name>`  

    - **Den här filen har kolumn rubriker i referens syfte**. Om CSV-filen har en rubrik på översta raden väljer du det här alternativet. Platsen ignorerar rubrik raden under importen.  

1. Om filen som du importerar har fler än två objekt på varje rad använder du **kolumn** och **tilldelar** för att ange vilka kolumner som representerar användare och enheter, och vilka kolumner som ska ignoreras under importen.  

1. Slutför guiden.  


## <a name="let-users-create-their-own-device-affinities"></a>Låt användarna skapa egna enhets tillhörigheter

Konfigurera en användare för att skapa en egen mappning mellan användare och enhet i Software Center.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Konfigurera-platsen så att den tillåter användare som skapats av användarens enhets tillhörighet  

1 i Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **klient inställningar** .  

1. Om du vill ändra standard klient inställningarna väljer du **standard klient inställningar**. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.

    Om du vill skapa anpassade klient agent inställningar går du till gruppen **skapa** på fliken **Start** i menyfliksområdet och väljer **skapa anpassade klient användar inställningar**.

    > [!NOTE]  
    > Om du ändrar standard klient inställningarna distribuerar-platsen dem till alla datorer i hierarkin. Mer information finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

1. I gruppen **mappning mellan användare och enhet** aktiverar du inställningen för att **tillåta att användare definierar sina primära enheter**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Konfigurera en mappning mellan användare och enhet i Software Center

Från och med version 1902, Använd Software Center för att ange tillhörighet.

1. Gå till fliken **alternativ** i Software Center.

1. I avsnittet **arbets uppgifter** väljer du alternativet **Jag använder regelbundet den här datorn för mitt arbete**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Konfigurera en mappning mellan användare och enhet i program katalogen

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. I program katalogen väljer du **Mina system**.  

1. Välj alternativet **Jag använder regelbundet den här datorn för mitt arbete**.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Hantera begäranden från användare om att skapa mappningar till enheter

När du inaktiverar klient inställningen för att **automatiskt konfigurera mappning mellan användare och enhet från användnings data**måste du godkänna alla mappningar mellan användare och enhet manuellt.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Godkänna eller avvisa en begäran om mappning mellan användare och enhet  

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

1. Välj den användar-eller enhets samling som du vill hantera tillhörighets begär Anden för.  

1. På fliken **Start** i menyfliksområdet i gruppen **samling** väljer du **Hantera tillhörighets begär Anden**.  

1. I dialog rutan **Hantera begär Anden om mappning mellan användare och enhet** väljer du en tillhörighets förfrågan och väljer sedan **Godkänn** eller **avvisa**.  


## <a name="next-steps"></a>Nästa steg

Du kan också använda Microsoft Intune för att hitta den primära användningen av en registrerad enhet. Mer information finns i [hitta den primära användaren av en Intune-enhet](https://docs.microsoft.com/intune/find-primary-user) i Intune-dokumentationen.
