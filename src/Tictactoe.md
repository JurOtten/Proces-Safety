# 2.Tasks


## 2.1.State Diagram for Task 1: Game Initialization

```plantuml
@startuml PRG1_Start_Spel

!theme spacelab-white
skinparam backgroundcolor transparent

[*] -right-> WACHTEN : PLC Power-up  
WACHTEN --> START : Startknop ingedrukt  
START --> SPEL_BEZIG : Speler geselecteerd\nRandom keuze gemaakt  
SPEL_BEZIG -d-> PRG2_Speler_Zet_Figuur  

state WACHTEN {  
    WACHTEN : Wachten op start  
    WACHTEN : PLC actief, geen spel bezig  
}  

state START {  
    START : Startspel wordt geactiveerd  
    START : Willekeurige spelerselectie  
}  

state SPEL_BEZIG {  
    SPEL_BEZIG : Spel is gestart  
    SPEL_BEZIG : Eerste beurt begint  
}  

@enduml



```

## 2.2.State Diagram for Task 2: Player Turn

```plantuml

@startuml PRG2_Speler_Zet_Figuur

!theme spacelab-white
skinparam backgroundcolor transparent

[*] -right-> WACHT_OP_BEURT : Speler geselecteerd  
WACHT_OP_BEURT --> ZET_CONTROLEREN : Speler kiest vakje  
ZET_CONTROLEREN --> ZET_GEDAAN : Geldige zet gedaan  
ZET_CONTROLEREN -d-> WACHT_OP_BEURT : Ongeldige zet  
ZET_GEDAAN --> BEURT_WISSEL : Wissel speler  
BEURT_WISSEL --> PRG3_Winnaar_Check  

state WACHT_OP_BEURT {  
    WACHT_OP_BEURT : Wachten op speleractie  
}  

state ZET_CONTROLEREN {  
    ZET_CONTROLEREN : Controleren of zet geldig is  
}  

state ZET_GEDAAN {  
    ZET_GEDAAN : Zet is geplaatst  
}  

state BEURT_WISSEL {  
    BEURT_WISSEL : Wisselen van speler  
}  

@enduml



```



## 2.3.State Diagram for Task 3: Win or Draw Check

```plantuml

@startuml PRG3_Winnaar_Check

!theme spacelab-white
skinparam backgroundcolor transparent

[*] -right-> WINNAAR_CONTROLEREN : Zet geplaatst  
WINNAAR_CONTROLEREN --> SPELER_1_WIN : Speler 1 wint  
WINNAAR_CONTROLEREN --> SPELER_2_WIN : Speler 2 wint  
WINNAAR_CONTROLEREN --> GELIJK_SPEL : Gelijkspel  
WINNAAR_CONTROLEREN -d-> PRG2_Speler_Zet_Figuur : Geen winnaar, spel gaat door  
SPELER_1_WIN -d-> PRG4_Reset_Spel  
SPELER_2_WIN -d-> PRG4_Reset_Spel  
GELIJK_SPEL -d-> PRG4_Reset_Spel  

state WINNAAR_CONTROLEREN {  
    WINNAAR_CONTROLEREN : Check winstcondities  
}  

state SPELER_1_WIN {  
    SPELER_1_WIN : Speler 1 heeft gewonnen  
}  

state SPELER_2_WIN {  
    SPELER_2_WIN : Speler 2 heeft gewonnen  
}  

state GELIJK_SPEL {  
    GELIJK_SPEL : Geen vakjes meer over\nSpel eindigt in gelijkspel  
}  

@enduml

```


## 2.4.State Diagram for Task 4: Reset Game

```plantuml

@startuml PRG4_Reset_Spel

!theme spacelab-white
skinparam backgroundcolor transparent

[*] -right-> WACHT_OP_RESET : Spel is afgelopen  
WACHT_OP_RESET --> RESET_ACTIEF : Resetknop ingedrukt  
RESET_ACTIEF --> RESET_COMPLETE : Alle variabelen gereset  
RESET_COMPLETE --> PRG1_Start_Spel : Wachten op nieuwe start  

state WACHT_OP_RESET {  
    WACHT_OP_RESET : Wachten op resetknop  
}  

state RESET_ACTIEF {  
    RESET_ACTIEF : Alle variabelen terugzetten  
}  

state RESET_COMPLETE {  
    RESET_COMPLETE : Spel volledig gereset  
}  

@enduml


```


