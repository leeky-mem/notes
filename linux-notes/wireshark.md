# Wireshark

## Add OpenThread support
- Configure Wireshark according to [this](https://openthread.io/guides/pyspinel/wireshark) manual.
- Add user to wireshark group\
  `sudo usermod -aG wireshark <user>`
- Flash the 802.15.4 sniffer [firmware](https://github.com/NordicSemiconductor/nRF-Sniffer-for-802.15.4/releases) to an nRF52840_dongle\
  `nrfjprog --chiperase --family nrf52 --program nrf802154_sniffer_dongle.hex`
- In case the nRF 802.15.4 sniffer firmware does not work build the OpenThread ot-rcp firmware binary according to [this](https://openthread.io/guides/build#binaries) manual
- Install the pyspinel package\
  `sudo pacman -S python-pyspinel`
- Add the following symlink:
  ```bash
  mkdir ~/.local/lib/wireshark/extcap
  ln -s ~/.local/lib/wireshark/extcap/ ~/.local/lib/wireshark/extcap/
  ```
