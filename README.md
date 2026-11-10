# Beach Draw - vlastní stránka pro vaši hráčku

Webová stránka, která sama sleduje turnaje vaší dcery (nebo více hráček) v beachvolejbale:

- rozlosování, skupiny, play-off a výsledky,
- nasazení a přihlášky na turnaje 14 dní dopředu,
- žebříčky Pražské beachligy a ABV s odkazem na profil,
- vzájemné zápasy proti konkrétní soupeřce nebo dvojici,
- čeština i angličtina, funguje i na mobilu.

Data se berou z **volejbalpraha.cz** (Pražská beachliga a Letní beachliga) a z **cvf.cz** (ABV celostátní a MČR, kategorie U14 až U20 ženy). Oblastní turnaje ABV se nesledují.

**Nic se neplatí.** Stránka běží zdarma na GitHubu. Potřebujete jen e-mail, počítač s prohlížečem a asi 15 minut.

> Stránka bude veřejná: uvidí ji každý, kdo zná adresu, včetně fotek.

---

## Krok 1: Založte si účet na GitHubu

1. Otevřete **https://github.com/signup**.
2. Zadejte e-mail, heslo a **uživatelské jméno** (např. `novakovi`).
   Uživatelské jméno bude součástí adresy stránky, tak vyberte něco krátkého bez diakritiky.
3. Potvrďte e-mail. Placený tarif nepotřebujete, nabídky přeskočte.

## Krok 2: Vytvořte si kopii šablony

1. Po přihlášení otevřete **https://github.com/ondrahnat/beach-sablona**.
2. Vpravo nahoře klikněte na zelené tlačítko **Use this template** a pak **Create a new repository**.
3. Do pole **Repository name** napište `beach` (malými písmeny).
4. Nechte zvolené **Public**.
5. Klikněte dole na **Create repository**.

## Krok 3: Zapněte webovou stránku

1. Ve vašem novém repozitáři klikněte nahoře na **Settings** (ozubené kolečko).
2. V levém menu klikněte na **Pages**.
3. U položky **Source** vyberte **GitHub Actions**.

Víc tu nastavovat nemusíte.

## Krok 4: Nahrajte fotky (nepovinné)

1. Vraťte se na hlavní stránku repozitáře (klikněte nahoře na **Code**).
2. Klikněte na **Add file** a pak **Upload files**.
3. Přetáhněte fotku hráčky. Název souboru bez diakritiky a mezer, např. `foto-anna.jpg`.
   Nejlépe čtvercová fotka obličeje, stačí menší rozlišení (do 1 MB).
4. Dole klikněte na zelené **Commit changes**.

Bez fotky se zobrazí iniciály.

## Krok 5: Vyplňte, koho sledovat (soubor config.json)

1. Na hlavní stránce repozitáře klikněte na soubor **config.json**.
2. Vpravo nahoře klikněte na **tužku** (Edit this file).
3. Přepište obsah podle vzoru níže a klikněte na zelené **Commit changes** (a v okně znovu **Commit changes**).

**Jedna hráčka:**

```json
{
  "title": "Nováková Beach Draw",
  "players": [
    { "name": "Anna Nováková", "nick": "Anička", "photo": "foto-anna.jpg" }
  ],
  "historyFrom": "2022-08-01"
}
```

**Dvě hráčky (nebo víc, oddělené čárkou):**

```json
{
  "title": "Novákovy Beach Draw",
  "players": [
    { "name": "Anna Nováková", "nick": "Anička", "photo": "foto-anna.jpg" },
    { "name": "Eva Nováková", "nick": "Evča", "photo": "" }
  ],
  "historyFrom": "2022-08-01"
}
```

Co jednotlivé řádky znamenají:

