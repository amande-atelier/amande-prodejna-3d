# Amande — 3D model nové prodejny (interaktivní editor)

Živě: https://amande-atelier.github.io/amande-prodejna-3d/

Prostor po KB bance (~129 m², 8,9 × 15,6 m + výklenek), editor vybavení, světel SG20 E 48V, podlah a stěn.

## Ovládání editoru (tlačítko 🛠 Editor)
- **Objekty**: klik na položku v katalogu → klik do prostoru. Tažení = přesun, R = otočit, Del = smazat, Ctrl+D = duplikát, šipky = posun po 5 cm (Shift = 25 cm).
- **Výběr objektu**: přesné X/Z v metrech, jemné otočení po 5°, u regálů/gondol/štendrů/pultů/kabinek/nik posuvník šířky.
- **Zpět/Vpřed**: ↶ ↷ v hlavičce editoru, Ctrl+Z / Ctrl+Shift+Z (60 kroků).
- **📏 Měření**: 2 kliknutí na podlahu = vzdálenost v metrech (Esc konec).
- **📸 Foto**: uloží PNG snímek aktuálního pohledu.
- **Podlaha**: presety + malování zón 0,5 m.
- **Světla**: tracky (podélně/příčně), svítidla dle katalogu SG20 E, stmívání, CCT, míření.
- **Stěny**: výlohy a dveře na stěnách + barva výmalby (přebarví i vyzděné stěnky).
- **Soubor**: pojmenované návrhy (localStorage), export/import JSON.

Vše se průběžně ukládá do prohlížeče (localStorage, klíč `amande3d_v17`).

## Technika
Jeden soubor `index.html` (three.js 0.160 z CDN, ES module). `logo-data.js` = podsvícené logo.
Stav se serializuje jako JSON v6: `{v, cine, tracks, objekty, svetla, steny, podlaha, denni, gmult, stenaC}`.
