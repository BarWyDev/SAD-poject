# Projekt końcowy: Analiza cen nieruchomości w Kalifornii

## Opis projektu

Projekt realizuje eksploracyjną analizę danych (EDA) na zbiorze danych **California Housing Prices** zgodnie z wymaganiami projektu końcowego z przedmiotu Statystyczna Analiza Danych.

## Struktura projektu

```
projekt_koncowy/
├── README.md                    # Ten plik
├── projekt_housing.ipynb        # Główny notebook z analizą  
├── housing.csv                  # Dane California Housing
└── requirements.txt             # Wymagane biblioteki
```

## Zbiór danych

**California Housing Prices** - dane z kalifornijskiego spisu mieszkaniowego z 1990 roku zawierające informacje o:
- Cenach nieruchomości (median_house_value) - **zmienna zależna**
- Lokalizacji geograficznej (longitude, latitude)
- Charakterystykach mieszkaniowych (wiek, liczba pokoi, sypialni)
- Danych demograficznych (populacja, dochody, gospodarstwa domowe)
- Bliskości oceanu (ocean_proximity)

Źródło: [Kaggle - California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices)

## Pytania badawcze

1. Jakie są główne czynniki wpływające na ceny nieruchomości w Kalifornii?
2. Czy lokalizacja geograficzna ma znaczący wpływ na wartość nieruchomości?
3. Jak dochód mieszkańców koreluje z cenami domów?
4. Czy istnieją znaczące różnice w cenach według bliskości oceanu?
5. Jakie charakterystyki mieszkaniowe mają największy wpływ na cenę?

## Struktura analizy

Zgodnie z wymaganiami projekt zawiera następujące sekcje:

### 1. Wprowadzenie (2 punkty)
- Opis zbioru danych i jego pochodzenia
- Definicja pytań badawczych
- Opis zmiennych

### 2. Czyszczenie i porządkowanie danych (4 punkty)
- Diagnostyka danych (typy, rozmiar, podstawowe statystyki)
- Analiza braków danych z wizualizacją (heatmapy, shadowmapy)
- Identyfikacja i analiza obserwacji odstających
- Imputacja braków danych
- Weryfikacja reguł biznesowych i logicznych

### 3. Wizualizacje (4 punkty)
- **Wizualizacja 1**: Rozkład cen nieruchomości i boxploty według bliskości oceanu
- **Wizualizacja 2**: Mapa geograficzna cen w Kalifornii
- **Wizualizacja 3**: Korelacja dochodu z cenami (scatterplot + hexbin)
- **Wizualizacja 4**: Charakterystyki mieszkaniowe vs ceny (4 subploty)
- **Wizualizacja 5**: Macierz korelacji głównych zmiennych

### 4. Analiza opisowa (4 punkty)
- **Analiza 1**: Statystyki opisowe według bliskości oceanu + test ANOVA
- **Analiza 2**: Macierz korelacji i regresja liniowa (dochód -> cena)
- **Analiza 3**: Segmentacja geograficzna (Bay Area, LA, Coastal, Inland)

### 5. Wnioski (2 punkty)
- Odpowiedzi na pytania badawcze
- Główne odkrycia i wzorce
- Ograniczenia analizy
- Rekomendacje na przyszłość

## Wymagane biblioteki

```python
pandas>=1.3.0
numpy>=1.20.0
matplotlib>=3.4.0
seaborn>=0.11.0
scipy>=1.7.0
jupyter>=1.0.0
```

## Instalacja i uruchomienie

1. Sklonuj/pobierz projekt
2. Zainstaluj wymagane biblioteki:
   ```bash
   pip install -r requirements.txt
   ```
3. Uruchom Jupyter Notebook:
   ```bash
   jupyter notebook projekt_housing.ipynb
   ```

## Główne wyniki

### Kluczowe czynniki wpływające na ceny:
- **Dochód mieszkańców** (r≈0.69) - najsilniejszy predyktor
- **Lokalizacja geograficzna** - nieruchomości na wybrzeżu znacznie droższe
- **Liczba pokoi/sypialni na gospodarstwo** - pozytywna korelacja

### Różnice regionalne:
- **Bay Area**: najwyższe ceny (średnia ~$370k)
- **Los Angeles**: wysokie ceny
- **Wybrzeże**: średnie-wysokie ceny  
- **Inland**: najniższe ceny (średnia ~$125k)

### Statystyki:
- Korelacja dochód-cena: r≈0.69
- Wzrost dochodu o $10k → wzrost ceny o ~$42k
- Dochód wyjaśnia 47% wariancji cen

## Autorzy

[Miejsce na nazwiska członków zespołu]

## Licencja

Projekt edukacyjny - Statystyczna Analiza Danych 