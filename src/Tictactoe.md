# Tic-tac-toe
'Hier is de diagram gemaakt van Tic-tac-toe'

```plantuml
@startuml
[*] --> WachtenOpStart
WachtenOpStart --> Starten : GVL.game_status == 0 && GVL.Begin_Knop == TRUE
Starten --> Player1Start : tempRand == 0
Starten --> Player2Start : tempRand == 1
Player1Start --> Bezig : GVL.game_status := 1
Player2Start --> Bezig : GVL.game_status := 1
Bezig --> [*]
@enduml


@startuml
[*] --> WachtenOpZet
WachtenOpZet --> ZetGedaan : GVL.game_status == 1 && GVL.Rechthoek_1 t/m 9 == TRUE && NOT (GVL.Driehoek_1 t/m 9 OR GVL.Rondje_1 t/m 9)
ZetGedaan --> BeurtWissel : zetGedaan == TRUE
BeurtWissel --> WinCheck : GVL.game_status := 2
WinCheck --> [*]
@enduml


@startuml
[*] --> ControleerWinnaar

ControleerWinnaar --> Speler1Gewonnen : GVL.Driehoek_1 AND GVL.Driehoek_2 AND GVL.Driehoek_3
ControleerWinnaar --> Speler2Gewonnen : GVL.Rondje_1 AND GVL.Rondje_2 AND GVL.Rondje_3
ControleerWinnaar --> Gelijkspel : (GVL.Driehoek_1 t/m 9 OR GVL.Rondje_1 t/m 9)
Speler1Gewonnen --> EindeSpel : GVL.winnaar := 1
Speler2Gewonnen --> EindeSpel : GVL.winnaar := 2
Gelijkspel --> EindeSpel : GVL.Gelijkspel := TRUE

EindeSpel --> [*]
@enduml

@startuml
[*] --> WachtenOpReset
WachtenOpReset --> Resetten : GVL.Reset_Knop == TRUE
Resetten --> [*] : Reset alle variabelen naar beginstatus
@enduml

