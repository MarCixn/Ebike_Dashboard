# Ebike Dashboard - Założenia Projektowe

## Architektura systemu

```
[STM32] <--UART--> [nRF52832 Ebyte E73] <--BLE--> [PWA Dashboard]
```

### Komponenty

| Komponent | Rola |
|-----------|------|
| STM32 | Główny kontroler ebike, odczytuje dane z pojazdu |
| nRF52832 (Ebyte E73-2G4M04S1B) | Moduł BLE, pośredniczy między STM32 a telefonem |
| PWA Dashboard | Aplikacja webowa w przeglądarce (GitHub Pages) |

## Funkcje dashboardu

- **Prędkość** - aktualna prędkość w km/h
- **Prąd** - pobór prądu w A
- **Bateria** - napięcie (V) + poziom naładowania (%)
- **Temperatury** - silnik, kontroler, zewnętrzna, 3x bateria
- **Limit prędkości** - ustawiany przez użytkownika
- **System PIN** - zabezpieczenie dostępu
- **Blokada roweru** - zdalne blokowanie/odblokowanie
- **PWA** - działa offline, można zainstalować na telefonie

## UUID charakterystyk BLE

| Charakterystyka | UUID |
|-----------------|------|
| Service | 12345678-1234-5678-1234-56789abcdef0 |
| Speed | 12345678-1234-5678-1234-56789abcdef1 |
| Current | 12345678-1234-5678-1234-56789abcdef2 |
| Battery | 12345678-1234-5678-1234-56789abcdef3 |
| Temperatures | 12345678-1234-5678-1234-56789abcdef4 |
| Max Speed | 12345678-1234-5678-1234-56789abcdef5 |
| PIN | 12345678-1234-5678-1234-56789abcdef6 |
| Lock | 12345678-1234-5678-1234-56789abcdef7 |

## Struktura plików

```
C:\xampp\htdocs\xd\           # Dashboard PWA
├── index.html                # Główna strona
├── manifest.json             # PWA manifest
├── sw.js                     # Service Worker
└── PROJECT.md                # Ten plik

C:\Users\MarCixn\NRF_Dashboard\   # Firmware nRF52
├── src\main.c                # Kod BLE
├── prj.conf                  # Konfiguracja Zephyr
└── app.overlay               # Devicetree overlay
```

## Hardware

- **MCU BLE**: Ebyte E73-2G4M04S1B (nRF52832)
- **Programator**: J-Link V9 (clone)
- **SDK**: nRF Connect SDK v3.2.3
