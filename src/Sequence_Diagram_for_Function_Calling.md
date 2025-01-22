# 4.Sequence Diagram for Function Calling

```plantuml
@startuml
entity GVL
entity Functies

GVL -> Functies : StartSpel()
Functies -> GVL : Stel actieve speler in
Functies -> GVL : Zet lampjes aan
GVL -> GVL : Zet game_status naar 1

GVL -> Functies : ZetFiguur(Rechthoek_X)
Functies -> GVL : Plaats figuur in vak
GVL -> Functies : WisselBeurt()
Functies -> GVL : Wissel actieve speler en lampjes
GVL -> GVL : Zet game_status naar 2

GVL -> Functies : ControleerWinnaar()
Functies -> GVL : Controleer winnende combinatie
alt Winnaar gevonden
    Functies -> GVL : Stel winnaar in
    Functies -> GVL : Zet winnende lamp aan
    GV -> GVL : Zet game_status naar 3
else Geen winnaar
    Functies -> GVL : Controleer gelijkspel
    alt Gelijkspel
        Functies -> GVL : Stel gelijkspel in
    else Nog vrije vakken
        Functies -> GVL : Ga door naar volgende beurt
    end
end

GVL -> Functies : ResetSpel()
Functies -> GVL : Reset alle variabelen

@enduml



```

Uitleg:

- Dit diagram toont de interacties tussen de speler, de spelvariabelen en de functies die de logica van het spel beheren. Het laat zien hoe functies worden aangeroepen om de status van het spel bij te houden en de spelbeurten te beheren.


