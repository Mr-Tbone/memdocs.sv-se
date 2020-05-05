---
title: Planera certifikat mal len behörigheter
titleSuffix: Configuration Manager
description: Lär dig mer om att planera för de behörigheter som du behöver för att konfigurera de certifikatmallar som Configuration Manager använder.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 91434b70ca514430ab4cfd6815186bc6d6bc33db
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210136"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Planera för certifikat mal len behörigheter för certifikat profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Följande information kan hjälpa dig att planera hur du konfigurerar behörigheter för de certifikatmallar som Configuration Manager används när du distribuerar certifikat profiler.  

## <a name="default-security-permissions-and-considerations"></a>Standardsäkerhetsbehörigheter och överväganden  
 De standard säkerhets behörigheter som krävs för de certifikatmallar som Configuration Manager ska använda för att begära certifikat för användare och enheter är följande:  

- Läs och registrera för det konto som programpoolen för registreringstjänsten för nätverksenheter använder  

- Läs för det konto som kör Configuration Manager-konsolen  

  Mer information om de här säkerhets behörigheterna finns i [Konfigurera certifikat infrastruktur](../deploy-use/certificate-infrastructure.md).  

  När du använder den här standardkonfigurationen kan inte användare och enheter begära certifikat direkt från certifikatmallarna och alla begäranden måste initieras av registreringstjänsten för nätverksenheter. Det här är en viktig begränsning eftersom dessa certifikatmallar måste konfigureras med **Anges i begäran** för certifikatmottagaren, vilket innebär en risk för personifiering om en icke registrerad användare eller en komprometterad enhet begär ett certifikat. I standardkonfigurationen måste registreringstjänsten för nätverksenheter initiera en sådan begäran. Risken för personifiering kvarstår dock om tjänsten som kör registreringstjänsten för nätverksenheter har komprometterats. Undvik den här risken genom att följa alla rekommenderade säkerhetsmetoder för registreringstjänsten för nätverksenheter och den dator som kör den här rolltjänsten.  

  Om standardsäkerhetsbehörigheterna inte uppfyller dina affärskrav har du ett annat alternativ för att konfigurera säkerhetsbehörigheterna för certifikatmallarna: du kan lägga till behörigheterna Läs och Registrera för användare och datorer.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Lägga till läs- och registreringsbehörigheter för användare och datorer  
 Det kan vara lämpligt att lägga till Läs-och registrerings behörigheter för användare och datorer om ett separat team hanterar infrastrukturen för certifikat utfärdare (CA) och att det separata teamet vill Configuration Manager verifiera att användarna har ett giltigt Active Directory Domain Services konto innan de skickar en certifikat profil för att begära ett användar certifikat. För den här konfigurationen måste du specificera en eller flera säkerhetsgrupper som innehåller användarna och därefter ge grupperna läs- och registreringsbehörigheter på certifikatmallarna. I det här scenariot hanterar CA-administratören säkerhetskontrollen.  

 På liknande visa kan du specificera en eller flera säkerhetsgrupper som innehåller datorkonton och därefter ge grupperna läs- och registreringsbehörigheter på certifikatmallarna. Om du distribuerar en datorcertifikatprofil till en dator som är en domänmedlem måste datorkontot för den aktuella datorn ges läs- och registreringsbehörigheter. De här behörigheterna krävs inte om datorn inte är en domän medlem. Till exempel om det är en arbets grupps dator eller en personlig mobil enhet.  

 Trots att den här konfigurationen använder en extra säkerhetskontroll rekommenderar vi den inte. Orsaken är att de angivna användare eller ägare av enheterna kan begära certifikat oberoende av Configuration Manager och ange värden för certifikat ämnet som kan användas för att personifiera en annan användare eller enhet.  

 Om du dessutom specificerar konton som inte kan autentiseras när certifikatbegäran uppstår kommer certifikatbegäran att misslyckas. Certifikatbegäran misslyckas till exempel om den server som kör registreringstjänsten för nätverksenheter är i en Active Directory-skog som inte är betrodd av den skog som innehåller certifieringsregistreringsplatsens platssystemserver. Du kan konfigurera certifieringsregistreringsplatsen att fortsätta om ett konto inte kan autentiseras på grund av att det inte kommer något svar från en domänkontrollant. Det är dock inte en rekommenderad säker metod.  

 Observera att om certifieringsregistreringsplatsen är konfigurerad att kontrollera kontobehörigheter och det finns en domänkontrollant som avvisar autentiseringsbegäran (till exempel om kontot är utelåst eller har raderats) så kommer certifikatregistreringsbegäran att misslyckas.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Så här kontrollerar du läs- och registreringsbehörigheter för användare och domänmedlemsdatorer  

1.  På den plats system server som är värd för certifikat registrerings platsen skapar du följande DWORD-register nyckel för att ha värdet 0: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Om ett konto inte kan autentiseras på grund av att det saknas ett svar från en domänkontrollant och du vill kringgå behörighetskontrollen:  

    -   På den plats system server som är värd för certifikat registrerings platsen skapar du följande DWORD-register nyckel för att ha värdet 1: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Öppna fliken **Säkerhet** i certifikatutfärdarens mall certifikategenskaper och lägg till en eller fler säkerhetsgrupper för att ge användar- eller enhetskontona läs- och registreringsbehörigheter.  
