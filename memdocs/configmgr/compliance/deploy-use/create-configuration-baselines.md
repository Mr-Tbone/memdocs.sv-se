---
title: Skapa konfigurationsbaslinjer
titleSuffix: Configuration Manager
description: Skapa konfigurations bas linjer i Configuration Manager som du kan distribuera till en samling.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 01355230d0dc8969555740cc25a08e0b8d2967d0
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240481"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Skapa konfigurations bas linjer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Konfigurations bas linjer i Configuration Manager innehåller fördefinierade konfigurations objekt och eventuellt andra konfigurations bas linjer. När en konfigurationsbaslinje har skapats kan du distribuera den till en samling så att enheter i samlingen hämtar konfigurationsbaslinjen och använder den för att utvärdera sin kompatibilitet.  

> [!TIP]
> Det finns inget sätt att ange i vilken ordning som Configuration Manager klienten utvärderar konfigurations objekt i en bas linje. Den är icke-deterministisk.<!-- MEMDocs#175 -->

## <a name="configuration-baselines"></a>Konfigurationsbaslinjer

 Konfigurations bas linjer i Configuration Manager kan innehålla vissa revisioner av konfigurations objekt eller kan konfigureras att alltid använda den senaste versionen av ett konfigurations objekt. Mer information om revisioner av konfigurations objekt finns i [hanterings aktiviteter för konfigurations data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Det finns två metoder som du kan använda för att skapa konfigurations bas linjer:  

- Importera konfigurationsdata från en fil. Du startar guiden **Importera konfigurationsdata**genom att klicka på **Importera konfigurationsdata** under noden **Konfigurationsobjekt** eller **Konfigurationsbaslinjer** på arbetsytan **Tillgångar och efterlevnad**. Mer information finns i [Importera konfigurations data](import-configuration-data.md).

- Skapa en ny dialogruta med hjälp av dialogrutan **Skapa konfigurationsbaslinje** .  

## <a name="create-a-configuration-baseline"></a>Skapa en konfigurationsbaslinje

Använd följande procedur för att skapa en konfigurations bas linje med hjälp av dialog rutan **skapa konfigurations bas linje** :  

1. I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad**  >  **kompatibilitetsinställningar**  >  **konfigurations bas linjer**.  

2. Klicka på **Skapa konfigurationsbaslinje** i gruppen **Skapa** på fliken **Start**.  

3. Ange ett unikt namn och en beskrivning för konfigurationsbaslinjen i dialogrutan **Skapa konfigurationsbaslinje** . Du kan använda högst 255 tecken för namnet och 512 tecken för beskrivningen.  

4. Listan **Konfigurationsdata** visar alla konfigurationsobjekt eller konfigurationsbaslinjer som ingår i den här konfigurationsbaslinjen. Lägg till ett nytt konfigurationsobjekt eller en ny konfigurationsbaslinje genom att klicka på **Lägg till** . Du kan välja bland följande objekt:  

   - **Konfigurations objekt**  

   - **Program uppdateringar**  

   - **Konfigurations bas linjer**  
     > [!IMPORTANT]
     > Du måste begränsa varje konfigurations bas linje till högst 1000 program varu uppdateringar.
5. Använd listan **ändra syfte** för att ange beteendet för ett konfigurations objekt som du har valt i listan **konfigurations data** . Du kan välja bland följande objekt:  

   -   **Obligatoriskt**: konfigurations bas linjen utvärderas som inkompatibel om konfigurationsobjektet inte identifieras på en klienten het. Om det upptäcks utvärderas det för kompatibilitet  

   -   **Valfritt**: konfigurationsobjektet utvärderas endast för kompatibilitet om programmet som det refererar till finns på klient datorer. Om programmet inte hittas markeras inte konfigurations bas linjen som inkompatibel (gäller endast program konfigurations objekt).  

   -   **Tillåts**inte: konfigurations bas linjen utvärderas som inkompatibel om konfigurationsobjektet identifieras på klient datorer (gäller endast program konfigurations objekt).  

   > [!NOTE]
   >  Listan **Ändra syfte** är bara tillgänglig om du klickade på alternativet **Det här konfigurationsobjektet innehåller programinställningar** på sidan **Allmänt** i guiden **Skapa konfigurationsobjekt**.  

6. Använd listan **Ändra ändring** och välj en specifik eller den senaste ändringen av konfigurationsobjektet vars kompatibilitet ska utvärderas på klientenheter eller välj **Använd alltid senaste** om du alltid vill använda den senaste versionen. Mer information om revisioner av konfigurations objekt finns i [hanterings aktiviteter för konfigurations data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Om du vill ta bort ett konfigurations objekt från konfigurations bas linjen väljer du ett konfigurations objekt och klickar sedan på **ta bort**.  

8. Från och med version 1806 väljer du om du **alltid vill använda den här bas linjen för samhanterade klienter**. När det här alternativet är markerat tillämpas den här bas linjen även på klienter som hanteras av Intune.  Detta undantag kan användas för att konfigurera inställningar som krävs av din organisation men som ännu inte är tillgängliga i Intune.

9. Du kan också klicka på **Kategorier** för att tilldela kategorier till bas linjen för sökning och filtrering. 

10. Stäng dialogrutan **Skapa konfigurationsbaslinje** och skapa konfigurationsbaslinjen genom att klicka på **OK** .  

>[!NOTE]
> Om du ändrar en befintlig bas linje, till exempel inställningen **Använd alltid den här bas linjen för samhanterade klienter**, ökar bas linjens innehålls version. Klienterna måste utvärdera den nya versionen för att uppdatera bas linje rapporteringen.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a>Inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper
<!--3608345-->
*(Lanseras i version 1910)*

Från och med version 1910 kan du lägga till utvärdering av anpassade konfigurations bas linjer som en bedömnings regel för efterlevnadsprinciper. När du skapar eller redigerar en konfigurations bas linje har du ett alternativ för att **utvärdera den här bas linjen som en del av utvärderingen av efterlevnadsprinciper**. När du lägger till eller redigerar en regel för efterlevnadsprinciper har du ett villkor som kallas **Inkludera konfigurerade bas linjer i utvärderingen av efterlevnadsprinciper**. För samhanterade enheter, och när du konfigurerar Intune att ta Configuration Manager utvärderings resultat för efterlevnad som en del av den övergripande kompatibilitetsstatus, skickas den här informationen till Azure AD. Du kan sedan använda den för villkorlig åtkomst till dina Office 365-resurser. Mer information finns i [villkorlig åtkomst med samhantering](../../comanage/quickstart-conditional-access.md).

Om du vill inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper gör du följande:

- Skapa och distribuera en efterlevnadsprincip till en användar samling med en regel för att [**Inkludera konfigurerade bas linjer i utvärderingen av efterlevnadsprinciper**](#bkmk_CA).
- Välj [**utvärdera den här bas linjen som en del av utvärderingen av efterlevnadsprinciper**](#bkmk_eval-baseline) i en konfigurations bas linje som distribueras till en enhets samling.

> [!IMPORTANT]
> Se till att du uppfyller [kraven för samhantering](../../comanage/overview.md#prerequisites)när du riktar in dig på enheter som hanteras tillsammans.

### <a name="example-evaluation-scenario"></a>Exempel på utvärderings scenario

När en användare är en del av en samling som är riktad mot en efterlevnadsprincip som innehåller regel villkoret **Inkludera konfigurerade bas linjer i utvärderingen av efterlevnadsprinciper**, alla bas linjer med utgångs punkt i alternativet **utvärdera den här bas linjen som en del av alternativet utvärdering av efterlevnadsprincip** som är markerat och som distribueras till användaren eller användarens enhet utvärderas för kompatibilitet. Till exempel:

- `User1`är en del av `User Collection 1` .
- `User1`använder `Device1` , som finns i `Device Collection 1` och `Device Collection 2` .
- `Compliance Policy 1`har villkoret **Inkludera konfigurerade bas linjer i bedömnings** regeln för efterlevnadsprinciper och distribueras till `User Collection 1` .
- `Configuration Baseline 1`har **utvärdera denna bas linje som en del av utvärderingen av efterlevnadsprinciper** valt och distribueras till `Device Collection 1` .
- `Configuration Baseline 2`har **utvärdera denna bas linje som en del av utvärderingen av efterlevnadsprinciper** valt och distribueras till `Device Collection 2` .

I det här scenariot `Compliance Policy 1` utvärderas, när de utvärderas för att `User1` använda `Device1` , både `Configuration Baseline 1` och `Configuration Baseline 2` .

- `User1`använder ibland `Device2` .
- `Device2`är medlem i `Device Collection 2` och `Device Collection 3` .
- `Device Collection 3`har `Configuration Baseline 3` distribuerats till den, men **utvärdera den här bas linjen som en del av utvärderingen av efterlevnadsprinciper** är inte markerad.

Vid `User1` användning `Device2` `Configuration Baseline 2` utvärderas endast när det `Compliance Policy 1` utvärderas.

> [!NOTE]
><!--5582516-->
> Om policyn för efterlevnad utvärderar en ny bas linje som aldrig har utvärderats på klienten tidigare, kan den rapportera bristande efterlevnad. Detta inträffar om utvärderingen av bas linjen fortfarande körs när kompatibiliteten utvärderas. Du kan lösa problemet genom att klicka på **kontrol lera efterlevnad** i **Software Center**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>Skapa och distribuera en efterlevnadsprincip med en regel för utvärdering av efterlevnadsprincip för efterlevnad

1. I arbets ytan **till gångar och efterlevnad** expanderar du **kompatibilitetsinställningar**och väljer sedan noden **efterlevnadsprinciper** .
1. Klicka på **skapa policy för efterlevnad** i menyfliksområdet för att öppna **guiden skapa efterlevnadsprincip**. 
1. På sidan **Allmänt** väljer du **regler för efterlevnad för enheter som hanteras med Configuration Manager-klienten**.
   - Enheter måste hanteras med Configuration Manager-klienten för att inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper.
1. Välj plattformar på sidorna **plattformar som stöds** .
1. På sidan **regler** väljer du **ny**och väljer sedan alternativet **Inkludera konfigurerade bas linjer i bedömnings** villkor för efterlevnadsprinciper.

   ![Ta med konfigurerade bas linjer i bedömnings villkor för efterlevnadsprincip](./media/3608345-create-compliance-policy-rule.png)

1. Klicka på **OK**och klicka sedan på **Nästa** för att komma till sidan **Sammanfattning** .
1. Verifiera dina val och klicka på **Nästa** och sedan på **Stäng**.
1. Högerklicka på den princip som du skapade i noden **efterlevnadsprinciper** och välj **distribuera**.
1. Välj din samling, inställningar för generering av aviseringar och schema för utvärdering av kompatibilitet för principen.
1. Klicka på **OK** för att distribuera policyn för efterlevnad.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Välj en konfigurations bas linje och markera utvärdera denna bas linje som en del av utvärderingen av efterlevnadsprinciper

1. I arbets ytan **till gångar och efterlevnad** expanderar du **kompatibilitetsinställningar**och väljer noden **konfigurations bas linjer** .
1. Högerklicka på en befintlig bas linje som har distribuerats till en enhets samling och välj sedan **Egenskaper**. Om det behövs kan du skapa en ny bas linje.
   - Bas linjen måste distribueras till en enhets samling, inte en användar samling.
1. Aktivera **utvärdera den här bas linjen som en del av utvärderings inställningen för efterlevnadsprinciper** .
   - För samhanterade enheter som har Intune som **enhets konfigurations** auktoritet, se alltid till att **tillämpa den här bas linjen även för samhanterade klienter** .
1. Spara ändringarna i konfigurations bas linjen genom att klicka på **OK** .

   ![Dialog rutan Egenskaper för konfigurations bas linje](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Loggfiler för anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper

- ComplianceHandler. log
- SettingsAgent. log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Nästa steg

[Importera konfigurationsdata](import-configuration-data.md)
