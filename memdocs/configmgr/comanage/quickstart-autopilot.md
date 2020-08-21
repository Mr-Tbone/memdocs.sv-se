---
title: Windows Autopilot med samhantering
titleSuffix: Configuration Manager
description: Använd Windows autopilot med samhantering i Configuration Manager för att förenkla uppsättningen nya Windows 10-enheter.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9888190f516bd8e876e9f197b6d15c26a6e6e3cf
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695077"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot med samhantering

Det är spännande att ta emot en ny Windows 10-enhet. Det kan dock ta tid att konfigurera alla inställningar och appar så att du kan vara produktiv. Samhantering löser detta problem med enhets etableringen med Windows autopilot.

Autopilot ger en förenklad upplevelse för både dig och dina användare i följande situationer:
- Konfigurera och förkonfigurera nya Windows 10-enheter  
- Återställa, återanvänd och återställa befintliga enheter  

Autopiloten minskar tiden, resurserna och komplexiteten som är kopplade till att distribuera, hantera och ta enheter ur bruk. Samtidigt är upplevelsen för dina användare strömlinjeformad och lätt från första starten.

Windows autopilot stöder flera scenarier, som alla är maximerade med samhantering:

- Användare kan driva sina egna distributioner av nya enheter i antingen Active Directory med hybrid Azure AD-anslutning eller Azure Active Directory (Azure AD)  

- Du kan ställa in självdistribuerade nya enhets distributioner i Azure AD för delade enheter och kiosker  

- Med Windows autopilot för befintliga enheter använder du Configuration Manager för att migrera en befintlig enhet från Windows 7 och Active Directory till Windows 10 och Azure AD  

I följande videoklipp är Senior program hanterare Danny Guillory och huvudsaklig program hanterare Anders Mcmurrays diskuterar och demonstrera Windows autopilot med samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Fördelar

När du använder samhantering och autopilot tillsammans, ser du till att nya enheter som anger ditt nätverk slutar med samma tillstånd som hantering. I den här installationen registreras enheter i Intune och har en Configuration Manager-klient.  Du kan använda den nya etablerings modellen för Windows 10 och hjälpa dig att eliminera behovet av att skapa, underhålla och uppdatera anpassade OS-avbildningar. 

I alla dessa scenarier kan du automatiskt [Aktivera samhantering](how-to-prepare-Win10.md) av Intune. Den här automationen hjälper till med etablerings processen och för pågående hantering av enheten.

Med autopilot behöver du inte bekymra dig om avbildningar och driv rutiner. Fokusera på att allokera enheter genom denna automatiserade process med hjälp av Intune och Configuration Manager via samhantering.


Så här gör du för att använda samhantering och autopilot tillsammans:

#### <a name="reduce-time-costs-and-complexity"></a>Minska tid, kostnader och komplexitet
Windows autopilot använder den OEM-optimerade versionen av Windows 10 som är förinstallerad på enheten. Den här konfigurationen sparar organisationer för att kunna underhålla anpassade avbildningar och driv rutiner för varje enhets modell som används. I stället för att ändra avbildningen av enheten, omvandla den befintliga Windows 10-installationen till ett "affärs klart" läge. Den tillämpar inställningar och principer, installerar appar och ändrar utgåvan av Windows 10. Du kan till exempel uppgradera från Windows 10 Pro till Windows 10 Enterprise så att du har stöd för avancerade funktioner.

#### <a name="improve-the-user-experience"></a>Förbättra användar upplevelsen
Den bästa användar upplevelsen orsakar minsta möjliga avbrott och hjälper dem att komma tillbaka till att fokusera på sitt arbete. Windows autopilot erbjuder en enkel metod för att hjälpa dina användare att komma igång snabbt med några få enkla klick och deras autentiseringsuppgifter för Azure AD. För många organisationer med ett stort antal fjärranslutna anställda använder du Windows autopilot för att leverera nya enheter direkt från tillverkaren.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Använd autopilot och Configuration Manager för att migrera befintliga Windows 7-enheter till Windows 10
Med Windows autopilot för befintliga enheter skapar du en konfigurations fil och distribuerar den med en Configuration Manager aktivitetssekvens. Den här processen migrerar enkelt befintliga enheter från Windows 7 till Windows 10. Du kan använda en signatur Windows 10-avbildning i Configuration Manager och sedan tillämpa den på den befintliga Windows 7-enheten med autopilot-konfigurationen. När användaren startar enheten använder de den autopilotbaserade onboarding-processen.

Här följer stegen för autopilot för befintliga enheter:

![Process översikt för Windows autopilot för befintliga enheter](media/autopilot-for-existing-devices.png)

1. Distribuera grup princip för att omdirigera kända mappar till OneDrive
2. Generera konfigurations fil för autopilot
3. Distribuera aktivitetssekvens för att uppgradera till Windows 10
4. Windows 10-dator går via autopilot vid första starten

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modern enhets etablering för alla typer av arbetare
Med autopilot kan du nu tillhandahålla en kostnads fri OS-distribution till ej bemannade enheter eller delade enheter med hjälp av själv distributions läge. Den här installationen uppfyller behoven hos alla olika typer av arbetare. Dessutom kontrollerar Windows autopilot-funktionen reset att reetablering av en enhet till en ny användare är enkel och enkel. Den här processen fören klar vad som traditionellt varit svårt att utföra när du har säsongs-eller kontrakts arbetare. 



## <a name="case-study"></a>Fallstudie

Den tyska logistik-och järn vägs fraktens företags DB-Schenker använder autopilot för att öka den anställdas produktivitet och frigöra IT-team från att arbeta med dagliga support uppgifter. DB-Schenker har flyttats bort från den traditionella avbildningen och ersatt den med etableringen via molnet. De använder nu Azure AD-Join och Intune för att snabbt få igång nya enheter. 

I stället för att låta deras avlopps tid för fjärranställda resa till en plats med IT-tjänster, använder DB Schenker nu Windows autopilot. De levererar sina anställdas maskin vara direkt från tillverkaren till sitt lokala fält kontor. Arbets tagaren ansluter den nya enheten till Internet och loggar in med sina autentiseringsuppgifter för Azure AD. Enheten ansluter sedan till de program och tjänster som DB-Schenker IT-avdelningen tilldelar användarens enskilda profil.

Mer information finns i [globalt logistik företag som centraliserar IT, som bearbetar anställda med modern digital arbets plats](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Värde förslag

Skapa tillfredsställelse i din organisation genom att skapa en bättre användar upplevelse för dina användare. Använd Windows autopilot för att sänka kostnaderna. Frigör din tid och fokusera på andra projekt för att öka värdet och effekten för din organisation.



## <a name="configure"></a>Konfigurera

Mer information finns i följande artiklar:

[Använd Intune för att skapa Windows autopilot-profiler](/intune/enrollment-autopilot)

[Windows Autopilot för befintliga enheter](../../autopilot/existing-devices.md)