<!-- This include file is for both the Android Enterprise framework and the APP data protection framework. Therefore, do not edit this file to be specific to either.-->

Innan du distribuerar ramverket rekommenderar Microsoft att du använder en ringmetod för att testa verifieringen. Att definiera distributionsringar är vanligtvis en engångshändelse (eller åtminstone ovanligt). IT bör dock gå tillbaka till dessa grupper för att säkerställa att ordningsföljden fortfarande är korrekt.

Microsoft rekommenderar följande distributionsringsmetod för ramverket:

| Distributionsring  | Klient  | Utvärderingsverktyg  | Utdata  | Tidslinje  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Kvalitetskontroll  | Klientorganisation före produktion  | Mobilkapacitetsägare, säkerhet, riskbedömning, sekretess, UX  | Validering av funktionellt scenario, utkastdokumentation  | 0–30 dagar  |
| Förhandsgranskning  | Klientorganisation för produktion  | Mobilkapacitetsägare, UX  | Validering av slutanvändarscenario, användarriktad dokumentation  | 7–14 dagar, efter kvalitetskontroll  |
| Produktion  | Klientorganisation för produktion  | Mobilkapacitetsägare, IT-support  | E.t.  | 7 dagar till flera veckor, efter förhandsgranskning  |

Alla ändringar av appskyddsprinciper ska först utföras i en förproduktionsmiljö så att man förstår effekterna av principändringarna. När testningen är klar kan ändringarna flyttas till produktion och tillämpas på en delmängd av produktionsanvändare, IT-avdelningen och andra tillämpliga grupper. Slutligen kan distributionen slutföras till övriga mobilanvändare. Att distribuera ut till produktion kan ta längre tid beroende på ändringarnas grad av påverkan. Om det inte finns någon användarpåverkan så borde ändringen distribueras snabbt. Om det finns en användarpåverkan kan distributionen behöva gå långsammare på grund av behovet att kommunicera ändringarna till användarpopulationen.