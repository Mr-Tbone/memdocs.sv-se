---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590548"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a>Azure AD-autentisering fungerar inte
<!--7569264-->
Configuration Manager användningen av tjänsten Azure Active Directory (Azure AD) Security Token fungerar inte. **CCM_STS. log** på hanterings platsen innehåller en post som liknar följande fel: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` den innehåller även HRESULT-0x80131040.

Ett annat problem är problem med en Cloud Management Gateway (CMG). Om du kör CMG Connection Analyzer går det inte att testa CMG-kanalen för hanterings platsen med följande fel:`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Det här problemet beror på en versions avvikelse med ett stöd bibliotek.

Undvik problemet genom att kopiera **System.IdentityModel.Tokens.JWT.dll** från mappen \bin\X64 i installations katalogen på plats servern till mappen SMS_CCM \ CCM_STS \Bin på hanterings platsen.
