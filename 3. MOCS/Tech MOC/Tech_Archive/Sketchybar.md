---
created: 2024-04-22T20:45
type: Programming Note
programming language: 
related: 
completed: false
updated: 2024-05-27T13:29
---
---

Sketchy Bar: [GitHub Page](https://github.com/FelixKratz/SketchyBar)

# Setup 

##### 1° Hide MacOS Bar
- Go to: System Settings > Control Center 
- Scroll all down 
- Set `Automatically hide and show the menu bar` to `Always`

##### Install SketchyBar
Run in your terminal `brew install SketchyBar

```shell
brew tap FelixKratz/formulae
brew install sketchybar
````

Run these commands to add default `~/.config/sketchybar` example configuration:

```shell
mkdir -p ~/.config/sketchybar
cp /opt/homebrew/opt/sketchybar/share/sketchybar/examples/sketchybarrc ~/.config/sketchybar/sketchybarrc
mkdir ~/.config/sketchybar/plugins
cp -r /opt/homebrew/opt/sketchybar/share/sketchybar/examples/plugins/ ~/.config/sketchybar/plugins/
chmod +x ~/.config/sketchybar/plugins/*
```

##### Install default nerd font

Run the following two commands:

```shell
brew tap homebrew/cask-fonts
rew install --cask homebrew/cask-fonts/font-jetbrains-mono-nerd-font
```

##### Install command line JSON processor (jq)

Run the following command to install jq:

```shell
brew install jq
```

##### Startup sketchybar

Run the following command:

```shell
brew services start sketchybar
```

---

# Config

In SketchyBar there are 2 files for each component. One for the actual item and one for the script. Before setting up each plugin, there are a few [default settings](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/sketchybarrc) and [variables](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/variables.sh) set. I won’t be explaining them as they are quite straightforward and can be understood through the [documentation](https://felixkratz.github.io/SketchyBar/).

The configurations — item file and script file — will be shown and some implementation details will be shown after.

> Note: Icons won’t show up on Medium or GitHub, so copy them and they should show up. If they still aren’t visible, ensure you are using a [Nerd Font](https://www.nerdfonts.com/).

## Spaces

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/spaces.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/space.sh)

```sh
#!/usr/bin/env bash  
  
SPACE_ICONS=("1" "2" "3" "4" "5" "6" "7" "8" "9" "10")  
  
sketchybar --add item spacer.1 left \  
 --set spacer.1 background.drawing=off \  
 label.drawing=off \  
 icon.drawing=off \  
 width=10  
  
for i in {0..9}; do  
 sid=$((i + 1))  
 sketchybar --add space space.$sid left \  
  --set space.$sid associated_space=$sid \  
  label.drawing=off \  
  icon.padding_left=10 \  
  icon.padding_right=10 \  
  background.padding_left=-5 \  
  background.padding_right=-5 \  
  script="$PLUGIN_DIR/space.sh"  
done  
  
sketchybar --add item spacer.2 left \  
 --set spacer.2 background.drawing=off \  
 label.drawing=off \  
 icon.drawing=off \  
 width=5  
  
sketchybar --add bracket spaces '/space.*/' \  
 --set spaces background.border_width="$BORDER_WIDTH" \  
 background.border_color="$RED" \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.color="$BAR_COLOR" \  
 background.height=26 \  
 background.drawing=on  
  
sketchybar --add item separator left \  
 --set separator icon= \  
 icon.font="$FONT:Regular:16.0" \  
 background.padding_left=26 \  
 background.padding_right=15 \  
 label.drawing=off \  
 associated_display=active \  
 icon.color="$YELLOW"
```

```sh
#!/usr/bin/env bash  
  
source "$HOME/.config/sketchybar/variables.sh" # Loads all defined colors  
  
SPACE_ICONS=("1" "2" "3" "4" "5" "6" "7" "8" "9" "10")  
  
SPACE_CLICK_SCRIPT="yabai -m space --focus $SID 2>/dev/null"  
  
if [ "$SELECTED" = "true" ]; then  
 sketchybar --animate tanh 5 --set "$NAME" \  
  icon.color="$RED" \  
  icon="${SPACE_ICONS[$SID - 1]}" \  
  click_script="$SPACE_CLICK_SCRIPT"  
else  
 sketchybar --animate tanh 5 --set "$NAME" \  
  icon.color="$COMMENT" \  
  icon="${SPACE_ICONS[$SID - 1]}" \  
  click_script="$SPACE_CLICK_SCRIPT"  
fi
```

> Note: The space config includes the separator icon (shaped like `>`)

To change what icons are used for spaces. change `SPACE_ICONS` in the plugin file. The defaults are numbers from `1–10`. Having fewer spaces is allowed and won’t impact the functionality of the component.

## Front App

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/front_app.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/front_app.sh)

```sh
#!/usr/bin/env sh  
  
COLOR="$WHITE"  
  
sketchybar \  
 --add item front_app left \  
 --set front_app script="$PLUGIN_DIR/front_app.sh" \  
 icon.drawing=off \  
 background.height=26 \  
 background.padding_left=0 \  
 background.padding_right=10 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.color="$BAR_COLOR" \  
 label.color="$COLOR" \  
 label.padding_left=10 \  
 label.padding_right=10 \  
 associated_display=active \  
 --subscribe front_app front_app_switched
```

```sh
#!/usr/bin/env sh  
  
case "$SENDER" in  
"front_app_switched")  
 sketchybar --set "$NAME" label="$INFO"  
 ;;  
esac
```

---
## Music

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/spotify.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/spotify.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$GREEN"  
  
sketchybar --add item spotify q \  
 --set spotify \  
 scroll_texts=on \  
 icon=󰎆 \  
 icon.color="$COLOR" \  
 icon.padding_left=10 \  
 background.color="$BAR_COLOR" \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.padding_right=-5 \  
 background.drawing=on \  
 label.padding_right=10 \  
 label.max_chars=23 \  
 associated_display=active \  
 updates=on \  
 script="$PLUGIN_DIR/spotify.sh" \  
 --subscribe spotify media_change
```

```sh
#!/usr/bin/env bash  
  
STATE="$(echo "$INFO" | jq -r '.state')"  
APP="$(echo "$INFO" | jq -r '.app')"  
  
if [ "$STATE" = "playing" ] && [ "$APP" == "Spotify" ]; then  
 MEDIA="$(echo "$INFO" | jq -r '.title + " - " + .artist')"  
 sketchybar --set "$NAME" label="$MEDIA" drawing=on  
else  
 sketchybar --set "$NAME" drawing=off  
fi
```

In order to see the current audio from any application not solely Spotify, remove `&& [ "$APP" == "Spotify" ]`. The current config uses `media_change`, which at the time of writing this article is experimental and has a few issues, so alternatively you can use `update_freq`.

## CPU

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/cpu.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/cpu.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$YELLOW"  
  
sketchybar --add item cpu right \  
 --set cpu \  
 update_freq=3 \  
 icon.color="$COLOR" \  
 icon.padding_left=10 \  
 label.color="$COLOR" \  
 label.padding_right=10 \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.padding_right=5 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.color="$BAR_COLOR" \  
 background.drawing=on \  
 script="$PLUGIN_DIR/cpu.sh"
```

```
#!/usr/bin/env bash  
  
sketchybar --set "$NAME" icon="" label="$(ps -A -o %cpu | awk '{s+=$1} END {s /= 8} END {printf "%.1f%%\n", s}')"
```

## Volume

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/volume.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/sound.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$GREEN"  
  
sketchybar \  
 --add item sound right \  
 --set sound \  
 icon.color="$COLOR" \  
 icon.padding_left=10 \  
 label.color="$COLOR" \  
 label.padding_right=10 \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.padding_right=5 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.color="$BAR_COLOR" \  
 background.drawing=on \  
 script="$PLUGIN_DIR/sound.sh" \  
 --subscribe sound volume_change
```

```sh
#!/usr/bin/env bash  
  
VOLUME=$(osascript -e "output volume of (get volume settings)")  
MUTED=$(osascript -e "output muted of (get volume settings)")  
  
if [ "$MUTED" != "false" ]; then  
 ICON="󰖁"  
 VOLUME=0  
else  
 case ${VOLUME} in  
 100) ICON="" ;;  
 [5-9]*) ICON="" ;;  
 [0-9]*) ICON="" ;;  
 *) ICON="" ;;  
 esac  
