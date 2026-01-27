	HSP (High-Speed PHY) (5 GHz)


# Twarde statystki
## Prędkości przesyłania danych

1. 6, 9 , 12 , 18, 24, 36, 48, 54 Mbit
2. 6, 12, 24 jest wymuszone

## Zasięg transmisji

- 100 m na zewnątrz, 10 metrów w budynku

## Częstotliwość

- 5.15-5.25, 5.25-5.35, 525-5.825
- ISM band ???

## Bezpieczeństwo

- [[LAB 003 | WEP]]

## Jakość obsługi

- Best Efford tylko

## Wady / Zalety

1. Wady
	- większe rozproszenie przez wyższe pasmo
	- brak QoS
2. Zalety
	- Dopasowany do standardów 802.x 
	- Darmowe ISM-band,
	- prosty system
	- używa mniej zajętego pasma 5 GHz

## Kanały

1. center frequency = 5000 + 5*channel number
2. Numery kanałów - 36-64 co 4 oraz 149 -161 co 4

### Szerokość kanłów

- 20 MHz
# OFDM

## Modulacje:

- BPSK
- QPSK
- 16-QAM
- 64-QAM

## Parametry:

- Użyteczny symbol - 3.2 us
- Interwał bezpieczeństwa - 0.8 us
- Rozmiar FFT - 64
- Używa 52 podnośnych (48 danych i 4 pilotażowych)
- Odstęp 312.5 kHz


# Warstwa Fizyczna

## Ramka PHY

- PCLP preambuła 
- PLCP header - 6 Mbit/s
- Dane - możliwe prędkości przesyłu 