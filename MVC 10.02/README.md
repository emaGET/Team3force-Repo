MVC Refactoring

1. toggleDarkMode(button)

FØR:

Funksjonen gjorde alt på én gang: endret knappen direkte, sjekket knappeteksten for å vite tilstanden, og hadde ingen variabel for å lagre om dark mode var på eller av.

PROBLEMER:

Funksjonen hadde ingen variabel i modellen for å holde oversikt over mørk modus-tilstanden: 
i stedet for å huske om tilstanden var lys eller mørk, sjekket den bare ikonet (en sol eller en måne) for å se om den var i lys eller mørk modus.

Deretter endret den HTML-koden direkte på skjermen i stedet for å kalle opp updateScreen().

En enkelt funksjon som i utgangspunktet endret data, bestemte hva som skulle gjøres på stedet og viste det på skjermen.

ETTER:

Jeg splitter funksjonen i tre deler. toggleDarkModeState() (MODEL) bytter bare verdien i model.isDarkMode.
handleToggleDarkMode() (CONTROLLER) er sjefen som sier "ok, endre 
verdien først, så oppdater skjermen".
createDarkModeButton() (VIEW) 
lager HTML-en for knappen og velger riktig ikon avhengig av tilstanden.

HVORFOR ER DET BEDRE?

Variabel model.isDarkMode alltid forteller hvis er dark mode på eller av.
Og hver funksjon gjør kun sin greie.
Når noe krasjer, det er enkelt å finne ut hvilken funksjon fungerer ikke.

2. updateView()

FØR:

Funksjonen var ikke det vi trengte. Vi trengte at den skulle oppdatere hele siden, i stedet for bare å endre teksten i ett enkelt element.

PROBLEM:
Vi hadde allerede updateScreen() som bygger hele siden på nytt, og updateView() lot ikke updateScreen() håndtere all visning/rendering (den manipulerte DOM direkte).

LØSNING:
Slettet hele funksjonen, og lot updateScreen() vise model.valgtMedlem direkte i HTML-en. Så endret jeg selvfølgelig findRandomMember() til å kalle updateScreen() i stedet for updateView().

HVORFOR ER DET BEDRE:
Nå er det bare én funksjon (updateScreen()) som håndterer all visning/rendering. Modellen lagrer data, og updateScreen() viser dem.