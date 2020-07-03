---
title: Samhantering för Windows 10-enheter
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar Windows 10-enheter samtidigt med hjälp av både Configuration Manager och Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/01/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: a7f38f48946244deb6026d040c44159d0384f7b1
ms.sourcegitcommit: efe89408a3948b79b38893174cb19268ee37c8f3
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854447"
---
# <a name="what-is-co-management"></a>Vad är samhantering?

<!-- 1350871 -->
Samhantering är ett av de främsta sätten att koppla din befintliga Configuration Manager-distribution till Microsoft 365 molnet. Det hjälper dig att låsa upp fler moln drivna funktioner som villkorlig åtkomst.

Med samhantering kan du hantera Windows 10-enheter samtidigt med både Configuration Manager och Microsoft Intune. Med den kan du lägga till din befintliga investering i Configuration Manager i molnet genom att lägga till nya funktioner. Genom att använda samhantering har du flexibiliteten att använda den teknik lösning som passar bäst för din organisation.

När en Windows 10-enhet har Configuration Manager-klienten och har registrerats i Intune får du fördelarna med båda tjänsterna. Du kan kontrol lera vilka arbets belastningar, om du vill, byta utfärdare från Configuration Manager till Intune. Configuration Manager fortsätter att hantera alla andra arbets belastningar, inklusive de arbets belastningar som du inte växlar till Intune, och alla andra funktioner i Configuration Manager den samhanteringen inte stöder.

Du kan också piloterar en arbets belastning med en separat samling av enheter. Med pilotering kan du testa Intune-funktionen med en delmängd av enheterna innan du växlar en större grupp.

![Översikts diagram över samhantering](media/co-management-overview.svg)

[Visa diagrammet i full storlek](media/co-management-overview.svg)

