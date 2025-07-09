
# 🚗 Dynamic Pricing for Urban Parking Lots (Summer Analytics 2025)

This project implements a real-time dynamic pricing engine for 14 urban parking spaces. Built as part of the **Summer Analytics 2025 Capstone**, the project simulates demand-based and competition-aware pricing using Python and real-time simulation.

## 📌 Overview

Urban parking lots often suffer from static pricing, leading to either overcrowding or underuse. This system adjusts prices dynamically using features like occupancy, queue length, traffic, vehicle type, special days, and competitor proximity.

We implement 3 models:
- **Model 1 (Baseline)**: Linear price update using occupancy ratio.
- **Model 2 (Demand-based)**: Weighted demand score with normalization.
- **Model 3 (Competitive)**: Adds competitor-aware adjustments using geo-proximity.

Each model is implemented in a separate Colab notebook (links below).

## 🛠 Tech Stack

- **Python 3.11**
- **Pandas / NumPy** — for data manipulation and model logic
- **Bokeh** — for real-time price visualization
- **Google Colab** — for development and execution

## 📈 Architecture Diagram (Mermaid)

```mermaid
graph TD
    A[dataset.csv (static)] -->|Stream simulation| B[Colab Notebook]
    B --> C[Feature Extraction]
    C --> D[Pricing Logic (Model 1 / 2 / 3)]
    D --> E[Bokeh Visualization]
    D --> F[Price Adjustment]
    F --> G[Competitor Price Check]
    G --> D
```

## 🔍 Project Workflow

1. **Data Ingestion**: Static CSV simulates real-time data stream (18 timepoints/day × 73 days).
2. **Feature Engineering**: Calculates occupancy %, queue, traffic level, etc.
3. **Model Logic**: Implements pricing formula as per model:
   - Model 1: `Price += α * (Occupancy / Capacity)`
   - Model 2: `Price = Base × (1 + λ × DemandScore)`
   - Model 3: Adds competitor-based logic using Haversine distance.
4. **Competitor Analysis**: Nearby lots within 0.5km are compared; price is adjusted accordingly.
5. **Visualization**: Real-time plots via Bokeh for all 14 locations.

## 📂 Project Structure

- [`model1.ipynb`](https://colab.research.google.com/drive/1TwGVIQ0JwDR9jrWjIFXx2PD_OK0cVMKD) — Baseline Linear Model
- [`model2.ipynb`](https://colab.research.google.com/drive/10DB5cZnURwJUWppjnnjGzkD2oK10IvCC) — Demand-Based Model
- [`model3.ipynb`](https://colab.research.google.com/drive/1OOOUDt7eNDrMMFcNFmH_Tu2s6rXskVVT) — Competitive Pricing Model

## 📌 Key Assumptions

- Base price starts at **$10**
- Prices capped between **0.5x and 2x** base
- Vehicle type weights: Car = 1.0, Bike = 0.7, Truck = 1.5
- Traffic mapped as Low = 0, Medium = 1, High = 2
- Competitor considered if within **0.5 km**

## 📊 Visual Output

Each notebook produces interactive Bokeh plots showing price evolution over time for each parking location. Model 3 also smooths values using daily averages or rolling means.

## 📝 Optional Enhancements

- Rerouting suggestions can be integrated (currently mimicked via price suppression).
- Stream processing with Pathway could replace the manual timestamp loop for deployment.

## 📄 Report (Optional)

A report PDF can be added to summarize findings, demand weights, and decision logic.

---

Developed as part of the Summer Analytics 2025 Capstone — CnA Club × Pathway.
