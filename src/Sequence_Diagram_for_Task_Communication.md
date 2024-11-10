# 3.Sequence Diagram for Task Communication

```plantuml

@startuml
actor Speler
entity GVL

Speler -> GVL : Start het spel (Begin_Knop)
GVL -> GVL : Verhoog randomCounter
GVL -> GVL : Genereer pseudo-willekeurig getal (tempRand)
GVL -> GVL : Bepaal speler 1 of 2
GVL -> GVL : Zet Player_1_Lamp / Player_2_Lamp
GVL -> GVL : Zet game_status naar 1

Speler -> GVL : Zet figuur (Rechthoek_X)
GVL -> GVL : Controleer speler (Player_1/Player_2)
GVL -> GVL : Plaats figuur (Driehoek/Rondje)
GVL -> GVL : Zet zetGedaan = TRUE
GVL -> GVL : Verander beurt (Player_1/Player_2)
GVL -> GVL : Zet game_status naar 2

GVL -> GVL : Controleer winnaar (Driehoek/Rondje lijnen)
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
    GVL -> GVL : Controleer gelijkspel
    alt Gelijkspel
        GVL -> GVL : Zet Gelijkspel = TRUE
        GVL -> GVL : Zet Player_1_Lamp en Player_2_Lamp uit
    end
    GVL -> GVL : Zet game_status naar 1 (terug naar beurtfase)
end

Speler -> GVL : Reset het spel (Reset_Knop)
GVL -> GVL : Reset alle variabelen naar beginstatus

@enduml

```
Uitleg:

- Het sequentie diagram toont de communicatie tussen de speler (Speler), de spelvariabelen (GVL), en de functies die de kernlogica van het spel verwerken. De flow omvat het starten van het spel, het plaatsen van zetten, het controleren van winnaars en het resetten van het spel.