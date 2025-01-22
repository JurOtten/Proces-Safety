# 3.Sequence Diagram for Task Communication

```plantuml

@startuml
actor Speler
entity GVL

Speler -> GVL : Start spel (Begin_Knop)
GVL -> GVL : Spelerstatus = "spelend"
GVL -> GVL : Spelstatus = "beurt spelen"
GVL -> GVL : Verhoog randomCounter
GVL -> GVL : Genereer pseudo-willekeurig getal
GVL -> GVL : Bepaal actieve speler
GVL -> GVL : Zet Player_1_Lamp / Player_2_Lamp aan

Speler -> GVL : Zet figuur (Rechthoek_X)
GVL -> GVL : Controleer actieve speler
GVL -> GVL : Plaats figuur (Driehoek/Rondje)
GVL -> GVL : Zet zetGedaan = TRUE
GVL -> GVL : Wissel actieve speler
GVL -> GVL : Spelstatus = "controlefase"

GVL -> GVL : Controleer winnaar
alt Speler 1 wint
    GVL -> GVL : Spelerstatus = "gewonnen" (Speler 1)
    GVL -> GVL : Zet winnaar = 1
    GVL -> GVL : Zet Player_1_Lamp_G aan
    GVL -> GVL : Zet spelstatus = "eindfase"
else Speler 2 wint
    GVL -> GVL : Spelerstatus = "gewonnen" (Speler 2)
    GVL -> GVL : Zet winnaar = 2
    GVL -> GVL : Zet Player_2_Lamp_G aan
    GVL -> GVL : Zet spelstatus = "eindfase"
else Geen winnaar, controleer gelijkspel
    GVL -> GVL : Controleer gelijkspel
    alt Gelijkspel
        GVL -> GVL : Spelerstatus = "gelijkspel"
        GVL -> GVL : Zet Player_1_Lamp en Player_2_Lamp uit
        GVL -> GVL : Zet spelstatus = "eindfase"
    else Geen gelijkspel
        GVL -> GVL : Spelstatus = "beurt spelen" (Volgende ronde)
    end
end

Speler -> GVL : Reset spel (Reset_Knop)
GVL -> GVL : Reset spelerstatus = "inactief"
GVL -> GVL : Reset spelstatus = "niet gestart"
GVL -> GVL : Reset variabelen

@enduml


```
Uitleg:

- Het sequentie diagram toont de communicatie tussen de speler (Speler), de spelvariabelen (GVL), en de functies die de kernlogica van het spel verwerken. De flow omvat het starten van het spel, het plaatsen van zetten, het controleren van winnaars en het resetten van het spel.