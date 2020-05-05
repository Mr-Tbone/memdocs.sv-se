---
title: Konfigurera säkerhet
titleSuffix: Configuration Manager
description: Konfigurera säkerhetsrelaterade alternativ för Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718667"
---
# <a name="configure-security-in-configuration-manager"></a>Konfigurera säkerhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln för att hjälpa dig att konfigurera säkerhetsrelaterade alternativ för Configuration Manager. Den omfattar följande säkerhets alternativ:
- [Klient dator kommunikation](#BKMK_ConfigureClientPKI) för klient-PKI-certifikat  
- [Signering och kryptering](#BKMK_ConfigureSigningEncryption)  
- [Rollbaserad administration](#BKMK_ConfigureRBA)  
- [Hantera konton](#BKMK_ManageAccounts)  
- [Konfigurera Azure Active Directory](#bkmk_azuread)  
- [Konfigurera autentisering av SMS-provider](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a>Konfigurera inställningar för klient-PKI-certifikat  

Om du vill använda PKI-certifikat (Public Key Infrastructure) för klientanslutningar till platssystem som använder IIS (Internet Information Services) använder du följande procedur för att konfigurera inställningar för dessa certifikat.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Konfigurera inställningar för klient-PKI-certifikat  

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj den primära plats som ska konfigureras.  

2.  I menyfliksområdet väljer du **Egenskaper**. Växla sedan till fliken **klient dator kommunikation** .  

    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

3.  Välj inställningar för plats system som använder IIS.  

    - **Endast https**: klienter som är tilldelade till platsen använder alltid ett PKI-klientcertifikat när de ansluter till plats system som använder IIS.  

    - **Https eller http**: du kräver inte att klienter använder PKI-certifikat.  

    - **Använd Configuration Manager-genererade certifikat för HTTP-plats system**: Mer information om den här inställningen finns i [Enhanced http](../hierarchy/enhanced-http.md).  

4.  Välj inställningar för klient datorer.  

    - **Använd klientens PKI-certifikat (funktion för klientautentisering) när det är tillgängligt**: om du väljer inställningen **https eller http** plats server väljer du det här alternativet om du vill använda ett klient-PKI-certifikat för HTTP-anslutningar. Klienten använder det här certifikatet istället för ett självsignerat certifikat för att autentisera sig för platssystem. Om du väljer **endast https**väljs det här alternativet automatiskt.  

    Om det finns mer än ett giltigt PKI-klientcertifikat på en klient väljer du **ändra** för att konfigurera val metoder för klient certifikat.  

    Mer information om urvalsmetoden för klientcertifikat finns i [Planning for PKI client certificate selection](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **Klienterna kontrollerar listan över återkallade certifikat för plats system**: Aktivera den här inställningen för att klienter ska kunna kontrol lera din organisations CRL för återkallade certifikat.  

    Mer information om CRL-kontroll för klienter finns i [Planning for PKI certificate revocation](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Om du vill importera, Visa och ta bort certifikaten för betrodda rot certifikat utfärdare väljer du **Ange**.  

    Mer information finns i [Planera för BETRODDA PKI-rotcertifikat och listan certifikat utfärdare](plan-for-security.md#BKMK_PlanningForRootCAs).  


Upprepa den här proceduren för alla primära platser i hierarkin.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a>Konfigurera signering och kryptering  

Konfigurera de säkraste inställningarna för signering och kryptering för platssystem som alla platsens klienter stöder. De här inställningarna är speciellt viktiga när du tillåter att klienter kommunicerar med platssystem med självsignerade certifikat över HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Konfigurera signering och kryptering för en plats  

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj den primära plats som ska konfigureras.  

2.  I menyfliksområdet väljer du **Egenskaper**och växlar sedan till fliken **signering och kryptering** .  

    Den här fliken är bara tillgänglig på en primär plats. Om du inte ser fliken **signering och kryptering** kontrollerar du att du inte är ansluten till en central administrations plats eller en sekundär plats.  

3.  Konfigurera signerings-och krypterings alternativen för klienter att kommunicera med platsen.  

    - **Kräv signering**: klienter signerar data innan de skickas till hanterings platsen.  

    - **KRÄV SHA-256**: klienter använder sha-256-algoritmen när data signeras.  

    > [!WARNING]  
    >  **Kräv inte SHA-256** utan att först bekräfta att alla klienter stöder denna hash-algoritm. Dessa klienter innehåller dem som kan tilldelas till platsen i framtiden.  
    >   
    >  Om du väljer det här alternativet och klienter med självsignerade certifikat inte kan stödja SHA-256, Configuration Manager avvisar dem. SMS_MP_CONTROL_MANAGER-komponenten loggar meddelande-ID 5443.  

    - **Använd kryptering**: klienter krypterar klient inventerings data och status meddelanden innan de skickas till hanterings platsen. De använder 3DES-algoritmen.  

Upprepa den här proceduren för alla primära platser i hierarkin.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a>Konfigurera rollbaserad administration  

Rollbaserad administration kombinerar säkerhetsroller, säkerhetsomfattningar och tilldelade samlingar för att definiera den administrativa omfattningen för varje administrativ användare. Ett omfång inkluderar de objekt som en användare kan visa i-konsolen och de uppgifter som är relaterade till de objekt som de har behörighet att göra. Konfigurationer för rollbaserad administration används per plats i en hierarki.  

Mer information finns i [Konfigurera rollbaserad administration](../../servers/deploy/configure/configure-role-based-administration.md). I den här artikeln beskrivs följande åtgärder:  

-  Skapa anpassade säkerhetsroller  

-  Konfigurera säkerhetsroller  

-  Konfigurera säkerhetsomfattningar för ett objekt  

-  Konfigurera samlingar för att hantera säkerhet  

-  Skapa en ny administrativ användare  

- Ändra den administrativa användarens administrativa omfattning  

> [!IMPORTANT]  
>  Din egen  administrativa omfattning definierar de objekt och inställningar som du kan tilldela när du konfigurerar rollbaserad administration för en annan administrativ användare. Information om planering för rollbaserad administration finns i [grunderna i rollbaserad administration](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a>Hantera konton som Configuration Manager använder  

Configuration Manager stöder Windows-konton för många olika uppgifter och användnings områden. Använd följande procedur om du vill visa konton som är konfigurerade för olika uppgifter och för att hantera det lösen ord som Configuration Manager använder för varje konto:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Hantera konton som Configuration Manager använder  

1.  I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **säkerhet**och väljer sedan noden **konton** .  

2.  Om du vill ändra lösen ordet för ett konto väljer du kontot i listan. Välj sedan **Egenskaper** i menyfliksområdet.  

3.  Välj **Ange** för att öppna dialog rutan **Windows-användarkonto** . Ange det nya lösen ordet för Configuration Manager som ska användas för det här kontot.  

    > [!NOTE]  
    >  Det lösen ord som du anger måste matcha det här kontots lösen ord i Active Directory.  

Mer information finns i [konton som används i Configuration Manager](../hierarchy/accounts.md).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a>Konfigurera Azure Active Directory

Integrera Configuration Manager med Azure Active Directory (Azure AD) för att förenkla och moln aktivera din miljö. Gör det möjligt för webbplatsen och klienter att autentisera med hjälp av Azure AD. Mer information finns i **moln hanterings** tjänsten i [Konfigurera Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a>Konfigurera autentisering av SMS-provider

Från och med version 1810 kan du ange den lägsta autentiseringsnivån som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. Mer information finns i [Planera för SMS-providern](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Se även

- [Planera för säkerhet](plan-for-security.md)  

- [Säkerhet och sekretess för Configuration Manager-klienter](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Kommunikation mellan slut punkter](../hierarchy/communications-between-endpoints.md)  

- [Teknisk referens för kryptografiska kontroller](cryptographic-controls-technical-reference.md)  

- [Certifikatkrav för PKI](../network/pki-certificate-requirements.md)  
