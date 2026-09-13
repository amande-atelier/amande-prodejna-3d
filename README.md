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

## Osvětlovací okruhy (jističe)
Záložka **Okruhy** v editoru + tlačítko **💡 Okruhy** ve spodní liště (v tom režimu klik na svítidlo
ve scéně přepne celý jeho jistič). Okruhy dle Frederikova videa z 13. 9. 2026:

| Okruh | Co napájí |
|---|---|
| `SV1` | nika 1 · nika 2 |
| `AMBIENT` | prostřední světla (taky na SV1) |
| `SV34` | styling + předek prodejny |
| `SV5` | zázemí · chodba s botami · kuchyňka · WC |
| `NIKY` | osvětlení **uvnitř** nik — ze zásuvek, mimo hlavní okruhy |
| `KABINKY` | řízené, Sonoff už zaregistrovaný |
| `NEURCENO` | světlo nad pokladnou a nad nikou 3 — jistič nebyl řečen |

Okruh se drží na svítidle v poli `o`. Zhasnutí řeší jediné místo — `aktualizujSvitidlo()`.
**⚡ Rozdělit svítidla podle polohy** udělá hrubý první nástřel, pak se doladí po jednom.
`SONOFF` objekt je nachystaný na reálné spínání, ale `aktivni:false` — dokud se nedoplní
endpoint a ID zařízení, nic se neodesílá, jen se loguje do konzole.

## Technika — DŮLEŽITÉ pro další AI úpravy
`index.html` je **jeden samostatný soubor** — HTML + CSS + celý JS inline v `<script type="module">`.
Loader částí ani `VER` už neexistují: složky `parts/p1..p3` v repu sice zůstaly, ale **nikdo je nenačítá**
a jejich obsah je zastaralý (loader zmizel commitem `3218da8`). Neupravuj je — edituj `index.html`.
Kontrola syntaxe: vyříznout obsah `<script type="module">` do `.mjs` a `node --check`.

three.js 0.160 z CDN (importmap), `logo-data.js` = podsvícené logo.
Stav se serializuje jako JSON **v6**: `{v, cine, tracks, objekty, svetla, steny, podlaha, denni, gmult, okruhy}`.
localStorage klíč **`amande3d_v19`**. Starší uložené návrhy se načtou: chybějící okruhy se doplní
jako zapnuté a svítidla bez `o` spadnou do `NEURCENO`.

Deploy = commit do větve `main` (GitHub Pages, legacy build z rootu).
