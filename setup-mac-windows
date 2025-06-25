#!/usr/bin/env bash

echo "🔧 Beginne Windows-liken Setup auf macOS..."

# 1. Admin-Sudo-Kontrolle
sudo -v

# 2. Homebrew prüfen oder installieren
if ! command -v brew &>/dev/null; then
  echo "📦 Homebrew nicht gefunden – wird installiert..."
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
  eval "$(/opt/homebrew/bin/brew shellenv)"
fi

# 3. Grund-Tools installieren
brew update
brew install --cask google-chrome raycast rectangle alt-tab

# 4. Dock & Systemeinstellungen konfigurieren
echo "⚙️ Systemeinstellungen anpassen..."

# Dock unten + autohide + ohne Vergrößerung
defaults write com.apple.dock orientation -string "bottom"
defaults write com.apple.dock autohide -bool true
defaults write com.apple.dock magnification -bool false
defaults write com.apple.dock tilesize -int 36

# Entferne alle aktuellen Dock-Icons
defaults delete com.apple.dock persistent-apps
defaults delete com.apple.dock persistent-others

# Füge nur Chrome + Finder + Systemeinstellungen hinzu
defaults write com.apple.dock persistent-apps -array-add \
  '<dict><key>tile-data</key><dict><key>file-data</key><dict>'\
  '<key>_CFURLString</key><string>/Applications/Google Chrome.app</string>'\
  '<key>_CFURLStringType</key><integer>0</integer></dict></dict>'
defaults write com.apple.dock persistent-apps -array-add \
  '<dict><key>tile-data</key><dict><key>file-data</key><dict>'\
  '<key>_CFURLString</key><string>/System/Applications/Finder.app</string>'\
  '<key>_CFURLStringType</key><integer>0</integer></dict></dict>'

# Systemverhalten (Scrollrichtung + Rechtsklick)
defaults write NSGlobalDomain com.apple.swipescrolldirection -bool false
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadRightClick -bool true
defaults write NSGlobalDomain AppleEnableSecondaryClick -bool true

# Finder-Anpassungen
defaults write com.apple.finder ShowPathbar -bool true
defaults write com.apple.finder ShowStatusBar -bool true
defaults write com.apple.finder FXPreferredViewStyle -string "clmv"
defaults write com.apple.finder NewWindowTarget -string "PfLo"
defaults write com.apple.finder NewWindowTargetPath -string "file://${HOME}/Desktop/"
killall Finder

# F-Tasten ohne Fn-Taste als Standard
defaults write -g com.apple.keyboard.fnState -bool true

# Neustart des Docks
killall Dock

echo "✅ Setup abgeschlossen! Dein macOS ist jetzt Windows-näher konfiguriert."
echo "Starte Raycast, AltTab & Rectangle für vollen Effekt."
