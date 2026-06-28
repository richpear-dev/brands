![Richpear Home](https://cdn.jsdelivr.net/gh/richpear-devs/brands@master/core_integrations/_homeassistant/logo.png)

# Richpear Home — repozitář log a ikon integrací

Tento repozitář obsahuje ikony a loga všech značek, které Richpear Home
podporuje.

Repozitář slouží ke generování statického webu, který tyto obrázky poskytuje
pro použití v projektech Richpear Home. Cílem je mít centralizovaný
repozitář obrázků značek.

## Jak to funguje

Tento repozitář poskytuje dvě hlavní složky pro ukládání obrázků:

- `core_integrations`: Obsahuje obrázky pro integrace dodávané přímo
  s jádrem Richpear Home Core.
- `custom_integrations`: Obsahuje obrázky pro vlastní integrace
  (custom components). Starší složka: Od verze RP Home 2026.3.0 mohou vlastní komponenty zahrnovat své ikony značky přímo. Více informací najdete v [oznámení o Brands Proxy API](https://docs.richpear.cz/blog/2026/02/24/brands-proxy-api).

Každá z těchto dvou hlavních složek obsahuje složky domén. Každá složka domény je
pojmenována podle `domain` integrace a musí odpovídat doméně nastavené v souboru
`manifest.json` dané integrace.

Složka domény může obsahovat osm souborů:

- `icon.png`: Čtvercová ikona ve stylu avataru, představující značku nebo produkt dané domény.
- `dark_icon.png`: Ikona optimalizovaná pro tmavé motivy (je-li potřeba).
- `logo.png`: Logo značky nebo produktu dané domény.
- `dark_logo.png`: Logo optimalizované pro tmavé motivy (je-li potřeba).
- `icon@2x.png`: hDPI verze `icon.png`
- `dark_icon@2x.png`: hDPI verze `dark_icon.png`
- `logo@2x.png`: hDPI verze `logo.png`
- `dark_logo@2x.png`: hDPI verze `dark_logo.png`

Tyto obrázky jsou poskytovány v následujícím formátu:

- `https://brands.richpear.cz/[domain]/icon.png`
- `https://brands.richpear.cz/[domain]/dark_icon.png`
- `https://brands.richpear.cz/[domain]/logo.png`
- `https://brands.richpear.cz/[domain]/dark_logo.png`
- `https://brands.richpear.cz/[domain]/icon@2x.png`
- `https://brands.richpear.cz/[domain]/dark_icon@2x.png`
- `https://brands.richpear.cz/[domain]/logo@2x.png`
- `https://brands.richpear.cz/[domain]/dark_logo@2x.png`
- `https://brands.richpear.cz/_/[domain]/icon.png`
- `https://brands.richpear.cz/_/[domain]/dark_icon.png`
- `https://brands.richpear.cz/_/[domain]/logo.png`
- `https://brands.richpear.cz/_/[domain]/dark_logo.png`
- `https://brands.richpear.cz/_/[domain]/icon@2x.png`
- `https://brands.richpear.cz/_/[domain]/dark_icon@2x.png`
- `https://brands.richpear.cz/_/[domain]/logo@2x.png`
- `https://brands.richpear.cz/_/[domain]/dark_logo@2x.png`

### Zpracování chybějících obrázků

Web umí poskytovat obrázky jak s fallbackem na zástupný obrázek (placeholder),
tak bez něj.

### Bez fallbacku na placeholder

Tato metoda používá prosté URL **BEZ** `/_/` v cestě URL.
Chybějící obrázek vrátí chybu 404.

Například: <`https://brands.richpear.cz/[domain]/icon.png`>

- Pokud doméně chybí soubor `icon.png`, vrátí se 404.
- Pokud doméně chybí soubor `logo.png`, poskytne se místo něj `icon.png` (je-li dostupný).
- Pokud doméně chybí soubor `icon@2x.png`, poskytne se místo něj `icon.png` (je-li dostupný).
- Pokud doméně chybí soubor `logo@2x.png`:
  - poskytne se `icon@2x.png`, je-li dostupný a `logo.png` chybí,
  - jinak se poskytne `logo.png` (je-li dostupný).
- Pokud chybí obrázek optimalizovaný pro tmavé motivy (s prefixem „dark_"), poskytne se místo něj jeho protějšek bez prefixu (je-li dostupný).

### S fallbackem na placeholder

Tato metoda používá prosté URL **S** `/_/` v cestě URL.
Chybějící obrázek vrátí zástupný obrázek (placeholder) oznamující, že logo/ikona chybí.
To platí i pro domény, pokud chybí celá doména integrace.

Například: <`https://brands.richpear.cz/_/[domain]/icon.png`>

### Cachování

Všechny ikony a loga jsou prohlížeči cachovány po dobu 7 dnů, takže přidání a změny mohou nějakou dobu trvat, než se dostanou ke všem uživatelům. To dává uživatelům plné výhody lokálního cachování s minimální revalidací a chrání před chybějícím obsahem během výpadku internetu.

Obrázky jsou současně cachovány službou Cloudflare po dobu 24 hodin. To umožňuje začít distribuovat změny uživatelům relativně rychle, aniž by se ztratily výhody CDN. Také to zaručuje, že jednoduché obnovení (F5) přinese obsah ne starší než 1 den.

Cache Cloudflare se rovněž zcela vyprázdní v každé hlavní verzi Richpear Home Core.

## Specifikace obrázků

Všechny obrázky musí splňovat následující požadavky:

- Typ souboru všech obrázků musí být PNG.
- Měly by být řádně komprimované a optimalizované (bezztrátová komprese je preferována) pro použití na webu.
- Preferován je prokládaný (interlaced) formát (známý také jako progresivní).
- Preferovány jsou obrázky s průhledností.
- Pokud je k dispozici více obrázků, preferují se ty optimalizované pro bílé pozadí.
  - Obrázky optimalizované pro tmavé pozadí lze označit prefixem `dark_`.
- Obrázek by měl být oříznutý, aby obsahoval minimum prázdného místa na okrajích.
  To zahrnuje bílé/černé/barevné okraje nebo průhledný prostor kolem samotného
  předmětu obrázku.
- Vlastní integrace nesmí používat obrázky se značkou Richpear Home, protože to může u koncového uživatele vyvolat dojem, že jde o interní/oficiální integraci.

### Požadavky na obrázek ikony

Kromě obecných požadavků na obrázky uvedených výše platí pro obrázek ikony
také následující požadavky:

- Poměr stran musí být 1:1 (čtverec).
- Velikost ikony musí být:
  - 256×256 pixelů pro běžnou verzi.
  - 512×512 pixelů pro hDPI verzi.

### Požadavky na obrázek loga

Kromě obecných požadavků na obrázky uvedených výše platí pro obrázek loga
také následující požadavky:

- Preferuje se obrázek na šířku (landscape).
- Poměr stran by měl respektovat logo dané značky.
- Nejkratší strana obrázku musí být:
  - Alespoň 128 pixelů, ale ne větší než 256 pixelů pro běžnou verzi.
  - Alespoň 256 pixelů, ale ne větší než 512 pixelů pro hDPI verzi.
- Maximální velikost v pixelech pro nejkratší stranu obrázků je samozřejmě preferována.

## Použití stejného obrázku pro logo i ikonu

Pokud značka používá stejný obrázek pro logo i ikonu (např. pokud má logo čtvercový poměr stran),
přidejte pouze obrázky ikony. Ikona se použije jako fallback pro logo.

## Použití stejného loga a ikony pro různé značky

Aby byla velikost tohoto repozitáře co nejefektivnější,
je pro core integrace povoleno symlinkování složek domén se stejnými ikonami/logy. Proces nasazení
u našeho hostingu tyto symlinky během nasazení rozbalí
na skutečné soubory.

Vezměte prosím na vědomí, že symlinky by se měly vytvářet pouze mezi
adresáři domén integrací. Adresáře `_placeholder` a `_homeassistant` jsou speciální
případy a nové adresáře s podtržítkem (`_`) by se neměly vytvářet.

Symlinky aktuálně nejsou ve složce custom integrations povoleny.

Názvy adresářů musí vždy odpovídat doméně integrace. Další
adresáře nejsou povoleny.

## Konflikt domény integrace mezi vlastními a core integracemi

Je možné, že se vlastní integrace a core integrace střetnou na
úrovni názvu `domain`. V takových případech má přednost doména
core integrace.

## Tipy, nástroje a zdroje

Při přidávání nové sady ikon a log vám mohou s nalezením potřebných obrázků
a jejich úpravou podle našich specifikací pomoci následující zdroje:

- [**RedKetchup Image Resizer**](https://redketchup.io/image-resizer):
  Mění velikost většiny formátů obrázků, včetně SVG, do libovolného formátu
  přímo ve vašem prohlížeči.
- [**Worldvectorlogo**](https://worldvectorlogo.com/):
  Tisíce SVG obrázků značek, které jsou ideální jako základ.
- [**Wikimedia Commons**](https://commons.wikimedia.org/):
  Obsahuje mnoho kvalitních obrázků.

Mnoho značek (zejména těch větších) často nabízí na svých
(firemních) webech press kit, který obsahuje kvalitní obrázky.

## Právní upozornění k ochranným známkám

Všechny názvy produktů, ochranné známky a registrované ochranné známky v obrázcích v tomto
repozitáři jsou majetkem příslušných vlastníků. Všechny obrázky v tomto
repozitáři jsou projektem Richpear Home používány pouze pro účely identifikace.

Použití těchto názvů, ochranných známek a značek uvedených v těchto obrazových souborech
neznamená jejich schválení (endorsement).
