# ESPHome LED Effects

Felles adressebare LED-animasjoner for ESPHome, laget for ESP32 og ESP8266.

**Effekter:** Rainbow, Random Twinkle, Twinkle, Fireworks, Flicker, Blue Scan,
Gold Glitter, Fire, Aurora Borealis og Halloween - Haunted.

## Legg til på en ESPHome-enhet

Lim inn følgende i den **lokale** ESPHome-konfigurasjonen:

```yaml
packages:
  led_animasjoner:
    url: https://github.com/tony9700/esphome-led-effects
    files:
      - effects/common.yaml
    ref: main
    refresh: 5min
```

Den lokale `light:`-konfigurasjonen må bruke **`id: stripe`**.
Da merges effektlisten fra pakken inn på samme lys.

Eksempel for ESP32 og WS2811:

```yaml
light:
  - platform: esp32_rmt_led_strip
    id: stripe
    name: "WS2811 LED"
    pin: GPIO17
    chipset: WS2811
    channel_colors: RGB
    num_leds: 100
    max_refresh_rate: 25ms
    rmt_symbols: 128
    use_psram: false
```

Tilpass GPIO, LED-type, fargerekkefølge og antall LED-er for hver enhet.
Behold nettverksoppsett, astrour, MQTT og passord lokalt. Se
[`examples/esp32-rmt.yaml`](examples/esp32-rmt.yaml) og
[`examples/esp8266-neopixelbus.yaml`](examples/esp8266-neopixelbus.yaml).

### Viktige merknader

- Fjern tidligere lokale effekter med samme navn, for å unngå duplikater.
- `refresh: 5min` betyr kun at **ESPHome-byggeverktøyet** kan hente ny
  GitHub-kode ved kompilering. ESP-enheten oppdateres **ikke automatisk**:
  bygg ny firmware og installer OTA.
- Når installasjonene er stabile, bruk en versjonstag i `ref:` i stedet for
  `main` for å unngå utestede endringer.
- **Ikke legg inn Wi-Fi-passord, API-nøkler, MQTT-passord eller andre hemmeligheter
  i dette offentlige repositoryet.** Hold dem i lokal `secrets.yaml`.
- En 12 V WS2811-stripe skal fortsatt ha 12 V strømforsyning. For en 3,3 V ESP32
  kan datasignalet nivåskiftes til 5 V, eksempelvis med 74AHCT125 og felles GND.
- Effektlisten har blitt syntaksgjennomgått, men er **ikke fullkompilert på maskinvare**.
  Test én enhet før flere oppdateres.

## Vedlikehold

Endre `effects/common.yaml`, commit til GitHub, og kompiler og installer
ny firmware på de enhetene som skal få de nye animasjonene.

Fire-effekten bruker en varmetabell som følger antall LED-er, så den er ikke
begrenset til en fast størrelse slik den gamle implementasjonen var.
