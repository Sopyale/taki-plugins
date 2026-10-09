# taki-plugins – telepítés és használat (weboldal-projekt)

Három eszköz, három forrás:

| Eszköz | Marketplace URL (Plugins → Add marketplace) | Plugin |
|---|---|---|
| Ponytail | már fent van | ponytail |
| Graphify | `Sopyale/taki-plugins` (ez a repó) | graphify |
| Agent Skills | `anthropics/skills` | example-skills (+ igény szerint document-skills) |

## 1. Telepítés

### Graphify
1. Előfeltétel (egyszer, már megvan): `uv tool install graphifyy` – a skill ezt a parancssori eszközt hívja.
2. Töltsd fel ezt a mappát egy új GitHub repóba (`taki-plugins`).
3. Claude → Settings → Plugins → Add → Add marketplace → `Sopyale/taki-plugins` → Sync.
4. Discover fülön: **graphify** → Install.
5. A korábbi kézi telepítés duplikátum lenne – töröld: `graphify uninstall` (PowerShell), vagy hagyd és ne telepítsd a plugint.

### Agent Skills (Anthropic hivatalos)
1. Add marketplace → `anthropics/skills` → Sync. (Ez a repó már marketplace, nem kell becsomagolni.)
2. Telepítsd az **example-skills** plugint. Weboldalhoz ebből ezek számítanak:
   - `frontend-design` – egyedi, nem sablonszerű dizájn
   - `webapp-testing` – az oldal kipróbálása böngészőben (Playwright)
   - `theme-factory` – színek/betűk témákba szervezve
   - `brand-guidelines` – arculat betartása
3. A **document-skills** (Word/Excel/PDF/PowerPoint) csak akkor kell, ha dokumentumokat is gyártasz.

## 2. Napi használat a weboldal-projektben

Nyisd meg a projektmappát (Claude Code vagy a desktop app „Add folder”), aztán:

**Első alkalommal – térkép a projektről**
```
/graphify .
```
→ `graphify-out/graph.html` (kattintható gráf), `GRAPH_REPORT.md`, `graph.json`.
Tedd a `.gitignore`-ba: `graphify-out/`

**Kérdezés a kódról (keresgélés helyett)**
```
/graphify query "hol töltődik be a navigációs menü?"
/graphify path "Header" "contact form"
/graphify explain "ProductCard"
```

**Változtatás után frissítés**
```
/graphify . --update
```
vagy egyszer `graphify hook install` → minden commit után magától frissül.

**Új oldal / szekció építése** – csak kérd, a skillek maguktól bekapcsolnak:
> „Készíts egy árazás szekciót a főoldalra, a meglévő stílushoz illően.”
→ frontend-design tervez, ponytail a legkisebb működő változtatást írja.

**Tesztelés**
> „Nyisd meg az oldalt helyben és nézd meg, működik-e a kapcsolati űrlap mobilon.”
→ webapp-testing.

**Átnézés élesítés előtt**
```
/ponytail-review        # az utolsó módosítás ellenőrzése
/ponytail-audit         # az egész projekt: hibák, biztonság, felesleges kód
```

## 3. Ajánlott sorrend egy feladatnál
1. `/graphify . --update` – friss térkép
2. Kérés megfogalmazása (pl. új szekció)
3. „Teszteld le” – webapp-testing
4. `/ponytail-review`
5. Commit

---
A graphify skill az eredeti Graphify-Labs/graphify (v0.9.82, Windows-változat) változatlan másolata, Apache-2.0/MIT licenc alatt (lásd `plugins/graphify/LICENSE*`).
