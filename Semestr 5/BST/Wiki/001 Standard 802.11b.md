# Twarde Statystyki 

## Prędkość przesyłania 

- 1, 2, 5.5, 11 Mbit/s

## Zasięg transmisji

- 300 metrów na zewnątrz
- 30 metrów wewnątrz
- 10 metrów wewnątrz przy maksymalnej prędkości

## Częstotliwość

- 2.4 GHz - ISM band

## Bezpieczeństwo

- [[LAB 003 | WEP]]

## Jakość transmisji

- Best Efford tylko

## Wady i Zalety
1. Wady
	- Duże interferencje na 2.4 GHz
	- bez Qos
	- Niska prędkość relatywnie
2. Zalety
	- dużo systemów zainstalowych z tym
	- dużo doświadczenia
	- dostępny wszędzie
	- ISM-band darmowe
	- dużo vendorów
	- zintegrowane z laptopami
	- prosty system

# Modulacje 

- 1 i 2 Mbit/s używają 11-bitowego Bakera i DBPSK dla 1 oraz DQPSK dla 2
- Wyższe prędkości używają CCK
### DSSS

- 14 kanałów każdy 22 Mhz szerokości co 5 MHz
- 1 kanał to 2.412 GHz
- Stany i Kanada to 11 kanałów 
- Europa to kanałów 13
- Frnacja 10 -13
- Hiszpania 10 -11
- Japonia 14
- 3 nie nachodzące kanały

# Warstwa Fizyczna

## Ramka PHY
#### Long
- PLCP preambuła
	- synchronizacja 128
	- SFD 16 
	- 1 Mbit na sekunde DBPSK
- PLCP nagłówek
	- sygnał - modulacja typ oraz prędkośc
	- HEC 
	- 48 bit
	- 1Mbit na sekunde DBPSK
- Dane
#### Short

- PLCP preambuła
	- 56 synchronizacja
	- SFD 16
	- 1 Mbit na sekund DBPSK
- PLCP nagłówek 
	- 48 bit
	- 2 Mbit na sekunde DQPSK

#### IFS

1. SIFS - 10 us 
2. DIFS - SIFS + 2 slot time - 50 us
	1. Slot time - 20 us