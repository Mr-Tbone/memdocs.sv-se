---
title: Skapa Endpoint Protection Point plats system roll
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar Endpoint Protection för att hantera säkerhet och skadlig kod på Configuration Manager klient datorer.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710834"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Skapa en Endpoint Protection-platssystemroll

*Gäller för: Configuration Manager (aktuell gren)*

Platssystemrollen för Endpoint Protection-platser måste installeras innan du kan använda Endpoint Protection. Den får endast installeras på en platssystemserver och den måste installeras längst upp i hierarkin på en central administrationsplats eller en fristående primär plats.

Använd någon av följande metoder beroende på om du vill installera en ny plats system Server för Endpoint Protection eller använda en befintlig plats system Server:
- [Installera på en ny plats system Server](#new-site-system-server)
- [Installera på en befintlig plats system Server](#existing-site-system-server)

> [!IMPORTANT]
>  När du installerar en Endpoint Protection Point installeras en Endpoint Protection-klient på den server som är värd för Endpoint Protection Point. Tjänster och genomsökningar har inaktiverats på den här klienten för att den ska kunna finnas samtidigt som eventuell befintlig lösning för program mot skadlig kod som finns installerad på servern. Om du senare aktiverar den här servern för hantering genom Endpoint Protection och väljer alternativet för att ta bort eventuella program från tredje part, kommer produkten från tredje part inte att tas bort. Du måste avinstallera den här produkten manuellt.

## <a name="new-site-system-server"></a>Ny plats system Server

1.  Klicka på **Administration**i Configuration Manager-konsolen.

2.  I arbetsytan **Administration** expanderar du **Platskonfiguration** och klickar sedan på **Systemroller för servrar och platser**.

3.  På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa platssystemserver**.

4.  På sidan **Allmänt** anger du allmänna inställningar för platssystemet och klickar sedan på **Nästa**.

5.  Välj **Endpoint Protection-plats** i listan med tillgängliga roller på sidan **Urval för systemroll** och klicka sedan på **Nästa**.

6.  På sidan **Endpoint Protection** markerar du kryssrutan **Jag accepterar licensvillkoren för Endpoint Protection** och klickar sedan på **Nästa**.

    > [!IMPORTANT]
    >  Du kan inte använda Endpoint Protection i Configuration Manager om du inte accepterar licens villkoren.

7.  På sidan **moln skydds tjänst** väljer du den informations nivå som du vill skicka till Microsoft för att hjälpa till att utveckla nya definitioner och klickar sedan på **Nästa**.

    > [!NOTE]
    >  Det här alternativet konfigurerar moln skydds tjänsten (tidigare kallade Microsoft Active Protection Service-eller MAPS-inställningar) som används som standard. Du kan sedan konfigurera anpassade inställningar för varje princip för program mot skadlig kod som du skapar. Anslut till moln skydds tjänsten för att hjälpa till att skydda datorerna genom att tillhandahålla Microsoft med exempel på skadlig kod som kan hjälpa Microsoft att hålla definitionerna av skadlig kod mer aktuella. När du ansluter till moln skydds tjänsten kan Endpoint Protection klienten dessutom använda tjänsten dynamisk signatur för att hämta nya definitioner innan de publiceras till Windows Update. Mer information finns i [skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).

8.  Slutför guiden.


## <a name="existing-site-system-server"></a>Befintlig plats system Server

1.  Klicka på **Administration**i Configuration Manager-konsolen.

2.  I arbets ytan **Administration** expanderar du **plats konfiguration**, klickar på **system roller för servrar och platser**och väljer sedan den server som du vill använda för Endpoint Protection.

3.  På fliken **Hem** går du till gruppen **Server** och klickar på **Lägg till platssystemroller**.

4.  På sidan **Allmänt** anger du allmänna inställningar för platssystemet och klickar sedan på **Nästa**.

5.  Välj **Endpoint Protection-plats** i listan med tillgängliga roller på sidan **Urval för systemroll** och klicka sedan på **Nästa**.

6.  På sidan **Endpoint Protection** markerar du kryssrutan **Jag accepterar licensvillkoren för Endpoint Protection** och klickar sedan på **Nästa**.

    > [!IMPORTANT]
    >  Du kan inte använda Endpoint Protection i Configuration Manager om du inte accepterar licens villkoren.

7.  På sidan **moln skydds tjänst** väljer du den informations nivå som du vill skicka till Microsoft för att hjälpa till att utveckla nya definitioner och klickar sedan på **Nästa**.

    > [!NOTE]
    >  Med det här alternativet konfigureras inställningarna för moln skydds tjänsten (tidigare kallade MAPS) som används som standard. Du kan konfigurera anpassade inställningar för varje princip för program mot skadlig kod som du konfigurerar. Mer information finns i [skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).

8.  Slutför guiden.
