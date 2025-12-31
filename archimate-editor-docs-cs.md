# ArchiMate Editor - Uživatelská příručka

Webový editor pro tvorbu a správu architektonických modelů podle standardu ArchiMate 3.2 s rozšířeními pro správu architektonických rozhodnutí (ADR), poznámek a úkolů.

## Online verze a stažení

- **Online verze:** https://mrt.site44.com/archimate-editor.html
- **GitHub:** https://github.com/michalradacz/archimate-editor

Na GitHubu najdete:
- Editor ke stažení jako jeden HTML soubor
- DokuWiki plugin pro integraci s wiki systémem
- Dokumentaci aplikace v češtině i angličtině
- JSON Schema pro validaci AJX formátu (`ajx-schema.json`)

---

## Obsah

1. [Úvod](#úvod)
2. [Formát AJX](#formát-ajx)
3. [Rozhraní editoru](#rozhraní-editoru)
4. [Správa modelu](#správa-modelu)
5. [Práce s prvky](#práce-s-prvky)
6. [Práce s vazbami](#práce-s-vazbami)
7. [Diagramy](#diagramy)
8. [Úkoly](#úkoly)
9. [Poznámky](#poznámky)
10. [Architektonická rozhodnutí (ADR)](#architektonická-rozhodnutí-adr)
11. [Generátor textu](#generátor-textu)
12. [Import a export](#import-a-export)
13. [Slučování modelů](#slučování-modelů)
14. [Hromadné operace s příznaky](#hromadné-operace-s-příznaky)
15. [DokuWiki plugin](#dokuwiki-plugin)
16. [Tipy a triky](#tipy-a-triky)
17. [Klávesové zkratky](#klávesové-zkratky)
18. [Referenční příručka ArchiMate](#referenční-příručka-archimate)

---

## Úvod

ArchiMate Editor je kompletní nástroj pro modelování podnikové architektury podle specifikace ArchiMate 3.2 od The Open Group. Editor běží přímo v prohlížeči bez nutnosti instalace a ukládá data lokálně do prohlížeče.

### Hlavní vlastnosti

- **ArchiMate 3.2** - podpora všech 60 typů prvků a 11 typů vazeb s kontrolou validity
- **Vícejazyčné rozhraní** - čeština a angličtina
- **Automatické ukládání** - data se ukládají do prohlížeče
- **Import/export** - formáty AJX (JSON) a ArchiMate Open Exchange XML
- **Slučování modelů** - import vybraných částí z jiného modelu
- **Úkoly** - evidence a sledování úkolů pro rozvoj architektury
- **Poznámky** - Markdown poznámky s verzováním
- **ADR (Architecture Decision Records)** - správa architektonických rozhodnutí
- **Generátor textu** - tvorba dokumentace z modelu pomocí šablon
- **Diagramy** - vizuální náhled s exportem do SVG
- **Hromadné operace** - práce s příznaky (tagy)
- **Přístupnost** - plně přístupné rozhraní pro odečítače obrazovky
- **DokuWiki integrace** - plugin pro spolupráci v týmu

---

## Formát AJX

**AJX (ArchiMate JSON eXchange)** je standardní formát pro výměnu ArchiMate modelů založený na JSON. Soubory mají příponu `.ajx`.

### Struktura AJX souboru

```json
{
  "exportDate": "2025-01-15T10:30:00.000Z",
  "archimateVersion": "3.2",
  "model": {
    "id": "id-model-001",
    "name": "Název modelu",
    "version": "1.0",
    "documentation": "Popis modelu",
    "dublinCore": { ... },
    "properties": []
  },
  "elements": [...],
  "relationships": [...],
  "diagrams": [...],
  "adr": [...],
  "notes": [...],
  "tasks": [...]
}
```

### Rozšíření AJX formátu

Editor používá standardní AJX formát pro ArchiMate modely a přidává tři rozšíření:

- **adr** - Architecture Decision Records (architektonická rozhodnutí)
- **notes** - Poznámky s Markdown podporou a verzováním
- **tasks** - Úkoly pro správu rozvoje architektury

Podrobná specifikace všech polí je v souboru `ajx-schema.json` (JSON Schema).

### Výhody formátu AJX

- Čitelný pro člověka i stroj
- Snadno verzovatelný v Git
- Jednoduchá integrace s jinými nástroji
- Validovatelný pomocí JSON Schema
- Kompaktnější než XML

---

## Rozhraní editoru

### Záhlaví

V záhlaví najdete:
- **Název modelu** - kliknutím přejdete na záložku Model
- **Verze modelu** - zobrazuje aktuální verzi
- **Statistiky** - počet prvků, vazeb, diagramů a vrstev
- **Přepínač jazyka** - CZ/EN

### Záložky

Editor je rozdělen do devíti hlavních záložek:

1. **Model** - metadata a nastavení modelu
2. **Prvky** - správa architektonických prvků
3. **Vazby** - správa vztahů mezi prvky
4. **Diagramy** - tvorba a správa pohledů
5. **Úkoly** - evidence a sledování úkolů
6. **Poznámky** - textové poznámky s Markdown
7. **ADR** - architektonická rozhodnutí
8. **Nástroje** - generátor textu a hromadné operace
9. **Export/Import** - výměna dat s jinými systémy
10. **Reference** - přehled ArchiMate specifikace

---

## Správa modelu

### Základní informace

- **ID modelu** - unikátní identifikátor (automaticky generován)
- **Název modelu** - zobrazuje se v záhlaví
- **Verze** - verzování modelu
- **Dokumentace** - podrobný popis modelu (podporuje Markdown)

### Dublin Core metadata

Standardizovaná metadata podle ISO 15836:

| Pole | Popis |
|------|-------|
| Tvůrce | Autor nebo odpovědná osoba |
| Vydavatel | Organizace zodpovědná za publikaci |
| Datum | Datum vytvoření nebo publikace |
| Jazyk | Jazyk obsahu (cs, en, de...) |
| Práva | Licenční informace |
| Předmět | Téma nebo klíčová slova |
| Popis | Stručný popis obsahu |

### Vlastní vlastnosti

Můžete přidat libovolný počet vlastních vlastností ve formátu klíč-hodnota. Použijte tlačítko **Přidat vlastnost** a vyplňte název a hodnotu.

---

## Práce s prvky

### Vytvoření nového prvku

1. Vyberte **vrstvu** (Strategy, Business, Application...)
2. Vyberte **typ prvku** - seznam se filtruje podle vrstvy
3. Vyplňte **název** prvku
4. Volitelně přidejte:
   - **Stereotyp** - rozšíření typu (např. "microservice")
   - **Určuje** - odkaz na zákon, standard nebo řídicí dokument
   - **Příznaky** - tagy oddělené čárkou pro kategorizaci
   - **Popis** - podrobná dokumentace (podporuje Markdown)
5. Klikněte **Uložit prvek**

### Automatické generování ID

ID prvku se generuje automaticky z typu a názvu:
- `BusinessProcess` + "Zpracování objednávky" → `bp-zpracovani-objednavky`

### Operace s prvky

| Ikona | Akce | Popis |
|-------|------|-------|
| ✏️ | Editace | Otevře prvek k úpravě |
| 📋 | Duplikování | Vytvoří kopii s novým ID |
| 🗑️ | Smazání | Smaže prvek i jeho vazby |

### Filtrování prvků

Nad tabulkou jsou filtry:
- **Vrstva** - filtr podle vrstvy
- **Typ** - filtr podle typu prvku
- **Stereotyp** - filtr podle stereotypu
- **Příznaky** - filtr podle tagů (včetně "bez příznaků")
- **Diagram** - filtr podle příslušnosti k diagramu
- **Hledat** - fulltextové vyhledávání

Tlačítko **Zrušit filtry** vymaže všechny filtry.

### Řazení a sloupce

- **Řazení** - kliknutím na záhlaví sloupce
- **Skrývání sloupců** - tlačítko "Sloupce" pro výběr zobrazených sloupců

---

## Práce s vazbami

### Kaskádový výběr

Formulář pro vazby používá inteligentní kaskádový výběr:

1. **Vrstva zdroje** → filtruje typy zdrojových prvků
2. **Typ zdroje** → filtruje konkrétní zdrojové prvky
3. **Zdrojový prvek** → vyberete konkrétní prvek
4. **Vrstva cíle** → filtruje typy cílových prvků
5. **Typ cíle** → filtruje konkrétní cílové prvky
6. **Cílový prvek** → vyberete konkrétní prvek
7. **Typ vazby** → zobrazí pouze povolené typy podle specifikace

### Kontrola validity vazeb

Editor automaticky kontroluje, zda je vazba povolena podle ArchiMate 3.2. Nepovolené kombinace nejsou v nabídce.

### Náhled tvrzení

Po výběru zdroje, cíle a typu vazby se zobrazí náhled ve formě věty:
> "Zdrojový prvek **poskytuje** Cílovému prvku"

### Filtrování vazeb

- **Zdrojový prvek** - filtr podle zdroje
- **Cílový prvek** - filtr podle cíle
- **Typ vazby** - filtr podle typu
- **Příznaky** - filtr podle tagů
- **Diagram** - filtr podle příslušnosti k diagramu
- **Hledat** - fulltextové vyhledávání

### Rychlý filtr z tabulky prvků

V tabulce prvků můžete kliknout na číslo vazeb a přejít na filtrovaný seznam vazeb pro daný prvek.

---

## Diagramy

Diagramy (pohledy) umožňují organizovat prvky do logických skupin a vizualizovat jejich vztahy.

### Vytvoření diagramu

1. Zadejte **název diagramu**
2. Volitelně přidejte **popis**
3. Klikněte **Vytvořit diagram**

### Editor diagramu

Po kliknutí na **Otevřít** se zobrazí editor s třemi podzáložkami:

#### Prvky diagramu

- Přidávání prvků pomocí kaskádového výběru (vrstva → typ → prvek)
- Seznam prvků v diagramu s možností odebrání
- Prvky lze přidávat i odebírat

#### Vazby diagramu

- Automaticky zobrazuje vazby mezi prvky v diagramu
- Pouze pro čtení - vazby se spravují v záložce Vazby

#### Náhled

Vizuální náhled diagramu:
- Prvky jsou zobrazeny jako obdélníky s barvou podle vrstvy
- Vazby jsou zobrazeny jako čáry s odpovídajícími značkami
- Tlačítko **Stáhnout SVG** exportuje náhled jako vektorový obrázek

---

## Úkoly

Systém úkolů umožňuje evidovat a sledovat práci potřebnou pro rozvoj architektury s kompletní auditní stopou.

### Vytvoření úkolu

1. Klikněte **+ Nový úkol**
2. Vyplňte povinné pole **Název**
3. Nastavte **Stav** a **Prioritu**
4. Volitelně vyplňte:
   - **Číslo** - automaticky generováno
   - **Řešitel** - kdo úkol řeší
   - **Zadavatel** - kdo úkol založil
   - **Termín** - datum dokončení
   - **Příznaky** - tagy pro kategorizaci
   - **Popis úkolu** - detailní popis (Markdown)
   - **Aktuální stav** - poznámky k průběhu řešení
   - **Propojené prvky/vazby** - vazba na model
5. Klikněte **Uložit**

### Stavy úkolu

| Stav | Ikona | Popis |
|------|-------|-------|
| Nový | ⚪ | Nově založený úkol |
| Probíhá | 🔵 | Aktivně řešený úkol |
| Blokováno | 🔴 | Úkol je blokován |
| Ke kontrole | 🟡 | Čeká na kontrolu/schválení |
| Hotovo | 🟢 | Dokončený úkol |
| Zrušeno | ⚫ | Zrušený úkol |

### Priority

| Priorita | Barva | Popis |
|----------|-------|-------|
| Kritická | 🔴 červená | Nejvyšší priorita |
| Vysoká | 🟠 oranžová | Vysoká priorita |
| Střední | 🟡 žlutá | Běžná priorita |
| Nízká | 🟢 zelená | Nízká priorita |

### Filtrování úkolů

- **Stav** - filtr podle stavu
- **Priorita** - filtr podle priority
- **Řešitel** - filtr podle přiřazeného řešitele
- **Hledat** - fulltextové vyhledávání

### Historie stavů

Každá změna stavu nebo aktuálního stavu se zaznamenává do historie včetně:
- Datum a čas změny
- Kdo změnu provedl
- Popis aktuálního stavu v době změny

### Export úkolů

- **📄 Uložit jako Markdown** - stáhne jednotlivý úkol jako .md soubor
- **📋 Kopírovat Markdown** - zkopíruje do schránky
- **📦 Exportovat všechny úkoly** - stáhne všechny úkoly jako jeden soubor

### Propojení s modelem

Úkoly lze propojit s prvky a vazbami modelu pomocí multi-selectu. V náhledu úkolu jsou propojené položky klikatelné.

### Indikátor zpoždění

Úkoly po termínu jsou v tabulce zvýrazněny červeně s ikonou ⚠️.

---

## Poznámky

Systém poznámek umožňuje vytvářet dokumentaci s podporou Markdown a verzování.

### Vytvoření poznámky

1. Klikněte **+ Nová poznámka**
2. Vyplňte **Název** a **Autor**
3. Volitelně přidejte **Příznaky** (tagy)
4. Napište **Obsah** (podporuje Markdown)
5. Propojte s **prvky** a **vazbami** modelu
6. Klikněte **Uložit**

### Verzování

- Každé uložení vytvoří novou verzi
- V editoru lze zobrazit historii verzí
- Lze obnovit předchozí verzi

### Náhled poznámky

- Kliknutím na název otevřete náhled
- Markdown se renderuje do formátovaného HTML
- Propojené prvky/vazby jsou klikatelné

### Kopírování obsahu

- **📋** v tabulce - rychlé kopírování obsahu do schránky
- **📋 Kopírovat** v náhledu - kopírování s potvrzením

---

## Architektonická rozhodnutí (ADR)

ADR (Architecture Decision Records) slouží k evidenci a sledování architektonických rozhodnutí s kompletním životním cyklem.

### Vytvoření ADR

1. Klikněte **+ Nové ADR**
2. Vyplňte povinné pole **Název**
3. Nastavte **Stav** rozhodnutí
4. Volitelně vyplňte:
   - **Číslo** - automaticky generováno (podporuje alfanumerické)
   - **Autor**, **Schvalovatel**, **Rozhodovatelé**
   - **Kontext** - pozadí a důvod rozhodnutí (Markdown)
   - **Rozhodnutí** - samotné rozhodnutí (Markdown)
   - **Důsledky** - dopady rozhodnutí (Markdown)
   - **Alternativy** - zvažované možnosti
   - **Implementace** - stav a termíny implementace
   - **Související ADR** - nahrazuje, je nahrazeno, souvisí
   - **Propojené prvky/vazby** - vazba na model
   - **Odkazy** - externí URL reference
5. Klikněte **Uložit**

### Stavy ADR

| Stav | Ikona | Popis |
|------|-------|-------|
| Rozpracováno | ⚪ | Příprava rozhodnutí |
| Navrženo | 🔵 | Čeká na schválení |
| Projednáváno | 💬 | Probíhá diskuze |
| Vráceno | 🔙 | Vráceno k přepracování |
| Schváleno | 🟢 | Schválené rozhodnutí |
| Zamítnuto | 🔴 | Zamítnuté rozhodnutí |
| Aktualizováno | 🔄 | Rozhodnutí bylo aktualizováno |
| Implementováno | 🟣 | Rozhodnutí je implementováno |
| Sledováno | 👁️ | Rozhodnutí je sledováno |
| Zastaralé | 🟠 | Rozhodnutí je zastaralé |
| Nahrazeno | ⚫ | Nahrazeno jiným ADR |
| Uzavřeno | 🔒 | Uzavřené rozhodnutí |

### Alternativy a výběr

- Přidejte alternativy s názvem a popisem
- Vyberte zvolenou alternativu z rozbalovacího seznamu
- Popište důvod výběru

### Historie stavů

Každá změna stavu se automaticky zaznamenává včetně data a autora.

### Export ADR

- **📄 Uložit jako Markdown** - stáhne jednotlivé ADR
- **📋 Kopírovat Markdown** - zkopíruje do schránky
- **📦 Exportovat všechny ADR** - stáhne všechna ADR jako jeden soubor

---

## Generátor textu

Generátor vytváří textové výstupy z modelu pomocí šablon s placeholdery.

### Zdroje dat

Generátor umí generovat text z:
- **Prvky** - aktuální seznam prvků (respektuje filtry)
- **Vazby** - aktuální seznam vazeb (respektuje filtry)
- **Úkoly** - všechny úkoly
- **Poznámky** - všechny poznámky
- **ADR** - všechna architektonická rozhodnutí

### Šablony

Zadejte šablonu s placeholdery ve složených závorkách:
```
{Název} je {Typ} ve vrstvě {Vrstva}.
```

### Dostupné placeholdery

#### Pro prvky
- `{ID}`, `{Název}`, `{Typ}`, `{Vrstva}`
- `{Stereotyp}`, `{Určuje}`, `{Příznaky}`, `{Popis}`

#### Pro vazby
- `{ID}`, `{Typ}`, `{Název}`, `{Popis}`, `{Příznaky}`, `{Statement}`
- Zdroj: `{Zdroj}`, `{ZdrojID}`, `{ZdrojVrstva}`, `{ZdrojTyp}`, `{ZdrojStereotyp}`, `{ZdrojUrčuje}`, `{ZdrojPříznaky}`, `{ZdrojPopis}`
- Cíl: `{Cíl}`, `{CílID}`, `{CílVrstva}`, `{CílTyp}`, `{CílStereotyp}`, `{CílUrčuje}`, `{CílPříznaky}`, `{CílPopis}`

#### Pro úkoly
- `{ID}`, `{Číslo}`, `{Název}`, `{Stav}`, `{Priorita}`
- `{Řešitel}`, `{Zadavatel}`, `{Termín}`, `{Příznaky}`
- `{Popis}`, `{AktuálníStav}`, `{Vytvořeno}`, `{Aktualizováno}`

#### Pro poznámky
- `{ID}`, `{Název}`, `{Autor}`, `{Příznaky}`
- `{Obsah}`, `{Vytvořeno}`, `{Aktualizováno}`, `{PočetVerzí}`

#### Pro ADR
- `{ID}`, `{Číslo}`, `{Název}`, `{Stav}`
- `{Autor}`, `{Schvalovatel}`, `{Datum}`, `{Příznaky}`
- `{Kontext}`, `{Rozhodnutí}`, `{Důsledky}`
- `{PočetAlternativ}`, `{VybranáAlternativa}`

### Možnosti

- **Přeskočit prázdné** - vynechá položky kde by placeholder byl prázdný

---

## Import a export

### Export

| Formát | Popis |
|--------|-------|
| **Export AJX** | Stažení modelu ve formátu AJX (JSON) |
| **Kopírovat AJX** | Zkopíruje AJX data do schránky |
| **Export XML** | ArchiMate Open Exchange formát |
| **Export CSV** | Prvky a vazby jako CSV soubory |

### Import

Podporované formáty:
- **AJX** - ArchiMate JSON eXchange (.ajx)
- **XML** - ArchiMate Open Exchange (.xml)

#### Možnosti importu

1. **Ze souboru** - tlačítko "Vyberte soubor"
2. **Vložením** - vložte data do textového pole
3. **Ze schránky** - tlačítko "Vložit ze schránky"
4. **Drag & Drop** - přetažením souboru na stránku

---

## Slučování modelů

Sloučení umožňuje importovat vybrané části z jiného modelu.

### Strategie sloučení

| Strategie | Popis |
|-----------|-------|
| Ponechat stávající | Při kolizi ID zachová původní |
| Přepsat novými | Při kolizi ID nahradí novým |
| Ručně vybrat | Umožní vybrat konkrétní položky |

### Ruční výběr

Při volbě "Ručně vybrat":
1. Načtěte soubor ke sloučení
2. Přepínejte mezi záložkami **Prvky**, **Vazby** a **Diagramy**
3. Zaškrtněte položky k importu
4. Klikněte **Sloučit modely**

### Označení importovaných položek

Importované položky dostanou automaticky příznak `Import z: [název zdrojového modelu]`.

---

## Hromadné operace s příznaky

### Dostupné operace

| Operace | Popis |
|---------|-------|
| Přidat příznak | Přidá tag ke všem vybraným položkám |
| Odebrat příznak | Odebere tag ze vybraných položek |
| Nahradit příznak | Nahradí jeden tag jiným |

### Výběr položek

- Zaškrtněte položky pro operaci
- **Vybrat vše** / **Odebrat vše**
- **Vybrat aktuálně filtrované** - vybere položky odpovídající aktivním filtrům

---

## DokuWiki plugin

Editor lze integrovat s DokuWiki pomocí přiloženého pluginu.

### Instalace

1. Rozbalte `archimateeditor.zip` do `lib/plugins/`
2. Plugin se automaticky aktivuje

### Použití

Vložte do wiki stránky:
```
<archimate instance="nazev-instance">
</archimate>
```

### Funkce

- Editor se otevírá v popup okně
- Tlačítko **Uložit do Wiki** ukládá přímo do wiki stránky
- Data se přenášejí pomocí postMessage API
- Podpora více instancí na jedné stránce

---

## Tipy a triky

### Automatické ukládání

Model se automaticky ukládá do prohlížeče po každé změně.

### Našeptávání

- **Stereotypy** - nabízí dříve použité stereotypy
- **Příznaky** - nabízí existující tagy z celého modelu (včetně ADR, poznámek a úkolů)
- **Názvy vazeb** - nabízí dříve použité názvy

### Propojování položek

Úkoly, poznámky i ADR lze propojit s prvky a vazbami modelu. Propojené položky jsou v náhledech klikatelné.

### Sdílené příznaky

Příznaky (tagy) jsou sdílené mezi prvky, vazbami, úkoly, poznámkami i ADR. Umožňuje to snadné propojování souvisejících položek.

### Markdown podpora

Markdown je podporován v:
- Dokumentaci modelu
- Popisu prvků a vazeb
- ADR (kontext, rozhodnutí, důsledky, alternativy)
- Poznámkách
- Popisu a stavu úkolů

### Zálohování

Pravidelně exportujte model do AJX souboru. Data v prohlížeči mohou být smazána při vyčištění historie.

---

## Klávesové zkratky

| Zkratka | Akce |
|---------|------|
| Tab | Přechod mezi poli formuláře |
| Enter | Potvrzení formuláře |
| Escape | Zavření modálního okna |
| Ctrl+S | Uložení do Wiki (v DokuWiki režimu) |

---

## Referenční příručka ArchiMate

### Vrstvy

| Vrstva | Barva | Popis |
|--------|-------|-------|
| Strategy | Hnědá | Strategické prvky - zdroje, schopnosti |
| Business | Zlatá | Byznysové prvky - aktéři, procesy, služby |
| Application | Modrá | Aplikační prvky - komponenty, služby, data |
| Technology | Zelená | Technologické prvky - uzly, zařízení |
| Physical | Tmavě zelená | Fyzické prvky - vybavení, budovy |
| Implementation | Fialová | Implementační prvky - balíčky, dodávky |
| Motivation | Červená | Motivační prvky - stakeholdeři, cíle |
| Composite | Šedá | Složené prvky - lokace, seskupení |

### Typy vazeb

| Typ | Kategorie | Popis |
|-----|-----------|-------|
| Composition | Strukturální | Prvek se skládá z jiných prvků |
| Aggregation | Strukturální | Prvek sdružuje jiné prvky |
| Assignment | Strukturální | Přiřazení aktivního prvku k chování |
| Realization | Strukturální | Prvek realizuje jiný prvek |
| Serving | Závislostní | Prvek poskytuje funkcionalitu |
| Access | Závislostní | Prvek přistupuje k datům |
| Influence | Závislostní | Prvek ovlivňuje jiný prvek |
| Triggering | Dynamická | Prvek spouští jiný prvek |
| Flow | Dynamická | Tok informací nebo materiálu |
| Specialization | Ostatní | Prvek je specializací jiného |
| Association | Ostatní | Nespecifikovaný vztah |

---

## Podpora

Editor je open-source nástroj dostupný na GitHubu.

- **Online verze:** https://mrt.site44.com/archimate-editor.html
- **GitHub repozitář:** https://github.com/michalradacz/archimate-editor
- **Hlášení chyb:** https://github.com/michalradacz/archimate-editor/issues

### Systémové požadavky

- Moderní webový prohlížeč (Chrome, Firefox, Safari, Edge)
- JavaScript musí být povolen
- Pro ukládání je potřeba localStorage

### Známá omezení

- Data jsou ukládána lokálně v prohlížeči
- Při vyčištění dat prohlížeče se model smaže
- Doporučeno pravidelně exportovat zálohy

---

*Verze dokumentace: 2.0*
*ArchiMate® je registrovaná ochranná známka The Open Group.*
