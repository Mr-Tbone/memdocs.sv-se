---
title: Teknisk för hands version 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1712 för Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721278"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Funktioner i Technical Preview 1712 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1712. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. 

Granska [teknisk för hands version för Configuration Manager](technical-preview.md) innan du installerar den här versionen av Technical Preview. I artikeln får du bekanta dig med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Kända problem i den här tekniska för hands versionen:**
- **Uppdatering till en ny för hands version Miss lyckas när du har en plats server i passivt läge**. Om du har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)måste du avinstallera plats servern för passivt läge innan du uppdaterar till den nya för hands versionen. Du kan installera om den passiva läges plats servern efter att platsen har slutfört uppdateringen.

  Så här avinstallerar du plats servern för passivt läge:
  1. I Configuration Manager-konsolen går du till **Administration** > **Översikt** > **plats konfigurations** > **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.
  <!--sms489412-->


**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Uppgradera inte ersatta program automatiskt
<!-- 1351266 -->
I den här versionen har du möjlighet att konfigurera en program distribution för att inte automatiskt uppgradera eventuella ersatta versioner, baserat på [feedback från användarna](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior) Nu när du skapar distributionen, på sidan **distributions inställningar** i **guiden distribuera program vara**, för antingen **tillgängligt** eller **obligatoriskt** installations syfte, kan du aktivera eller inaktivera alternativet för att **automatiskt uppgradera alla ersatta versioner av programmet**.


## <a name="install-multiple-applications-in-software-center"></a>Installera flera program i Software Center
<!-- 1357126 -->
Om en slutanvändare eller Skriv bords tekniker behöver installera flera program på en enhet, har Software Center nu stöd för att installera flera valda program. Detta gör att användaren är mer effektiv men väntar på att en installation ska slutföras innan du startar nästa.

När du använder Multi-SELECT-läge på fliken **program** , avgör följande kriterier vilka appar Software Center aktiverar för flera markeringar:
- Appen är synlig för användaren
- Appen är inte redan installerad
- Administratörs godkännande krävs inte eller har redan beviljats
- Appens status är tillgänglig (till exempel inte redan hämtat innehåll)

### <a name="try-it-out"></a>prova!
**I Configuration Manager-konsolen:** Distribuera till en användare eller enhet flera program för installation, antingen tillgängligt eller obligatoriskt (med tids gränsen i framtiden). Kräv inte administratörs godkännande. Mer information finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).

**I Software Center:**
 1. Fliken **program** ska öppnas som standard. 
 2. Om du vill ange Multi-SELECT-läge i listvyn klickar du på ikonen ny ![Ikon för Software Center-flera val](media/software-center-multi-select-apps.png) i det övre högra hörnet.
 3. Välj två eller fler appar som ska installeras genom att klicka på kryss rutan till vänster om apparna i listan.
 4. Klicka på knappen **Installera markerad** .

Apparna installeras som vanligt, bara nu i följd.


## <a name="client-based-pxe-responder-service"></a>Klient-based PXE responder service
<!-- 1357148 -->
En vanlig utmaning för kunder är att tillhandahålla PXE-tjänster på fjärr-och avdelnings kontor med lite eller ingen server infrastruktur. Distributions plats rollen stöder klient operativ system, men kan inte PXE-aktive ras på grund av beroendet av Windows Deployment Services.

Nya klient inställningar är nu tillgängliga för att aktivera en PXE responder-tjänst på Configuration Manager klienter. En PXE-aktiverad start avbildning måste finnas i PXE-svars klientens cacheminne.

### <a name="try-it-out"></a>prova!
Se till att det inte finns några befintliga PXE-aktiverade distributions platser eller andra PXE-servrar i test miljön som kan vara i konflikt med den här klienten PXE-svarare.

I Configuration Manager-konsolen:
1. I arbets ytan **program bibliotek** under **operativ system**: **skapa en aktivitetssekvens med**hjälp av den anpassade mallen.
   1. Klicka på **Lägg till**, Välj **Allmänt**och sedan **variabel steget Ange aktivitetssekvens** . Ange **SMSTSPersistContent** som variabel för aktivitetssekvensen och ange värdet **Sant**.
   1. Klicka på **Lägg till**, Välj **program vara**och sedan steget **Ladda ned paket innehåll** . Klicka på Gold-asterisken och välj sedan en PXE-aktiverad start avbildning. Ta med både x86 och x64-start avbildningar. Konfigurera steget för att placera det i **Configuration Manager-klientcachen**.
   1. Klicka på **Lägg till**, Välj **Allmänt**och sedan **variabel steget Ange aktivitetssekvens** . Ange **SMSTSPreserveContent** som variabel för aktivitetssekvensen och ange värdet **Sant**.
