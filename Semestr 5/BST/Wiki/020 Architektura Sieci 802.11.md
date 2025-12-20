---
tags: [architektura, definicje, bss, ess]
---
# Architektura Sieci IEEE 802.11

Standard definiuje warstwę fizyczną (PHY) i podwarstwę MAC. Architektura opiera się na "komórkach" radiowych.

## Elementy Składowe
* **STA (Station):** Każde urządzenie z interfejsem 802.11 (Laptop, Smartfon, AP).
* **AP (Access Point):** Stacja pełniąca funkcję "mostu" i zarządcy w trybie infrastruktury.
* **BSS (Basic Service Set):** Podstawowa "komórka". Zbiór stacji pod kontrolą jednego AP (Infrastructure BSS) lub grupa stacji połączonych bezpośrednio (IBSS/Ad-hoc).
    * Każdy BSS ma unikalny **BSSID** (zazwyczaj adres MAC radia AP).
* **DS (Distribution System):** System (zazwyczaj Ethernet) łączący wiele AP. To "kręgosłup" sieci.
* **ESS (Extended Service Set):** Wiele BSS-ów połączonych przez DS. Użytkownik widzi to jako jedną sieć (jeden SSID), mimo że przełącza się między AP.
* **Portal:** Punkt styku sieci 802.11 z inną siecią (np. 802.3 Ethernet). Zazwyczaj fizycznie wbudowany w AP.

## Usługi (Services)
Standard dzieli usługi na stacyjne (SS) i dystrybucyjne (DS).

| Usługi Stacyjne (SS)                   | Usługi Systemu Dystrybucyjnego (DS) |
| :------------------------------------- | :---------------------------------- |
| Uwierzytelnianie (Authentication)      | Asocjacja (Association)             |
| Od-uwierzytelnianie (Deauthentication) | Reasocjacja (Reassociation)         |
| Prywatność (Privacy/Encryption)        | Deasocjacja (Disassociation)        |
| Dostarczanie danych (Data Delivery)    | Integracja (Integration)            |
|                                        | Dystrybucja (Distribution)          |

> [!note] Roaming
> Roaming to *nie* jest standardowa usługa w podstawowym 802.11. To "Reasocjacja" pozwala na przemieszczanie się, ale decyzja "kiedy się przełączyć" należy do sterownika karty sieciowej klienta.