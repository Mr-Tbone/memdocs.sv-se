---
title: Endpoint Protection klient inställningar
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar anpassade klient inställningar för Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724323"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurera anpassade klientinställningar för Endpoint Protection

*Gäller för: Configuration Manager (aktuell gren)*

Den här proceduren konfigurerar anpassade klient inställningar för Endpoint Protection, som du kan distribuera till samlings enheter i hierarkin.

> [!IMPORTANT]  
>  Konfigurera bara standard Endpoint Protection klient inställningar om du är säker på att du vill att de ska gälla för alla datorer i hierarkin. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Aktivera Endpoint Protection och konfigurera anpassade klientinställningar

1. Klicka på **Administration**i Configuration Manager-konsolen.  

2. I arbetsytan **Administration** klickar du på **Klientinställningar**.  

3. Klicka på **Skapa anpassade klientenhetsinställningar** i gruppen **Skapa** på fliken **Start**.  

4. I dialogrutan **Skapa anpassade klientenhetsinställningar** anger du ett namn och en beskrivning för gruppen med inställningar och väljer sedan **Endpoint Protection**.  

5. Konfigurera de Endpoint Protection klient inställningar som du behöver. En fullständig lista över Endpoint Protection klient inställningar som du kan konfigurera finns i avsnittet Endpoint Protection i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#endpoint-protection).  

   > [!IMPORTANT]  
   >  Installera Endpoint Protection plats system rollen innan du konfigurerar klient inställningar för Endpoint Protection.  

6. Klicka på **OK** så att dialogrutan **Skapa anpassade klientenhetsinställningar** stängs. De nya klientinställningarna visas i noden **Klientinställningar** i arbetsytan **Administration** .  

7. Distribuera sedan de anpassade klient inställningarna till en samling. Välj de anpassade klient inställningar som du vill distribuera. Klicka på **distribuera**i gruppen **klient inställningar** på fliken **Start** .  

8. I dialogrutan **Välj samling** väljer du den samling som du vill distribuera klientinställningarna till och klickar sedan på **OK**. Den nya distributionen visas på fliken **Distributioner** i informationsrutan.  

