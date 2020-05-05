---
title: Teknisk för hands version 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1710 för Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 503bb6d2293b4b5efb1d84980225a9d7052e1656
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721299"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Funktioner i Technical Preview 1710 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1710. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Kända problem i den här tekniska för hands versionen:**
- **Stöd för Windows 10, version 1709 (även kallat uppdaterings uppdateringen)**.  Från och med den här Windows-versionen innehåller Windows Media flera versioner. När du konfigurerar en aktivitetssekvens för att använda ett uppgraderings paket för operativ system eller en operativ system avbildning måste du välja en [version som stöds för användning av Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Uppdatering till en ny för hands version Miss lyckas när du har en plats server i passivt läge**. När du kör en för hands version som har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), måste du avinstallera plats servern för passivt läge innan du kan uppdatera för hands versions platsen till den nya för hands versionen. Du kan installera om den passiva läges plats servern efter att platsen har slutfört uppdateringen.

  Så här avinstallerar du plats servern för passivt läge:
  1. I-konsolen går du till **Administration** > **Översikt** > **plats konfigurations** > **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.

**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Förbättringar för distribution av PowerShell-skript från Configuration Manager
I den här versionen stöder PowerShell-skript som du distribuerar nu användning av följande förbättringar: 
- **Säkerhets omfattningar**.  Skript använder nu säkerhets omfattningar för att styra skript redigering och körning. Detta görs genom att tilldela taggar som representerar användar grupper. Mer information om hur du använder säkerhets omfattningar finns i [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Real tids övervakning**. När du övervakar körningen av ett skript är det nu i real tid när skriptet körs.
- **Parameter validering**. Varje parameter i skriptet har en dialog ruta för **skript parameter egenskaper** där du kan lägga till verifiering för den parametern. När du har lagt till valideringen bör du få fel meddelanden om du anger ett värde för en parameter som inte uppfyller verifieringen.

Distribution av PowerShell-skript introducerades först i teknisk för hands [version för hands version 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Ytterligare förbättringar levererades med [Tech preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) och sedan [Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>prova!

Om du vill prova att använda funktionen kör skript, se [skapa och köra skript](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Begränsa Windows 10 Enhanced data så att endast data som är relevanta för Windows Analytics skickas Enhetens hälsotillstånd
<!-- 1356148 -->

I den här versionen kan du nu ställa in Windows 10-diagnostikens data insamlings nivå till **utökad (begränsad)**. Med den här inställningen kan du få användbara insikter om enheter i din miljö utan att enheterna rapporterar alla data på den **förbättrade** nivån med Windows 10 version 1709 eller senare.

Nivån utökad (begränsad) inkluderar mått från Basic-nivån, samt en delmängd av data som samlas in från den **förbättrade** nivån som är relevant för Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center förvränger inte längre ikoner som är större än 250x250  
<!-- 1356194 -->

I den här versionen kommer Software Center inte längre att snedvrida ikoner som är större än 250x250. Software Center gjorde sådana ikoner mer suddiga. Nu kan du ange en ikon med en pixel dimension på upp till 512x512 och den visas utan förvrängning.

### <a name="try-it-out"></a>prova!
Lägg till en ikon för din app i Software Center. Se [skapa program](../../apps/deploy-use/create-applications.md)om du vill testa det.


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Kontrol lera efterlevnad från Software Center för samhanterade enheter
<!-- 1356374 -->
I den här versionen kan användare använda Software Center för att kontrol lera efterlevnaden av sina samhanterade Windows 10-enheter även när villkorlig åtkomst hanteras av Intune. Mer information finns i [Co-Management för Windows 10-enheter](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Stöd för sårbarhets skydd
Den här versionen lägger till stöd för Windows Defender sårbarhet Guard. Du kan konfigurera och distribuera principer som hanterar alla fyra komponenter i sårbarhets Guard. Dessa komponenter omfattar:
-   Minska attackytan
-   Reglerad mappåtkomst
-   Sårbarhetsskydd
-   Nätverks skydd

Efterlevnadsprinciper för distribution av sårbarhets Guard-principer är tillgänglig i Configuration Manager-konsolen.

Mer information om sårbarhets skydd och vissa komponenter och regler finns i [Windows Defender sårbarhet Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) i dokumentations biblioteket för Windows.

### <a name="prerequisites"></a>Krav
Hanterade enheter måste köra Windows 10 1709 är Creators Update eller senare och uppfyller följande krav beroende på de komponenter och regler som har kon figurer ATS:

|Sårbarhets skydds komponent |Ytterligare krav|
|------------------------|------------------------|
| Minska attackytan  | [Windows Defender av real tids skydd]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) måste vara aktiverat på enheterna.  |
| Reglerad mappåtkomst  | [Windows Defender av real tids skydd]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) måste vara aktiverat på enheterna.   |
| Sårbarhetsskydd  | Inga  |
| Nätverks skydd  |  [Windows Defender av real tids skydd]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) måste vara aktiverat på enheterna.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Skapa en princip för sårbarhets skydd  <!--1355468 -->
1. Gå till **till gångar och efterlevnad** > **Endpoint Protection**i Configuration Manager-konsolen och klicka sedan på **Windows Defender sårbarhets skydd**.
2. På fliken **Start** går du till gruppen **skapa** och klickar på **Skapa princip för sårbarhet**.
3. Ange ett namn och en valfri beskrivning för konfigurationsobjektet på sidan **Allmänt** i guiden **Skapa konfigurationsobjekt**.
4. Välj sedan de komponenter för sårbarhets skydd som du vill hantera med den här principen. För varje komponent som du väljer kan du konfigurera ytterligare information.
   - **Minskning av attack ytan:** Konfigurera Office hot, skript hot och e-posthoten som du vill blockera eller granska. Du kan också undanta vissa filer eller mappar från den här regeln.
   - **Reglerad mappåtkomst:** Konfigurera blockering eller granskning och Lägg sedan till appar som kan kringgå den här principen.  Du kan också ange ytterligare mappar som inte skyddas som standard.
   - **Sårbarhets skydd:**  Ange en XML-fil som innehåller inställningar för att minimera utnyttjandet av system processer och appar. Du kan exportera dessa inställningar från Windows Defender Security Center-appen på en Windows 10-enhet.
   - **Nätverks skydd:** Ange Nätverks skydd för att blockera eller granska åtkomst till misstänkta domäner.
5. Slutför guiden för att skapa principen, som du senare kan distribuera till enheter.

### <a name="deploy-an-exploit-guard-policy"></a>Distribuera en princip för sårbarhets skydd     
När du har skapat principer för sårbarhets skydd kan du distribuera dem med hjälp av guiden Distribuera sårbarhets skydds princip. Det gör du genom att öppna Configuration Manager-konsolen till **till gångar och efterlevnad** > **Endpoint Protection**och sedan klicka på **distribuera sårbarhets Guard-princip**.

## <a name="limited-support-for-cng-certificates"></a>Begränsat stöd för CNG-certifikat
<!-- 1356191 -->
Från och med den här versionen kan du nu använda [Cryptography-API: t. ex. CNG-](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) certifikatmallar för följande scenarier:

- Klient registrering och kommunikation med en HTTPS-hanterings plats.   
- Program distribution och program distribution med en HTTPS-distributions plats.   
- Distribution av operativsystem.  
- SDK för klient meddelanden (med senaste uppdatering) och ISV-proxy.   
- Cloud Management Gateway konfiguration.  

Om du vill använda CNG-certifikat måste din certifikat utfärdare (CA) tillhandahålla mallar för CNG-certifikat för mål datorer.  Mal Lav bildinformationen varierar beroende på scenariot. följande egenskaper krävs dock:

- Fliken **kompatibilitet**

    - **Certifikat utfärdaren** måste vara Windows Server 2008 eller senare. (Windows Server 2012 rekommenderas.)

    - **Certifikat mottagaren** måste vara Windows Vista/Server 2008 eller senare. (Windows 8/Windows Server 2012 rekommenderas.)

- Fliken **kryptografi**

    - **Leverantörs kategori** måste vara **nyckel lagrings leverantör**.  Kunna

För bästa resultat rekommenderar vi att du skapar ämnes namnet från Active Directory information.  Använd DNS-namnet för **ämnes namnets format** och inkludera DNS-namnet i det alternativa ämnes namnet.  Annars måste du ange den här informationen när enheten registreras i certifikat profilen.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Förbättrade beskrivningar för väntande omstarter av datorer   <!--1356283 -->
I [Technical preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)lade vi till funktionen för att identifiera enheter som väntar på en omstart från Configuration Manager-konsolen.

Från och med den här tekniska för hands versionen visar konsolen ytterligare information som innehåller information om den process eller åtgärd som begär omstart.

## <a name="device-guard-policy-changes----1355092---"></a>Ändringar i Device Guard-princip <!-- 1355092 -->
Med 1710 Technical Preview-versionen har följande tre ändringar gjorts i förhållande till Device Guard-principer:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Device Guard-principer har bytt namn till Windows Defender Application Control-principer
Device Guard-principer har bytt namn till Windows Defender program kontroll principer. Till exempel heter **guiden skapa enhets skydds princip** guiden **skapa Windows Defender Application Control-princip**.

### <a name="restart-is-not-required-to-apply-policies"></a>Det krävs ingen omstart för att tillämpa principer
Från och med uppdaterings uppdateringen för Windows version 1709 kräver enheter som använder den nya versionen av Windows inte någon omstart för att tillämpa Windows Defender-program kontroll principer.

Att starta om är standardinställningen.

#### <a name="try-it-out"></a>prova!  

Följ dessa steg om du vill inaktivera omstarter:

1.  Öppna guiden **Skapa princip för program kontroll i Windows Defender** .
2.  På sidan **Allmänt** avmarkerar du kryss rutan för **tvinga fram en omstart av enheter så att den här principen kan tillämpas för alla processer**.
3.  Klicka på **Nästa** tills guiden har slutförts.

För äldre versioner av Windows tillämpas en automatisk omstart fortfarande.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Kör program vara som är betrodd av Intelligent Security Graph automatiskt

Administratörer har nu möjlighet att tillåta att låsta enheter kör betrodd program vara med ett bra rykte, vilket bestäms av Microsoft Intelligent Security Graph (ISG). ISG består av Windows Defender SmartScreen och andra Microsoft-tjänster.

Enheterna måste köra Windows Defender SmartScreen för att program varan ska vara betrodd.

#### <a name="try-it-out"></a>prova!  

Följ dessa steg om du vill låta en enhet som kör Windows Defender SmartScreen köra betrodd program vara:

1.  Öppna **guiden Skapa princip för program kontroll i Windows Defender**.
2.  På sidan **inkluderingar** markerar du kryss rutan för **att auktorisera program vara som är betrodd av intelligent Security Graph**.
3.  Lägg till de filer och mappar som du vill ska vara betrodda i rutan **betrodda filer eller** mappar.
4.  Klicka på **Nästa** tills guiden har slutförts.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Konfigurera och distribuera Windows Defender Application Guard-principer <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) är en ny Windows-funktion som hjälper dig att skydda dina användare genom att öppna obetrodda webbplatser i en säker isolerad behållare som inte är tillgänglig för andra delar av operativ systemet. I den här tekniska för hands versionen har vi lagt till stöd för att konfigurera den här funktionen med Configuration Manager kompatibilitetsinställningar som du konfigurerar och sedan distribuera till en samling. Den här funktionen kommer att publiceras i för hands versionen för 64-bitars versionen av Windows 10 Creators uppdatering. Om du vill testa den här funktionen nu måste du använda en för hands version av den här uppdateringen.

### <a name="before-you-start"></a>Innan du börjar
För att kunna skapa och distribuera Windows Defender Application Guard-principer måste de Windows 10-enheter som du distribuerar principen till konfigureras med en princip för nätverks isolering. Mer information finns i blogg inlägget som refereras senare. Den här funktionen fungerar bara med de senaste Windows 10 Insider-versionerna. För att testa det måste dina klienter köra en ny Windows 10 Insider-version.

### <a name="try-it-out"></a>prova!

Läs [blogg inlägget](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)för att förstå grunderna om Windows Defender Application Guard.

Så här skapar du en princip och bläddrar bland de tillgängliga inställningarna:
1. I **Configuration Manager** -konsolen väljer du **till gångar och efterlevnad**.
2. I arbets ytan **till gångar och efterlevnad** väljer du **Översikt** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa Windows Defender Application Guard-princip**.
4. Med blogg inlägget som referens kan du bläddra bland och konfigurera de tillgängliga inställningarna för att testa funktionen.
5. I den här versionen har vi lagt till den nya nätverks definitions sidan i guiden. Här anger du företagets identitet och definierar företagets nätverks gränser.

    > [!NOTE]
    > Windows 10-datorer lagrar bara en lista över nätverks isolering på klienten. I den här versionen kan du skapa två olika typer av nätverks isolerings listor (en från Windows Information Protection och en från Windows Defender Application Guard) och distribuera dem till klienten. Om du distribuerar båda principerna måste dessa listor för nätverks isolering matcha. Om du distribuerar listor som inte matchar samma klient kommer distributionen att Miss Don.

    Du hittar mer information om hur du anger nätverks definitioner i [Windows Information Protection-dokumentationen] – [skydda dina företags data med Windows information Protection (Pia)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. När du är klar slutför du guiden och distribuerar principen till en eller flera Windows 10-enheter.

### <a name="further-reading"></a>Mer information

Läs mer om Windows Defender Application Guard i [det här blogg inlägget](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Mer information om fristående läge för Windows Defender Application Guard finns i [det här blogg inlägget](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
