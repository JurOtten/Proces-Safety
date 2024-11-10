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
WachtenOpZet --> ZetGedaan : GVL.game_status == 1 && GVL.Rechthoek_(1 t/m 9) == TRUE && NOT (GVL.Driehoek_(1 t/m 9) OR GVL.Rondje_(1 t/m 9))
ZetGedaan --> BeurtWissel : zetGedaan == TRUE
BeurtWissel --> WinCheck : GVL.game_status := 2
WinCheck --> [*]
@enduml

@startuml
[*] --> ControleerWinnaar

ControleerWinnaar --> Speler1Gewonnen : GVL.Driehoek_1 AND GVL.Driehoek_2 AND GVL.Driehoek_3
ControleerWinnaar --> Speler2Gewonnen : GVL.Rondje_1 AND GVL.Rondje_2 AND GVL.Rondje_3
ControleerWinnaar --> Gelijkspel : (GVL.Driehoek_(1 t/m 9) OR GVL.Rondje_(1 t/m 9)
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

@startuml
actor Player1
actor Player2
participant "Game" as Game
participant "Board" as Board

Player1 -> Game: startGame()
Player2 -> Game: startGame()
Game -> Board: initialize()

Game -> Game: determineFirstPlayer()
alt Random player chosen
    Game -> Player1: Player1 starts
else
    Game -> Player2: Player2 starts
end

loop each turn
    alt Player1's turn
        Player1 -> Game: makeMove(x, y)
        Game -> Board: updateBoard(x, y, Player1)
    else Player2's turn
        Player2 -> Game: makeMove(x, y)
        Game -> Board: updateBoard(x, y, Player2)
    end

    alt Check for win
        Game -> Board: checkWin()
        Board -> Game: win = true
        alt Player1 wins
            Game -> Player1: declareWinner(Player1)
        else Player2 wins
            Game -> Player2: declareWinner(Player2)
        end
        break
    end

    alt Check for draw
        Game -> Board: isDraw()
        Board -> Game: draw = true
        Game -> Player1: declareDraw()
        Game -> Player2: declareDraw()
        break
    end
    
    Game -> Player1: nextTurn()
    Game -> Player2: nextTurn()
end
@enduml



```
