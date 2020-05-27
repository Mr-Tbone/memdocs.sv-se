---
title: Tokenbaserad autentisering för CMG
titleSuffix: Configuration Manager
description: Registrera en klient i det interna nätverket för en unik token eller skapa en token för Mass registrering för Internetbaserade enheter.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3a05c10d1f73fa0817febdd591190f6bc2ff0a0e
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587270"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Tokenbaserad autentisering för Cloud Management Gateway

*Gäller för: Configuration Manager (aktuell gren)*

<!--5686290-->

CMG (Cloud Management Gateway) stöder många typer av klienter, men även med [utökad http](../../plan-design/hierarchy/enhanced-http.md)kräver dessa klienter ett certifikat för [klientautentisering](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Detta certifikat krav kan vara svårt att etablera på Internetbaserade klienter som inte ofta ansluter till det interna nätverket, inte kan ansluta Azure Active Directory (Azure AD) och inte har någon metod för att installera ett PKI-utfärdat certifikat.

Från och med version 2002, utökar Configuration Manager enhetens support med följande metoder:

- Registrera i det interna nätverket för en unik token

- Skapa en token för Mass registrering för Internetbaserade enheter

För att dra full nytta av den här funktionen kan du, när du har uppdaterat platsen, även uppdatera klienter till den senaste versionen. Det fullständiga scenariot fungerar inte förrän klient versionen också är den senaste. Om det behövs kontrollerar du att du [befordrar den nya klient versionen till produktion](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

Configuration Manager-klienten tillsammans med hanterings platsen hanterar denna token, så det finns inget versions beroende för operativ system. Den här funktionen är tillgänglig för alla [klient-OS-versioner som stöds](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Dessa metoder har endast stöd för enhets drivna hanterings scenarier.
>
> Microsoft rekommenderar att du ansluter enheter till Azure AD. Internet-baserade enheter kan använda Azure AD för att autentisera med Configuration Manager. Det aktiverar också både enhets-och användar scenarier oavsett om enheten är ansluten till Internet eller om den är ansluten till det interna nätverket. Mer information finns i [Installera och registrera klienten med hjälp av Azure AD-identitet](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Registrera dig för det interna nätverket

Den här metoden kräver att klienten först registreras med hanterings platsen i det interna nätverket. Klient registrering sker vanligt vis direkt efter installationen. Hanterings platsen ger klienten en unik token som visar att den använder ett självsignerat certifikat. När klienten växlar till Internet, för att kommunicera med CMG, paras det självsignerade certifikatet med hanterings platsens utfärdade token. Klienten förnyar token en gång i månaden och den är giltig i 90 dagar.

Platsen aktiverar den här funktionen som standard.

## <a name="create-a-bulk-registration-token"></a>Skapa en token för Mass registrering

Om du inte kan installera och registrera klienter i det interna nätverket skapar du en token för Mass registrering. Använd den här token när klienten installeras på en Internetbaserad enhet och registreras via CMG. Token för Mass registrering har en kort giltighets tid och lagras inte på klienten eller platsen. Det gör att klienten kan generera en unik token, som parats ihop med det självsignerade certifikatet, som gör det möjligt att autentisera med CMG.

1. Logga in på plats servern på den översta nivån i hierarkin med lokal administratörs behörighet.

1. Öppna en kommandotolk som administratör.

1. Kör verktyget från `\bin\X64` mappen i installations katalogen för Configuration Manager på plats servern: `BulkRegistrationTokenTool.exe`. Skapa en ny token med `/new` parametern. Till exempel `BulkRegistrationTokenTool.exe /new`. Mer information finns i [användning av token för Mass registrering](#bulk-registration-token-tool-usage).

1. Kopiera token och spara den på en säker plats.

1. Installera Configuration Manager-klienten på en Internetbaserad enhet. Inkludera klient installations parametern: [**/regtoken**](about-client-installation-properties.md#regtoken). Följande exempel på kommando raden innehåller andra obligatoriska konfigurations parametrar och egenskaper:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Mer information om den här kommando raden finns i [Installera och registrera klienten med hjälp av Azure AD-identitet](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Den här processen är liknande och använder bara Azure AD-egenskaperna.

### <a name="known-issues"></a>Kända problem

Du kan inte skapa en token för Mass registrering på en plats som har en plats server i passivt läge.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Användning av token för Mass registrering

`BulkRegistrationTokenTool.exe` Verktyget finns i `\bin\X64` mappen i installations katalogen för Configuration Manager på plats servern. Logga in på plats servern och kör den som administratör. Det stöder följande kommando rads parametrar:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Visa den här användnings informationen.

Exempel: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Skapa en ny token för Mass registrering.

Exempel: `BulkRegistrationTokenTool.exe /new`

Verktyget visar följande information:
  
- Ett GUID som platsen använder för att spåra utfärdade token
- Giltighets perioden för token, som är tre dagar som standard.
- Token för Mass registrering.

Token lagras inte på klienten eller på platsen. Se till att kopiera token från kommando tolken och lagra på en säker plats.

#### <a name="lifetime"></a>/lifetime

Använd with `/new` parameter för att ange giltighets perioden för token. Ange ett heltals värde i minuter. Standardvärdet är 4 320 (tre dagar). Det maximala värdet är 10 080 (sju dagar).

Exempel: `BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>Se även

- [Planera för Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md)

- [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](deploy-clients-cmg-azure.md)