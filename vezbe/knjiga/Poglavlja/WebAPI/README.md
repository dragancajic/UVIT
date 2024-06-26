[Vežbe](../../../README.md)

[Knjiga](../../README.md)

---

<style>
.domaci-zadatak {
    border: 5px solid gold;
    padding: 10px;
    margin-bottom: 20px;
}

.domaci-zadatak .naslov {
    font-weight: bold;
    text-align: center;
    display: block;
}

.domaci-zadatak .tekst {
    border-top: 2px dashed black;
    border-bottom: 2px dashed black;
    padding-top: 10px;
    /* padding-bottom: 10px; */
}
</style>

# 5. JavaScript i Web API

Sada kada smo savladali osnovne koncepte jezika JavaScript, u stanju smo da primenimo stečena znanja radi kreiranja klijentskih aplikacija. U ovom uvodnom poglavlju u delu 3 - "Programiranje klijentskih veb aplikacija", diskutovaćemo o tome šta klijentske aplikacije predstavljaju iz ugla programera, kako se one implementiraju i koji su to osnovni elementi _interfejsa programiranja aplikacija_ (engl. _application programming interface_, skr. _API_) koji su nam dostupni na raspolaganju za kreiranje klijentskih aplikacija.

_Klijentska aplikacija_ predstavlja veb aplikaciju koja se sastoji od skupa HTML datoteka i resursa koje te HTML datoteke koriste, a koja se izvršava na klijentskom računaru, tj. na računaru korisnika. Već smo videli veliki broj resursa koje jedna HTML datoteka može da koristi. Neki od primera su: CSS datoteke, slike, veb lokacije (u kontekstu veza) i JS datoteke. Zapravo, sve aplikacije koje smo do sada pravili predstavljaju klijentske aplikacije. Najčešće se klijentske aplikacije izvršavaju u okviru veb pregledača i takve aplikacije ćemo i mi programirati. Drugim rečima, naše klijentske aplikacije će se osloniti na različite elemente koji su implementirani u veb pregledačima, kao što je mašina za izvršavanje JavaScript koda, mašina za iscrtavanje u pogledu veb pregledača, mehanizmi za upravljanje komunikacijom putem mreže, itd. Međutim, klijentske aplikacije se ugrubo mogu podeliti u dve vrste:

1. _Statičke_ klijentske aplikacije su one koje ne zahtevaju izvršavanje JavaScript koda.

2. _Dinamičke_ klijentske aplikacije su one koje zahtevaju izvršavanje JavaScript koda.

Mi smo do sada (sa izuzetkom poglavlja 4 - "Programski jezik JavaScript" gde smo demonstrirali elemente programskog jezika JavaScript) kreirali isključivo statičke klijentske aplikacije. Ove aplikacije su bile sačinjene od definicija strukture pomoću HTML datoteka i definicija stilova te strukture pomoću CSS datoteka, uz eventualno prikazivanje resursa poput slika ili veza. U ovom poglavlju ćemo se baviti dinamičkim klijentskim aplikacijama, odnosno, naučićemo kako da pišemo JavaScript kodove koje izvršavaju neke dinamičke aktivnosti na veb prezentaciji, na primer, menjanje stilova HTML elemenata, obrada podataka u formularu, dohvatanje podataka sa serverskih aplikacija preko mreže, i dr.

## 5.1 Web API

