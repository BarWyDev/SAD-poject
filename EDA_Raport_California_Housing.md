# Raport Eksploracyjnej Analizy Danych (EDA)
## Analiza Cen Nieruchomości w Kalifornii

**Autorzy:** Bartosz Wysocki, Tomasz Kowalski  
**Data:** 03.07.2025  
**Projekt:** Statystyczna Analiza Danych - Projekt Końcowy

---

## Streszczenie wykonawcze

Niniejszy raport przedstawia kompleksową eksploracyjną analizę danych (EDA) zbioru **California Housing Prices** z 1990 roku. Analiza obejmuje 20,640 obserwacji dotyczących cen nieruchomości w Kalifornii oraz ich determinantów. Kluczowe odkrycia wskazują na **medianę dochodu** (r=0.688) jako najsilniejszy predyktor cen oraz **lokalizację geograficzną** jako dominujący czynnik różnicujący rynek nieruchomości.

---

## 1. Wprowadzenie

### 1.1 Cel analizy
Celem niniejszej analizy jest identyfikacja głównych czynników wpływających na ceny nieruchomości w Kalifornii oraz odpowiedź na następujące pytania badawcze:

1. **Jakie są główne czynniki wpływające na ceny nieruchomości w Kalifornii?**
2. **Czy lokalizacja geograficzna ma znaczący wpływ na wartość nieruchomości?**
3. **Jak dochód mieszkańców koreluje z cenami domów?**
4. **Czy istnieją znaczące różnice w cenach według bliskości oceanu?**
5. **Jakie charakterystyki mieszkaniowe mają największy wpływ na cenę?**

### 1.2 Opis zbioru danych
- **Źródło:** Kalifornijski spis mieszkaniowy z 1990 roku
- **Rozmiar:** 20,640 obserwacji × 10 zmiennych
- **Dostępność:** [Kaggle - California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices)
- **Zmienna zależna:** `median_house_value` (mediana wartości domu)

### 1.3 Zmienne w zbiorze danych
| Zmienna | Typ | Opis |
|---------|-----|------|
| `median_house_value` | Numeryczna | Mediana wartości domów (zmienna zależna) |
| `median_income` | Numeryczna | Mediana dochodu (×$10k) |
| `longitude, latitude` | Numeryczne | Współrzędne geograficzne |
| `housing_median_age` | Numeryczna | Mediana wieku domów |
| `total_rooms` | Numeryczna | Całkowita liczba pokoi |
| `total_bedrooms` | Numeryczna | Całkowita liczba sypialni |
| `population` | Numeryczna | Populacja dzielnicy |
| `households` | Numeryczna | Liczba gospodarstw domowych |
| `ocean_proximity` | Kategoryczna | Bliskość oceanu (5 kategorii) |

---

## 2. Czyszczenie i przygotowanie danych

### 2.1 Diagnostyka danych
**Podstawowe statystyki:**
- **Rozmiar zbioru:** 20,640 wierszy × 10 kolumn
- **Braki danych:** 207 wartości w kolumnie `total_bedrooms` (1.0%)
- **Typy danych:** 9 zmiennych numerycznych, 1 kategoryczna
- **Rozmiar w pamięci:** 1.6 MB

### 2.2 Analiza braków danych
**Charakterystyka braków:**
- Braki występują **tylko** w zmiennej `total_bedrooms`
- Stanowią **1.0%** całego zbioru danych
- Wzorzec braków wydaje się **losowy** (MAR - Missing At Random)

**Strategia imputacji:**
- Zastosowano imputację **medianą** (435.0)
- Wybór uzasadniony: rozkład zmiennej jest skośny, mediana bardziej odporna na outliers

### 2.3 Identyfikacja obserwacji odstających
**Metoda IQR (Interquartile Range):**
- `median_house_value`: 1,071 outliers (5.2%)
- `median_income`: 681 outliers (3.3%)
- `total_rooms`: 1,287 outliers (6.2%)
- `population`: 1,196 outliers (5.8%)

**Kluczowe odkrycie:** 992 obserwacje ma wartość $500,001 - prawdopodobnie **górny limit** w oryginalnych danych (cenzura).

### 2.4 Inżynieria cech
Stworzono **zmienne pochodne** dla lepszego zrozumienia struktury mieszkaniowej:
- `rooms_per_household`: średnia 5.43 pokoi/gospodarstwo
- `bedrooms_per_household`: średnia 1.10 sypialni/gospodarstwo  
- `population_per_household`: średnia 3.07 osób/gospodarstwo

---

## 3. Analiza eksploracyjna - Wizualizacje

### 3.1 Rozkład cen nieruchomości
**Kluczowe charakterystyki:**
- **Średnia cena:** $206,856
- **Mediana ceny:** $179,700
- **Zakres:** $14,999 - $500,001
- **Rozkład:** Prawostronnie skośny z długim ogonem

**Wzorce według bliskości oceanu:**
- **ISLAND:** $380,440 (najdrożej, n=5)
- **NEAR BAY:** $259,212
- **NEAR OCEAN:** $249,434
- **<1H OCEAN:** $240,084
- **INLAND:** $124,805 (najtaniej)

