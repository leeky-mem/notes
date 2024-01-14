## Run yakuake in an Xorg context in a wayland environment to get all behavior features
`QT_QPA_PLATFORM=xcb yakuake &.`\
### To autostart yakuake in Xorg context
Copy: `/usr/share/applications/org.kde.yakuake.desktop` to `$XDG_CONFIG_DIR/autostart/org.kde.yakuake.desktop`\
Add `Exec=yakuake` to `Exec=env QT_QPA_PLATFORM=xcb yakuake` in the autostart .desktop file

## Nice Themes
- Cattppuccin Sky-Dark
- Solarized
