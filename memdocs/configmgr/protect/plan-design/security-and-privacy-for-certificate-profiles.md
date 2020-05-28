---
title: Säkerhet och sekretess för certifikatprofiler
titleSuffix: Configuration Manager
description: Lär dig mer om rekommenderade säkerhets metoder för hantering av certifikat profiler för användare och enheter i Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3825ef9b9b1efd576a31742e0fdbe7c2bc3b1628
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906851"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Säkerhet och sekretess för certifikat profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Rekommenderade säkerhetsmetoder för certifikatprofiler  
 Använd följande rekommenderade säkerhetsmetoder när du hanterar certifikatprofiler för användare och enheter.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Identifiera och följ rekommenderade säkerhetsmetoder för registreringstjänsten för nätverksenheter. Det innefattar att i Internet Information Services (IIS) konfigurera att webbplatsen för registreringstjänsten ska begära SSL och ignorera klientcertifikat.|Mer information finns i [rikt linjer för registrerings tjänsten för nätverks enheter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).|  
|När du konfigurerar SCEP-certifikatprofiler ska du välja det säkraste alternativet som enheterna och infrastrukturen har stöd för.|Identifiera, implementera och följ de säkerhetsmetoder som har rekommenderats för enheterna och infrastrukturen.|  
|Definiera mappning mellan användare och enhet manuellt i stället för att tillåta att användarna identifierar sina primära enheter. Aktivera inte användningsbaserad konfigurering.|Om du klickar på alternativet **Tillåt endast certifikatregistering på användarens primära enhet** i en SCEP-certifikatprofil ska information som samlas in från användare eller enheten inte betraktas som auktoriserande. Om du distribuerar SCEP-certifikatprofiler med den här konfigurationen och en betrodd administrativ användare inte anger mappning mellan användare och enhet, kan ej auktoriserade användare få förhöjda behörigheter och tilldelas autentiseringscertifikat.<br /><br /> **Obs:** Om du aktiverar användnings baserad konfiguration samlas den här informationen in med hjälp av tillstånds meddelanden som inte skyddas av Configuration Manager. Minimera hotrisken genom att använda SMB-signering eller IPsec mellan klientdatorerna och hanteringsplatsen.|  
|Lägg inte till läs- och registreringsbehörigheter för användare av certifikatmallar, och konfigurera inte certifikatregistreringsplatsen att hoppa över certifikatmallskontrollen.|Även om Configuration Manager stöder ytterligare kontroll om du lägger till säkerhets behörigheterna för läsa och registrera för användare, och du kan konfigurera certifikat registrerings platsen att hoppa över den här kontrollen om autentisering inte är möjlig, är ingen av säkerhets skäl säkerhets praxis. Mer information finns i [Planera för certifikat mal len behörigheter för certifikat profiler](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Sekretessinformation för certifikatprofiler  
 Du kan använda certifikatprofiler för att distribuera rotcertifikatutfärdar- och klientcertifikat, och sedan kontrollera enheternas kompatibilitet när profilerna har aktiverats. Hanterings platsen skickar kompatibilitetsinformation till plats servern och Configuration Manager lagrar informationen i plats databasen. Kompatibilitetsinformationen innehåller certifikategenskaper, som mottagarnamn och tumavtryck. Informationen krypteras när enheter skickar den till hanteringsplatsen men den lagras inte i krypterat format på platsdatabasen. Informationen sparas i databasen tills den raderas av platsunderhållsaktiviteten **Ta bort föråldrade data för Configuration Manager**, vilket som standard sker var 90:e dag. Du kan konfigurera borttagningsintervallet. Information om kompatibilitet skickas inte till Microsoft.  

 Certifikat profiler använder information som Configuration Manager samlar in med hjälp av identifiering. Mer information om sekretess information för identifiering finns i avsnittet **Sekretess information för identifiering** i [säkerhet och sekretess för Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Certifikat som utfärdas till användare eller enheter kan ge åtkomst till konfidentiell information.  

 Som standard utvärderas inte certifikatprofiler av enheter. Du måste också konfigurera certifikatprofilerna och sedan distribuera dem till användare eller enheter.  

 Innan du konfigurerar certifikatprofiler bör du tänka igenom dina sekretesskrav.  