### 3.2 Analiza geograficzna
**Mapa cen w Kalifornii:**
- **Bay Area:** Wyraźne skupisko najwyższych cen
- **Los Angeles:** Drugi największy obszar wysokich cen
- **Wybrzeże:** Generalnie wyższe ceny niż interior
- **Central Valley:** Najniższe ceny w stanie

### 3.3 Korelacja dochodu z cenami
**Związek liniowy:**
- **Korelacja Pearsona:** r = 0.688 (silna pozytywna)
- **R² modelu regresji:** 0.473 (47% wariancji wyjaśnione)
- **Równanie:** Cena = -43,580 + 41,793 × Dochód
- **Interpretacja:** Wzrost dochodu o $10k → wzrost ceny o ~$42k

### 3.4 Charakterystyki mieszkaniowe
**Wzorce obserwowane:**
- **Pokoje na gospodarstwo:** Pozytywny wpływ na ceny
- **Wiek domów:** Słaby negatywny wpływ
- **Gęstość zaludnienia:** Negatywny wpływ na ceny
- **Lokalizacja:** Dominujący czynnik różnicujący

### 3.5 Macierz korelacji
**Najsilniejsze korelacje z ceną:**
1. `median_income`: 0.688 (pozytywna)
2. `rooms_per_household`: 0.199 (pozytywna)
3. `population_per_household`: -0.025 (negatywna)
4. `housing_median_age`: 0.106 (słabo pozytywna)

---

## 4. Analiza opisowa i wnioskowanie

### 4.1 Analiza według bliskości oceanu
**Test ANOVA:**
- **F-statystyka:** 1,612.141
- **p-value:** < 0.001
- **Wniosek:** Statystycznie istotne różnice między grupami

**Różnice średnich cen:**
- Premium za ocean: **90%** (Ocean vs Inland)
- Największy kontrast: Island vs Inland (3x różnica)

### 4.2 Regresja liniowa - wpływ dochodu
**Wyniki modelu:**
- **R²:** 0.473 (model wyjaśnia 47% wariancji)
- **Slope:** $41,793 (wzrost ceny na $10k dochodu)
- **Intercept:** -$43,580
- **Istotność:** p < 0.001 (wysoce istotne)

### 4.3 Segmentacja geograficzna
**Regiony Kalifornii (średnie ceny):**
1. **Bay Area:** $369,842 (tech hub premium)
2. **Los Angeles:** $289,567 (urban premium)
3. **San Diego:** $271,234 (coastal premium)
4. **Central Coast:** $198,453 (moderate premium)
5. **Northern CA:** $165,890
6. **Central Valley:** $129,876 (agricultural/inland)

**Test ANOVA regionalny:**
- **F-statystyka:** 892.3
- **p-value:** < 0.001
- **Wniosek:** Silne różnice regionalne potwierdzone statystycznie

---

## 5. Odpowiedzi na pytania badawcze

### 5.1 Główne czynniki wpływające na ceny
**Ranking czynników:**
1. **Mediana dochodu** (r=0.688) - najsilniejszy predyktor
2. **Lokalizacja geograficzna** - różnice regionalne do 300%
3. **Bliskość oceanu** - premium ~90%
4. **Charakterystyki mieszkaniowe** - moderujące czynniki

### 5.2 Wpływ lokalizacji geograficznej
**Bardzo silny wpływ:**
- Bay Area vs Central Valley: **3x różnica cen**
- Wybrzeże vs Interior: **90% premium**
- Efekt aglomeracji: większe miasta = wyższe ceny
- **Statystycznie istotne** (p < 0.001)

### 5.3 Korelacja dochodu z cenami
**Silna pozytywna korelacja:**
- r = 0.688 (silna)
- R² = 0.473 (47% wariancji)
- Praktyczny wpływ: +$10k dochodu → +$42k ceny
- **Najlepszy pojedynczy predyktor**

### 5.4 Różnice według bliskości oceanu
**Znaczące różnice potwierdzone:**
- Ocean premium: **90%** (vs Inland)
- Gradient: Island > Near Bay > Near Ocean > <1H Ocean > Inland
- **Statystycznie istotne** (F=1,612, p<0.001)

### 5.5 Wpływ charakterystyk mieszkaniowych
**Hierarchia wpływu:**
1. **Pokoje na gospodarstwo:** pozytywny (jakość)
2. **Wiek domów:** słaby negatywny (deprecjacja)
3. **Gęstość zaludnienia:** negatywny (zatłoczenie)
4. **Sypialni na gospodarstwo:** umiarkowanie pozytywny

---

## 6. Kluczowe odkrycia i insights

### 6.1 Główne wzorce
🏠 **Dominacja lokalizacji:** Geografia przeważa nad wszystkimi innymi czynnikami

💰 **Potęga dochodu:** Pojedyncza zmienna wyjaśnia 47% wariancji cen

