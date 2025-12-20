# ArchiMate Editor - Uživatelská příručka

Webový editor pro tvorbu a správu architektonických modelů podle standardu ArchiMate 3.2.

## Online verze a stažení

- **Online verze:** https://mrt.site44.com/archimate-editor.html
- **GitHub:** https://github.com/michalradacz/archimate-editor

Na GitHubu najdete:
- Editor ke stažení jako jeden HTML soubor
- Dokumentaci aplikace
- JSON Schema pro validaci AJX formátu

## Obsah

1. [Úvod](#úvod)
2. [Formát AJX](#formát-ajx)
3. [Rozhraní editoru](#rozhraní-editoru)
4. [Správa modelu](#správa-modelu)
5. [Práce s prvky](#práce-s-prvky)
6. [Práce s vazbami](#práce-s-vazbami)
7. [Diagramy](#diagramy)
8. [Generátor textu](#generátor-textu)
9. [Import a export](#import-a-export)
10. [Slučování modelů](#slučování-modelů)
11. [Hromadné operace s příznaky](#hromadné-operace-s-příznaky)
12. [Tipy a triky](#tipy-a-triky)
13. [Klávesové zkratky](#klávesové-zkratky)
14. [Referenční příručka ArchiMate](#referenční-příručka-archimate)

---

## Úvod

ArchiMate Editor je kompletní nástroj pro modelování podnikové architektury podle specifikace ArchiMate 3.2 od The Open Group. Editor běží přímo v prohlížeči bez nutnosti instalace a ukládá data lokálně do prohlížeče.

### Hlavní vlastnosti

- Podpora všech 60 typů prvků ArchiMate 3.2
- Všech 11 typů vazeb s kontrolou validity podle specifikace
- Vícejazyčné rozhraní (čeština, angličtina)
- Automatické ukládání do prohlížeče
- Import/export ve formátech AJX a ArchiMate Open Exchange XML
- Slučování modelů s možností ručního výběru
- Generátor textových popisů z modelu
- Hromadné operace s příznaky (tagy)
- Vizuální náhled diagramů s exportem do SVG
- Plně přístupné rozhraní pro odečítače obrazovky

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
    "dublinCore": {
      "creator": "Autor",
      "publisher": "Vydavatel",
      "date": "2025-01-15",
      "language": "cs",
      "rights": "Licence",
      "subject": "Téma",
      "description": "Popis"
    },
    "properties": []
  },
  "elements": [...],
  "relationships": [...],
  "diagrams": [...]
}
```

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
- **Statistiky** - počet prvků, vazeb a diagramů
- **Přepínač jazyka** - CZ/EN

### Záložky

Editor je rozdělen do šesti hlavních záložek:

1. **Model** - metadata a nastavení modelu
2. **Prvky** - správa architektonických prvků
3. **Vazby** - správa vztahů mezi prvky
4. **Diagramy** - tvorba a správa pohledů
5. **Generátor** - generování textových výstupů
6. **Export/Import** - výměna dat s jinými systémy

---

## Správa modelu

### Základní informace

- **ID modelu** - unikátní identifikátor (automaticky generován)
- **Název modelu** - zobrazuje se v záhlaví
- **Verze** - verzování modelu
- **Dokumentace** - podrobný popis modelu

### Dublin Core metadata

Standardizovaná metadata podle ISO 15836:

- **Tvůrce** - autor nebo odpovědná osoba
- **Vydavatel** - organizace zodpovědná za publikaci
- **Datum** - datum vytvoření nebo publikace
- **Jazyk** - jazyk obsahu (cs, en, de...)
- **Práva** - licenční informace
- **Předmět** - téma nebo klíčová slova
- **Popis** - stručný popis obsahu

### Vlastní vlastnosti

Můžete přidat libovolný počet vlastních vlastností ve formátu klíč-hodnota. Použijte tlačítko **Přidat vlastnost** a vyplňte název a hodnotu.

### Tlačítka

- **Uložit metadata** - uloží změny
- **Reset** - obnoví výchozí hodnoty

---

## Práce s prvky

### Vytvoření nového prvku

1. Vyberte **vrstvu** (Strategy, Business, Application...)
2. Vyberte **typ prvku** - seznam se filtruje podle vrstvy
3. Vyplňte **název** prvku
4. Volitelně přidejte:
   - **Stereotyp** - rozšíření typu (např. "microservice" pro ApplicationComponent)
   - **Určuje** - odkaz na zákon, standard nebo řídicí dokument
   - **Příznaky** - tagy oddělené čárkou pro kategorizaci
   - **Popis** - podrobná dokumentace
5. Klikněte **Uložit prvek**

### Automatické generování ID

ID prvku se generuje automaticky z typu a názvu:
- `BusinessProcess` + "Zpracování objednávky" → `bp-zpracovani-objednavky`

### Editace prvku

- Klikněte na ikonu **tužky** v tabulce
- Formulář se předvyplní hodnotami prvku
- Po úpravách klikněte **Uložit prvek**

### Duplikování prvku

- Klikněte na ikonu **kopírování** v tabulce
- Vytvoří se kopie s novým ID (přidá se suffix `-copy`)
- Kopie se otevře k editaci

### Smazání prvku

- Klikněte na ikonu **koše** v tabulce
- Potvrďte smazání
- **Pozor:** Smažou se i všechny vazby spojené s prvkem

### Filtrování prvků

Nad tabulkou jsou filtry:
- **Vrstva** - filtr podle vrstvy
- **Typ** - filtr podle typu prvku
- **Stereotyp** - filtr podle stereotypu
- **Příznaky** - filtr podle tagů
- **Hledat** - fulltextové vyhledávání

Tlačítko **Zrušit filtry** vymaže všechny filtry.

### Řazení tabulky

Kliknutím na záhlaví sloupce seřadíte tabulku:
- První klik: vzestupně (A→Z)
- Druhý klik: sestupně (Z→A)

### Skrývání sloupců

Klikněte na **Sloupce** a vyberte které sloupce chcete zobrazit. Nastavení se ukládá.

### Nápověda k typům

Po výběru typu prvku se zobrazí stručný popis podle specifikace ArchiMate.

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

Editor automaticky kontroluje, zda je vazba povolena podle ArchiMate 3.2:
- Povolené vazby jsou zobrazeny zeleně
- Nepovolené kombinace nejsou v seznamu

### Náhled tvrzení

Po výběru zdroje, cíle a typu vazby se zobrazí náhled ve formě věty:
> "Zdrojový prvek **poskytuje** Cílovému prvku"

### Automatické ID vazby

ID vazby se generuje automaticky jako kombinace ID zdroje a cíle.

### Volitelné atributy

- **Název vazby** - volitelný popis vazby
- **Popis** - podrobná dokumentace
- **Příznaky** - tagy pro kategorizaci

### Filtrování vazeb

- **Zdrojový prvek** - filtr podle zdroje
- **Cílový prvek** - filtr podle cíle
- **Typ vazby** - filtr podle typu
- **Název** - filtr podle názvu
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

### Správa diagramů

- **Upravit popis** - změna dokumentace diagramu
- **Smazat** - odstranění diagramu (prvky zůstanou)

---

## Generátor textu

Generátor vytváří textové výstupy z modelu pomocí šablon s placeholdery.

### Šablony

Zadejte šablonu s placeholdery v hranatých závorkách:
```
[název] je [typ] ve vrstvě [vrstva].
```

### Dostupné placeholdery

#### Pro prvky
- `[id]` - identifikátor prvku
- `[název]` - název prvku
- `[typ]` - typ prvku
- `[vrstva]` - vrstva prvku
- `[stereotyp]` - stereotyp
- `[určuje]` - určující dokument
- `[příznaky]` - příznaky/tagy
- `[popis]` - dokumentace

#### Pro vazby
- `[id]` - identifikátor vazby
- `[typ]` - typ vazby
- `[zdroj]` - název zdrojového prvku
- `[cíl]` - název cílového prvku
- `[název]` - název vazby
- `[popis]` - dokumentace vazby
- `[příznaky]` - příznaky vazby
- `[sloveso]` - sloveso vazby (poskytuje, realizuje...)

### Filtry

Můžete omezit generování na:
- Vybranou **vrstvu**
- Vybraný **typ prvku/vazby**
- Vybraný **stereotyp**
- Vybrané **příznaky**

### Možnosti

- **Přeskočit prázdné** - vynechá položky kde by placeholder byl prázdný
- **Generovat pro prvky/vazby** - přepínač zdroje dat

### Výstup

- Vygenerovaný text lze zkopírovat do schránky
- Tlačítko **Vymazat** smaže výstup

---

## Import a export

### Export AJX

Klikněte **Export AJX** pro stažení modelu ve formátu AJX (JSON). Soubor bude mít název podle modelu s příponou `.ajx`.

### Kopírovat AJX

Zkopíruje AJX data do schránky pro vložení jinam.

### Export XML

Exportuje model ve formátu **ArchiMate Open Exchange** (standardní XML formát pro výměnu mezi nástroji).

### Export CSV

Exportuje prvky a vazby jako CSV soubory pro import do tabulkových procesorů.

### Import

Podporované formáty:
- **AJX** - ArchiMate JSON eXchange (.ajx)
- **XML** - ArchiMate Open Exchange (.xml)

#### Import ze souboru

1. Klikněte **Vyberte soubor**
2. Vyberte .ajx nebo .xml soubor
3. Klikněte **Importovat**

#### Import vložením

1. Vložte AJX nebo XML data do textového pole
2. Klikněte **Importovat**

#### Vložit ze schránky

Tlačítko **Vložit ze schránky** automaticky vloží obsah schránky. Na mobilních zařízeních nebo při nedostupnosti Clipboard API se zobrazí modální okno pro ruční vložení.

### Smazat vše

Tlačítko **Smazat vše** vymaže celý model včetně všech prvků, vazeb a diagramů.

---

## Slučování modelů

Sloučení umožňuje importovat vybrané části z jiného modelu do aktuálního.

### Strategie sloučení

- **Ponechat stávající** - při kolizi ID zachová původní prvek
- **Přepsat novými** - při kolizi ID nahradí novým prvkem
- **Ručně vybrat** - umožní vybrat konkrétní prvky a vazby

### Ruční výběr

Při volbě "Ručně vybrat":

1. Načtěte soubor ke sloučení
2. Přepínejte mezi záložkami **Prvky** a **Vazby**
3. Použijte **vyhledávání** pro rychlé nalezení
4. Zaškrtněte položky k importu
5. Tlačítka **Vybrat vše** / **Odebrat vše** pracují s viditelnými položkami

#### Výběr podle vazeb

1. Přepněte na záložku **Vazby**
2. Všechny prvky se automaticky odškrtnou
3. Zaškrtněte požadované vazby
4. Zdrojové a cílové prvky se automaticky vyberou
5. Klikněte **Sloučit modely**

#### Výběr podle prvků

1. Zůstaňte na záložce **Prvky**
2. Odškrtněte prvky které nechcete
3. Vazby mezi vybranými prvky se importují automaticky
4. Klikněte **Sloučit modely**

### Označení importovaných položek

Importované prvky a vazby dostanou automaticky příznak s názvem zdrojového modelu, např. `Import z: Zdrojový model`.

### Statistiky

Po sloučení se zobrazí statistiky:
- Počet přidaných/přepsaných prvků
- Počet přidaných/přepsaných vazeb
- Počet přidaných/přepsaných diagramů

---

## Hromadné operace s příznaky

### Otevření modálního okna

Klikněte na tlačítko **Hromadné operace** v sekci filtrů.

### Výběr rozsahu

- **Prvky** - operace s příznaky prvků
- **Vazby** - operace s příznaky vazeb

### Výběr položek

- Zaškrtněte položky pro operaci
- **Vybrat vše** / **Odebrat vše** - hromadný výběr
- **Vybrat aktuálně filtrované** - vybere položky odpovídající aktivním filtrům

### Dostupné operace

#### Přidat příznak
Přidá zadaný příznak ke všem vybraným položkám (pokud ho ještě nemají).

#### Odebrat příznak
Odebere zadaný příznak ze všech vybraných položek.

#### Nahradit příznak
Nahradí jeden příznak jiným ve všech vybraných položkách.

---

## Tipy a triky

### Automatické ukládání

Model se automaticky ukládá do prohlížeče po každé změně. Při opětovném otevření se načte poslední stav.

### Rychlá navigace z vazeb

V tabulce prvků zobrazuje sloupec "Vazby" počet vazeb. Kliknutím na číslo přejdete na filtrovaný seznam vazeb pro daný prvek.

### Našeptávání

- **Stereotypy** - nabízí dříve použité stereotypy
- **Příznaky** - nabízí existující příznaky z modelu
- **Názvy vazeb** - nabízí dříve použité názvy

### Validace vazeb

Editor automaticky kontroluje validitu vazeb podle ArchiMate 3.2 specifikace. Nepovolené kombinace nejsou v nabídce.

### Drag & Drop

Soubory lze importovat přetažením na stránku.

### Dublin Core

Vyplňte Dublin Core metadata pro lepší interoperabilitu s jinými nástroji a pro dokumentaci modelu.

### Verze modelu

Používejte pole Verze pro sledování změn modelu v čase.

### Zálohování

Pravidelně exportujte model do AJX souboru jako zálohu. Data v prohlížeči mohou být smazána při vyčištění historie.

---

## Klávesové zkratky

| Zkratka | Akce |
|---------|------|
| Tab | Přechod mezi poli formuláře |
| Enter | Potvrzení formuláře (v některých kontextech) |
| Escape | Zavření modálního okna |

---

## Referenční příručka ArchiMate

### Vrstvy

| Vrstva | Barva | Popis |
|--------|-------|-------|
| Strategy | Hnědá | Strategické prvky - zdroje, schopnosti, hodnotové toky |
| Business | Zlatá | Byznysové prvky - aktéři, procesy, služby |
| Application | Modrá | Aplikační prvky - komponenty, služby, data |
| Technology | Zelená | Technologické prvky - uzly, zařízení, artefakty |
| Physical | Tmavě zelená | Fyzické prvky - vybavení, budovy, materiály |
| Implementation | Fialová | Implementační prvky - pracovní balíčky, dodávky |
| Motivation | Červená | Motivační prvky - stakeholdeři, cíle, požadavky |
| Composite | Šedá | Složené prvky - lokace, seskupení |

### Typy vazeb

| Typ | Kategorie | Popis |
|-----|-----------|-------|
| Composition | Strukturální | Prvek se skládá z jiných prvků |
| Aggregation | Strukturální | Prvek sdružuje jiné prvky |
| Assignment | Strukturální | Přiřazení aktivního prvku k chování |
| Realization | Strukturální | Prvek realizuje jiný prvek |
| Serving | Závislostní | Prvek poskytuje funkcionalitu jinému |
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

Na GitHubu najdete:
- Editor ke stažení jako samostatný HTML soubor
- Tuto dokumentaci v češtině i angličtině
- JSON Schema (`ajx-schema.json`) pro validaci AJX souborů

### Systémové požadavky

- Moderní webový prohlížeč (Chrome, Firefox, Safari, Edge)
- JavaScript musí být povolen
- Pro ukládání je potřeba localStorage

### Známá omezení

- Data jsou ukládána lokálně v prohlížeči
- Při vyčištění dat prohlížeče se model smaže
- Doporučeno pravidelně exportovat zálohy

---

*Verze dokumentace: 1.0*
*ArchiMate® je registrovaná ochranná známka The Open Group.*
