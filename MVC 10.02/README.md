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