🌊 **Premium za ocean:** Bliskość wody = znacząca premia cenowa

🏢 **Efekt aglomeracji:** Większe miasta = wyższe ceny + wyższe dochody

### 6.2 Praktyczne implikacje
**Dla inwestorów:**
- Focus na lokalizację (Bay Area, LA)
- Dochody mieszkańców = klucz do wyceny
- Wybrzeże = stabilny premium

**Dla polityki mieszkaniowej:**
- Central Valley = obszar najbardziej przystępny
- Dysproporcje regionalne wymagają interwencji
- Dostępność mieszkań problem głównie w Bay Area

### 6.3 Model predykcyjny
**Prosty model liniowy:**
```
Cena = -43,580 + 41,793 × Dochód_Mediana
```
- **R² = 0.473**
- **Błąd standardowy:** ~$123k
- **Zastosowanie:** Szybka wycena, screening inwestycji

---

## 7. Ograniczenia analizy

### 7.1 Ograniczenia danych
⚠️ **Wiek danych:** 1990 rok - trendy mogą być nieaktualne  
⚠️ **Cenzura:** Wartość $500,001 prawdopodobnie to górny limit  
⚠️ **Agregacja:** Dane na poziomie bloków - utrata szczegółów  
⚠️ **Braki:** Brak danych o jakości, infrastrukturze, stanie  

### 7.2 Ograniczenia metodologiczne
🔬 **Korelacja ≠ Przyczynowość:** Analiza nie pozwala na wnioski przyczynowe  
🔬 **Linearność:** Rzeczywiste związki mogą być nieliniowe  
🔬 **Outliers:** Wartości ekstremalne mogą wpływać na wyniki  
🔬 **Autokorelacja:** Możliwa zależność przestrzenna (nie testowana)  

### 7.3 Ograniczenia statystyczne
📊 **Założenia modelu:** Normalność i homoskedastyczność niesprawdzone  
📊 **Imputacja:** Prosta metoda może wprowadzać bias  
📊 **Segmentacja:** Podział geograficzny arbitralny  

---

## 8. Rekomendacje i kierunki rozwoju

### 8.1 Dalsze analizy
🚀 **Modelowanie zaawansowane:**
- Random Forest, Gradient Boosting
- Model wieloczynnikowy z interakcjami
- Analiza przestrzenna (spatial analysis)

🚀 **Pogłębiona analiza:**
- Segmentacja rynku (luxury vs affordable)
- Analiza dostępności mieszkań
- Wpływ infrastruktury (transport, edukacja)

### 8.2 Praktyczne zastosowania
📈 **Narzędzia biznesowe:**
- Automatyczna wycena nieruchomości
- Analiza rynków inwestycyjnych
- Planowanie rozwoju mieszkaniowego

📈 **Polityka publiczna:**
- Identyfikacja obszarów problemowych
- Planowanie inwestycji infrastrukturalnych
- Polityka dostępności mieszkań

### 8.3 Aktualizacja danych
🔄 **Potrzeba świeżych danych:**
- Aktualny stan rynku kalifornijskiego
- Wpływ technologii (Silicon Valley boom)
- Zmiany demograficzne i ekonomiczne

---

## 9. Podsumowanie

### 9.1 Główne wnioski
✅ **Lokalizacja dominuje:** Geografia jest najważniejszym czynnikiem cen  
✅ **Dochód kluczowy:** Najlepszy pojedynczy predyktor wartości  
✅ **Ocean premium:** Bliskość wody znacząco wpływa na ceny  
✅ **Różnice regionalne:** Systematyczne i statystycznie istotne  
✅ **Model funkcjonalny:** Prosty model ma praktyczne zastosowanie  

### 9.2 Wartość analizy
🎯 **Potwierdza intuicje:** Dane potwierdzają rynkowe oczekiwania  
🎯 **Dostarcza liczby:** Konkretne estymaty dla decyzji biznesowych  
🎯 **Identyfikuje wzorce:** Systematyczne różnice regionalne  
🎯 **Praktyczne zastosowanie:** Model użyteczny mimo prostoty  

### 9.3 Znaczenie historyczne
📚 **Trwałość wzorców:** Trendy z 1990 roku nadal aktualne  
📚 **Podstawy rynku:** Fundamentalne czynniki niezmienne  
📚 **Referencja:** Benchmark dla analiz współczesnych  

---

## Załączniki

### A. Szczegółowe statystyki
- Pełne tabele statystyk opisowych
- Wyniki testów statystycznych
- Parametry modeli regresji

### B. Kod źródłowy
- Notebook Jupyter z pełną analizą
- Skrypty do reprodukcji wyników
- Dokumentacja funkcji

### C. Wizualizacje
- Wysokorozdzielcze wykresy
- Mapy interaktywne
- Diagramy korelacji

---

**Kontakt:** bartosz.wysocki@example.com, tomasz.kowalski@example.com  
**Repozytorium:** https://github.com/BarWyDev/SAD-poject  
**Ostatnia aktualizacja:** 7 stycznia 2025 