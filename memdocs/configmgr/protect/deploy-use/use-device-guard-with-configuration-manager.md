---
title: Hantera Windows Defender Application Control
titleSuffix: Configuration Manager
description: Lär dig hur du använder Configuration Manager för att hantera Windows Defender Application Control.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0dcd519a7703b5de94f779dc5dbe48aa0d34a3bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700471"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Windows Defender program kontroll hantering med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

## <a name="introduction"></a>Introduktion
Windows Defender Application Control är utformat för att skydda datorer mot skadlig kod och annan icke-betrodd program vara. Det förhindrar att skadlig kod körs genom att se till att endast godkänd kod, som du vet, kan köras.

Windows Defender Application Control är ett programvarubaserad säkerhets lager som tillämpar en explicit lista över program som tillåts köras på en dator. Program kontroll har ingen egen maskin-eller firmware-förutsättning. Program kontroll principer som distribueras med Configuration Manager aktivera en princip på datorer i mål samlingar som uppfyller minimi kraven för Windows-version och SKU som beskrivs i den här artikeln. Du kan också aktivera hypervisor-baserat skydd av program kontroll principer som distribueras via Configuration Manager genom att grupprincip på kompatibel maskin vara.

Läs mer om Windows Defender Application Control i [Windows Defender Application Control Deployment Guide](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - Från och med Windows 10, version 1709, kallas kod integritets principer för Windows Defender för program kontroll.
   > - Från och med Configuration Manager version 1710 har Device Guard-principer bytt namn till Windows Defender-program kontroll principer.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Använda Windows Defender Application Control med Configuration Manager

Du kan använda Configuration Manager för att distribuera en Windows Defender-princip för program kontroll. Med den här principen kan du konfigurera det läge där Windows Defender-programkontrollen körs på datorer i en samling. 

Du kan konfigurera något av följande lägen:

1. **Tvingande aktive rad** – endast betrodda körbara filer får köras.
2. **Granska endast** – Tillåt att alla körbara filer körs, men logga ej betrodda körbara filer som körs i händelse loggen för den lokala klienten.

> [!Tip]  
> Den här funktionen introducerades först i version 1702 som en [för hands versions funktion](../../core/servers/manage/pre-release-features.md). Från och med version 1906 är det inte längre en för hands versions funktion.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Vad kan köras när du distribuerar en Windows Defender Application Control-princip?

Med Windows Defender Application Control kan du kontrol lera vad som kan köras på datorer som du hanterar. Den här funktionen kan vara användbar för datorer i hög säkerhets avdelningar, där det är viktigt att oönskad program vara inte kan köras.

När du distribuerar en princip kan följande körbara filer köras:

- Windows operativ Systems komponenter
- Maskin varu dev Center-drivrutiner (som har Windows Hardware Quality Labs-signaturer)
- Windows Store-appar
- Configuration Manager-klienten 
- All program vara som distribueras via Configuration Manager att datorer installeras efter att Windows Defender Application Control-principen har bearbetats. 
- Uppdateringar av Windows-komponenter från:
    - Windows Update
    - Windows Update för företag
    - Windows Server Update Services
    - Configuration Manager
    - Valfritt, program vara med goda rykte som bestäms av Microsoft Intelligent Security Graph (ISG). ISG innehåller Windows Defender SmartScreen och andra Microsoft-tjänster. Enheten måste köra Windows Defender SmartScreen och Windows 10 version 1709 eller senare för att program varan ska vara betrodd.

>[!IMPORTANT]
>Dessa objekt omfattar inte program som *inte* är inbyggda i Windows och som automatiskt uppdateras från Internet eller program uppdateringar från tredje part, oavsett om de installeras via någon av de uppdaterings mekanismer som nämns ovan eller från Internet. Endast program varu ändringar som distribueras, även om den Configuration Manager klienten kan köras.

## <a name="before-you-start"></a>Innan du börjar

Innan du konfigurerar eller distribuerar Windows Defender Application Control-principer bör du läsa följande information:

- Windows Defender Application Control Management är en för hands versions funktion för Configuration Manager och kan komma att ändras.
- Om du vill använda Windows Defender-programkontrollen med Configuration Manager måste datorer som du hanterar köra Windows 10 Enterprise version 1703 eller senare.
- När en princip har bearbetats på en klient dator konfigureras Configuration Manager som ett hanterat installations program på den klienten. Program vara som distribueras via den, efter att princip processerna har bearbetats, är automatiskt betrodda. Program vara som installeras av Configuration Manager innan Windows Defender Application Control-principens processer är inte automatiskt betrodda.
- Schemat för utvärdering av standard kompatibilitet för program kontroll principer, som kan konfigureras under distributionen, är en gång per dag. Om problem i princip bearbetningen observeras kan det vara fördelaktigt att konfigurera schema för utvärdering av kompatibilitet så att det blir kortare, till exempel en gång i timmen. Det här schemat avgör hur ofta klienter försöker att bearbeta en Windows Defender-princip för program kontroll om ett fel inträffar.
- Oavsett vilket tvingande läge du väljer, när du distribuerar en Windows Defender-princip för program kontroll, kan klient datorer inte köra HTML-program med fil namns tillägget. HTA.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Så här skapar du en Windows Defender Application Control-princip
1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.
2. I arbets ytan **till gångar och efterlevnad** expanderar du **Endpoint Protection**och klickar sedan på **Windows Defender Application Control**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa program kontroll princip**.
4. Ange följande inställningar på sidan **Allmänt** i **guiden Skapa program kontroll princip**:
    - **Namn** – ange ett unikt namn för den här Windows Defender Application Control-principen. 
    - **Beskrivning** – alternativt anger du en beskrivning för principen som hjälper dig att identifiera den i Configuration Manager-konsolen.
    - **Framtvinga omstart av enheter så att den här principen kan tillämpas för alla processer** – när principen har bearbetats på en klient dator schemaläggs en omstart av klienten enligt **klient inställningarna** för **omstart av datorn**.
        - Enheter som kör Windows 10 version 1703 eller tidigare startas alltid om automatiskt.
        - Från och med Windows 10 version 1709 kommer program som körs på enheten inte att ha den nya program kontroll principen tillämpad på dem förrän efter en omstart. Program som startas när principen tillämpas kommer dock att påverka den nya principen för program kontroll. 
    - **Tvingande läge** – Välj någon av följande tvingande metoder för Windows Defender Application Control på klient datorn.
        - **Tvångs åtgärd aktive rad** – Tillåt endast betrodda körbara filer.
        - **Granska endast** – Tillåt att alla körbara filer körs, men logga ej betrodda körbara filer som körs i händelse loggen för den lokala klienten.
5. På fliken **inkluderingar** i **guiden Skapa program kontroll princip**väljer du om du vill **auktorisera program vara som är betrodd av intelligent Security Graph**.
6. Klicka på **Lägg till** om du vill lägga till förtroende för vissa filer eller mappar på datorer. I dialog rutan **Lägg till betrodd fil eller mapp** kan du ange en lokal fil eller en mappsökväg som ska vara betrodd. Du kan också ange en fil-eller mappsökväg på en fjärran sluten enhet som du har behörighet att ansluta till. När du lägger till förtroende för specifika filer eller mappar i en Windows Defender-princip för program kontroll kan du:
    - Lösa problem med hanterade installations beteenden
    - Verksamhetsbaserade appar som inte kan distribueras med Configuration Manager
    - Lita på appar som ingår i en distributions avbildning för operativ system. 
8. Klicka på **Nästa**för att slutföra guiden.

>[!IMPORTANT]
>Det finns bara stöd för att inkludera betrodda filer eller mappar på klient datorer som kör version 1706 eller senare av Configuration Manager-klienten. Om eventuella inkluderings regler ingår i en Windows Defender-princip för program kontroll och principen distribueras till en klient dator som kör en tidigare version på den Configuration Manager klienten, kommer principen inte att tillämpas. Att uppgradera dessa äldre klienter löser problemet. Principer som inte innehåller några inkluderings regler kan fortfarande tillämpas på äldre versioner av Configuration Manager-klienten.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Så här distribuerar du en Windows Defender Application Control-princip
1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.
2. I arbets ytan **till gångar och efterlevnad** expanderar du **Endpoint Protection**och klickar sedan på **Windows Defender Application Control**.
3. I listan med principer väljer du den som du vill distribuera. gå sedan till fliken **Start** , gruppen **distribution** och klicka på **distribuera program kontroll princip**.
4. I dialog rutan **distribuera program kontroll princip** väljer du den samling som du vill distribuera principen till. Konfigurera sedan ett schema för när klienterna utvärderar principen. Slutligen väljer du om klienten kan utvärdera principen utanför några konfigurerade underhålls fönster.
5. När du är färdig klickar du på **OK** för att distribuera principen. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Övervaka en Windows Defender Application Control-princip

Använd informationen i artikeln [övervaka](../../compliance/deploy-use/monitor-compliance-settings.md) kompatibilitetsinställningar för att hjälpa dig att övervaka att den distribuerade principen har tillämpats på alla datorer på rätt sätt.

Om du vill övervaka bearbetningen av en Windows Defender Application Control-princip använder du följande loggfil på klient datorer:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

För att kontrol lera att den angivna program varan blockeras eller granskas, se följande händelse loggar för lokal klient:

1. Om du vill blockera och granska körbara filer använder du **program och tjänster för att logga**  >  **Microsoft**  >  **Windows**  >  **kod integritet**  >  **Operational**.
2. Om du vill blockera och granska Windows Installer-och skriptfiler använder du **program-och tjänst loggar**  >  **Microsoft**  >  **Windows**  >  **AppLocker**  >  **MSI och skript**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Säkerhets-och sekretess information för Windows Defender Application Control

- I den här för hands versionen ska du inte distribuera Windows Defender Application Control- **principer i en** produktions miljö. Det här läget är avsett att hjälpa dig att testa kapaciteten i en labb inställning.
- Enheter som har en princip som distribuerats till dem i **enbart gransknings** läge eller **tvingande aktiverat** läge och som inte har startats om för att genomdriva principen, är sårbara för ej betrodda program som installeras.
I den här situationen kan program varan fortsätta att kunna köras även om enheten startas om eller om du tar emot en princip i **tvingande aktiverat** läge.
- För att säkerställa att Windows Defender Application Control-principen är effektiv förbereder du enheten i en labb miljö. Sedan distribuerar du den **tvingande aktiverade** principen och startar slutligen om enheten innan du ger enheten till en slutanvändare.
- Distribuera inte en princip med **aktive rad tvång**och distribuera sedan en princip med **enbart granskning** till samma enhet. Den här konfigurationen kan leda till att ej betrodda program får köras.
- När du använder Configuration Manager för att aktivera Windows Defender-Programkontroll på klient datorer, förhindrar principen inte användare med lokal administratörs behörighet från att kringgå program kontroll principerna eller på annat sätt köra icke-betrodd program vara. 
- Det enda sättet att förhindra att användare med lokala administratörs rättigheter inaktiverar program kontroll är att distribuera en signerad binär princip. Den här distributionen är möjlig genom grupprincip men stöds för närvarande inte i Configuration Manager.
- Installation av Configuration Manager som ett hanterat installations program på klient datorer använder AppLocker-princip. AppLocker används bara för att identifiera hanterade installations program och alla tvångs åtgärder med Windows Defender-Programkontroll. 

## <a name="next-steps"></a>Nästa steg

 [Hantera principer för program mot skadlig kod och brandväggsinställningar](endpoint-antimalware-firewall.md)