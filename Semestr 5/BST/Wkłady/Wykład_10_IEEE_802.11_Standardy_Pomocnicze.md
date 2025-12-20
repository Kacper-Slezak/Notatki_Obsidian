---
tags:
  - wykład
  - standardy
  - bridge
  - regulatory
  - 80211g
alias:
  - Wykład 10 - Standardy Pomocnicze
---
# Wykład 10: IEEE 802.11 Część V - Standardy Pomocnicze i 802.11g

W tym wykładzie omawiane są standardy, które niekoniecznie zwiększają prędkość (poza 'g'), ale są niezbędne do poprawnego działania sieci w środowisku globalnym i korporacyjnym.

## 1. IEEE 802.11c (Bridge Operation Procedures)
Standard techniczny, kluczowy dla producentów Access Pointów (AP).
* **Problem:** AP działa jako most (Bridge) między medium bezprzewodowym (802.11) a przewodowym (802.3 Ethernet).
* **Rozwiązanie:** 802.11c definiuje procedury mapowania ramek i priorytetów (z 802.11e na 802.1D) w warstwie MAC.
* **Wymóg:** Każdy AP musi obsługiwać 802.11c, aby poprawnie przekazywać ramki do Systemu Dystrybucyjnego (DS).

## 2. IEEE 802.11d (Global Harmonization / World Mode)
Umożliwia produkcję jednego urządzenia Wi-Fi na cały świat, które dostosowuje się do lokalnych przepisów prawnych.
* **Działanie:** AP rozgłasza w ramkach Beacon informacje o "Domenie Regulacyjnej" (Regulatory Domain):
    * Kod kraju (np. PL, US, JP).
    * Listę dozwolonych kanałów.
    * Maksymalną moc nadawania.
* **Korzyść:** Klient (np. laptop) po włączeniu nasłuchuje AP. Jeśli usłyszy kod "JP" (Japonia), odblokuje kanał 14. Jeśli "US", zablokuje kanały 12-14.

## 3. IEEE 802.11f (IAPP - Inter-Access Point Protocol)
* **Status:** **Wycofany** (Zastąpiony przez 802.11r).
* **Cel:** Umożliwienie komunikacji między AP różnych producentów w celu obsługi roamingu.
* **Mechanizm:** Gdy stacja zmienia AP (Reassociation), nowy AP kontaktuje się ze starym AP (po Ethernecie), aby pobrać kontekst stacji (np. zbuforowane ramki).
* **Wada:** Brak bezpieczeństwa (przesyłanie danych jawnym tekstem), co doprowadziło do wycofania standardu.

## 4. IEEE 802.11g (Ewolucja w 2.4 GHz)
Wprowadzony w 2003 roku, aby przenieść prędkość z 802.11a (54 Mbps) do pasma 2.4 GHz.
* **Pasmo:** 2.4 GHz.
* **Modulacja:** **ERP-OFDM** (Extended Rate PHY).
* **Prędkości:** 6, 9, 12, 18, 24, 36, 48, 54 Mbps.
* **Kompatybilność wsteczna:** Musi współpracować z 802.11b (DSSS/CCK).

### Mechanizmy ochrony (Protection Mechanisms)
Gdy w sieci są stare urządzenia 802.11b, 802.11g musi zwolnić lub używać "ochraniaczy", aby nie zakłócić starszych stacji (które nie rozumieją modulacji OFDM).
1.  **RTS/CTS Protection:** Przed wysłaniem ramki OFDM (szybkiej), stacja wysyła RTS/CTS w modulacji DSSS (wolnej), aby wyciszyć stare urządzenia 'b'.
2.  **CTS-to-Self:** Stacja wysyła CTS do samej siebie (w DSSS), aby zarezerwować kanał. Mniejszy narzut niż pełne RTS/CTS.
* **Koszt:** Obecność chociaż jednej stacji 802.11b w sieci 802.11g drastycznie obniża przepustowość całej sieci (przez narzut nagłówków DSSS).