> [!Note]  
> När du samtidigt hanterar Windows 10-enheter med både Configuration Manager och Microsoft Intune kallas den här konfigurationen för *samhantering*. När du hanterar enheter med Configuration Manager och registrerar till en MDM-tjänst från tredje part kallas den här konfigurationen för *samexistens*. Att ha två hanterings myndigheter för en enskild enhet kan vara utmanande om de inte är korrekt dirigerade mellan de två. Med samhantering kan Configuration Manager och Intune utjämna [arbets belastningarna](#workloads) för att se till att det inte finns några konflikter. Den här interaktionen finns inte med tjänster från tredje part, så det finns begränsningar med hanterings funktionerna för samexistens. Mer information finns i [MDM-samexistens från tredje part med Configuration Manager](coexistence.md).

## <a name="paths-to-co-management"></a>Sökvägar till samhantering

Det finns två huvudsakliga sökvägar för att uppnå samhantering:  

- **Befintliga Configuration Manager-klienter**: du har Windows 10-enheter som redan är Configuration Manager-klienter. Du konfigurerar hybrid Azure AD och registrerar dem i Intune.  

- **Nya Internetbaserade enheter**: du har nya Windows 10-enheter som ansluter till Azure AD och registreras automatiskt i Intune. Du installerar Configuration Manager klienten för att uppnå ett samhanterings tillstånd.  

Mer information om sökvägar finns i [sökvägar till samhantering](quickstart-paths.md).

## <a name="benefits"></a>Fördelar

När du registrerar befintliga Configuration Manager-klienter i samhantering får du följande omedelbara värde:  

- Villkorlig åtkomst med enhetens efterlevnad  

- Intune-baserade fjärråtgärder, till exempel: restart, fjärr styrning eller fabriks återställning

- Central synlighet för enhetens hälso tillstånd  

- Länka användare, enheter och appar med Azure Active Directory (Azure AD)  

- Modern etablering med Windows autopilot  

- Fjärråtgärder

Mer information om det här omedelbara värdet från samhantering finns i snabb starts serien till [Cloud Connect with Co-Management](quickstarts.md).

Med samhantering kan du också dirigera med Intune för flera arbets belastningar. Mer information finns i avsnittet om [arbets belastningar](#workloads) .

## <a name="prerequisites"></a>Förutsättningar

Samhanteringen har följande krav inom följande områden:

- [Licensiering](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Behörigheter och roller](#permissions-and-roles)  

### <a name="licensing"></a>Licensiering

- Azure AD Premium

    > [!Note]  
    > En Enterprise Mobility + Security-prenumeration (EMS) inkluderar både Azure Active Directory Premium och Microsoft Intune.

- Minst en Intune-licens för dig som administratör för att få åtkomst till Intune-portalen.

    > [!Tip]
    > Se till att tilldela en Intune-licens till det konto som du använder för att logga in på din klient organisation. Annars Miss lyckas inloggningen med fel meddelandet "användaren känns inte igen".
    >
    > Du kanske inte behöver köpa och tilldela enskilda Intune-eller EMS-licenser till dina användare. Mer information finns i [vanliga frågor och svar om produkt och licensiering](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="configuration-manager"></a>Configuration Manager

Co-Management kräver Configuration Manager version 1710 eller senare.

Från och med Configuration Manager version 1806 kan du ansluta flera Configuration Manager-instanser till en enda Intune-klient. <!--1357944-->  

Om du aktiverar samhantering behöver du inte publicera din webbplats med Azure AD. För det [andra Sök vägs scenariot](#paths-to-co-management)kräver internetbaserade Configuration Manager klienter [Cloud Management Gateway](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG). CMG kräver att platsen har [publicerats till Azure AD för moln hantering](../core/servers/deploy/configure/azure-services-wizard.md).

### <a name="azure-ad"></a>Azure AD

- Windows 10-enheter måste vara anslutna till Azure AD. De kan vara någon av följande typer:  

  - [Hybrid Azure AD-ansluten](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid), där enheten är ansluten till din lokala Active Directory och registrerad med din Azure Active Directory.

  - Endast [Azure AD-ansluten](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Den här typen kallas ibland "molnbaserad domän ansluten")<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Konfigurera Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Aktivera automatisk registrering i Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Uppgradera dina enheter till Windows 10, version 1709 eller senare. Mer information finns i [införa Windows som en tjänst](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Windows 10 Mobile-enheter stöder inte samhantering.

### <a name="permissions-and-roles"></a>Behörigheter och roller

<!--SCCMDocs issue #667-->
| Åtgärd | Roll krävs |
|----|----|
| Konfigurera en gateway för moln hantering i Configuration Manager | Azure- **prenumerations hanterare** |
| Skapa Azure AD-appar från Configuration Manager | **Global administratör** för Azure AD |
| Importera Azure-appar i Configuration Manager | Configuration Manager **Fullständig administratör**<br>Inga ytterligare Azure-roller behövs |
| Aktivera samhantering i Configuration Manager | En Azure AD-användare<br>Configuration Manager **Fullständig administratör** med **alla** omfångs rättigheter.<!--SCCMDoc issue 626--> |

Mer information om Azure-roller finns i [förstå de olika rollerna](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Mer information om Configuration Manager roller finns i [grunderna i rollbaserad administration](../core/understand/fundamentals-of-role-based-administration.md).

## <a name="workloads"></a>Arbetsbelastningar

Du behöver inte byta arbets belastningar eller så kan du göra dem individuellt när du är klar. Configuration Manager fortsätter att hantera alla andra arbets belastningar, inklusive de arbets belastningar som du inte växlar till Intune, och alla andra funktioner i Configuration Manager den samhanteringen inte stöder.

Samhantering har stöd för följande arbets belastningar:

- Efterlevnadsprinciper  

- Windows Update principer  

- Resurs åtkomst principer  

- Slutpunktsskydd  

- Enhetskonfiguration  

- Office Klicka-och-kör-appar  

- Klientappar  

Mer information finns i [arbets belastningar](workloads.md).

## <a name="monitor-co-management"></a>Övervaka samhantering

Instrument panelen för samhantering hjälper dig att granska datorer som är samhanterade i din miljö. Diagrammen kan hjälpa till att identifiera enheter som kan behöva åtgärdas.

![Skärm bild av instrument panelen för samhantering](media/co-management-dashboard.png)

Mer information finns i [så här övervakar du samhantering](how-to-monitor.md).

## <a name="next-steps"></a>Nästa steg

- [Lär dig mer om omedelbar värde och kom igång med samhantering](quickstarts.md)  

- [Självstudie: Aktivera samhantering för befintliga Configuration Manager-klienter](tutorial-co-manage-clients.md)  
