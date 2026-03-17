# 🌬️ System Analityczno-Operacyjny „DAILY REPORT”

> ### 🚀 [KLIKNIJ TUTAJ, ABY OTWORZYĆ INTERAKTYWNE DEMO RAPORTU](https://moczarskimateusz.github.io/wind-predictions-public/reports/index.html)

> _(Demo umożliwia symulację awarii turbin i przeliczanie strat finansowych w locie)_

---

## 📋 1. Executive Summary

System **DAILY REPORT** to autorskie rozwiązanie klasy Decision Support System, zaprojektowane w celu precyzyjnego prognozowania generacji energii oraz aktywnej optymalizacji wyników finansowych aktywów wiatrowych. Narzędzie integruje zaawansowane modelowanie statystyczne z danymi rynkowymi (PSE) i meteorologicznymi (Open-Meteo).

Kluczowym założeniem projektu jest dostarczenie wysokiej jakości analityki operacyjnej przy obecnych ograniczeniach infrastrukturalnych IT, przy jednoczesnym zachowaniu pełnej gotowości do przyszłej integracji z systemami IoT/SCADA i widoków czasu rzeczywistego.

---

## 🏗️ 2. Proces Technologiczny i Inżynieria Cech

### A. Modelowanie Fizyki Atmosfery

W procesie przygotowania danych (Feature Engineering) zaimplementowano zaawansowane algorytmy fizyczne, wykraczające poza standardową analizę statystyczną:

- **Logarytmiczny Profil Wiatru:** System wykorzystuje prawo logarytmiczne do ekstrapolacji prędkości wiatru z wysokości referencyjnej (10m/80m) na rzeczywistą wysokość piasty konkretnej turbiny (**Hub Height**). Uwzględnienie parametru szorstkości terenu ($z_0$) pozwoliło na wyeliminowanie systematycznych błędów prognoz na niskich wysokościach.
- **Gęstość Powietrza (Air Density Proxy):** Algorytm wylicza gęstość powietrza na podstawie temperatury i ciśnienia. Pozwala to modelowi uwzględnić energię kinetyczną masy powietrza, co ma krytyczny wpływ na realną sprawność łopat turbiny.
- **Kodowanie Cykliczne:** Zastosowano transformacje trygonometryczne (sin/cos) dla zmiennych czasowych i kierunkowych, co umożliwiło systemowi rozpoznawanie wzorców dobowych oraz sezonowych.

### B. Strategia Modelowania ML

- **Algorytm:** Wykorzystano model regresyjny **XGBoost**, zoptymalizowany pod kątem mapowania nieliniowych krzywych mocy i zmiennej charakterystyki wietrzności.
- **Filtry fizyczne (Data Quality):** System automatycznie identyfikuje i usuwa anomalie z danych treningowych (np. „stuck sensors”, wymuszone przestoje awaryjne), zapobiegając zaburzeniom nauki modelu.
- **Integracja planów serwisowych:** Proces nauki uwzględnia historię przestojów (wykluczanie okresów serwisowych), dzięki czemu model uczy się rzeczywistej charakterystyki technicznej maszyn.

### C. Automatyzacja Pipeline’u Danych

System operuje w modelu autonomicznym poprzez integrację z zewnętrznymi interfejsami:

1.  **Open-Meteo API:** Pobór wysokorozdzielczych prognoz 15-minutowych dla precyzyjnych współrzędnych GPS.
2.  **PSE API (Portal Raportowy):** Ekstrakcja Rynkowych Cen Energii (RCE), umożliwiająca natychmiastową wycenę finansową prognozowanego wolumenu energii.

---

## 💰 3. Kluczowe Funkcjonalności Biznesowe

- **Smart Curtailment (Ochrona marży):** System automatycznie wykrywa godziny o ujemnych cenach energii i generuje rekomendacje zatrzymania produkcji, wyliczając kapitał uratowany przed stratą na Rynku Bilansującym.
- **Cyfrowy Bliźniak (Simulation suite):** Interaktywny interfejs operacyjny pozwala na dynamiczne symulowanie dostępności floty. Silnik JavaScript umożliwia ręczne nakładanie awarii/przestojów, przeliczając w czasie rzeczywistym wpływ tych zdarzeń na MWh i PLN.
- **Optymalizator serwisowy:** Autorski algorytm wskazuje najtańsze okno czasowe na prace techniczne w godzinach roboczych, minimalizując koszt utraconych korzyści (Opportunity Cost).
- **Analityka ryzyka:** Wykorzystanie wstęg ufności (±15%) dostarcza informacji o bezpiecznym korytarzu finansowym dla działów finansowych i tradingu.

---

## 📈 4. Wartość Dodana i Rozwój (ROI)

1.  **Ominięcie barier infrastrukturalnych:** Rozwiązanie dostarcza kluczowe dane zarządcze natychmiast, bez konieczności oczekiwania na IT.
2.  **Skalowalność:** Dzięki architekturze opartej na plikach konfiguracyjnych JSON, dodanie nowej farmy wiatrowej lub zmiana specyfikacji turbin odbywa się bez modyfikacji kodu źródłowego.

---

## 🛠️ Stack Techniczny

- **Backend:** Python (Pandas, NumPy, XGBoost, Joblib)
- **Integracje:** REST API (PSE, Open-Meteo)
- **Frontend/UI:** HTML5, CSS3 (Bootstrap), JavaScript (Logika obliczeniowa side-client)
- **Wizualizacja:** Plotly.js (Dynamiczne wykresy dwuosiowe)