fi  
  
sketchybar -m \  
 --set "$NAME" icon=$ICON \  
 --set "$NAME" label="$VOLUME%"

```

## Battery

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/battery.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/power.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$CYAN"  
  
sketchybar --add item battery right \  
 --set battery \  
 update_freq=60 \  
 icon.color="$COLOR" \  
 icon.padding_left=10 \  
 label.padding_right=10 \  
 label.color="$COLOR" \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.padding_right=5 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.color="$BAR_COLOR" \  
 background.drawing=on \  
 script="$PLUGIN_DIR/power.sh" \  
 --subscribe battery power_source_change
```

```sh
#!/usr/bin/env bash  
  
PERCENTAGE=$(pmset -g batt | grep -Eo "\d+%" | cut -d% -f1)  
CHARGING=$(pmset -g batt | grep 'AC Power')  
  
if [ "$PERCENTAGE" = "" ]; then  
 exit 0  
fi  
  
case ${PERCENTAGE} in  
9[0-9] | 100)  
 ICON=""  
 ;;  
[6-8][0-9])  
 ICON=""  
 ;;  
[3-5][0-9])  
 ICON=""  
 ;;  
[1-2][0-9])  
 ICON=""  
 ;;  
*) ICON="" ;;  
esac  
  
if [ "$CHARGING" != "" ]; then  
 ICON=""  
fi  
  
sketchybar --set "$NAME" icon="$ICON" label="${PERCENTAGE}%"
```