| Položka | Co tam napsat |
|---|---|
| `title` | Název stránky nahoře vlevo. |
| `name` | Jméno a příjmení **přesně tak, jak je hráčka zapsaná na volejbalpraha.cz a cvf.cz** (s háčky a čárkami). Podle toho se hledá. |
| `nick` | Přezdívka, která se zobrazí na kartě hráčky. Může být prázdná: `""`. |
| `photo` | Název souboru fotky z kroku 4. Bez fotky nechte `""`. |
| `historyFrom` | Od kdy dohledat starší turnaje (rok-měsíc-den). Starší než 2022 na webu nejsou. |

Pozor na uvozovky `"` a čárky. Mezi hráčkami je čárka, za poslední hráčkou ne. Když si nejste jistí, vložte text na **https://jsonlint.com** a klikněte na Validate.

## Krok 6: Počkejte na první stažení dat

1. Klikněte nahoře na záložku **Actions**.
2. Uvidíte běžící úlohu **Aktualizace dat** (žluté kolečko).
3. **Poprvé to trvá 10 až 30 minut**, protože se stahuje celá historie turnajů.
4. Hotovo je, když se objeví **zelená fajfka**.

## Krok 7: Otevřete stránku a pošlete ji rodině

Adresa je:

```
https://VASE-UZIVATELSKE-JMENO.github.io/beach/
```

Například pro uživatele `novakovi`: `https://novakovi.github.io/beach/`

Adresu pošlete komukoli. Nikdo nepotřebuje účet ani aplikaci. Na mobilu si ji můžete přidat na plochu (v prohlížeči **Sdílet** a **Přidat na plochu**).

---

## Jak to pak funguje

- Data se aktualizují **sama**: o víkendech každých 15 minut (cca 6 až 21 h), ve všední dny každé 3 hodiny.
- Tlačítko **Obnovit** na stránce jen načte nejnovější už stažená data. Stránka se navíc sama kontroluje každých 5 minut.
- Potřebujete aktualizaci hned? **Actions**, vlevo **Aktualizace dat**, vpravo **Run workflow** a znovu **Run workflow**. Za 1 až 2 minuty je hotovo.

## Časté situace

**Chci přidat další hráčku.**
Doplňte ji do `config.json` (krok 5). Při nejbližší aktualizaci se jí sama dohledá i historie.

**Některý turnaj chybí.**
Otevřete soubor `extra-links.txt`, tužkou ho upravte a na nový řádek vložte odkaz na turnaj
(např. `https://www.volejbalpraha.cz/beach/detail/1975` nebo odkaz na turnaj z cvf.cz). Commit changes.

**Hráčka už nehraje některou kategorii ABV a nechci ji vidět v žebříčku.**
Do řádku hráčky přidejte `"abvExclude": ["ZKY"]`. Kódy: `ZKY` = U16, `KKY` = U18, `JKY` = U20, `Z` = ženy. Příklad:
`{ "name": "Anna Nováková", "nick": "Anička", "photo": "", "abvExclude": ["ZKY"] }`

**Chci znovu dohledat celou historii.**
**Actions**, **Aktualizace dat**, **Run workflow**, zaškrtněte **Dohledat i celou historii turnajů** a spusťte.

**V Actions je červený křížek.**
Většinou byl web svazu chvíli nedostupný a další běh to spraví sám. Pokud se to stalo hned po úpravě `config.json`, je v něm nejspíš chyba v uvozovkách nebo čárkách (zkontrolujte na jsonlint.com).

**GitHub poslal e-mail, že plánované spouštění vypnul.**
Stává se po 60 dnech bez změn v repozitáři (typicky mimo sezónu). Otevřete **Actions**, **Aktualizace dat** a klikněte na **Enable workflow**.

**Chci stránku zrušit.**
**Settings**, úplně dole **Delete this repository**.

## Co stránka neumí

- U turnajů Pražské beachligy zhruba do jara 2025 web svazu nezveřejňoval jednotlivé zápasy. U nich se zobrazí jen přihlášené dvojice a body, ne výsledky zápasů.
- Sleduje jen ženské a smíšené mládežnické kategorie.
