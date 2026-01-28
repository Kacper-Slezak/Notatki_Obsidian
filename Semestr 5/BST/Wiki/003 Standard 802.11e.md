# Standard wprowadzający QoS 
## HCF

- Fundamentalny mechanizm dostępu do medium w 802.11e
- Zastąpił on DCF i PCF
- Jest to kombinacja dwóch typów dostępu EDCA (Enhanced Distributed Channel Access) i HCCA  (HCF Controlled Channel Access)
## APSD - Automatic Power Save Delivery 

- jest to bardziej wydajna obsługa oszczędności energii niż Power Save Poll
- użyteczne dla VoIP 
# BA - Block ACK

- pozwala na odpowiedź potwierdzającą cały okres TXOP w jednej ramce 
- mniejszy narzut protokołu

## NO ACK 

- ramki QoS mają pole czy jest potrzebny ACK czy brak ACK oi w przypadku braku ACK po prostu nie wysyłamy potwierdzenia
- pomaga w przypaku transmisji danych krytycznych czasowo

## DLS - Direct Link Setup 
## DLP - Direct Link Protocol

- Transmisja w BSS która pomija AP 
- Jedyna aktywność AP to zestawienie połączenia
# TXOP

- Defniujemy czas startowy oraz długość transmisji
- Aby mieć czas TXOP trzeba albo 
	- Wygrać EDCA rywalizacje
	- Albo otrzymać poll t trakcie okresu CP od HCCA
## EDCA

1. Mechanizm dostępu do medium wprowadzony w standardzie 802.11e
2. Rozszerzenie podstawowego DCF o usługi QoS
3. Działa na zasadzie definicji kategorii dostępu które są mapowane na 8 priorytetów
	1. Kategorie dostępu
		- Głos
		- Video
		- Best efford
		- Background
	2. Ruch o wyższym priorytecie otrzymuje dostęp do medium wcześniej
## HCCA

- Podobne do PCF 
- Jest to PC czyli okno w którym wybierasz po priorytecie która stacja dostaje QoS-poll
- Tej stacji zostaje przydzilony czas TXOP i ona może nadać ile chce w tym oknie
- i potem kolejna
