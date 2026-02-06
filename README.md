# Troškomer 📊

Aplikacija za analizu bankovnih izvoda iz Banca Intesa banke. Parsira PDF izvode, automatski kategorizuje transakcije i prikazuje statistiku potrošnje.

## Funkcionalnosti

### Učitavanje izvoda
- Upload PDF izvoda iz Banca Intesa
- Automatsko parsiranje tabela sa transakcijama
- Detekcija perioda (mesec/godina) iz datuma transakcija
- Čuvanje parsiranih podataka lokalno (CSV + metadata)

### Kategorisanje transakcija
Automatsko kategorisanje na osnovu ključnih reči:
- 🏥 **Apoteke** - LILLY, BENU, APOTEKA...
- 🩺 **Zdravstveni pregledi i analize** - MEDILAB, MEDILEK, FIZIOKINETIKPR...
- 🛒 **Marketi** - LIDL, MAXI, IDEA, TEMPO...
- 🧴 **Drogerije** - DM
- ⛽ **Gorivo** - NIS, MOL, OMV...
- 👗 **Odeća i obuća** - ZARA, H&M, NEW YORKER, TAKKO...
- 📱 **Računi i usluge** - A1, EPS, INFOSTAN, vrtić...
- 🍔 **Restorani i dostava** - WOLT, GLOVO, kafići, pekare...
- 💵 **Gotovina (ATM)** - podizanje novca
- 🚗 **Putarine** - PUTEVI SRBIJE
- 📚 **Knjižare** - LAGUNA, VULKAN, DELFI
- 💻 **Tech i pretplate** - APPLE, NETFLIX, SPOTIFY, OPENAI...
- 🏠 **Stanovanje** - stambena zajednica
- ⛷️ **Sport i rekreacija** - skijalista, fitness
- 💇 **Lepota i nega** - saloni
- 🦷 **Zdravlje** - stomatolog
- 🏦 **Transferi** - bezgotovinski prenos
- 💰 **Primanja** - plata
- 💱 **Menjačnica** - devizni račun
- ❓ **Ostalo** - nekategorisano

### Normalizacija brendova
Grupisanje različitih naziva u jedan brend:
- "LIDL CACAK", "LIDL 123" → **LIDL**
- "TAKKOFASHION", "TAKKO" → **TAKKO FASHION**
- "A1 SRBIJA", "A1 265" → **A1**
- itd.

### Prikaz pojedinačnog meseca
- Header sa nazivom meseca (gradient dizajn)
- Kategorije sa iznosima (expandable)
- Brendovi unutar svake kategorije
- Pojedinačne transakcije
- Bilans na dnu (primanja, potrošnja, bilans, broj transakcija)

### Ukupna statistika (svi meseci)
- Rang lista kategorija sortirana po max mesecu
- Za svaku kategoriju:
  - Max iznos i u kom mesecu
  - Prosek (samo meseci sa potrošnjom)
  - Top brend sa statistikom
- "Gde najviše trošiš?" sekcija

### Dodatne opcije
- **Rekategorizuj sve** - ponovo primeni pravila kategorisanja
- **Export u Excel** - sve transakcije, po kategorijama, po brendovima
- **3 dizajna** - Klasičan (expanders), Kartice, Tabovi

## Tehnički stack

- **Python 3.10+**
- **Streamlit** - web framework
- **pdfplumber** - parsiranje PDF-a
- **pandas** - obrada podataka
- **xlsxwriter** - Excel export

## Instalacija

```bash
# Kloniraj repo
git clone https://github.com/FilipCT/bank-statement-analyzer.git
cd bank-statement-analyzer

# Kreiraj virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ili: venv\Scripts\activate  # Windows

# Instaliraj dependencies
pip install -r requirements.txt

# Pokreni aplikaciju
streamlit run app.py
```

## Deployment na Streamlit Cloud

1. Push kod na GitHub (privatni repo preporučen)
2. Idi na [share.streamlit.io](https://share.streamlit.io)
3. Poveži GitHub nalog
4. Odaberi repo i `app.py`
5. Deploy!

### Čuvanje podataka na Streamlit Cloud
- Podaci se čuvaju u `data/` folderu
- Na Streamlit Cloud, filesystem je ephemeral (briše se pri redeploy-u)
- Za trajno čuvanje: commit `data/` folder u repo
- Upload novog izvoda radi privremeno dok ne redeploy-uješ

## Struktura projekta

```
bank-statement-analyzer/
├── app.py              # Glavna aplikacija
├── requirements.txt    # Python dependencies
├── README.md          # Dokumentacija
├── .gitignore         # Git ignore
└── data/
    └── statements/
        ├── 2025-08/
        │   ├── transactions.csv
        │   ├── metadata.json
        │   └── statement.pdf
        ├── 2025-09/
        ├── 2025-10/
        └── ...
```

## Dodavanje novih kategorija/ključnih reči

U `app.py`, pronađi `CATEGORIES` dictionary i dodaj ključne reči:

```python
CATEGORIES = {
    "🛒 Marketi": [
        "LIDL", "MAXI", "NOVA_KLJUCNA_REC"  # dodaj ovde
    ],
    # ...
}
```

Za normalizaciju brendova, koristi `BRAND_MAPPING`:

```python
BRAND_MAPPING = {
    "LIDL": ["LIDL", "LIDL CACAK", "LIDL123"],  # sve varijante
    # ...
}
```

Posle izmena, klikni "🔄 Rekategorizuj sve" da se primeni na postojeće izvode.

## Responsive dizajn

Aplikacija je prilagođena za mobilne uređaje:
- Kompaktni prikaz na malim ekranima
- Scrollable tabele
- Touch-friendly expanders

## Budući razvoj

Moguća poboljšanja:
- [ ] Grafikon potrošnje po mesecima
- [ ] Poređenje meseci
- [ ] Dark mode podrška za logo/tekst
- [ ] Cloud storage integracija (Google Sheets, Supabase)
- [ ] Automatsko prepoznavanje novih trgovaca
- [ ] Budget/limit upozorenja

## Autor

Filip Milićević

## Licenca

Privatni projekat - samo za ličnu upotrebu.
