---
title: Sökvägar till samhantering
titleSuffix: Configuration Manager
description: Förstå kraven för de två huvudsakliga sätten för att konfigurera samhantering.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d481976a6c86da67670871690ba16985a67c80d8
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746467"
---
# <a name="paths-to-co-management"></a>Sökvägar till samhantering

Det finns två huvudsakliga sätt att konfigurera samhantering. Det är viktigt att förstå kraven för varje sökväg. De måste ha en kombination av Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune och Windows 10. 

1. [Registrera befintliga Configuration Manager-hanterade enheter automatiskt i Intune](#bkmk_path1)  
2. [Starta Configuration Manager-klienten med modern etablering](#bkmk_path2)  

![Diagram över samhanterings vägar](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>Sökväg 1: registrera befintliga klienter automatiskt

Om du tar den här sökvägen kan du snabbt registrera dina befintliga Configuration Manager-hanterade enheter i Intune. Hantering av dessa enheter från Configuration Manager skiljer sig inte från innan du aktiverar samhantering. Nu får du till gång till alla molnbaserade förmåner. Den här sökvägen är transparent för dina användare.

Här är vad du behöver för att konfigurera det:
- Hybrid Azure AD
    - Ett av följande [hybrid identitets alternativ för Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Password-hash-synkronisering](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) med [sömlös enkel inloggning (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Direktautentisering](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) med [sömlös enkel inloggning (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Federerad enkel inloggning (med Active Directory Federation Services (AD FS) (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium-licens
    - Konfigurera hybrid Azure AD – Anslut (Välj ett alternativ):
        - För hanterade domäner
        - För federerade domäner
- Klient agent inställning för Hybrid Azure AD – Anslut
- Konfigurera automatisk registrering av enheter till Intune
- Aktivera samhantering i Configuration Manager

En själv studie kurs om den här sökvägen finns i [Självstudier: Aktivera samhantering för befintliga Configuration Manager-klienter](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a>Sökväg 2: bootstrap med modern etablering

Här är vad du behöver för att konfigurera det:

1. [Konfigurera utökad HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Skapa moln tjänster i Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Konfigurera hanterings platsen och klienterna så att de använder Cloud Management Gateway](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Använda Intune för att distribuera Configuration Manager-klienten](how-to-prepare-Win10.md)  

En själv studie kurs om den här sökvägen finns i [Självstudier: Aktivera samhantering för nya Internetbaserade enheter](tutorial-co-manage-new-devices.md).

