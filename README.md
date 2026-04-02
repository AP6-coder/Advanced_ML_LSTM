# LSTM — Long Short-Term Memory

> Een educatief project over LSTM-netwerken, met een theoretische onderbouwing en een praktisch voorbeeld aan de hand van energieverbruiksvoorspelling.

---

## Inhoud

- [Wat is LSTM?](#wat-is-lstm)
- [Structuur van dit project](#structuur-van-dit-project)
- [Theoretische presentatie](#theoretische-presentatie)
- [Praktisch voorbeeld — Energy Prediction](#praktisch-voorbeeld--energy-prediction)
- [Resultaten](#resultaten)
- [Installatie](#installatie)
- [Projectstructuur](#projectstructuur)

---

## Wat is LSTM?

LSTM (Long Short-Term Memory) is een type **Recurrent Neural Network (RNN)** dat speciaal ontworpen is voor **sequentiële data en tijdreeksen**. Klassieke RNN's hebben moeite met het onthouden van informatie over lange termijn — het zogenaamde geheugenprobleem. LSTM lost dit op met een **geheugencel** die bestaat uit drie poorten:

- **Forget gate** — beslist welke informatie vergeten wordt
- **Input gate** — beslist welke nieuwe informatie opgeslagen wordt
- **Output gate** — bepaalt wat doorgegeven wordt aan de volgende stap

Typische toepassingen zijn tijdreeksvoorspellingen, tekstgeneratie en vertalingen.

---

## Structuur van dit project

Dit project bestaat uit twee delen die elkaar aanvullen:

| Onderdeel | Beschrijving |
|---|---|
| Theoretische presentatie | Legt uit wat LSTM is, hoe de geheugencel werkt en waar het voor gebruikt wordt |
| Notebook | Past LSTM toe op een concreet probleem: het voorspellen van energieverbruik |

---

## Theoretische presentatie

De presentatie behandelt de volgende onderwerpen:

- Situering van LSTM binnen het bredere landschap van neurale netwerken (RNN, CNN, Feedforward)
- De werking van de geheugencel: cell state, hidden state en de drie gates
- Een visueel voorbeeld aan de hand van beurskoersdata met 1 hidden layer

De presentatie is terug te vinden in de map `presentation/`.

---

## Praktisch voorbeeld — Energy Prediction

Als demonstratie wordt LSTM toegepast op het voorspellen van huishoudelijk energieverbruik. Dit probleem leent zich goed voor LSTM omdat energieverbruik sterke temporele patronen heeft:

- Dagcyclus — 's nachts minder verbruik dan overdag
- Seizoenscyclus — in de winter meer dan in de zomer
- Weekcyclus — weekdagen vs weekenden

**Dataset**: UCI – Individual Household Electric Power Consumption
2.075.259 metingen per minuut, van december 2006 tot november 2010.

Twee modellen worden vergeleken:

| Model | Beschrijving |
|---|---|
| Linear Regression | Baseline — behandelt elke meting als een losse observatie |
| LSTM | Leert patronen over een sequentie van N uren |

Het notebook doorloopt het volledige proces: data laden, opschonen, feature engineering, modelbouw, training en evaluatie.

---

## Resultaten

| Model | MAE (kW) | RMSE (kW) | MAPE (%) | R² |
|---|---|---|---|---|
| Linear Regression (seq=24) | 0.3598 | 0.5027 | 46.18% | 0.5408 |
| LSTM (seq=24, 1 dag) | 0.3361 | 0.4752 | 43.28% | 0.5898 |
| LSTM (seq=48, 2 dagen) | 0.3314 | 0.4811 | 38.77% | 0.5770 |
| **LSTM (seq=168, 1 week)** | **0.3256** | 0.4793 | **37.72%** | 0.5803 |
| LSTM (seq=730, 1 maand) | 0.3266 | **0.4754** | 39.17% | **0.5827** |

Het LSTM-model met een contextvenster van 1 week presteert het best op MAE en MAPE, wat bevestigt dat weekpatronen een relevante rol spelen in energieverbruik.

---

## Installatie

### Via Google Colab (aanbevolen)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AP6-coder/Advanced_ML_LSTM/blob/main/notebooks/energy_lstm_prediction.ipynb)
Klik op de badge en het notebook opent direct in Colab — geen installatie vereist.

### Lokaal draaien

```bash
# 1. Clone de repository
git clone https://github.com/AP6-coder/Advanced_ML_LSTM.git
cd lstm-energy-prediction

# 2. Installeer dependencies
pip install -r requirements.txt

# 3. Open het notebook
jupyter notebook notebooks/energy_lstm_prediction.ipynb
```

---

## Projectstructuur

```
LSTM — Long Short-Term Memory/
│
├── README.md
│
├── presentation/
│   └── theoretische_presentatie_LSTM.pdf
│
├── notebooks/
│   └── energy_lstm_prediction.ipynb
│
├── results/
│   ├── 01_overview.png
│   ├── 04_prediction_vs_actual.png
│   └── 07_error_by_hour.png
│
├── requirements.txt
└── LICENSE
```

---

## Auteur

**Arthur Peters**

---

## Licentie

Dit project valt onder de [MIT License](LICENSE).