2. I arbets ytan **Administration** under **klient inställningar**: skapa en anpassad princip för klient enhets inställningar.
   1. Välj gruppen **Inställningar för klient-cache** .
   1. Ställ in inställningen **aktivera Configuration Manager klienten i fullständigt operativ system för att dela innehålls** inställningen till **Ja**.
   1. Ställ in inställningen **Aktivera PXE responder-tjänsten** på **Ja**.
   1. För inställningen **skapa ett självsignerat certifikat eller importera ett PKI-klientcertifikat** klickar du på **Ange ett certifikat**. Välj **Importera certifikat** om test miljön har PKI, annars klickar du på **OK** för att skapa ett självsignerat certifikat. 
   1. Konfigurera de återstående inställningarna efter behov för din test miljö. (Standardinställningarna bör fungera om det inte finns särskilda nätverks-eller säkerhets krav.)
3. Distribuera aktivitetssekvensen och anpassade klient inställningar till en samling mål klienter som PXE-svarare. Vänta tills principerna verkställs och att aktivitetssekvensen körs.
4. Starta en annan klient i samma undernät för PXE/nätverks start som normalt.

### <a name="known-issues"></a>Kända problem
- I redigeraren för aktivitetssekvenser visas en röd felikon för steget **Ladda ned paket innehåll** när du lägger till en start avbildning, men aktivitetssekvensen sparas. Om du öppnar den här aktivitetssekvensen igen i redigeraren visas även en ofarlig varning om att det inte går att hitta refererade objekt. <!-- sms427542 -->
- Start avbildningen från steget Ladda ned paket innehåll visas inte i den anpassade aktivitetssekvensen lista över referenser. Åtgärden **distribuera innehåll** är även tillgänglig. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Ändra i Configuration Manager-klient installationen  
Som ett resultat av din röst feedback för användare [installeras Silverlight inte längre på klienterna automatiskt.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Ändra till instrument panelen för Surface-enheter
På Surface-instrumentpanelen visas nu versioner av inbyggd program vara för Surface-enheter istället för operativ systemets version. I-konsolen går du till **övervakning** > av**Surface-enheter**. Du kan visa följande objekt:
- Procent av ytor
- Procent av Surface-modeller
- De fem främsta versionerna av inbyggd program vara
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Förbättringar av instrument panelen för Office 365-klient hantering 
På instrument panelen för Office 365-klient hantering visas nu en lista över relevanta enheter när diagram avsnitt är markerade. I-konsolen går du till**Översikt över** > **program varu bibliotek** >**Office 365-klient hantering**. Instrument panelen visas till höger. Om du väljer kriterier i diagrammet visas en lista över enheter.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Förbättringar av Configuration Manager-konsolen 
Vi har gjort följande förbättringar i Configuration Manager-konsolen, som var resultatet av din röst feedback från användaren.

- [Enhets lista visar primär användare](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): enhets listor under till gångar och efterlevnad, enheter, visar nu den primära användaren som standard. Den senast inloggade användaren kan också läggas till som en valfri kolumn. <!-- 1357280 -->
- [Byta namn på samlingar visas i befintliga samlings medlemskaps regler](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): om en samling är medlem i en annan samling och den har bytt namn, uppdateras det nya namnet under medlemskaps regler.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Förbättringar av operativ Systems distribution
Vi har gjort följande förbättringar av operativ Systems distributionen, varav vissa var resultatet av din röst feedback från användaren.
- [Standard logg visare i Start avbildningen](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): i Windows PE uppmanas du inte längre att välja om du vill göra det här programmet till standard visnings programmet för loggfiler när du startar CMTrace. exe. <!-- SMS 500897 -->
- Hämta paket innehålls steg: nu kan du lägga till Start avbildningar i det här steget i aktivitetssekvensen.


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 feedback Hub-appens integrering

Vi älskar feedback så mycket att vi nu har aktiverat feedback via [appen för feedback Hub](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) som är inbyggd i Windows 10. När du **lägger till nya kommentarer**, se till att välja kategorin **företags hantering** och välj sedan någon av följande under Kategorier:
- Configuration Manager-klient
- Configuration Manager-konsolen
- Configuration Manager OS-distribution
- Configuration Manager Server

Fortsätt att använda vår [röst sida för användare](https://configurationmanager.uservoice.com/) för att rösta på nya funktions idéer i Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
