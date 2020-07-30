---
title: Förbättrad HTTP
titleSuffix: Configuration Manager
description: Använd modern autentisering för att skydda klient kommunikation utan behov av PKI-certifikat.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79b4119a12826596fcc91fa1b4ead4e151e2ddd8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262106"
---
# <a name="enhanced-http"></a>Förbättrad HTTP

*Gäller för: Configuration Manager (aktuell gren)*

<!--1356889,1358460-->

> [!Tip]  
> Den här funktionen introducerades först i version 1806 som en [för hands versions funktion](../../servers/manage/pre-release-features.md). Från och med version 1810 är den här funktionen inte längre en för hands versions funktion.  

Microsoft rekommenderar att HTTPS-kommunikation används för alla Configuration Manager kommunikations vägar, men det är svårt för vissa kunder på grund av omkostnader för hantering av PKI-certifikat.

Configuration Manager version 1806 innehåller förbättringar av hur klienter kommunicerar med plats system. Det finns två primära mål för dessa förbättringar:  

- Du kan skydda känslig klient kommunikation utan att behöva certifikat för PKI-serverautentisering.  

- Klienter kan få säker åtkomst till innehåll från distributions platser utan att det behövs ett konto för nätverks åtkomst, ett PKI-certifikat och Windows-autentisering.  

All annan klient kommunikation är över HTTP. Utökad HTTP är inte detsamma som att aktivera HTTPS för klient kommunikation eller ett plats system.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI-certifikat är fortfarande ett giltigt alternativ för kunder med följande krav:  
>
> - All klient kommunikation är över HTTPS  
> - Avancerad kontroll över signerings infrastrukturen
>
> Om du redan använder PKI används även PKI-certifikatet som är kopplat till IIS även om utökad HTTP är aktiverat.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Olika

Följande scenarier drar nytta av dessa förbättringar:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a>Scenario 1: klient till hanterings plats

<!--1356889-->
[Azure Active Directory (Azure AD) – anslutna enheter](/azure/active-directory/devices/concept-azure-ad-join) och enheter med en [Configuration Manager Utfärdad token](../../clients/deploy/deploy-clients-cmg-token.md) kan kommunicera med en hanterings plats som är konfigurerad för http om du aktiverar utökat http för webbplatsen. Med utökad HTTP aktive rad genererar plats servern ett certifikat för hanterings platsen så att den kan kommunicera via en säker kanal.

> [!Note]  
> Det här scenariot kräver inte användning av en HTTPS-aktiverad hanterings plats, men stöds som ett alternativ till att använda utökad HTTP. Mer information om hur du använder en HTTPS-aktiverad hanterings plats finns i [Aktivera hanterings plats för https](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a>Scenario 2: klient till distributions plats

<!--1358228-->
En arbets grupp eller en Azure AD-ansluten klient kan autentisera och hämta innehåll via en säker kanal från en distributions plats som kon figurer ATS för HTTP. Dessa typer av enheter kan också autentisera och hämta innehåll från en distributions plats som kon figurer ATS för HTTPS utan att ett PKI-certifikat krävs på klienten. Det är svårt att lägga till ett certifikat för klientautentisering till en arbets grupp eller en Azure AD-ansluten klient.

Det här problemet omfattar distributions scenarier för operativ system med en aktivitetssekvens som körs från startmedia, PXE eller Software Center. Mer information finns i [konto för nätverks åtkomst](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a>Scenario 3: enhets identitet för Azure AD

<!--1358460-->
En Azure AD-ansluten eller en [hybrid Azure AD-enhet](/azure/active-directory/devices/concept-azure-ad-join-hybrid) utan en Azure AD-användare som är inloggad kan kommunicera säkert med den tilldelade platsen. Den molnbaserade enhets identiteten räcker nu för att autentisera med CMG och hanterings platsen för enhets drivna scenarier. (En användartoken krävs fortfarande för användarbaserade scenarier.)  


## <a name="features"></a>Funktioner

Följande Configuration Manager funktioner stöder eller kräver utökad HTTP:

- [Gateway för molnhantering](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [OS-distribution utan konto för nätverks åtkomst](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Aktivera samhantering för nya Internet-baserade Windows 10-enheter](../../../comanage/tutorial-co-manage-new-devices.md)
- [Appens godkännanden via e-post](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Administrations tjänst](../../../develop/adminservice/overview.md)
- [Visa nyligen anslutna konsoler](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Program uppdaterings platsen och relaterade scenarier har alltid stöd för säker HTTP-trafik med-klienter samt Cloud Management Gateway. Den använder en mekanism med hanterings platsen som skiljer sig från certifikat-eller tokenbaserad autentisering.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Förutsättningar  

- En hanterings plats som kon figurer ATS för HTTP-klientanslutningar. Ange det här alternativet på fliken **Allmänt** i egenskaperna för hanterings plats rollen.  

- En distributions plats som kon figurer ATS för HTTP-klientanslutningar. Ange det här alternativet på fliken **kommunikation** i egenskaperna för distributions plats rollen. Aktivera inte alternativet för att **tillåta att klienter ansluter anonymt**.  

- Publicera webbplatsen till Azure AD för moln hantering.  

- *Endast för [Scenario 3](#bkmk_scenario3) *: en klient som kör Windows 10 version 1803 eller senare och som är ansluten till Azure AD. Klienten kräver den här konfigurationen för Azure AD-enhetsautentisering.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Konfigurera platsen

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj platsen och välj **Egenskaper** i menyfliksområdet.  

2. Växla till fliken **klient dator kommunikation** .

    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

    Välj alternativet för **https eller http**. Aktivera sedan alternativet för att **använda Configuration Manager-genererade certifikat för HTTP-platssystem**.

> [!Tip]
> Vänta upp till 30 minuter på att hanterings platsen ska ta emot och konfigurera det nya certifikatet från platsen.

<!--3798957-->
Från och med version 1902 kan du också aktivera utökad HTTP för den centrala administrations webbplatsen. Använd samma process och öppna egenskaperna för den centrala administrations webbplatsen. Den här åtgärden aktiverar endast utökad HTTP för SMS-providerns roller på den centrala administrations platsen. Det är inte en global inställning som gäller för alla platser i hierarkin.

Du kan se dessa certifikat i Configuration Manager-konsolen. Gå till arbets ytan **Administration** , expandera **säkerhet**och välj noden **certifikat** . Leta efter **SMS-utfärdande** rot certifikat och plats server roll certifikat som utfärdats av SMS-utfärdande rot.

Mer information om hur klienten kommunicerar med hanterings platsen och distributions platsen med den här konfigurationen finns i [kommunikation från klienter till plats system och tjänster](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Se även

- [Planera för säkerhet](../security/plan-for-security.md)  

- [Säkerhet och sekretess för Configuration Manager-klienter](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurera säkerhet](../security/configure-security.md)  

- [Kommunikation mellan slut punkter](communications-between-endpoints.md)  
