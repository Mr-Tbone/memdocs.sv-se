---
title: Din enhet saknar ett certifikat | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/04/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: df973b18-9166-417d-8aa3-49edd2bda256
searchScope:
- User help
ROBOTS: NOINDEX, NOFOLLOW
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 341cb27d59786802124a575b04a2809ba6f3a987
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334463"
---
# <a name="your-android-device-is-missing-a-certificate-that-usually-comes-installed-on-your-phone"></a>Din Androidenhet saknar ett certifikat som normalt är installerat på telefonen

Om enheten inte har registrerats i Intune och den saknar ett certifikat som normalt är installerat på telefonen kan du inte logga in i företagsportalappen. Följande meddelande visas när du försöker logga in:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Du kan åtgärda det här problemet genom att hämta nödvändiga certifikat från [Digicert-certifikatsidan](https://www.digicert.com/digicert-root-certificates.htm).

1. Sök efter och hämta certifikatet __Baltimore CyberTrust Root__. Du kan också hämta det direkt [här](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).

2. Dra nedåt från överkanten på skärmen för att visa listan med dina senaste meddelanden och tryck på **BaltimoreCyberTrustRoot.crt**.

3. Din enhet kommer att uppmana dig att **Namnge certifikatet**. Ändra inte det standardnamn för certifikatet som visas.

4. Kontrollera att **Autentiseringsuppgift** är inställt på **Används för VPN och appar** och tryck sedan på **OK**.

    ![screenshot-certificate-name-dialog-showing-baltimore-certificate-name](./media/andr-cert_install-2-add_cert_name.png)

5. Stäng din webbläsare och företagsportalappen.

6. Öppna företagsportalappen igen. Du bör nu kunna logga in på företagsportalappen. Om du fortfarande inte kan använda företagsportalappen ska du kontakta företagets support med hjälp av informationen på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980) för ytterligare instruktioner.

>[!NOTE]
> Om installationen av det här certifikatet inte löser problemet och du ser meddelandet "certifikat saknas" måste du vidta ytterligare åtgärder för att[installera det saknade certifikatet](your-device-is-missing-an-IT-required-certificate-android.md).

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
