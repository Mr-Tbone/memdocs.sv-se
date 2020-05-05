---
title: Funktioner i Technical Preview 1704
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721411"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Funktioner i Technical Preview 1704 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1704. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Konfigurera Android-appar med konfigurations principer för appar
Du kan använda konfigurations principer för appar i Configuration Manager för att distribuera inställningar som kan krävas när en användare kör en app på Android for Work-enheter. Konfigurations principer för Android-appar är bara tillgängliga på enheter som kör Android for Work och gäller godkända appar från Play for Work-butiken.

### <a name="try-it-out"></a>Prova nu                 

I Configuration Manager-konsolen väljer du**konfigurations principer** för program **bibliotek** > **program hantering** > och väljer **skapa konfigurations princip för appar**. På sidan **Allmänt** i guiden kan du nu **välja en typ av konfigurations princip**. Ange den plattform som är mål för appens konfigurations princip: **konfigurations princip för Android for Work-appar**. Du kan antingen **Ange namn-och värdepar** eller **Bläddra till en JSON-fil för egenskaps listan**. Den nya konfigurations principen för appar visas i arbets ytan **program varu bibliotek** i noden **konfigurations principer för appar** . Om du vill associera en konfigurations princip för appar med distributionen av en Android for Work-app distribuerar du programmet som vanligt med hjälp av proceduren i avsnittet [distribuera program](../../apps/deploy-use/deploy-applications.md) .

## <a name="hardware-inventory-collects-secure-boot-information"></a>Maskin varu inventering samlar in information om säker start
Maskin varu inventering samlar nu in information om huruvida säker start är aktiverat på klienter. Den här informationen lagras i **SMS_Firmware** -klassen (lanserades i version 1702) och aktive ras i maskin varu inventeringen som standard. Mer information om maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Lägg till underordnade aktivitetssekvenser i en aktivitetssekvens
I den här versionen kan du lägga till ett nytt steg i aktivitetssekvensen som kör en annan aktivitetssekvens, vilket skapar en överordnad/underordnad relation mellan aktivitetssekvenser. På så sätt kan du skapa fler modulära aktivitetssekvenser som du kan använda igen.  

Tänk på följande när du lägger till en underordnad aktivitetssekvens till en aktivitetssekvens:

- De överordnade och underordnade aktivitetssekvenser kombineras effektivt till en enda princip som klienten kör.
- Det går inte att lägga till en underordnad aktivitetssekvens som är överordnad en annan aktivitetssekvens.
- Miljön är global. Om en variabel exempelvis anges av den överordnade aktivitetssekvensen och sedan ändras av den underordnade aktivitetssekvensen, ändras inte variabeln flytta framåt. På samma sätt gäller att om den underordnade aktivitetssekvensen skapar en ny variabel, är variabeln tillgänglig för de återstående stegen i den överordnade aktivitetssekvensen.
- Status meddelanden skickas per normal för en åtgärd för en aktivitetssekvens.
- Aktivitetssekvenser skriver poster till filen Smsts. log med nya logg poster som gör den tydlig när en underordnad aktivitetssekvens startar.
- I den tekniska för hands versionen för Configuration Manager version 1704, om den underordnade aktivitetssekvensen refererar till ett paket och du kör den överordnade aktivitetssekvensen från Software Center, kommer klienten inte att hitta paket innehållet när den underordnade aktivitetssekvensen körs. I det här scenariot måste du köra aktivitetssekvensen från media (startmedia, PXE osv.).  

    Om den underordnade aktivitetssekvensen använder steg som att **köra kommando raden** (utan någon paket referens), **format**, **BitLocker**osv., kommer aktivitetssekvensen att köras utan problem från Software Center.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Så här lägger du till en underordnad aktivitetssekvens i en aktivitetssekvens
1. I redigeraren för aktivitetssekvens klickar du på **Lägg till**, väljer **Allmänt**och klickar på **Kör aktivitetssekvens**.
2. Klicka på **Bläddra** för att välja den underordnade aktivitetssekvensen.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Läs in start avbildningar igen med den aktuella Windows PE-versionen
När du kör **uppdaterings distributions platser** på en vald start avbildning kan du nu välja att läsa in den senaste versionen av Windows PE (från installations katalogen för Windows ADK) i Start avbildningen. På sidan **Allmänt** i guiden finns information om Windows ADK-versionen som är installerad på plats servern, Windows ADK-versionen som Windows PE användes i Start avbildningen och versionen av Configuration Manager-klienten. Du kan använda den här informationen för att avgöra om du ska läsa in start avbildningen på nytt. Dessutom har en ny kolumn (**klient version**) lagts till när du visar start avbildningar i noden **Start avbildningar** så att du vet vilken version av Configuration Manager-klienten som varje start avbildning använder.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Så här läser du in en start avbildning med den aktuella Windows PE-versionen

1. I Configuration Manager-konsolen går du till**Start avbildningar**för **program varu bibliotekets** > **operativ system** > .
2. Välj en start avbildning och klicka på **Uppdatera distributions platser**.
3. På sidan **Allmänt** i guiden väljer du **Läs in start avbildningen på nytt med den aktuella versionen av Windows PE från installations programmet för Windows ADK**.

## <a name="improvements-to-operating-system-deployment"></a>Förbättringar av operativ Systems distribution
Vi har gjort följande förbättringar av distributionen av operativ system, vilket var resultatet av din röst feedback från användaren.

- [Ny operativ system **versions** kolumn för operativ Systems avbildningar](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): vi har lagt till en ny kolumn med namnet **OS-version** för att Visa versionen av operativ systemet för avbildningen när du visar information i noderna **operativ system avbildningar** och **uppgraderings paket för operativ system** . Endast versionen av det första indexet i. WIM visas. Gå till fliken **information** för avbildningen om du vill granska operativ system versioner för andra index.

- [Mer effektiv loggning i Smsts. log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): från och med den här versionen skrivs vi inte längre att skriva poster till filen Smsts. log för CCM_CIVersionInfo. PolicyID-information. Före den här versionen kan det finnas många poster med den här informationen, vilket gjorde det svårt att hitta mer relevant information i logg filen.
