
# kSnarf
kSnarf is a tool written in [Python](https://www.python.org/) that extracts various data points in real time or for a period of time in the past.

Point retention is handled by a local or remote [PostgreSQL](https://www.postgresql.org/) instance allowing for multi-user interaction.

Data visualization is left to the user.  Some ideas that come to mind are [Grafana](https://grafana.com/), [Plotly](https://plotly.com/) and [Maltego](https://www.maltego.com/).

The default usage for kSnarf is aimed at wireless traffic and works with any network card so long as it can drop to [Monitor Mode](https://www.geeksforgeeks.org/how-to-put-wifi-interface-into-monitor-mode-in-linux/) at a minimum.  [piCopilot](https://github.com/stryngs/piCopilot#lessons-learned-from-tools-like-picopilot) is one such tool leveraging the kSnarf libraries in this manner.

New public modules are added to kSnarf by request or as development takes place.  Current development for kSnarf is focused on [SDR](https://en.wikipedia.org/wiki/Software-defined_radio).

# Public modules
- [802.11](https://en.wikipedia.org/wiki/IEEE_802.11)
- [802.15](https://en.wikipedia.org/wiki/IEEE_802.15)
- [TPMS](https://en.wikipedia.org/wiki/Tire-pressure_monitoring_system)

# Privately available modules upon request
Support for various things such as Ethernet monitoring (802.3), IDS or IPS, **non-root code execution** and so forth may be requested via [chat](https://app.gitter.im/#/room/#kSnarf:gitter.im).

# Recommended, but optional hardware
- [HackRF One](https://greatscottgadgets.com/hackrf/one/)
- [SDR Dongle](https://hackerwarehouse.com/product/rtlsdr/)
- [Ubertooth One](https://greatscottgadgets.com/ubertoothone/)

# Required hardware
- Any 802.11 NIC capable of [Monitor mode](https://en.wikipedia.org/wiki/Monitor_mode)

# Recommended, but optional software
- [Aircrack-ng](https://www.aircrack-ng.org/)

# Getting started
Install PostgreSQL locally
```sql
CREATE ROLE root WITH SUPERUSER LOGIN;
ALTER USER root WITH PASSWORD 'idrop';
CREATE DATABASE idrop;
```

## Module requirements
```
python3 -m venv env
source env/bin/activate
python3 -m pip install RESOURCEs/*.tar.gz
```

## Getting started with 802.11 ([Scapy](https://github.com/secdev/scapy))
Modify ./system.conf if nothing else to ensure prop.nic makes sense, by default prop.nic is set to wlan1mon.
```bash
sudo python3 ./kSnarf.py
```
```bash
sudo psql idrop
```
```sql
SELECT * FROM main;
```

## Getting started with 802.15 ([Ubertooth One](https://greatscottgadgets.com/ubertoothone/))
```bash
sudo python3 ./kBlue.py
```
```bash
sudo psql idrop
```
```sql
SELECT * FROM blue;
```

## Getting started with TPMS ([rtl_433](https://github.com/merbanan/rtl_433))
The current implementation is a proof of concept which will be classed out and grown as more vendors are verified.
```bash
python3 ./kTpms.py
```
```sql
SELECT * FROM tpms;
```
