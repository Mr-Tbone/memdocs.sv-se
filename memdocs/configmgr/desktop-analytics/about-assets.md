---
title: Till gångar i Analytics för Station ära datorer
titleSuffix: Configuration Manager
description: Lär dig om enheter, driv rutiner och appar i Skriv bords analys.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722552"
---
# <a name="assets-in-desktop-analytics"></a>Till gångar i Analytics för Station ära datorer

När enheterna rapporterar data till Desktop Analytics innehåller den en förteckning över följande till gångar:

- Enheter
- Installerade appar  

I Service Portal väljer du **till gångar** i menyn Skriv bords analys.

## <a name="devices"></a>Enheter

På fliken **enheter** visas viktig information om alla enheter i din organisation som du registrerar till Skriv bords analys. Du kan sortera efter valfri kolumn eller filtrera efter specifika värden.

> [!NOTE]  
> Om instrument panelen inte rapporterar antalet enheter som du förväntar dig att se för din miljö, se [fel sökning av Skriv bords analys](troubleshooting.md).  

I en distributions plan finns det mer information om enheter. Mer information finns i [planera till gångar](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>Appar

Fliken **appar** visar alla installerade appar som tjänsten identifierar på dina Windows-enheter.

Viktiga **appar är** installerade på fler än 2% av registrerade enheter.

Konfigurera **betydelsen** av appar genom att ställa in en av följande kategorier:

- Kritisk
- Viktigt
- Ignorera
- Ej granskad
- Inte viktigt<!-- 3587232 -->

Välj appen i listan och välj **Redigera**. Den här åtgärden visar information om appen. Välj den **viktiga** List menyn och ange ett värde. Du kan också tilldela en **ägare**. Om du gör några ändringar väljer du **Spara**.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Automatiskt uppgraderings beslut av system-och Store-appar

<!-- 3587232 -->
Att identifiera **prioritets** -och **uppgraderings beslut** är viktigt för alla viktiga appar i arbets flödet för Skriv bords analys. För att minska dina ansträngningar när du kommenterar de här apparna markeras vissa typer av appar automatiskt som *inte viktiga*. Distributions planens uppgraderings beslut för de här apparna är också markerat som *klart*. Följande appar är kompatibla och bör fortsätta att fungera när du har uppgraderat Windows:

- Systemappar och komponenter som publicerats av Microsoft

- Appar som hanteras och uppdateras från Microsoft Store

> [!TIP]
> Hantera indata för alla appar på en global nivå eller per distributions plan.
>
> 1. I menyn **Hantera** i Skriv bords analys-portalen väljer du **till gångar**. Välj sedan **appar**.
>
> 2. Använd kolumnerna **typ** och **kategori** för att hantera dessa app-kategorier:
>
>    - För Store-appar, filtrera **typ** som **modern**
>    - Filtrera **kategori** som **bakgrunds process** eller Windows- **komponent** i system apps

I en distributions plan kan du också ställa in **uppgraderings beslutet**. Mer information finns i [planera till gångar](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Användning

<!-- 5533890 -->

- **Totalt antal installationer**: det här värdet är antalet installationer av den valda appen på alla registrerade enheter med Skriv bords analys.

- **Installations procent**: det här värdet är den valda appens installations procent mot det totala antalet registrerade Skriv bords enheter.

- **Enheter som startade den här appen under de senaste 30 dagarna**: det här värdet är antalet enheter där en användare startade den valda appen. Den innehåller bara enheter som har rapporterat användning under de senaste 30 dagarna. Det här antalet är över alla enheter som har registrerats med Desktop Analytics och som körs på alla versioner av Windows 10. Det är möjligt att antalet kan variera för en distributions plan.

## <a name="next-steps"></a>Nästa steg

- [Lär dig mer om distributions planer för Skriv bords analys](about-deployment-plans.md)  

- [Lär dig mer om säkerhets-och funktions uppdateringar](about-updates.md)  

- [Kompatibilitetskontroll i Desktop Analytics](compat-assessment.md)  