## Date

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/calendar.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/calendar.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$BLUE"  
  
sketchybar --add item calendar right \  
 --set calendar update_freq=15 \  
 icon.color="$COLOR" \  
 icon.padding_left=10 \  
 label.color="$COLOR" \  
 label.padding_right=10 \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.padding_right=5 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.color="$BAR_COLOR" \  
 background.drawing=on \  
 script="$PLUGIN_DIR/calendar.sh"
```

```sh
#!/usr/bin/env bash  
  
sketchybar --set "$NAME" icon="󰸗" label="$(date '+%a %d. %b')"
```

## Time

[item file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/items/clock.sh) and [script file](https://github.com/tcmmichaelb139/.dotfiles/blob/main/sketchybar/.config/sketchybar/plugins/clock.sh)

```sh
#!/usr/bin/env bash  
  
COLOR="$MAGENTA"  
  
sketchybar --add item clock right \  
 --set clock update_freq=1 \  
 icon.padding_left=10 \  
 icon.color="$COLOR" \  
 icon="" \  
 label.color="$COLOR" \  
 label.padding_right=5 \  
 label.width=78 \  
 align=center \  
 background.height=26 \  
 background.corner_radius="$CORNER_RADIUS" \  
 background.padding_right=2 \  
 background.border_width="$BORDER_WIDTH" \  
 background.border_color="$COLOR" \  
 background.color="$BAR_COLOR" \  
 background.drawing=on \  
 script="$PLUGIN_DIR/clock.sh"
```

```sh
#!/usr/bin/env bash  
  
LABEL=$(date '+%H:%M:%S')  
sketchybar --set "$NAME" label="$LABEL"
```

---