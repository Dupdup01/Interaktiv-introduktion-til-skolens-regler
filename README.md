# Interaktiv-introduktion-til-skolens-regler
## To-do liste
Her har vi lavet en trello, så vi nemmere har overblik om hvad der er blev et lavet, og hvad der mangler at blive lavet
![billede](https://github.com/user-attachments/assets/9174d642-b762-4fa4-b060-0c3294656d29)

## Lav UI
Lav en brætspils bane som png. banen skal være rund og inddelt i felter med forskellige farver. der skal være 30 felter med 6 forskellige farver fordelt ud på banen. lav farverne iøjnefaldende og lav et tydeligt start felt og et ende felt

https://www.canva.com/design/DAGrGq3wjvE/s2orty0u__IIsflQhaZh8A/edit?utm_content=DAGrGq3wjvE&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton

## 3-Lags modellen

## 4P modellen

## Videreudviklingsplan

## Lav flowchart
### Setup()
![billede](https://github.com/user-attachments/assets/b78ce949-6788-4d64-b2d7-7cb188b52d48)
### Draw()
![billede](https://github.com/user-attachments/assets/f397c10c-1dd5-48b1-b3d5-7f4756f0655b)
### mousePressed()
![billede](https://github.com/user-attachments/assets/d7eb43b6-5bea-4a16-ae9a-f546dabc4997)
### rollDice()
![billede](https://github.com/user-attachments/assets/f5ab4ecc-0400-4a6d-9562-41fea054d284)
### drawDice()
![billede](https://github.com/user-attachments/assets/41611e8d-13db-4b69-9149-bf9b71405b50)

## Lav koden
  // Denne kode er et udgangspunkt, hvor vi udelukkende har lavet et valg af kategori ud for værdien af terningen og en random spørgsmåls-funktion, hvor spørgsmålene     ikke kan udtrækkes igen efter de allerede udtrukket.

  // Liste med spørgsmål, der skal bruges når terningen viser et lige tal
  let spørgsmålEven = [
    "Må du dele din adgangskode med en anden person?",
    "Er det tilladt at bruge internettet på skolen til at tjekke din private e-mail?",
    "Må du bruge skolens netværk til at dele film, du har downloadet ulovligt?",
    "Skal undervisningsrelevante data gemmes på skolens servere?",
    "Er det i orden at forsøge at få adgang til andres filer på skolens netværk?",
  ];

// Korrekte svar til spørgsmålEven (i samme rækkefølge)
let svarEven = [
  "Nej",
  "Ja",
  "Nej",
  "Ja",
  "Nej",
];

// Liste med spørgsmål, der skal bruges når terningen viser et ulige tal
let spørgsmålOdd = [
  "Må du tilslutte din computer til skolens netværk via et netværkskabel?",
  "Skal din computer have de nyeste sikkerhedsopdateringer installeret?",
  "Er det et krav, at din computer har et opdateret antivirusprogram?",
  "Må du oprette et trådløst Access Point på skolen?",
  "Er det tilladt at dele filer via peer-to-peer netværk på skolens netværk?",
];

// Korrekte svar til spørgsmålOdd (i samme rækkefølge)
let svarOdd = [
  "Nej",
  "Ja",
  "Ja",
  "Nej",
  "Nej",
];

// Variabel til terningens værdi (1-6)
let terningTal = 0;

// De aktuelle spørgsmål og svar, der bliver vist på skærmen
let aktueltSpørgsmål = "";
let aktueltSvar = "";

// Om svaret skal vises (true/false)
let visSvar = false;

// Lister til at holde styr på hvilke spørgsmål, der allerede er brugt (for lige og ulige terningetal)
let spørgsmålBrugtEven = [];
let spørgsmålBrugtOdd = [];

function setup() {
  createCanvas(600, 400);  // Lav et lærred på 600x400 pixels
  textAlign(LEFT, CENTER); // Justér tekst til venstre og centrer lodret
  textSize(20);            // Sæt tekststørrelse til 20
  rollDice();              // Kast terningen og vælg et spørgsmål ved start
  visSvar = false;         // Start med at vise spørgsmål (ikke svar)
}

function draw() {
  background(240);         // Sæt baggrunden til lys grå

  fill(0);                 // Sort tekstfarve
  text("Terning slået: " + terningTal, 50, 50);       // Vis hvilket tal terningen viser
  text("Spørgsmål:", 50, 100);                        // Overskrift for spørgsmål
  text(aktueltSpørgsmål, 50, 130, width - 100);       // Vis det aktuelle spørgsmål

  if (visSvar && aktueltSvar !== "") {
    fill(0, 100, 0);       // Grøn tekst til svar
    text("Svar:", 50, 250); 
    text(aktueltSvar, 50, 280);                      // Vis svaret
  } else if (!visSvar) {
    fill(100);             // Grå tekst til prompt om at klikke
    text("Klik for at se svaret", 50, 250);          // Instruktion til brugeren
  }

  drawDice(terningTal, width - 150, 50);              // Tegn terningen øverst til højre
}

function mousePressed() {
  if (!visSvar) {
    // Hvis svaret ikke vises, så vis det næste gang der klikkes
    visSvar = true;
  } else {
    // Hvis svaret vises, så rul terningen og vis et nyt spørgsmål næste gang der klikkes
    visSvar = false;
    rollDice();
  }
}

function rollDice() {
  terningTal = int(random(1, 7));  // Kast terningen (1-6)

  if (terningTal % 2 === 0) {      // Hvis terningen er lige
    if (spørgsmålBrugtEven.length === spørgsmålEven.length) {
      // Hvis alle spørgsmål er brugt, vis besked
      aktueltSpørgsmål = "Der er ikke flere spørgsmål i bunken";
      aktueltSvar = "";
      return;
    }

    let idx;
    do {
      idx = int(random(spørgsmålEven.length));   // Vælg et tilfældigt indeks til et spørgsmål
    } while (spørgsmålBrugtEven.includes(idx));   // Sørg for det ikke er brugt før

    spørgsmålBrugtEven.push(idx);                  // Tilføj spørgsmålet til brugt-liste
    aktueltSpørgsmål = spørgsmålEven[idx];         // Sæt det aktuelle spørgsmål
    aktueltSvar = svarEven[idx];                    // Sæt det tilhørende svar
  } else {                                         // Hvis terningen er ulige
    if (spørgsmålBrugtOdd.length === spørgsmålOdd.length) {
      // Hvis alle spørgsmål er brugt, vis besked
      aktueltSpørgsmål = "Der er ikke flere spørgsmål i bunken";
      aktueltSvar = "";
      return;
    }

    let idx;
    do {
      idx = int(random(spørgsmålOdd.length));     // Vælg tilfældigt ulige spørgsmål
    } while (spørgsmålBrugtOdd.includes(idx));     // Sørg for ikke brugt før

    spørgsmålBrugtOdd.push(idx);                    // Tilføj til brugt-liste
    aktueltSpørgsmål = spørgsmålOdd[idx];           // Sæt aktuelt spørgsmål
    aktueltSvar = svarOdd[idx];                      // Sæt aktuelt svar
  }
}

// Funktion til at tegne en terning med det givne tal på en position (x, y)
function drawDice(value, x, y) {
  fill(255);          // Hvid terning baggrund
  stroke(0);          // Sort kant
  rect(x, y, 60, 60, 10);  // Tegn firkant med afrundede hjørner

  fill(0);            // Sorte prikker, hvor nul er sort
  let cx = x + 30;    // Midten af terningen i x-aksen
  let cy = y + 30;    // Midten af terningen i y-aksen
  let o = 15;         // Offset for prikker, bruges til at kontrollere lige afstand mellem prikkerne    

  // Tegn prikkerne afhængigt af terningens værdi
  if (value == 1) {
    circle(cx, cy, 8);
  }
  if (value == 2) {
    circle(cx - o, cy - o, 8);
    circle(cx + o, cy + o, 8);
  }
  if (value == 3) {
    circle(cx, cy, 8);
    circle(cx - o, cy - o, 8);
    circle(cx + o, cy + o, 8);
  }
  if (value == 4) {
    circle(cx - o, cy - o, 8);
    circle(cx + o, cy + o, 8);
    circle(cx - o, cy + o, 8);
    circle(cx + o, cy - o, 8);
  }
  if (value == 5) {
    circle(cx, cy, 8);
    circle(cx - o, cy - o, 8);
    circle(cx + o, cy + o, 8);
    circle(cx - o, cy + o, 8);
    circle(cx + o, cy - o, 8);
  }
  if (value == 6) {
    circle(cx - o, cy - o, 8);
    circle(cx + o, cy - o, 8);
    circle(cx - o, cy, 8);
    circle(cx + o, cy, 8);
    circle(cx - o, cy + o, 8);
    circle(cx + o, cy + o, 8);
  }
}