Klienterna konfigureras med de här inställningarna nästa gång de laddar ned klient principen. Mer information finns i [Starta princip hämtning för en Configuration Manager-klient](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Så här etablerar du Endpoint Protection klienten i en disk avbildning

Installera Endpoint Protection-klienten på en dator som du tänker använda som disk avbildnings källa för Configuration Manager OS-distribution. En sådan dator brukar kallas för en referensdator. När du har skapat operativ Systems avbildningen använder du Configuration Manager OS-distribution för att distribuera avbildningen.

> [!Important]  
> Windows 10 och Windows Server 2016 har Windows Defender installerat som standard. Du behöver inte den här proceduren i dessa versioner av Windows.  

Använd följande procedurer för att installera och konfigurera Endpoint Protection-klienten på en referens dator.


### <a name="prerequisites"></a>Krav

Följande lista innehåller de nödvändiga förutsättningarna för att installera Endpoint Protection-klient program vara på en referens dator.

- Du måste ha åtkomst till Endpoint Protection-klientens installations paket, **scepinstall. exe**. Hitta det här paketet i mappen **client** i mappen Configuration Manager-installation på plats servern.  

- Om du vill distribuera Endpoint Protection-klienten med organisationens konfiguration måste du skapa och exportera en princip för program mot skadlig kod. Ange sedan den här principen när du installerar Endpoint Protection-klienten manuellt. Mer information finns i [skapa och distribuera principer för program mot skadlig kod](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  Det går inte att exportera **principen för program mot skadlig kod för standard klienten**.  

- Om du vill installera Endpoint Protection-klienten med de senaste definitionerna kan du hämta dem från [Windows Defender säkerhets information](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> Från och med Configuration Manager 1802 behöver du inte installera Endpoint Protection Agent (SCEPInstall) på Windows 10-enheter. Om den redan är installerad på Windows 10-enheter kan Configuration Manager inte ta bort den. Administratörer kan ta bort Endpoint Protection-agenten på Windows 10-enheter som kör minst 1802-klient versionen. SCEPInstall. exe kanske fortfarande finns i C:\Windows\ccmsetup på vissa datorer, men nya klient installationer bör inte ladda ned den. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Så här installerar du Endpoint Protection-klienten på referens datorn

Installera Endpoint Protection-klienten lokalt på referens datorn från en kommando tolk. Hämta först installations filen **scepinstall. exe**. Mer information finns i [installera Endpoint Protection-klienten från en kommando tolk](#bkmk_manual-install).

Om det behövs kan du även inkludera en förkonfigurerad princip för program mot skadlig kod eller en princip för program mot skadlig kod som du tidigare har exporterat. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a>Så här installerar du Endpoint Protection-klienten från en kommando tolk

1. Kopiera **scepinstall. exe** från mappen **client** i mappen installations program för Configuration Manager till den dator där du vill installera Endpoint Protection-klientprogramvaran.  

2. Öppna en kommandotolk som administratör. Ändra katalogen till mappen med installations programmet. Kör `scepinstall.exe`sedan och Lägg till ytterligare kommando rads egenskaper som du behöver:


   |  Egenskap   |                                  Beskrivning                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Köra installations programmet tyst                           |
   |    `/q`     |                        Extrahera installationsfiler tyst                        |
   |    `/i`     |                           Kör installations programmet normalt                           |
   |  `/policy`  | Ange en princip fil för program mot skadlig kod för att konfigurera klienten under installationen |
   | `/sqmoptin` |     Anmäl dig till Microsoft Customer Experience Improvement Program (CEIP)     |


3. Slutför klient installationen genom att följa anvisningarna på skärmen.  

4. Om du har hämtat det senaste definitionspaketet, kopierar du det till klientdatorn och dubbelklickar sedan på paketet för att installera det.  

   > [!NOTE]  
   >  När installationen av den Endpoint Protection klienten har slutförts utför klienten automatiskt en definitions uppdaterings kontroll. Om den här uppdaterings kontrollen lyckas behöver du inte installera det senaste definitions uppdaterings paketet manuellt.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Exempel: installera klienten med en princip för program mot skadlig kod

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verifiera Endpoint Protection klient installationen

När du har installerat Endpoint Protection-klienten på referens datorn kontrollerar du att klienten fungerar som den ska.

1.  På referens datorn öppnar du **System Center Endpoint Protection** från meddelande fältet i Windows.  

2.  På fliken **Start** i dialog rutan **System Center Endpoint Protection** kontrollerar du att **real tids skyddet** är inställt **på on**.  

3.  Kontrol lera att **aktuell** visas för **virus-och spionprograms definitioner**.  

4.  För att se till att referens datorn är klar för avbildning väljer du **fullständig**under **skannings alternativ**och klickar sedan på **Sök nu**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Förbereda Endpoint Protection-klienten för avbildning

Utför följande steg för att förbereda Endpoint Protection-klienten för avbildning:

1. Logga in som administratör på referens datorn.  

2. Hämta och installera **PsExec** från [Windows Sysinternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Kör en kommando tolk som administratör, ändra katalogen till den mapp där du installerade PsTools och skriv sedan följande kommando:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Var försiktig när du kör Registereditorn på det här sättet. PsExec. exe Kör den i LocalSystem-kontexten.  

4. Ta bort följande register nycklar i Registereditorn:  

   > [!IMPORTANT]  
   >  Ta bort de här register nycklarna som det sista steget innan du avbildningen av referens datorn. Den Endpoint Protection klienten återskapar nycklarna när den startas. Om du startar om referens datorn tar du bort register nycklarna igen.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Du är nu redo att förbereda referens datorn för avbildning.

När du distribuerar en OS-avbildning som innehåller Endpoint Protection klienten, rapporterar den automatiskt information till enhetens tilldelade Configuration Manager plats. Klienten laddar ned och tillämpar alla riktade principer för skadlig kod.  



## <a name="see-also"></a>Se även

Mer information om operativ Systems distribution i Configuration Manager finns i [hantera OS-avbildningar](../../osd/get-started/manage-operating-system-images.md).

