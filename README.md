# esp-gate-opener
# ESP Gate Opener

Sistema per aprire e chiudere il cancello utilizzando un **ESP8266/ESP32**, un **modulo relay** e il **telecomando originale BFT**.

L’idea è semplice ma potente:
invece di collegarsi direttamente alla centralina del cancello, l’ESP “preme” in modo elettronico il pulsante del telecomando BFT, simulando un normale click.  
In questo modo:
- non modifichi la centralina del cancello
- usi un telecomando originale
- puoi controllare il cancello da **Home Assistant**, mantenendo comunque la possibilità di usare il telecomando a mano.

---

## 🚀 Funzionalità

- Apertura/chiusura del cancello tramite Home Assistant
- Comando da app, automazioni e dashboard
- Utilizzo del telecomando BFT originale (nessuna modifica alla centralina del cancello)
- Possibilità di aggiungere sensori di stato (cancello aperto/chiuso)
- Integrabile con scene e routine smart home

---

## 🔧 Hardware utilizzato

- **ESP8266** (es. NodeMCU / Wemos D1 Mini) oppure **ESP32**
- **Modulo relay 1 canale** (5V o compatibile con l’alimentazione scelta)
- **Telecomando BFT originale** del cancello  
  - con **due fili saldati** sui contatti del pulsante (simulazione pressione tasto)
- **Alimentatore 5V** per alimentare ESP e relay
- Cavi jumper / fili
- (Opzionale) Sensore magnetico / finecorsa per rilevare se il cancello è aperto o chiuso
- (Opzionale) Scatola di derivazione o box per proteggere l’elettronica

---

## ⚙️ Come funziona il progetto

1. Sul circuito del **telecomando BFT** vengono saldati due fili sui contatti del pulsante di apertura.
2. Questi due fili vengono collegati al contatto **COM** e **NO** del **relay**.
3. Il relay è controllato dall’**ESP8266/ESP32** tramite un pin digitale.
4. Quando Home Assistant invia il comando:
   - l’ESP attiva il relay per una frazione di secondo
   - il relay chiude il contatto come se premessi il pulsante del telecomando
   - il cancello si apre o si chiude normalmente.

In pratica, l’ESP non fa altro che “cliccare” il telecomando al posto tuo.

---

## 📂 Struttura del progetto

```
esp-gate-opener/
│
├─ esphome/               # Configurazione ESPHome (.yaml)
├─ schematics/            # Schema elettrico / collegamenti (ESP, relay, telecomando BFT)
├─ docs/                  # Foto del montaggio, note e documentazione extra
└─ README.md              # Questo file
```

Come iniziare
Preparazione del telecomando BFT
Apri il telecomando BFT.
Individua i contatti del pulsante di apertura.
Salda due fili sottili sui contatti del pulsante.
Collegamento al relay
Collega i due fili del telecomando al relay sui contatti COM e NO.
Collega il relay all’ESP (pin di controllo, VCC e GND).
Configurazione ESPHome
Copia il file YAML presente in esphome/ nel tuo progetto ESPHome.
Carica la configurazione sull’ESP8266/ESP32.
Integrazione con Home Assistant
Aggiungi il dispositivo ESPHome a Home Assistant.
Verifica che il pulsante di apertura funzioni dalla dashboard.
Test
Premi il pulsante da Home Assistant.
Controlla che il cancello risponda come con il telecomando normale.
