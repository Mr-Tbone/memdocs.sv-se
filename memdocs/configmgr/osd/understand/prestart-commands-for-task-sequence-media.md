---
title: Förinläsningskommandon för aktivitetssekvensmedier
titleSuffix: Configuration Manager
description: Skapa ett skript som ska användas för för inläsnings kommandot, distribuera det innehåll som är associerat med för inläsnings kommandot och konfigurera för inläsnings kommandot på mediet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 06c96d668d3c37b107ae8e290ebcd124e8a2b773
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124388"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>För inläsnings kommandon för media i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan skapa ett för inläsnings kommando i Configuration Manager att använda med start medier, fristående media och för beredda medier. Ett förinläsningskommando är ett skript eller en körbar fil som körs innan aktivitetssekvensen väljs, och kommandot kan användas för att interagera med användare i Windows PE. Förinläsningskommandot kan till exempel uppmana användaren att ange information och sedan spara informationen i aktivitetssekvensmiljön, eller hämta information i en aktivitetssekvensvariabel. När måldatorn startas körs kommandoraden innan principen hämtas från hanteringspunkten. Använd följande procedurer för att skapa ett skript för förinläsningskommandot, distribuera det innehåll som är associerat till förinläsningskommandot och konfigurera förinläsningskommandot för ett medium.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Skapa en skriptfil som ska användas för förinläsningskommandot  
 Aktivitetssekvensvariabler kan läsas eller skrivas med hjälp COM-objektet i Microsoft.SMS.TSEnvironment medan aktivitetssekvensen körs. I följande exempel används en Visual Basic-skriptfil för att hämta den aktuella loggplatsen från _SMSTSLogPath-aktivitetssekvensvariabeln. Skriptet konfigurerar också en anpassad variabel.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Skapa ett paket för skriptfilen och distribuera innehållet  
 När du har skapat skriptet eller den körbara filen för förinläsningskommandot, måste du skapa en paketkälla för lagring av de filer som är kopplade till skriptet eller den körbara filen. Du måste även skapa ett paket för filerna (inget program krävs) och sedan distribuera innehållet till en distributionsplats.  

 Mer information om hur du skapar ett paket finns i [paket och program](../../apps/deploy-use/packages-and-programs.md).  

 Mer information om hur du distribuerar innehållet finns i [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Konfigurera förinläsningskommando för medium  
 Du kan konfigurera ett förinläsningskommando i guiden Skapa aktivitetssekvensmedium för fristående medier, startbara medier och förberedda medier. Mer information om medie typerna finns i [skapa media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md). Använd följande metod för att skapa ett förinläsningskommando på ett medium.  

#### <a name="to-create-a-prestart-command-in-media"></a>Skapa ett förinläsningskommando på ett medium  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** expanderar du **operativ system**och klickar sedan på **aktivitetssekvenser**.  

3.  På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa aktivitetssekvensmedium** för att starta guiden Skapa aktivitetssekvensmedium.  

4.  På sidan **Välj medietyp** väljer du **Fristående medium**, **Startbart medium**eller **Förberett medium**och klickar sedan på **Nästa**.  

5.  Gå till sidan **Anpassning** i guiden. Mer information om hur du konfigurerar de andra sidorna i guiden finns i [skapa media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md).  

6.  På sidan **Anpassning** anger du följande information och klickar sedan på **Nästa**.  

    -   Välj **Aktivera förinläsningskommando**.  

    -   Ange i textrutan **Kommandorad** det skript eller den körbara fil som du har skapat för förinläsningskommandot.  

        > [!IMPORTANT]  
        >  Använd **cmd/c <för inläsnings kommando \> ** för att ange för inläsnings kommandot. Om till exempel TSScript.vbs är namnet på ditt förinläsningskommandoskript, anger du **cmd /C TSScript.vbs** i textrutan. Delen **cmd /C** öppnar ett nytt Windows-kommandotolksfönster och sökvägsmiljövariabeln används för att hitta skriptet eller den körbara filen. Du kan även ange en fullständig sökväg till förinläsningskommandot, men andra enhetsbokstäver kanske används på datorer med andra enhetskonfigurationer.  

    -   Välj **Ta med filer för förinläsningskommandot**.  

    -   Klicka på **Ange** för att välja det paket som är kopplat till förinlästningskommandots filer.  

    -   Klicka på **Bläddra** för att välja den distributionsplats där innehållet för förinläsningskommandot lagras.  

7.  Slutför guiden.  