Da bismo mogli da kreiramo dinamičke klijentske aplikacije, potrebno je da postoje funkcije ili objekti koji nam omogućavaju da koristimo te dinamičke funkcionalnosti u našim JavaScript aplikacijama. U "čistom" JavaScript jeziku koji smo videli do sada, to nije moguće. Umesto toga, moramo da se oslonimo na neke biblioteke koje nam to omogućavaju. Na primer, svi savremeni veb pregledači implementiraju skup biblioteka koji se naziva [Web API](https://developer.mozilla.org/en-US/docs/Web/API). Web API predstavlja obimnu kolekciju raznovrsnih funkcija ili objekata, podeljenih po manjim bibliotekama, koji nam omogućavaju da implementiramo raznovrsne funkcionalnosti u aplikacijama koje kodiramo u programskom jeziku JavaScript. Neke od tih funkcionalnosti su:

- **Komunikacija sa konzolom.** Objekat `console` koji smo koristili do sada zapravo nije ugrađen u sam jezik JavaScript, već je deo biblioteke [Console API](https://developer.mozilla.org/en-US/docs/Web/API/Console_API). To je zapravo i jedini objekat koji se nalazi u ovoj biblioteci.

- **Dinamičko menjanje HTML i CSS stranica.** Do sada smo sve veb stranice kodirali pisanjem HTML i CSS koda koji definišu strukturu tih stranica. Međutim, moguće je kombinacijom JavaScript jezika i biblioteke koja se zove [DOM API](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) promeniti strukturu napisanih stranica. Na primer, možemo dodavati nove elemente, brisati postojeće, menjati njihov stil itd. U nastavku teksta ćemo koristiti ovaj API da bismo kreirali dinamičke klijentske veb aplikacije.

- **Odlaganje izvršavanja funkcija.** Na primer, možemo reći JavaScript okruženju da izvrši neku funkciju nakon 5 sekundi (ovo ponašanje i njemu slična ćemo nadalje zvati _asinhronim izvršavanjem koda_). U nastavku teksta ćemo prikazati funkcije [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) i [setInterval](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval) kojima je moguće ovo postići.

- **Kontaktiranje serverskih aplikacija putem HTTP protokola.** Na primer, možemo kontaktirati neku serversku aplikaciju (bilo da je to aplikaciju koju smo mi implementirali ili koju je neko drugi implementirao) putem HTTP protokola i zatražiti da ta serverska aplikacija izvrši nekakvu akciju. Akcije mogu biti razne i zavise od implementacije te serverske aplikacije. Na primer, ove akcije mogu obuhvatati: dohvatanje ili skladištenje podataka u bazama podataka, dohvatanje dokumenata, slika i drugih resursa, prevođenje teksta, slanje elektronske pošte, obradu slika, itd. Ova komunikacija putem HTTP protokola se može izvršiti sinhrono ili asinhrono. Međutim, u praksi se obavezno koristi asinhroni pristup kako se aplikacija ne bi blokirala. U nastavku teksta ćemo prikazati tzv. _konstruktorsku funkciju_ [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) kojom je moguće ovo postići.

- **Crtanje u pogledu veb pregledača.** Postoje dva dela Web API biblioteke kojima je ovo moguće: [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) i [WebGL API](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API). O ovom API-ju neće biti reči u okviru kursa.

- **Skladištenje podataka u veb pregledaču.** Iako ćemo u nastavku kursa videti zašto se podaci pretežno skladište pomoću serverskih aplikacijama na serverima, nekada je zgodno čuvati i neke podatke na strani klijenta. Za te potrebe postoji [Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API) koji nudi različite mehanizme za skladištenje podataka u veb pregledačima. O ovom API-ju neće biti reči u okviru kursa.

Naravno, ovaj spisak izlistava tek jedan deo obimne biblioteke Web API.

## 5.2 Dinamičko menjanje HTML i CSS stranica. DOM API. 

O DOM stablu smo govorili još u poglavlju 1 - "Struktuiranje Veb dokumenata kroz HTML". U ovoj sekciji ćemo nešto detaljnije obratiti pažnju na ovu veoma važnu strukturu podataka.

Kada veb pregledač dohvati neki HTML dokument, on započinje proces parsiranja tog dokumenta i od njega pravi model tog dokumenta u okviru radne memorije koja mu je dodeljena od strane operativnog sistema. Nad tim modelom programeri mogu da izvršavaju razne operacije. Ukoliko su operacije takve da menjaju strukturu modela, veb pregledač će prepoznati da se takva akcija izvršila, te će osvežiti prikaz veb dokumenta u prozoru veb pregledača. Upravo pod ovim ponašanjem smatramo _dinamičko_ menjanje prikaza veb dokumenta.

Neka nam je dat naredni HTML dokument.

```html
<!DOCTYPE html>

<html>
  <head>
    <title>Moja pocetna stranica</title>
    <meta charset="UTF−8" />
  </head>

  <body>
    <h1>Ime i prezime</h1>
    <div>
      <p>Moj CV mozete pronaci <a href="cv.pdf">ovde</a>.</p>
    </div>
  </body>
</html>
```

Možemo da zamislimo strukturu HTML dokumenta kao ugnežđene kutije. Struktura HTML dokumenta iznad se vizualno može predstaviti kao na narednoj slici.

<div style="max-width: 98%;">
<img style="max-width: 100%;" src="./Slike/primer_stranice_za_dom.png" alt="">
</div>

Struktura kojom veb pregledač opisuje model HTML stranice prati ovaj grafički prikaz. Za svaku kutiju postoji objekat, sa kojim programeri mogu da interaguju da bi dohvatili njegova svojstva ili izvršavali neke metode. Ovakva reprezentacija se naziva _model objekata dokumenta_ (engl. _document object model_, skr. _DOM_). Preciznije, struktura podataka kojom se opisuje DOM je _m_-narno _stablo_ (engl. _tree_). Elementi su predstavljeni čvorima stabla i oni određuju njegovu strukturu. Ugnežđeni elementi predstavljaju _naslednike_ (engl. _child_) čvora koji je njihov _roditelj_ (engl. _parent_). Neki čvorovi imaju _listove_ (engl. _leaf_) za naslednike, što mogu biti tekstualni elementi, komentari i dr. Na primer, drvolika struktura prethodnog HTML dokumenta se može prikazati kao na narednoj slici<sup>[^1]</sup>. Plavom bojom su označeni čvorovi koji predstavljaju HTML elemente; zelenom bojom su označeni čvorovi koji predstavljaju tekstualni sadržaj; žutom bojom su označeni čvorovi koji predstavljaju tekstualni sadržaj sačinjen samo od belina.

[^1]: Alat koji je korišćen za vizualizaciju ovog DOM stabla se može pronaći na adresi [http://bioub.github.io/dom-visualizer/](http://bioub.github.io/dom-visualizer/){:target="\_blank"}

<div style="max-width: 98%;">
<img style="max-width: 100%;" src="./Slike/primer_stranice_za_dom.svg" alt="">
</div>

Dakle, da bismo mogli da dinamički upravljamo prikazom veb stranice, prvo što je potrebno uraditi jeste pronaći odgovarajuće elemente u DOM stablu, a zatim izvršiti odgovarajuće operacije nad njima. Upravo u ovom redosledu ćemo se upoznati sa radom nad DOM stablom.

### 5.2.1 Pretraga elemenata

U okviru JavaScript okruženja za izvršavanje u veb pregledačima postoji JavaScript objekat koji se naziva `document`, koji sadrži informacije o veb stranici i zapravo predstavlja koren DOM stabla. Ako želimo da pristupimo nekom elementu na veb stranici, odnosno, da pristupimo odgovarajućem čvoru DOM stabla koji predstavlja taj element u memoriji, najjednostavniji način jeste da započnemo pretragu od objekta `document`. Nad ovim objektom su definisani brojni metodi za pretragu elemenata koji su opisani u nastavku. Obratiti posebnu pažnju na povratnu vrednost ovih metoda - neki od metoda vraćaju jedan objekat, dok drugi vraćaju niz objekata.

- Metod `getElementById` omogućava dohvatanje jednog čvora na osnovu identifikatora koji je dodeljen tom elementu. Njegov argument je niska koja sadrži naziv identifikatora.

- Metod `getElementsByTagName` omogućava dohvatanje niza elemenata na osnovu imena elementa. Njegov argument je niska koja sadrži naziv elementa.

- Metod `getElementsByClassName` omogućava dohvatanje niza elemenata na osnovu
  imena klase. Njegov argument je niska koja sadrži naziv klase.

- Metod `querySelector` omogućava dohvatanje prvog elementa koji je obuhvaćen datim CSS selektorom. Njegov argument je niska koja sadrži CSS selektor.

- Metod `querySelectorAll` omogućava dohvatanje niza elemenata koji su obuhvaćen datim CSS selektorom. Njegov argument je niska koja sadrži CSS selektor.

Za sve metode koji vraćaju jedan objekat važi da, u slučaju da ne pronađu nijedan element koji odgovara datom argumentu, vraćaju `null`. Sa druge strane, za sve metode koji vraćaju niz objekata važi da, u slučaju da ne pronađu nijedan element koji odgovara datom argumentu, vraćaju prazan niz. Zbog toga je posebno potrebno voditi računa o obradi ovih slučajeva u kodu.

Naredni primer ilustruje korišćenje opisanih metoda.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 1</title>
  </head>

  <body>
    <p id="prvi_pasus">Ovo je primer</p>
    <p id="drugi_pasus" class="parni">rada sa DOM stablom</p>
    <p id="treci_pasus">u programskom jeziku JavaScript.</p>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
const prviPasus = document.getElementById('prvi_pasus');
if (prviPasus != null) {
  console.log('Uspešno smo pronašli element sa identifikatorom prvi_pasus');
}

const sviPasusi = document.getElementsByTagName('p');
const brojPasusa = sviPasusi.length;
if (brojPasusa > 0) {
  console.log(`Ova veb stranica sadrži ${brojPasusa} paragraf/a`);
}

const parniPasusi = document.getElementsByClassName('parni');
if (parniPasusi.length > 0) {
  console.log(
    `Ova veb stranica sadrži ${parniPasusi.length} element/elemenata sa klasom "parni"`
  );
}

const srednjiPasus = document.querySelector('.parni');
if (srednjiPasus != null) {
  console.log('Postoji makar jedan element sa klasom "parni"');
}

const sviPasusiPonovo = document.querySelectorAll('p');
if (sviPasusiPonovo.length > 0) {
  console.log(
    `Ponovo vidimo da ova veb stranica sadrži ${sviPasusiPonovo.length} paragraf/a`
  );
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/1/index.html"
   target="_blank">Pogledaj primer uživo (obavezno otvoriti konzolu)</a>

### 5.2.2 Upravljanje elementima

Nakon što smo uspešno dohvatili jedan element ili više njih, postavlja se pitanje koje sve operacije možemo izvršiti nad njima, odnosno, koje njihove delove možemo menjati dinamički. Grubo rečeno, sve operacije nad elementom se mogu podeliti u tri vrste:

1. Izmena sadržaja

2. Izmena vrednosti atributa

3. Izmena stila

#### Izmena sadržaja

Izmena sadržaja elementa podrazumeva izmenu same strukture koja je inicijalno opisana HTML kodom. Nad objektima koji predstavljaju HTML elemente su definisana dva svojstva:

- Svojstvo `innerHTML` obuhvata onaj HTML deo koda koji se nalazi u sadržaju elementa.

- Svojstvo `outerHTML` obuhvata onaj HTML deo koda koji predstavlja sam element zajedno sa njegovim sadržajem.

Vrednost ovih svojstava je niska koja sadrži odgovarajući tekstualni sadržaj. Napomenimo da `innerHTML` i `outerHTML` nisu ništa drugo do svojstva odgovarajućih JavaScript objekata, te se ona mogu koristiti za čitanje vrednosti (ukoliko ih samo navedemo, na primer, `console.log(objekat.innerHTML);`) ili za pisanje vrednosti (ukoliko im dodelimo neku vrednost, na primer, `objekat.innerHTML = '<p>Tekst</p>';`), kao i kod bilo kojih drugih JavaScript objekata. U nastavku teksta nećemo više skrenuti pažnju čitaocu na ovu osobinu kod drugih svojstava.

Na primer, ako posmatramo naredni HTML kod

```html
<div class="omotac">
  <h1>Naslov</h1>
</div>
```

svojstvo `innerHTML` elementa `div` obuhvata sve što se nalazi između otvarajuće etikete `<div>` i zatvarajuće etikete `</div>`, odnosno:

```
<h1>Naslov</h1>
```

dok svojstvo `outerHTML` istog elementa obuhvata otvarajuću etiketu `<div>`, zatvarajuću etiketu `</div>` kao i sve što se nalazi između, odnosno:

```
<div class="omotac"><h1>Naslov</h1></div>
```

Posledica ovog opažanja jeste da menjanjem svojstva `innerHTML` možemo transformisati sadržaj elemenata, dok menjanjem svojstva `outerHTML` možemo transformisati sam element, što naredni primer ilustruje.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 2</title>

    <style>
      div {
        border: 5px solid black;
      }

      main {
        border: 5px solid red;
      }
    </style>
  </head>

  <body>
    <div id="prvi">
      <h1>Prvi naslov</h1>
    </div>

    <div id="drugi">
      <h1>Drugi naslov</h1>
    </div>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
const prviDiv = document.getElementById('prvi');
if (prviDiv != null) {
  prviDiv.innerHTML = '<h2>Prvi podnaslov</h2>';
} else {
  console.log('Ne mogu da pronadjem element sa identifikatorom "prvi".');
}

const drugiDiv = document.getElementById('drugi');
if (drugiDiv != null) {
  drugiDiv.outerHTML = `<main id="drugi">
            <h2>Drugi podnaslov</h2>
        </main>`;
} else {
  console.log('Ne mogu da pronadjem element sa identifikatorom "drugi".');
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/2/index.html"
   target="_blank">Pogledaj primer uživo</a>

#### Izmena vrednosti atributa

Kao što znamo, veliki broj HTML elemenata ima različite atribute koji ih dodatno okarakterišu. Na primer, element `img` ima atribut `src` koji definiše lokaciju slike koja je potrebno da se prikaže, element `a` ima atribut `href` koji definiše lokaciju resursa ka kojem je potrebno kreirati vezu, itd. HTML elementima možemo dinamički menjati vrednosti atributa tako što promenimo vrednost odgovarajućeg svojstva objekta u DOM stablu koji odgovara tom elementu. Naredni primer ilustruje promenu resursa ka kojem vodi veza.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 3</title>
  </head>

  <body>
    <a href="">"Bezveze" link :)</a>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
const veze = document.getElementsByTagName('a');
if (veze.length > 0) {
  const prvaVeza = veze[0];

  // Postavljamo nove vrednosti za atribute href i target
  prvaVeza.href = 'https://matfuvit.github.io/UVIT/';
  prvaVeza.target = '_blank';

  // Ažuriramo tekst u vezi
  prvaVeza.innerHTML = 'Početna stranica kursa';
} else {
  console.log('Na ovoj stranici ne postoje veze.');
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/3/index.html"
   target="_blank">Pogledaj primer uživo</a>

Na adresi [https://www.w3schools.com/jsref/default.asp](https://www.w3schools.com/jsref/default.asp){:target="\_blank"} u sekciji _HTML Element Objects Reference_ moguće je pronaći za svaki HTML element spisak atributa čije se vrednosti mogu dinamički menjati, zajedno sa njihovim opisima.

#### Izmena stila

Pored menjanja sadržaja i karakteristika HTML elemenata, JavaScript jezikom je moguće menjati i sam stil prikaza elemenata. Stil elemenata se dinamički može promeniti izmenom vrednosti narednih dva svojstava:

- Svojstvo `style` predstavlja objekat koji sam sadrži veliki broj svojstava koji odgovaraju nama već poznatim CSS svojstvima. Promenom nekog od svojstava u svojstvu `style` direktno utičemo na promenu odgovarajućeg CSS svojstva. Na primer, ukoliko nad nekim elementom koji je predstavljen promenljivom `element` izvršimo naredbu `element.style.color = 'white';`, tada će se promeniti boja teksta odgovarajućeg HTML elementa na belu boju. Napomenimo da za CSS svojstva čiji nazivi predstavljaju validne JavaScript identifikatore, kao što su `color`, `border`, `padding`, itd. važi da postoje svojstva u JavaScript objektu koji predstavlja HTML element u DOM stablu sa _istim tim nazivom_. Međutim, CSS svojstva čiji nazivi sadrže crticu, kao što su `background-color`, `border-left-width`, `font-family` itd. ne predstavljaju validne JavaScript identifikatore. Zbog toga, u JavaScript objektu koji predstavlja HTML element u DOM stablu postoje svojstva čiji su nazivi dobijeni eliminisanjem crtice iz naziva CSS svojstava i kapitalizacijom prvog karaktera nakon crtice (u pitanju je takozvana _kamilja notacija_), na primer, `backgroundColor`, `borderLeftWidth`, `fontFamily`, itd.

- Svojstvo `className` predstavlja nisku koja sadrži vrednost HTML atributa `class`. Kao i sam atribut, vrednost ovog svojstva predstavlja jedna klasa ili više njih, pri čemu važi da, ukoliko želimo da elementu dodelimo više klasa, potrebno je da navedemo karakter razmaka između svakog naziva klase.

Naredni primer ilustruje promenu stila paragrafa u HTML dokumentu korišćenjem ova dva svojstva.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 4</title>

    <style>
      .paragraf {
        border: 5px salmon inset;
        padding: 10px;
      }

      .neparni {
        background-color: rgba(255, 105, 180, 0.6);
        text-transform: lowercase;
      }
    </style>
  </head>

  <body>
    <p>Paragraf sa indeksom 0</p>
    <p>Paragraf sa indeksom 1</p>
    <p>Paragraf sa indeksom 2</p>
    <p>Paragraf sa indeksom 3</p>
    <p>Paragraf sa indeksom 4</p>
    <p>Paragraf sa indeksom 5</p>
    <p>Paragraf sa indeksom 6</p>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
const paragrafi = document.getElementsByTagName('p');

for (const i in paragrafi) {
  const paragraf = paragrafi[i];

  if (i % 2 === 0) {
    // Nazivi CSS svojstava koja nemaju crticu
    // odgovaraju nazivima JavaScript objekata DOM stabla.
    paragraf.style.padding = '10px';
    paragraf.style.color = 'BlueViolet';

    // Nazivi CSS svojstava koja imaju crticu
    // transformisu se u JavaScript objektima DOM stabla
    // tako sto se crtice uklanjaju,
    // a naredno slovo nakon crtice postaje veliko (camelCase imenovanje).
    paragraf.style.backgroundColor = '#FFECA1';
    paragraf.style.textTransform = 'uppercase';
  } else {
    paragraf.className = 'neparni paragraf';
  }
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/4/index.html"
   target="_blank">Pogledaj primer uživo</a>

Na adresi [https://www.w3schools.com/jsref/dom_obj_style.asp](https://www.w3schools.com/jsref/dom_obj_style.asp){:target="\_blank"} moguće je pronaći spisak svojstava svojstva `style` čije se vrednosti mogu dinamički menjati, zajedno sa njihovim opisima.

### 5.2.3 Dinamičko dodavanje i brisanje elemenata

U ovoj sekciji ćemo opisati i demonstrirati metode definisane nad čvorovima DOM stabla koji se koriste za dinamičko kreiranje, dodavanje i brisanje elemenata koji se nalaze (ili koji treba da se nalaze) u DOM stablu.

Već smo diskutovali o svojstvima `innerHTML` i `outerHTML` koji se mogu koristiti za dodavanje elemenata (tako što se postavi njihova vrednost na nisku koja sadrži HTML kod) ili brisanje elemenata (tako što se postavi njihova vrednost na, recimo, praznu nisku). Međutim, ovo može predstavljati bezbednosni rizik jer niska koja se postavlja može sadržati kod koji ne treba biti umetnut. Dodatno, ovaj proces može biti sporiji u odnosu na ostale metode, koje ćemo izložiti o ovoj sekciji<sup>[^2]</sup>.

[^2]: Videti [testove brzine](http://jsben.ch/6uEsf){:target="\_blank"}

#### Kreiranje novih čvorova

Da bismo element dodali u DOM stablo, prvo je potrebno da ga kreiramo. U tu svrhu, na raspolaganju nam je metod `document.createElement` koja kreira jedan HTML element. Argument ovog metoda je niska koja sadrži naziv HTML elementa koji se kreira.

Međutim, kao što znamo, nisu svi čvorovi u DOM stablu HTML elementi. Metod `document.createTextNode` kreira jedan tekstualni čvor u stablu, odnosno, čvor koji sadrži tekstualni sadržaj. Argument ovog metoda je niska koja sadrži tekst koji će biti prikazan.

#### Dodavanje elemenata

Da bismo dodali novokreirani element u DOM stablo, prvo je potrebno da pronađemo roditeljski čvor u čiji sadržaj ćemo umetnuti taj element, a zatim da nad roditeljskim čvorom pozovemo metod `appendChild`. Argument ovog metoda je objekat koji predstavlja čvor koji se dodaje u DOM stablo. Napomenimo da se ovim metodom uvek dodaju čvorovi na kraj sadržaja roditeljskog elementa.

Naredni primer ilustruje dinamičko kreiranje HTML strukture koja stoji u komentaru u HTML kodu.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 5</title>
  </head>

  <body>
    <!-- <div>
        <h1>JavaScript</h1>
        <p>Super jezik, ali samo ako znamo kako se koristi :)</p>
        <ul>
            <li>Može da se koristi na klijentskoj strani</li>
            <li>Ali i na serverskoj</li>
        </ul>
    </div> -->

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
/** Funkcija kreira HTML strukturu zadatog elementa `body` korišćenjem svojstva `innerHTML`.
 *
 * @param {Body} body Element čija će HTML struktura biti dinamički kreirana.
 */
function napravi_html_strukturu_1(body) {
  body.innerHTML = `<div>
            <h1>JavaScript</h1>
            <p>Super jezik, ali samo ako znamo kako se koristi :)</p>
            <ul>
                <li>Može da se koristi na klijentskoj strani</li>
                <li>Ali i na serverskoj</li>
            </ul>
        </div>`;
}

/** Funkcija kreira HTML strukturu zadatog elementa `body` korišćenjem metoda `document.createElement` za kreiranje novih čvorova DOM stabla i metoda `appendChild` nad roditeljskim čvorom za povezivanje roditeljskog čvora i dete čvora.
 *
 * @param {Body} body Element čija će HTML struktura biti dinamički kreirana.
 */
function napravi_html_strukturu_2(body) {
  // Prvo kreiramo promenljive koje predstavljaju HTML elemente
  const div = document.createElement('div');
  const h1 = document.createElement('h1');
  const h1_text = document.createTextNode('JavaScript');
  const p = document.createElement('p');
  const p_text = document.createTextNode(
    'Super jezik, ali samo ako znamo kako se koristi :)'
  );
  const ul = document.createElement('ul');
  const li1 = document.createElement('li');
  const li1_text = document.createTextNode(
    'Može da se koristi na klijentskoj strani'
  );
  const li2 = document.createElement('li');
  const li2_text = document.createTextNode('Ali i na serverskoj');

  // A zatim iz povezemo u drvoliku strukturu
  body.appendChild(div);
  div.appendChild(h1);
  div.appendChild(p);
  div.appendChild(ul);
  h1.appendChild(h1_text);
  p.appendChild(p_text);
  ul.appendChild(li1);
  ul.appendChild(li2);
  li1.appendChild(li1_text);
  li2.appendChild(li2_text);
}

const bodies = document.getElementsByTagName('body');
if (bodies.length > 0) {
  const body = bodies[0];
  // napravi_html_strukturu_1(body);
  napravi_html_strukturu_2(body);
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/5/index.html"
   target="_blank">Pogledaj primer uživo</a>

Napomenimo da u funkciji `napravi_html_strukturu_2` nismo morali sve elemente prvo da kreiramo. Na primer, mogli smo prvo da kreiramo objekat elementa `div`, pa da ga povežemo sa roditeljskim objektom `body`. Nakon toga smo mogli da kreiramo objekat elementa `h1`, pa da ga povežemo sa roditeljskim objektom `div`, itd.

#### Brisanje elemenata

Procedura brisanja elemenata iz DOM stabla liči na proceduru umetanja elemenata: prvo je potrebno pronaći roditeljski čvor iz kojeg se brišu elementi, a zatim je nad tim elementom potrebno pozvati metod `removeChild`. Argument ovog metoda je objekat koji predstavlja dete čvor roditeljskog čvora.

Čitalac se može zapitati na koji način se može dohvatiti dete koje je potrebno obrisati. Kao i svaka druga funkcija, i metod `removeChild` prihvata objekat koji briše po referenci. To znači da nije bitan način na koji je objekat koji se briše dohvaćen. Sledi nekoliko primera načina na koji je moguće dohvatiti objekat koji se briše, a koji bi trebalo da inspiriše čitaoca da razmisli o drugim načinima:

- Jedan pristup bi mogao biti da se elementu koji se briše dodeli identifikator, pa da se iskoristi metod `document.getElementById` za dohvatanje tog objekta. Tako dohvaćeni objekat se dalje prosleđuje metodu `removeChild`.

- Neki drugi pristup bi mogao biti iteriranjem kroz svojstvo `children` roditeljskog čvora koji predstavlja niz dece čvorova koji se nalaze u sadržaju. Napomenimo da ovaj niz sadrži samo čvorove koji predstavljaju HTML elemente. Nasuprot njega, svojstvo `childNodes` predstavlja niz dece čvorova koji obuhvataju i tekstualne čvorove.

Naredni primer ilustruje drugi pristup, pri čemu se za svako dete čvor ispituje da li sadrži klasu kojom se u HTML delu koda označava da je potrebno da bude obrisano[^3].

[^3]: Zašto u JavaScript kodu koristimo metod `indexOf` nad svojstvom `className` umesto da vršimo poređenje `className === 'obrisi_mene'`?

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 6</title>
  </head>

  <body>
    <ul>
      <li class="obrisi_mene">Stavka liste 0</li>
      <li class="obrisi_mene">Stavka liste 1</li>
      <li>Stavka liste 2</li>
      <li>Stavka liste 3</li>
      <li>Stavka liste 4</li>
      <li class="obrisi_mene">Stavka liste 5</li>
      <li class="obrisi_mene">Stavka liste 6</li>
    </ul>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
/**
 * Funkcija koja određuje da li stavka liste treba biti obrisana. Funkcija proverava da li stavka liste sadrži klasu `obrisi_mene`.
 * @param {Node} stavka Element koji predstavlja stavku liste koja se proverava.
 * @returns {boolean} Rezultat ispitivanja uslova za brisanje stavke.
 */
function stavka_treba_biti_obrisana(stavka) {
  if (stavka.className.indexOf('obrisi_mene') != -1) {
    return true;
  } else {
    return false;
  }

  // Moze i samo:
  // return stavka.className.indexOf('obrisi_mene') != -1;
}

const liste = document.getElementsByTagName('ul');
if (liste.length > 0) {
  const lista = liste[0];
  const stavke = lista.children;
  const brojStavki = stavke.length;

  // Moramo da brišemo od kraja niza do početka,
  // zato što poziv removeChild menja sam niz lista.children,
  // tako da for-in i for-of petlje ne bi funkcionisale ispravno.
  for (let i = brojStavki - 1; i >= 0; --i) {
    if (stavka_treba_biti_obrisana(stavke[i])) {
      lista.removeChild(stavke[i]);
    }
  }
} else {
  console.log('Dokument nema liste!');
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/6/index.html"
   target="_blank">Pogledaj primer uživo</a>

#### Zamena postojećeg elementa drugim elementom

Nekada je potrebno da izvršimo zamenu elemenata. Na primer, ukoliko bi trebalo da sve naslove na stranici zamenimo podnaslovima, prvo bismo morali da postavimo novokreirane čvorove koji predstavljaju podnaslove na odgovarajuće pozicije (na primer, korišćenjem metoda `insertAdjacentElement` [(dokumentacija)](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement) umesto metoda `appendChild`), a zatim da obrišemo sve čvorove koji predstavljaju naslove.

Međutim, time je potrebno da kodiramo dve operacije koje implementiraju delove iste logike. Ukoliko dođe do problema u bilo kojem delu, trebalo bi da efekat bude kao da nismo učinili nikakvu izmenu, što obradu grešaka čini znatno komplikovanijom.

Na sreću, dostupan je metod `replaceChild` koji radi upravo ono što je nama potrebno. Ovaj metod ima dva argumenta: prvi argument je objekat koji će se nalaziti u DOM stablu nakon zamene, a drugi argument je objekat koji će biti obrisan iz DOM stabla nakon zamene. Slično kao i `appendChild` i `removeChild`, i ovaj metod se poziva nad roditeljskim čvorom, što znači da drugi argument mora biti objekat koji predstavlja dete roditeljskog čvora. U slučaju da dođe do greške, metod će prijaviti da je došlo do greške i nikakva izmena neće biti izvršena.

Naredni primer ilustruje korišćenje ovog metoda zamenom svih `span` elemenata `img` elementima.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 7</title>
  </head>

  <body>
    <div id="galerija_slika">
      <span>Ovde treba da bude slika širine 100px.</span>
      <p>Ovo je opis slike.</p>

      <span>Ovde treba da bude slika širine 100px.</span>
      <p>Ovo je opis slike.</p>

      <span>Ovde treba da bude slika širine 100px.</span>
      <p>Ovo je opis slike.</p>

      <span>Ovde treba da bude slika širine 100px.</span>
      <p>Ovo je opis slike.</p>
    </div>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
const galerija = document.getElementById('galerija_slika');
const elementi_galerije = galerija.children;

for (const elem of elementi_galerije) {
  // Zamenjujemo sve `span` elemente `img` elementima
  if (elem.tagName.toLowerCase() === 'span') {
    const slika = document.createElement('img');
    slika.src = 'portret.jpg';
    slika.width = 100;

    galerija.replaceChild(/* šta ubacujemo */ slika, /* šta izbacujemo */ elem);
  }
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/7/index.html"
   target="_blank">Pogledaj primer uživo</a>

### 5.2.4 Pridruživanje osluškivača događaja elementima

Većina dinamičkih klijentskih veb aplikacija podrazumeva da postoji nekakva _akcija_ koja se izvršava kada se _dogodi_ nekakva aktivnost. Primeri aktivnosti koje bi mogle da se dogode na stranici su:

- Korisnik je kliknuo mišem na dugme
- Korisnik je uneo novi karakter u polje formulara
- Korisnik je kliknuo dugme za slanje podataka iz formulara
- Veb aplikacija je završila učitavanje
- Veb aplikacija je dobila rezultat komunikacije sa serverskom aplikacijom
- ...

Kada se neka od ovih (i njima sličnih) aktivnosti dogodi u toku rada veb aplikacije, kažemo da sistem _okida_ (engl. _fire_) specijalnu vrstu signala koji se naziva _događaj_ (engl. _event_). Ispostavlja se da u JavaScript okruženju postoji sistem zasnovan na _osluškivačima_ (engl. _handler_ ili _listener_) koji predstavljaju delove koda (najčešće su u pitanju funkcije) koji se izvršavaju kada se događaj, za koji je osluškivač postavljen, okine. Implementiranje ovih delova koda od strane programera nazivamo _pridruživanje osluškivača događajima_ (engl. _registering an event handler_).

Da bismo mogli da pridružimo osluškivač događaju potrebne su nam informacije koje se dobijaju odgovaranjem na naredna tri pitanja:

1. Nad kojim HTML elementom se događaj okida?

2. Koji je naziv događaja koji se okida?

3. Koja je akcija koju je potrebno izvršiti okidanjem tog događaja nad tim elementom?

Na primer, neka je potrebno nad HTML elementom koji je predstavljen promenljivom `element`, pri okidanjem događaja `event` izvršiti funkciju `element_event`. Pridruživanje osluškivača događaja se u tom slučaju izvršava narednim pozivom metoda `addEventListener`:

```js
element.addEventListener('event', element_event);
```

Napomenimo da korišćenjem ovog pristupa možemo omogućiti da se za isti događaj više funkcija izvršava jedna za drugom jednostavno pozivanjem ovog metoda više puta:

```js
element.addEventListener('event', element_event_1);
element.addEventListener('event', element_event_2);
// itd.
```

Ukoliko od nekog trenutka više ne želimo da osluškivač bude pridružen događaju, onda možemo pozvati metod `removeEventListener` koji uklanja tačno jedan prethodno pridruženi osluškivač događaju:

```js
element.removeEventListener('event', element_event);
```

Naredni primer ilustruje pridruživanje osluškivača događaja klikom miša nad dugmićima. Funkcije koje implementiraju osluškivače će biti izvršene tek onda kada korisnik klikne na odgovarajuće dugmiće.

Datoteka `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Primer 8</title>

    <style>
      #kvadrat {
        display: block;
        width: 100px;
        height: 100px;
        border: 5px solid hotpink;
        margin: 20px;
      }

      input[type='button'] {
        width: 200px;
        height: 50px;
        margin: 20px;
        font-size: 30px;
        background-color: lightblue;
        border: 1px solid gray;
      }

      input[type='button']:active {
        background-color: rgb(137, 178, 192);
        border: 5px inset gray;
      }
    </style>
  </head>

  <body>
    <input type="button" id="uvecaj" value="+" />
    <input type="button" id="smanji" value="-" />

    <div id="kvadrat"></div>

    <script src="index.js"></script>
  </body>
</html>
```

Datoteka `index.js`:

```js
let velicina = 100;
const korak = 50;
const kvadrat = document.getElementById('kvadrat');

function uvecaj_click() {
  velicina += korak;
  kvadrat.style.width = velicina + 'px';
  kvadrat.style.height = velicina + 'px';
}

function smanji_click() {
  if (velicina - korak < 0) {
    return;
  }

  velicina -= korak;
  kvadrat.style.width = velicina + 'px';
  kvadrat.style.height = velicina + 'px';
}

if (kvadrat != null) {
  const uvecaj = document.getElementById('uvecaj');
  if (uvecaj != null) {
    uvecaj.addEventListener('click', uvecaj_click);
  }

  const smanji = document.getElementById('smanji');
  if (smanji != null) {
    smanji.addEventListener('click', smanji_click);
  }
} else {
  console.log('Ne postoji element sa identifikatorom "kvadrat"!');
}
```

<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/8/index.html"
   target="_blank">Pogledaj primer uživo</a>

Na adresi [https://developer.mozilla.org/en-US/docs/Web/Events](https://developer.mozilla.org/en-US/docs/Web/Events){:target="\_blank"} moguće je pronaći spisak svih događaja, grupisanih po kategorijama koji predstavljaju izvore okidanja tih događaja, zajedno sa njihovim opisima.

Napomenimo još i da, prilikom definisanja osluškivača, ukoliko je potrebno da dohvatimo objekat nad kojim se postavlja osluškivač, moguće je koristiti ključnu reč `this`, sa istom semantikom kao kod definisanja metoda objekta.

#### Alternativni metodi pridruživanja osluškivača događajima

Pridruživanje osluškivača događajima je moguće izvršiti i na drugi način. U pitanju je korišćenje odgovarajućih svojstava čvorova DOM stabla koji odgovaraju HTML elementima. Na primer, čvor koji odgovara elementima `input` čiji je atribut `type="button"` (dakle, dugmići) sadrži atribut `onclick` čija je vrednost funkcija koja implementira osluškivač događaja naziva `click`, odnosno, kliktaj mišem na dugme. U prethodnom primeru, umesto linije:

```js
uvecaj.addEventListener('event', uvecaj_click);
```

mogli bismo kodirati liniju:

```js
uvecaj.onclick = uvecaj_click;
```

Prednost korišćenja ovog pristupa u odnosu na `addEventListener` je u tome što je on podržaniji u starijim verzijama veb pregledača. Međutim, nedostatak ovog pristupa u odnosu na `addEventListener` jeste u tome što možemo postaviti najviše jedan osluškivač. Na primer, nakon izvršavanja koda:

```js
element.onclick = handler_1;
element.onclick = handler_2;
```

Prilikom okidanja događaja `click`, biće pozvan (tj. izvršen) samo osluškivač koji implementira funkcija `handler_2`, dok je osluškivač koji implementira funkcija `handler_1` izgubljen. Postoje načini da se ovo prevaziđe, ali svaki od njih uvodi nove probleme, pri čemu nijedan od njih problema ne daje elegantno rešenje u odnosu na korišćenje pristupa zasnovan na metodima `addEventListener` i `removeEventListener`.

### 5.2.5 Obrada podataka u formularu

U [poglavlju 1](../HTML/README.md) bilo je reči o HTML elementima kojima predstavljamo različita polja za unos podataka. Sada ćemo videti kako možemo dohvatati podatke iz formulara i testirati njihove vrednosti u odnosu na predefinisane domene. Više reči o tome kako se podaci iz formulara šalju ka serveru biće kada budemo pričali o načinu obrađivanja podataka na serveru.

U nastavku ćemo koristiti formular koji smo ranije napravili i izgleda kao na slici:

<div style="max-width: 98%;">
<img style="max-width: 100%;" src="./Slike/formular.png" alt="">
</div>

Odgovarajući kod za formular sa slike možete pronaći [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Primeri/9/index.html).

Pre nego što pređemo obradu formulara, primetimo da element `form` ima postavljen atribut `novalidate`. Ovaj atribut, poput prethodno pomenutih atributa `checked` i `readonly`, ne dobija vrednost već samo navođenje tog atributa elementu označava da element ima to svojstvo. Ukoliko formularu dodamo ovaj atribut onda se neće vršiti automatska provera unetih vrednosti. Podrazumevano ponašanje je provera svakog polja da li zadovoljava uslove koji su postavljeni atributima.

Prvo što treba da uradimo jeste da dohvatimo formular. To možemo učiniti preko identifikatora `formular` koji smo mu prethodno zadali korišćenjem metode `querySelector` ili `getElementById`.

```js
const f = document.querySelector('#formular');
```

Na nivou formulara je definisan događaj `'submit'` koji se izvršava nakon što korisnik klikne na element `<input type="submit">` koji se nalazi u sadržaju tog formulara. Pri završetku osluškivača koji se postavlja nad tim događajem, veb pregledač šalje podatke iz formulara na adresu naznačenu atributom `action` formulara. Metod slanja podataka tim HTTP zahtevom se definiše atributom `method` tog formulara, a njegove vrednosti mogu biti `GET` ili `POST`, koje odgovaraju istoimenim HTTP metodima. Međutim, moramo razumeti kako je potrebno sprečiti veb pregledač da pošalje ovaj zahtev u slučaju da dođe do problema u validaciji podataka u formularu.

Ono o čemu nismo diskutovali kada smo govorili o događajima jeste da funkcija koja predstavlja osluškivač nad nekim događajem može prihvatati i jedan parametar (u kodu ispod `ev`). Ovaj parametar predstavlja objekat koji sadrži razne informacije o samom događaju koji je okinut nad formularom. Ukoliko osluškivač za akciju `submit` pridružujemo korišćenjem metoda `addEventListener()`, u slučaju greške potrebno je da sprečimo podrazumevano ponašanje, što je upravo slanje podataka, a to činimo pozivom metoda `preventDefault()` nad događajem `ev`.

Za početak možemo odrediti promenljivu u koju ćemo smestiti trenutni element koji obrađujemo kao i promenljivu u koju smeštamo element za greške.

```js
f.addEventListener('submit', function (ev) {
  // Pomocna promenljiva
  let polje;

  // U okviru polja za gresku bice upisivane greske
  const greska = document.querySelector('#greska');

  // U nastavku kod ide ovde ...
});
```

Krenimo redom po formularu i ispitujmo svako od polja. Ukoliko naiđemo na neku neregularnost, dovoljno je da vratimo vrednost `false` u ovoj funkciji. Ime i prezime korisnika je obavezno polje. Očekuje se da dužina bude manja od _30_, tj. od vrednosti atributa `maxlength`. Kada dohvatimo polje formulara, njegovi atributi su nam dostupni kao svojstva odgovarajućeg objekta. Zato možemo pristupati svojstvima `value` i `maxLength` u narednom fragmentu koda:

```js
polje = document.querySelector('#ime_prezime');
const imePrezime = polje.value.trim();
const maxDuzina = polje.maxLength || 30;
if (imePrezime === '' || imePrezime.length > maxDuzina) {
  // Obrada greške se može sastojati od narednih koraka:
  // 1. Prijavi korisniku da je došlo do greške (opciono, ali korisno)
  greska.textContent = 'Nekorektna vrednost u polju za ime i prezime!';
  // 2. Fokusiraj korisniku polje za koje validacija nije prošla (opciono, ali korisno)
  polje.focus();
  // 3. Spreči propagiranje događaja 'submit' nadalje (obavezno)
  ev.preventDefault();
  // 4. Prekini dalju validaciju (obavezno)
  return false;
}
```

Pošto se element nalazi na vrhu stranice, a sam formular je malo veći i na manjim uređajima neće biti vidljivi svi elementi u istom trenutku, u slučaju greške možemo staviti element koji sadrži neispravnu vrednost u fokus kako bi korisniku odmah bio prikazan element koji treba da izmeni. U te svrhe koristimo metod `focus` koji pozivamo nad elementom koji želimo da stavimo u fokus odnosno da se pozicioniramo na stranici tako da taj element bude vidljiv.

Datum rođenja korisnika treba da bude oblika `gggg-mm-dd`. Metod `substr`, definisan nad niskama, vraća podnisku date niske i prihvata dva argumenta: prvi je indeks od kojeg podniska počinje, a drugi je broj karaktera, tj. dužina željenje podniske. Podsetimo se, funkcija `Number.parseInt` konvertuje broj koji je zapisan kao niska u numeričku vrednost. Slično, dostupna je funkcija `Number.parseFloat`. Ukoliko konverzija ne uspe, rezultat je `NaN`.

```js
polje = document.querySelector('#datum_rodjenja');
const datumRodjenja = polje.value;
const godina = parseInt(datumRodjenja.substr(0, 4));
const mesec = parseInt(datumRodjenja.substr(5, 2));
const dan = parseInt(datumRodjenja.substr(8, 2));

if (
  isNaN(dan) ||
  isNaN(mesec) ||
  isNaN(godina) ||
  dan < 1 ||
  dan > 31 ||
  mesec < 1 ||
  mesec > 12 ||
  godina < 0
) {
  greska.textContent = 'Nekorektna vrednost u polju za datum rodjenja!';
  polje.focus();
  ev.preventDefault();
  return false;
}

if (datumRodjenja.charAt(4) != '-' || datumRodjenja.charAt(7) != '-') {
  greska.textContent = 'Datum rodjenja treba da bude u formatu gggg-mm-dd';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Email adresa korisnika treba da sadrzi karakter `@` i barem jednu tačku nakon tog karaktera. Metod `indexOf` vraća prvo pojavljivanje niske koja je zadata kao argument u niski nad kojom se poziva. Ukoliko niska-argument ne postoji u datoj niski, onda funkcija vraća `-1`. Slično, metod `lastIndexOf` vraća poslednje pojavljivanje niske-argumenta.

```js
polje = document.querySelector('#email');
const email = polje.value;
const manki = email.indexOf('@');
const poslednjaTackica = email.lastIndexOf('.');

if (manki === -1 || poslednjaTackica === -1 || poslednjaTackica < manki) {
  greska.textContent = 'Nekorektna vrednost u polju za email adresu.';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Url adresa korisnika treba da pocinje sa `http://`.

```js
polje = document.querySelector('#veb_adresa');
const vebAdresa = polje.value;

if (vebAdresa.substr(0, 7) != 'http://') {
  greska.textContent = 'Nekorektna vrednost u polju za veb adresu.';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Korisničko ime korisnika je obavezno polje. Treba da se sastoji samo od malih i velikih slova i da bude dužine barem _5_ karaktera. Metod `String.fromCharCode` konstruiše nisku koja sadrži karakter čiji je kod zadat brojem koji se prosleđuje kao argument.

```js
polje = document.querySelector('#username');
const korisnickoIme = polje.value.trim();

if (korisnickoIme.length < 5) {
  greska.textContent = 'Korisnicko ime nije dovoljno dugo.';
  polje.focus();
  ev.preventDefault();
  return false;
}

const malaSlova = [];
const velikaSlova = [];
for (let i = 0; i < 26; ++i) {
  malaSlova[i] = String.fromCharCode(97 + i);
  velikaSlova[i] = String.fromCharCode(65 + i);
}

for (let i = 0; i < korisnickoIme.length; ++i) {
  const tekuciKarakter = korisnickoIme.charAt(i);

  if (
    malaSlova.indexOf(tekuciKarakter) === -1 &&
    velikaSlova.indexOf(tekuciKarakter) === -1
  ) {
    greska.textContent = 'Nedozvoljeni karakter u polju za korisnicko ime.';
    polje.focus();
    ev.preventDefault();
    return false;
  }
}
```

Pre nego što vidimo kod za validaciju šifre, napomenimo da smo definisali funkciju koja izračunara broj cifara u datoj niski. Ova funkcija će nam biti korisna za dalju validaciju.

```js
/**
 * Izračunava broj cifara koje se nalaze u datoj niski.
 * @param {string} vrednost niska
 * @returns broj cifara u niski `vrednost`
 */
function prebrojCifre(vrednost) {
  let brojCifara = 0;
  for (let i = 0; i < vrednost.length; ++i) {
    const tekuciKarakter = vrednost.charAt(i);
    if ('0123456789'.indexOf(tekuciKarakter) !== -1) {
      ++brojCifara;
    }
  }

  return brojCifara;
}
```

Šifra korisnika je obavezna i mora da sadrži barem dve cifre.

```js
polje = document.querySelector('#password');
const sifra = polje.value.trim();

if (sifra === '') {
  greska.textContent = 'Polje za sifru je obavezno.';
  polje.focus();
  ev.preventDefault();
  return false;
}

const brojCifara = prebrojCifre(sifra);

if (brojCifara < 2) {
  greska.textContent = 'Polje za sifru mora da sadrzi barem dve cifre.';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Polje za fakultet mora biti odabrano. Da bismo za element `select` dohvatili indeks vrednosti koja je odabrana, možemo nad odgovarajućim objektom dohvatiti svojstvo `selectedIndex`. Ukoliko je ova vrednost jednaka _0_, nijedna opcija nije odabrana.

```js
polje = document.querySelector('#fakultet');

if (polje.selectedIndex === 0) {
  greska.textContent = 'Odaberite fakultet.';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Godina studija mora biti odabrana. Do sada smo sve elemente formulara dohvatali putem njihovih identifikatora. Umesto ovog pristupa, pokažimo jedan novi CSS selektor koji se češće koristi za elemente formulara, na primer, radio dugmad. Da bismo dohvatili sve `input` elemente koji imaju postavljen odgovarajući atribut, na primer, `name="godina"`, možemo koristiti selektor oblika `element[atribut='vrednost']`, tj. u ovom slučaju `input[name='godina']`. Očigledno pošto ovakvih elemenata može biti više (radio dugmad ne bi imalo smisla koristiti kada bi postojao samo jedan odabir, te ih uvek ima više od jednog), koristićemo metod `querySelectorAll`. Za svako radio dugme možemo ispitati da li je izabrano tako što pristupimo njegovom svojstvu `checked` koje predstavlja Bulovu vrednost.

```js
let indikatorGodine = false;
polje = document.querySelectorAll('input[name="godina"]');

for (let i = 0; i < polje.length; ++i) {
  let godina = polje[i];

  if (godina.checked) {
    indikatorGodine = true;
    break;
  }
}

if (!indikatorGodine) {
  greska.textContent = 'Godina studija je obavezno polje.';
  polje.focus();
  ev.preventDefault();
  return false;
}
```

Polja lista interesovanja i napomena su opciona, tako da smo ovime završili obradu podataka u ovom formularu.

Osim reagovanje na akciju slanja podataka, možemo dodati i reagovanje na događaj kojim se sadržaj polja u formularu vraćaju na podrazumevana, tako što postavimo osluškivač nad događajem `reset`. Slično kao i za `submit`, povratna vrednost funkcije koja se postavlja za osluškivač određuje da li će sadržaj polja u formularu biti vraćena na podrazumevane vrednosti ili ne. Ukoliko bismo, na primer, želeli da korisnik odabere da li želi zaista da resetuje formular, možemo implementirati osluškivač tako što u njemu iskoristimo funkciju `window.confirm` koja će prikazati prozor sa dugmićima "OK" i "Cancel" i tekstom koji je prosleđen kao argument. Ako korisnik klikne na "OK", funkcija vraća `true`, a inače vraća `false`.

```js
f.addEventListener('reset', function (ev) {
  const treba_resetovati = window.confirm('Da li zelite da ponistite unos?');

  if (!treba_resetovati) {
    ev.preventDefault();
    return false;
  }
  return true;
});
```

Takođe, moguće je postaviti i osluškivače nad samim elementima formulara. Neki od zanimljivih događaja za koje se mogu postaviti osluškivači su:

- Događaj `'focus'` se ispaljuje kada je element u fokusu. Element može dobiti fokus ako, na primer, mišem kliknemo na taj element.

- Događaj `'blur'` se ispaljuje kada element izgubi fokus.

- Događaj `'change'` se ispaljuje kada element izgubi fokus i, pritom, vrednost polja elementa se izmenila.

- Događaj `'input'` se ispaljuje kada se elementu promeni vrednost. Na primer, svakim unosom ili brisanjem karaktera biće ispaljen ovaj događaj.

Naravno, ovo su samo neki od tih događaja. Za detaljniju listu događaja možete posetiti adresu [https://developer.mozilla.org/en-US/docs/Web/Events](https://developer.mozilla.org/en-US/docs/Web/Events){:target="\_blank"}.

Opisane događaje ćemo ilustrovati nad elementom formulara u kojem korisnik unosi lozinku:

```js
const s = document.getElementById('password');

s.addEventListener('focus', function () {
  const brojCifara = prebrojCifre(this.value.trim());
  // Ukoliko šifra ne ispunjava uslove, prikazujemo poruku.
  if (brojCifara < 2) {
    upozorenje.style.display = 'block';
  }
});

s.addEventListener('blur', function () {
  // Kada element izgubi fokus, sakrivamo poruku.
  upozorenje.style.display = 'none';
});

s.addEventListener('change', function () {
  const brojCifara = prebrojCifre(this.value.trim());
  // Ukoliko šifra ne ispunjava uslove,
  // prikazujemo poruku u obaveštajnom prozoru.
  // Poruka se prikazuje nakon što element izgubi fokus,
  // ukoliko je vrednost polja izmenjena.
  if (brojCifara < 2) {
    window.alert('Šifra mora da sadrži bar dve cifre!');
  }
});

s.addEventListener('input', function () {
  const upozorenje = document.getElementById('upozorenje');
  const sifra = this.value.trim();
  const brojCifara = prebrojCifre(sifra);

  // Ukoliko šifra ne ispunjava uslove, prikazujemo poruku.
  if (brojCifara < 2) {
    upozorenje.style.display = 'block';
  }
  // Ukoliko je uslov ispunjen, sakrivamo poruku.
  else {
    upozorenje.style.display = 'none';
  }
});
```

Celo rešenje je dato [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Primeri/9/index.js).

## 5.3 Osnovni elementi asinhronog programiranja. Odlaganje izvršavanja funkcija.

Za većinu kodova koje smo do sada videli kažemo da se izvršavaju *sinhrono*, odnosno, da se sve radnje u njima izvršavaju sekvencijalno, tj. jedna za drugom. Na primer, pogledajmo naredni kod: 

```js
function f1() { /* ... */ }
function f2() { /* ... */ }
function f3() { /* ... */ }

f1();
f2();
f3();
```

Ovaj kod se izvršava sinhrono. To zapravo znači da poziv funkcije `f2` neće biti izvršen sve dok se ne završi izračunavanje funkcije `f1`. Takođe, funkcija `f3` neće biti pozvana sve dok se ne završi izračunavanje funkcije `f2`.

Kada pozovemo funkciju koja izvršava neku akciju, ona se vraća tek kada je akcija završena i tada može da vrati neki rezultat. Ovim se program stopira za ono vreme koliko je bilo potrebno toj akciji da se završi. Ovo može biti potencijalno problematično. Pogledajmo naredni kod:

```js
/* ... */
function dohvatiPodatkeSaInterneta() { 
  pošaljiZahtev(); 
  const podaci = čekajDokNeStignuPodaci(); 
  return podaci; 
}
function uradiNekuSkupuOperacijuSaPodacima(podaci) { /* ... */ }
function prikažiGlavniDeoStranice() { /* ... */ }

const podaci = dohvatiPodatkeSaInterneta();
uradiNekuSkupuOperacijuSaPodacima(podaci);
prikažiGlavniDeoStranice();
```

Kao što smo rekli, da bi se funkcija `prikažiGlavniDeoStranice` izvršila, prvo moraju da se u celosti izvrše funkcije `dohvatiPodatkeSaInterneta` i `uradiNekuSkupuOperacijuSaPodacima`, tim redosledom. Ako izračunavanje ovih funkcija traje (relativno) dugo, na primer, 15 sekundi, onda će korisnik prilikom otvaranja veb stranice u pregledaču gledati 15 sekundi u prazan ekran, pre nego što se pozove funkcija `prikažiGlavniDeoStranice` koja prikazuje glavni sadržaj stranice.

U prethodnom primeru koda, rešenje ovog problema je poprilično jednostavno. Sve što je potrebno da uradimo jeste da promenimo redosled poziva funkcija, tako da se one "važnije" funkcije pozovu prve, a one koje su "manje važne" pozovu nakon njih. Dakle:

```js
prikažiGlavniDeoStranice();
const podaci = dohvatiPodatkeSaInterneta();
uradiNekuSkupuOperacijuSaPodacima(podaci);
```

Međutim, ovo nije uvek moguće. Aplikacije koje se programiraju u praksi se sastoje od desetine hiljada funkcija. Odrediti poredak izvršavanja ovih funkcija po "važnosti" je praktično nemoguće. Umesto toga, potrebno je promeniti implementaciju funkcija tako da koriste tzv. asinhroni model izvršavanja koda.

Osnovna ideja *asinhronog* modela programiranja jeste da, umesto da program čeka na neka izračunavanja (na primer, da čeka da se podaci dohvate sa interneta) dok ima drugog posla, on će izvršavati ostale funkcije koje može odmah da izračuna. Onoga trenutka kada "pristignu" izračunavanja, tek tada će pozvati funkcije koje su čekale na ta izračunavanja.

Pogledajmo sada neke delove Web API biblioteke kojima možemo ostvariti asinhrono izvršavanje koda. U nastavku teksta ćemo videti dva mehanizma: odlaganje izvršavanja funkcija i kontaktiranje serverskih aplikacija putem HTTP protokola.

### 5.3.1 Odlaganje izvršavanja funkcija. Funkcije povratnih poziva.

Jedan pristup asinhronom programiranju jeste da se funkcije koje izvršavaju duge ili spore akcije konstruišu tako da prihvataju dodatni argument koji predstavlja tzv. *funkciju povratnog poziva* (engl. *callback function*). Takve akcije se započnu, a zatim kada se završe, funkcija povratnog poziva se poziva sa rezultatom te akcije. Ako bolje pogledamo, ova semantika u potpunosti oslikava asinhroni model programiranja koji smo opisali u uvodu.

Kao primer ovog modela, možemo razmotriti funkciju `setTimeout`, dostupnu i u veb pregledačima i u Node.js platformi, koja prihvata dva argumenta: funkciju povratnog poziva i broj milisekundi. Ova funkcija postavlja tajmer koji traje prosleđeni broj milisekundi i po isteku tajmera, poziva se prosleđena funkcija povratnog poziva:

```js
console.log('Start!');
setTimeout(function() {
  console.log('Tick');
}, 2000);
```

Ako otvorimo konzolu, prvo što ćemo primetiti jeste da se ispiše:

```js
Start!
```

Nakon dve sekunde, ispis se menja u 

```js
Start!
Tick
```

Vidimo da se anonimna funkcija povratnog poziva koju smo prosledili funkciji `setTimeout` izvršila asinhrono, u ovom slučaju, tek nakon što je istekao tajmer koju je postavila funkcija `setTimeout`.

Slično, metod `setInterval` omogućava učestalo izvršavanje zadate funkcije povratnog poziva kao prvi argument u pravilnim vremenskim razmacima čija se perioda zadaje drugim argumentom. Za upravljanje ovim pozivima koristi se povratna vrednost metoda. Pre svega, pozivom metoda `clearInterval`, kojem se prosleđuje povratna vrednost metoda `setInterval`, može se prekinuti dalje ponavljanje poziva. Na primer:

```js
// Ispiši Tick! svake sekunde
const si = setInterval(function() {
  console.log('Tick!');
}, 1000);

// Nakon 5 sekundi, prekini dalje ispisivanje
setTimeout(function() {
  clearInterval(si);
}, 5500);
```

Rezultat ispisa:

```js
Tick!
Tick!
Tick!
Tick!
Tick!
```

## 5.4 Komunikacija sa serverskim aplikacijama putem HTTP protokola. `XMLHttpRequest` objekti.

Za izvršavanje koda u ostatku ove sekcije, neophodno je u direktorijumu gde se nalaze ovi primeri pokrenuti veb server. Ukoliko samo otvorimo `.html` datoteku u veb pregledaču, on će koristiti `file://` protokol za učitavanje te datoteke. Međutim, neki od primera koriste HTTP komunikaciju za dohvatanje podataka (kako bi se ilustrovala asinhronost akcija kroz praktične primere), te je neophodno pristupati primerima preko `http://`
protokola. Ovo možemo najjednostavnije uraditi u alatu `Visual Studio Code`, u okviru kojeg je dostupna ekstenzija naziva `Live Server` autora Ritvik Deja (eng. Ritwick Dey). Nakon instalacije ekstenzije, potrebno je otvoriti direktorijum sa primerima u `Visual Studio Code` alatu. Zatim, desnim klikom na datoteku koju želimo da otvorimo (na primer, `index.html`) otvoriti pomoćni meni iz koga je potrebno odabrati opciju `Open with Live Server`. Alternativno, moguće je aktivirati `Live Server` klikom na dugme `Go Live` u statusnoj liniji alata. Ako se otvorio veb pregledač na adresi `http://127.0.0.1:5500/`, onda je veb server korektno pokrenut.Poželjno je otvoriti i konzolu u alatima za razvijanje.

Da bismo poslali asinhroni HTTP zahtev ka nekom resursu (ovakvi zahtevi se još nazivaju i *AJAX* zahtevi, skraćeno od *Asynchronous JavaScript And XML*), potrebno je kreirati objekat klase `XMLHttpRequest`, otvoriti url ka resursu, i poslati zahtev. Nakon što se od serverske aplikacije stigne HTTP odgovor, objekat će sadržati korisne informacije poput tela HTTP odgovora i statusnog koda. Ovaj objekat prolazi kroz razna stanja, kao što je "otvorena konekcija", "finalno stanje" i dr. Svako stanje ima svoj kod.

Kao što smo rekli, prvo je potrebno kreirati objekat, koji se inicijalizuje u stanje `UNSET` (kod je *0*):

```js
let xhr = new XMLHttpRequest();
```

Zatim je potrebno formirati HTTP zahtev pozivom metoda `open`. Njegovi argumenti su: 
1. HTTP metod koji se koristi, 
2. URL resursa,
3. Bulova vrednost koja označava da li se zahtev vrši sinhrono ili asinhrono (podrazumevana vrednost je `true`, što označava asinhronost, te ga nije potrebno navesti). Metod ima i dodatne argumente za korisničko ime i lozinku.

```js
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts/');
```

U ovom trenutku se mogu postaviti zaglavlja HTTP zahteva pomoću `setRequestHeader` metode, na primer, `xhr.setRequestHeader(imePolja, vrednost)`. Zatim je potrebno dodati funkcije povratnog poziva koje će vršiti nekakvu obradu pristiglog odgovora ili, ono što se često radi, obradu pri promeni stanja asinhronog zahteva. 

Odgovor zahteva je sadržan u svojstvima `response`, `responseText` ili `responseXML` u zavisnosti od tipa odgovora. U slučaju greške, svojstvo `statusText` sadrži statusnu poruku koja odgovara HTTP statusnoj poruci. Na primer:

```js
xhr.addEventListener('load', function() {
  // Proveravamo da li je odgovor servera sa vrednoscu 200 preko polja zahteva status.
  if (xhr.status === 200) {
    console.log(xhr.response);
  } 
  else {
    console.error(xhr.statusText);
  }
});
```

Događaj `'load'` se izvršava kada objekat pređe u finalno stanje `DONE` (kod je *4*). Događaj `error` se izvršava kada dođe do greske prilikom zahteva:

```js
xhr.addEventListener('error', function() {
  console.error('Problem prilikom slanja zahteva');
});
```

Alternativa je moguća postavljanjem osluškivača nad događajem `readystatechange` koji će pozvati funkciju povratnog poziva prilikom svake promene stanja:

```js
xhr.addEventListener('readystatechange', function() {
  switch(xhr.readyState) {
    case XMLHttpRequest.DONE:
      if (xhr.status === 200) {
        console.log(xhr.response);
      }
      else {
        console.error(xhr.statusText);
      }
  }
});
```

Konačno, potrebno je poslati HTTP zahtev, što se vrši metodom `send`. U zavisnosti od tipa zahteva, opcioni argument metode `send` predstavlja telo zahteva.

```js
xhr.send();
```

Celokupan kod je dat u nastavku:

```js
let xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts/');
xhr.addEventListener('readystatechange', function() {
  switch(xhr.readyState) {
    case XMLHttpRequest.DONE:
      if (xhr.status === 200) {
        console.log(xhr.response);
      }
      else {
        console.error(xhr.statusText);
      }
  }
});
xhr.send();
```

Iako jednostavan, ovaj primer ilustruje važan koncept, a to je kreiranje komunikacije između klijentskih i serverskih aplikacija korišćenjem `XMLHttpRequest` objekta. Na ovu temu ćemo se osvrnuti još jednom, kada se budemo upoznali sa kreiranjem naših serverskih aplikacija.

### 5.4.1 Rad sa podacima u JSON formatu

_JavaScript Object Notation_ (skr. _JSON_) predstavlja standardni format teksta koji služi za reprezentaciju podataka, zasnovan na JavaScript sintaksi zapisivanja objekata. JSON se često koristi za razmenu podataka između veb aplikacija (na primer, za slanje podataka od serverske aplikacije ka klijentskoj aplikaciji, kako bi se ti podaci prikazali na veb stranici, ili obrnuto, za slanje podataka od klijentske aplikacije ka serverskoj aplikaciji kako bi se ti podaci skladištili u nekoj bazi podataka). Iako JSON sintaksa vrlo liči na sintaksu zapisivanja JavaScript objekata, JSON se koristi potpuno nezavisno od samog jezika JavaScript, i razni programski jezici ili biblioteke implementiraju mogućnost za upravljanje podacima zapisanim u JSON formatu. Naravno, mi ćemo se u nastavku fokusirati na upotrebu JSON formata u programskom jeziku JavaScript.

Kada kažemo da su neki podaci zapisani u JSON formatu, zapravo mislimo da su ti podaci zapisani u nekakvoj niski. Da bismo išta mogli da uradimo sa tim podacima, potrebno je da ih prvo pretvorimo u JavaScript objekte. Naravno, važno je da postoje mehanizmi za pretvaranje već izračunatih i pripremljenih podataka u JSON niske. 

JSON niska se može čuvati u datoteci, što je u susštini obična tekstualna datoteka sa ekstenzijom `.json`. Podaci zapisani u JSON formatu imaju MIME tip `application/json`.

#### Pretvaranje između JavaScript vrednosti i JSON niski

Kao u prethodnom primeru kad smo dohvatali informacije sa interneta, često dobijamo kao odgovor JSON nisku, koju je potrebno da konvertujemo u odgovarajuću JavaScript vrednost. Takođe, kada želimo da pošaljemo neke podatke putem mreže, potrebno je da ih konvertujemo u JSON nisku pre slanja. Na sreću, u JavaScript jeziku postoje ugrađeni mehanizmi za obradu JSON niski. Za ove potrebe ćemo koristiti ugrađeni objekat `JSON`, dostupan u veb pregledačima, koji sadrži naredna dva metoda:

- `parse()`: Prihvata JSON nisku kao parametar i vraća JavaScript vrednost kao rezultat.
- `stringify()`: Prihvata JavaScript vrednost kao argument i vraća JSON nisku.

Možemo prikazati korišćenje prvog metoda kroz ažuriranu verziju prethodnog primera. Ova verzija radi istu stvar kao i malopre - dohvata podatke sa serverske aplikacije - ali ovoga puta koristimo metod `parse()` kako bismo pretvorili rezultat u JavaScript vrednost, nad kojom možemo izvršiti nekakvu akciju:

```js
let xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts/');
xhr.addEventListener('readystatechange', function() {
  switch(xhr.readyState) {
    case XMLHttpRequest.DONE:
      if (xhr.status === 200) {
        const stringJSON = xhr.response;
        console.log(stringJSON, typeof stringJSON);
        // Pretvaranje niske zapisane u JSON formatu u JavaScript vrednost
        const posts = JSON.parse(stringJSON);
        console.log(posts, typeof posts);

        for (const post of posts) {
          document.body.innerHTML += `<p>${post.id}. ${post.title}</p>`;
        }
      }
      else {
        console.error(xhr.statusText);
      }
  }
});
xhr.send();
```

Kao što možete pretpostaviti, `JSON.stringify()` radi na suprotan način. Naredni JavaScript kod će pretvoriti vrednost promenljive `myObj`, što je objekat koji živi u memoriji veb pregledača, u nisku `myString` koja predstavlja tekstualnu reprezentaciju tog objekta, zapisanu u JSON formatu.

```js
let myObj = { name: "Chris", age: 38 };
console.log(myObj, typeof myObj);

// Pretvaranje JavaScript vrednosti u nisku zapisanu u JSON formatu
let myString = JSON.stringify(myObj);
console.log(myString, typeof myString);
```

#### JSON struktura

Kao što smo opisali iznad, JSON predstavlja format zapisa niske koji veoma liči na notaciju zapisivanja JavaScript objekata. U ovom formatu možemo zapisati neke osnovne tipove podataka, kao što bismo i u standardnom JavaScript objektu - niske, brojeve, nizove, Bulove vrednosti i druge objekte. Ovo nam omogućava da kreiramo kompleksne hijerarhije podataka, na primer:

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

Ako bismo nisku iznad učitali u JavaScript program, a zatim ga parsirali u promenljivu `superHeroes`, onda bismo mogli da pristupimo podacima unutar parsiranog objekta korišćenjem tačka-notacije ili notacije sa uglastim zagradama. Na primer:

```js
superHeroes.homeTown
superHeroes['active']
```

Ako želimo da pristupimo podacima koji su dublje u hijerarhiji, možemo ulančavati nazive svojstava i indekse nizova, koliko god je to neophodno. Na primer, ako želimo da pristupimo trećoj supermoći drugog heroja iz liste, to bismo uradili izrazom:

```js
superHeroes.members[1]['powers'][2]
```

Kod za ovaj primer možete pronaći [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Primeri/10/superHeroes.html).

#### Nizovi u JSON

JSON niska ne mora sadržati samo objekte na vrhu hijerarhije podataka, već može imati i nizove. Niska koja je zapisana ispod takođe predstavlja validnu JSON nisku:

```json
[
  {
    "name": "Molecule Man",
    "age": 29,
    "secretIdentity": "Dan Jukes",
    "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
  },
  {
    "name": "Madame Uppercut",
    "age": 39,
    "secretIdentity": "Jane Wilson",
    "powers": [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```

Da bismo pristupili nekom podatku, potrebno je da prvo pristupimo objektu na odgovarajućem indeksu (naravno, nakon parsiranja niske). Na primer, ako je niska iznad parsirana u promenljivu `superHeroes`, onda možemo pristupiti prvoj moći prvog superheroja pomoću izraza `superHeroes[0]["powers"][0]` ili `superHeroes[0].powers[0]`.

Kod za ovaj primer možete pronaći [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Primeri/11/superHeroes.html).

#### Napomene

- JSON predstavlja format za zapisivanje podataka - on ne može da čuva vrednosti funkcija ili `undefined` vrednosti.
- JSON zahteva da se oko svih niski navode dvostruki navodnici.
- Za razliku od JavaScript-a gde nazivi svojstava u objektima ne moraju imati navodnike, u JSON formatu svi nazivi svojstava obavezno moraju biti obavijeni dvostrukim navodnicima.
- Čak i jedna pogrešno zapisana zapeta ili dvotačka može da poremeti ceo format i da parsiranje ne bude uspešno. Zbog toga bi trebalo validirati niske pre slanja drugim veb aplikacijama (mada, automatski-generisane niske pomoću biblioteka će ređe imati greške). Ručno zapisane JSON niske je moguće validirati poput alata kao što je [JSONLint](http://jsonlint.com/).
- JSON niska može čuvati i jednostavne vrednosti, ne samo nizove i objekte. Na primer, ako niska zapisana u JSON formatu sadrži samo jednu nisku ili jedan broj, onda je ona validna JSON niska.

## 5.3 Zadaci za vežbu

> Zadatak 1: Potrebno je implementirati klijentsku aplikaciju koja prikazuje preporučene knjige. Neka je dat niz objekata, pri čemu svaki objekat sadrži naredne podatke o knjigama: naziv knjige, autor, isbn, godina izdavanja i URL do slike prednjih korica. U programskom jeziku JavaScript:
1. Napisati funkciju `kreirajDOMPodstabloZaKnjigu(knjiga)` koja prihvata objekat koji sadrži podatke o jednoj knjizi. Na osnovu ovog objekta je potrebno izgraditi DOM podstablo tako da svaka knjiga bude prikazana kao na narednoj slici. Zabranjeno je korišćenje `innerHTML` i `outerHTML` atributa. Sva stilizovanja uraditi putem `style` atributa.
![](./Zadaci/zadatak1/postavke.png)
2. Napisati funkciju `prikažiSveKnjige(nizKnjiga)` koja prikazuje knjige iz prosleđenog niza u `div` elementu čiji je identifikator `preporuceneKnjige`. Ako ovakav element ne postoji, prikazati korisniku poruku u obaveštajnom prozoru. Koristiti funkciju napisanu pod 1.

Rešenje zadatka možete pronaći [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Zadaci/zadatak1/).

> Zadatak 2: Napisati HTML datoteku koja sadrži dva naslova, "Types" i "Toppings", praznu tabelu ispod prvog naslova i praznu listu ispod drugog naslova. Napisati JavaScript kod koji šalje asinhroni HTTP GET zahtev na <a href="https://codepen.io/chriscoyier/pen/EAIJj.js">https://codepen.io/chriscoyier/pen/EAIJj.js</a>. U slučaju da je sve prošlo bez greške, prikazati podatke iz odgovora u formatu kao na narednoj slici. U slučaju neuspešnog zahteva ispisati odgovarajuću poruku.

![](./Zadaci/zadatak2/postavke.png)

Rešenje zadatka možete pronaći [ovde](https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Zadaci/zadatak2/).

<div class="domaci-zadatak">
    <span class="naslov">Domaći zadatak 1</span> 
    <div class="tekst">
        <p>Neka je data datoteka <a href="https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Domaci/Resursi/zadatak1/index.html">index.html</a> koja predstavlja osnovu klijentske veb aplikacije.</p>

<p>Zadatak je da implementiramo klijentsku veb aplikaciju koja ispunjava naredni opis. Klikom na dugme “Prikaži podatke” na stranici se prikazuju informacije o studentima u vidu tabele. Prelaskom miša preko neke od ćelija u prvoj koloni (odnosno, ćelija koje sadrže indekse), želimo da se postavi pozadinska boja te ćelije na sivu. Klikom na neku od ćelija koja sadrži indeks, želimo da se u elementu pored tabele prikažu informacije o odabranom studentu.</p>

<p><strong><em>Implementacioni detalji zadatka</em></strong></p>

<p>Sva rešenja čuvati u datoteci `index.js`.</p>

<p>a) Kreirati promenljivu `studenti` koja treba da sadrži podatke o studentima iz naredne tabele. Koristiti odgovarajuće tipove podataka za predstavljanje datih vrednosti. Ova promenljiva se koristi u narednim zahtevima.</p>

<table>
  <thead>
    <tr>
      <th>indeks</th>
      <th>ime</th>
      <th>prezime</th>
      <th>datum_rodjenja</th>
      <th>mesto_rodjenja</th>
      <th>datum_upisa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>20140021</td>
      <td>Milos</td>
      <td>Peric</td>
      <td>20.01.1995.</td>
      <td>Beograd</td>
      <td>06.07.2014.</td>
    </tr>
    <tr>
      <td>20140022</td>
      <td>Marijana</td>
      <td>Savkovic</td>
      <td>11.03.1995.</td>
      <td>Kraljevo</td>
      <td>05.07.2014.</td>
    </tr>
    <tr>
      <td>20130023</td>
      <td>Sanja</td>
      <td>Terzic</td>
      <td>09.11.1994.</td>
      <td>Beograd</td>
      <td>04.07.2013.</td>
    </tr>
    <tr>
      <td>20130024</td>
      <td>Nikola</td>
      <td>Vukovic</td>
      <td>17.09.1994.</td>
      <td> </td>
      <td>04.07.2013.</td>
    </tr>
    <tr>
      <td>20140025</td>
      <td>Marijana</td>
      <td>Savkovic</td>
      <td>04.02.1995.</td>
      <td>Kraljevo</td>
      <td>06.07.2014.</td>
    </tr>
    <tr>
      <td>20140026</td>
      <td>Zorica</td>
      <td>Miladinovic</td>
      <td>08.10.1995.</td>
      <td>Vranje</td>
      <td>06.07.2014.</td>
    </tr>
    <tr>
      <td>20130027</td>
      <td>Milena</td>
      <td>Stankovic</td>
      <td> </td>
      <td> </td>
      <td> </td>
    </tr>
  </tbody>
</table>

<p>b) Napisati funkciju `kreiraj_red_tabele(student)` koja kreira objekat koji predstavlja red tabele, pri čemu svaka ćelija u redu odgovara vrednostima koje su sadržane u promenljivoj `student`. Ne koristiti svojstva `innerHTML` i `outerHTML` za dinamičko dodavanje elemenata.</p>

<p>c) Napisati funkciju `postavi_hover_stil()` koja nad objektom koji je poziva kao metod postavlja pozadinsku boju na sivu.</p>

<p>d) Napisati funkciju `ukloni_hover_stil()` koja nad objektom koji je poziva kao metod postavlja pozadinsku boju na belu.</p>

<p>e) Napisati funkciju `odaberi_studenta()` koja redom:</p>
<ul>
  <li>Briše sadržaj elementa sa identifikatorom `odabran_student`.</li>
  <li>U element sa identifikatorom `odabran_student` dodaje naslov sa tekstom.</li>
  <li>Pronalazi studenta iz niza `studenti` na osnovu indeksa koji se nalazi kao sadržaj objekta nad kojim se funkcija poziva kao metod.</li>
  <li>U element sa identifikatorom `odabran_student`, za svaku vrednost koja se sadrži u pronađenom studentu, dodaje po jedan paragraf čiji je sadržaj kao na narednoj slici.
</li>
</ul>

<img style="max-width: 100%;" src="./Domaci/Resursi/odabran_student.png" alt="">

<p>f) Napisati funkciju `postavi_osluškivače_nad_prvom_kolonom()` koja nad prvom tabelom u dokumentu pronalazi prve ćelije u svakom redu tabele, i za svaku od tih ćelija redom:</p>
<ul>
  <li>Postavlja osluškivač `postavi_hover_stil` za događaj 'mouseenter'</li>
  <li>Postavlja osluškivač `ukloni_hover_stil` za događaj 'mouseleave'</li>
  <li>Postavlja osluškivač `odaberi_studenta` za događaj 'click'</li>
</ul>

<p>g) Napisati funkciju `prikaži_podatke()` koja redom:</p>
<ul>
  <li>Kreira tabelu na osnovu podataka iz promenljive studenti kao na narednoj slici. Dozvoljeno je korišćenje funkcije `kreiraj_red_tabele`. Ne koristiti svojstva `innerHTML` i `outerHTML` za dinamičko dodavanje elemenata.
  <img style="max-width: 100%;" src="./Domaci/Resursi/prikazani_podaci.png" alt="">
  </li>
  <li>Postavlja osluškivače pozivom funkcije postavi_osluškivače_nad_prvom_kolonom.</li>
</ul>

<p>Takođe, postaviti osluškivač prikaži_podatke za događaj 'click' nad dugmetom čiji je identifikator prikazi_podatke.</p>

<p>h) Obraditi sve greške u implementaciji.</p>
    </div>
</div>

<div class="domaci-zadatak">
    <span class="naslov">Domaći zadatak 2</span> 
    <div class="tekst">
        U primeru sa formularom smo rekli da su interesovanja opciona (primetimo da smo zbog toga koristili `checkbox` elemente). Istražiti kako bismo u JavaScript jeziku nametnuli ograničenje da korisnik mora da odabere makar 2 interesovanja i napisati odgovarajući kod kojim se proverava to ograničenje.
    </div>
</div>

<div class="domaci-zadatak">
    <span class="naslov">Domaći zadatak 3</span> 
    <div class="tekst">
        Napisati JavaScript kod koji bi "u hodu" proveravao da li je korisničko ime dužine više od 5 karaktera. Drugim rečima, potrebno je da, nakon što korisnik unese korisničko ime nedozvoljene dužine i pređe na naredno polje, veb pregledač prikaže poruku "Korisničko ime mora biti duže od 5 karaktera!" funkcijom window.alert().
    </div>
</div>

<div class="domaci-zadatak">
    <span class="naslov">Domaći zadatak 4</span> 
    <div class="tekst">
        Napisati HTML datoteku koja sadrži formular dat na narednoj slici. Napisati JavaScript kod koji nakon klika na dugme "Izračunaj površinu" izračunava i ispisuje vrednost površine trougla. U slučaju unosa nekorektnih vrednosti, treba ispisati poruku o grešci u obaveštajnom prozoru veb pregledača. Za računanje površine koristiti Heronov obrazac.
    </div>
    <img style="max-width: 100%;" src="./Domaci/Slike/zadatak5.png" alt="">
</div>

<div class="domaci-zadatak">
    <span class="naslov">Domaći zadatak 5</span> 
    <div class="tekst">
        Neka je data datoteka <a href="https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Domaci/Resursi/zadatak2/index.html">index.html</a> koja predstavlja osnovu klijentske veb aplikacije. Stilovi su dati u datoteci <a href="https://github.com/MatfUVIT/UVIT/blob/master/vezbe/knjiga/Poglavlja/WebAPI/Domaci/Resursi/zadatak2/index.css">index.css</a>. Zadatak je da implementiramo klijentsku veb aplikaciju koja ispunjava naredni opis. Korisnik treba da unese datum u polje "Odaberite datum" i tekst u polje "Unesite podsetnik". Klikom na dugme "Unesi novi podsetnik" na stranici se prikazuje nova stavka "To-do" liste. Prikaz aplikacije je dat na narednoj slici.
        <img style="max-width: 100%;" src="./Domaci/Resursi/todo.png" alt="">
        <p><strong>Implementacioni detalji zadatka</strong></p>

<p>Sva rešenja čuvati u datoteci `index.js`.</p>

<p>a) Na početku je lista prazna. Kreirati globalnu promenljivu `toDoLista` koja predstavlja prazan niz obaveza. Ova promenljiva se koristi u narednim zahtevima.</p>

<p>b) Napisati funkciju `prikažiListu()` koja redom:</p>
<ul>
    <li>Briše sve elemente iz sadržaja elementa sa identifikatorom `lista`.</li>
    <li>Za svaku stavku iz promenljive `toDoLista` kreira dete čvor elementa sa identifikatorom `lista`, pri čemu novokreirani čvor treba da zadovoljava naredni HTML i CSS kod:</li>
</ul>

<pre id="dz-2-3">
</pre>

<script>
    document.querySelector("#dz-2-3").innerText = 
`<div class="stavka">
    <p style="font-style: italic; margin-left: 10px;">
        Podsetnik za datum DATUM_PODSETNIKA:
    </p>
    <p style="width: 80%; margin: auto; word-wrap: break-word;">
        TEKST_PODSETNIKA
    </p>
</div>`;
</script>

`DATUM_PODSETNIKA` i `TEKST_PODSETNIKA` treba da budu zamenjeni datumom i tekstom iz stavke liste (videti sliku iznad). Ne koristiti svojstva `innerHTML` i `outerHTML` za dinamičko dodavanje ili brisanje elemenata.

<p>c) Napisati funkciju `dodajStavkuListe()` koja redom:</p>
<ul>
    <li>Dohvata informaciju o datumu iz elementa sa identifikatorom `datum` i provera da li je korisnik uneo datum (da li je vrednost polja prazna niska).</li>
    <li>Dohvata informaciju o tekstu podsetnika iz elementa sa identifikatorom `tekst` i provera da li je korisnik uneo taj tekst (da li je vrednost polja prazna niska).</li>
    <li>Ukoliko su svi podaci uneti, kreira novu stavku koja sadrži te dve informacije i pamti je u promenljivu `toDoLista`.</li>
    <li>Poziva funkciju `prikažiListu` da bi se osvežio prikaz obaveza na stranici.</li>
</ul>

Ne koristiti svojstva `innerHTML` i `outerHTML` za dinamičko dodavanje ili brisanje elemenata.

<p>d) Pridružiti funkciju `dodajStavkuListe` kao osluškivač elementa sa identifikatorom `napravi-todo` na događaju kliktaj miša.</p>

<p>e) Obraditi sve greške u implementaciji.</p>
    </div>
</div>

---

[Knjiga](../../README.md)

[Vežbe](../../../README.md)

<!--
<div style="max-width: 98%;">
<img style="max-width: 100%;" src="./Slike/.png" alt="">
</div>
-->

<!--
<a style="border: 2px solid gray; display: inline-block; padding: 15px; background-color: rgb(114, 211, 250); color: black;"
   href="./Primeri/X/index.html"
   target="_blank">Pogledaj primer uživo (obavezno otvoriti konzolu)</a>
-->
