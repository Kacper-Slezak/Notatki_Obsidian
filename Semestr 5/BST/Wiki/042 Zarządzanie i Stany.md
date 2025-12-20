---
tags: [zarządzanie, stany, power-save, scanning]
---
# Zarządzanie Siecią WLAN

## Maszyna Stanów (State Machine)
Stacja nie może po prostu wysłać danych. Musi przejść przez proces przyłączania.

1.  **Stan 1: Unauthenticated, Unassociated**
    * Stan początkowy (np. po włączeniu).
    * Stacja może wysyłać tylko: Class 1 Frames (Probe, Beacon, Auth, ACK).
    * Próba wysłania danych = AP odsyła `Deauthentication`.
2.  **Stan 2: Authenticated, Unassociated**
    * Po wymianie ramek **Authentication** (sukces).
    * Stacja jest "znana", ale nie ma dostępu do sieci (DS).
    * Dozwolone: Class 1 + Class 2 Frames (Association, Reassociation).
3.  **Stan 3: Authenticated, Associated**
    * Po wymianie ramek **Association** (sukces).
    * Pełny dostęp do sieci. AP przekazuje ramki do Internetu.
    * Dozwolone: Wszystkie ramki (Class 1, 2, 3).

## Skanowanie (Wykrywanie Sieci)
* **Pasywne (Passive):** Nasłuchiwanie ramek **Beacon** wysyłanych okresowo przez AP (np. co 100 ms). Oszczędza energię.
* **Aktywne (Active):** Stacja wysyła **Probe Request** (na każdym kanale). AP odpowiada ramką **Probe Response**. Szybsze, ale zużywa baterię.

## Zarządzanie Energią (Power Management)
WLAN jest "prądożerny", więc stacje często śpią (Sleep Mode).

* **Zasada:** Stacja wyłącza radio i budzi się tylko na ramki Beacon (zgodnie z interwałem DTIM).
* **TIM (Traffic Indication Map):** Mapa bitowa w Beaconie.
    * Jeśli Twój bit = 1, to AP ma dla Ciebie dane w buforze.
    * Stacja wysyła **PS-Poll** (Power Save Poll), żeby pobrać te dane.
* **DTIM (Delivery TIM):** Licznik co ile Beaconów wysyłane są dane Broadcast/Multicast. Wymaga wybudzenia wszystkich stacji.