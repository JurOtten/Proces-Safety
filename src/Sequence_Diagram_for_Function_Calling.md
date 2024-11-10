# 4.Sequence Diagram for Function Calling

```plantuml

@startuml
actor Speler
entity GVL
entity Functies

Speler -> GVL : Start het spel (Begin_Knop)
GVL -> Functies : Verhoog randomCounter()
Functies -> GVL : Verhoog randomCounter
GVL -> Functies : GenereerPseudoWillekeurigGetal()
Functies -> GVL : Genereer pseudo-willekeurig getal (tempRand)
GVL -> Functies : BepaalSpeler()
Functies -> GVL : Zet Player_1 / Player_2 aan of uit
GVL -> GVL : Zet Player_1_Lamp / Player_2_Lamp aan
GVL -> GVL : Zet game_status naar 1

Speler -> GVL : Zet figuur (Rechthoek_X)
GVL -> Functies : ControleerSpeler()
Functies -> GVL : Controleer wie aan de beurt is (Player_1/Player_2)
GVL -> Functies : PlaatsFiguur()
Functies -> GVL : Plaats Driehoek / Rondje in vakje
GVL -> GVL : Zet zetGedaan = TRUE
GVL -> Functies : WisselBeurt()
Functies -> GVL : Wissel Player_1 en Player_2
GVL -> GVL : Zet game_status naar 2

GVL -> Functies : ControleerWinnaar()
Functies -> GVL : Controleer of er een winnaar is (Driehoek/Rondje lijnen)
alt Speler 1 wint
    GVL -> GVL : Zet winnaar = 1
    GVL -> GVL : Zet Player_1_Lamp_G aan
    GVL -> GVL : Zet Player_2_Lamp uit
    GVL -> GVL : Zet game_status naar 3
else Speler 2 wint
    GVL -> GVL : Zet winnaar = 2
    GVL -> GVL : Zet Player_2_Lamp_G aan
    GVL -> GVL : Zet Player_1_Lamp uit
    GVL -> GVL : Zet game_status naar 3
else Geen winnaar, check gelijkspel
    GVL -> Functies : ControleerGelijkspel()
    Functies -> GVL : Controleer of het gelijkspel is
    alt Gelijkspel
        GVL -> GVL : Zet Gelijkspel = TRUE
        GVL -> GVL : Zet Player_1_Lamp en Player_2_Lamp uit
    end
    GVL -> GVL : Zet game_status naar 1 (terug naar beurtfase)
end

Speler -> GVL : Reset het spel (Reset_Knop)
GVL -> Functies : ResetSpel()
Functies -> GVL : Reset alle variabelen naar beginstatus

@enduml

```

Uitleg:

- Dit diagram toont de interacties tussen de speler, de spelvariabelen en de functies die de logica van het spel beheren. Het laat zien hoe functies worden aangeroepen om de status van het spel bij te houden en de spelbeurten te beheren.