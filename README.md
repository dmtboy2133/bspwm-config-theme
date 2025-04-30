# bspwm-config-theme
# Руководство по настройке темы Waybar

## Введение
Это руководство поможет вам настроить и кастомизировать тему для Waybar - расширяемой панели статуса для оконных менеджеров (Sway, Hyprland, i3, BSPWM и других).

## Требования
- Установленный Waybar (проверьте командой `which waybar`)
- Базовые навыки работы с терминалом
- Текстовый редактор (nvim, vim, VS Code и др.)

## 1. Базовая настройка Waybar

### Создание конфигурационных файлов
Если папка конфигурации Waybar отсутствует:
```bash
mkdir -p ~/.config/waybar
```

Создаем основные файлы:
```bash
touch ~/.config/waybar/{config,style.css}
```

### Пример минимального конфига
Откройте файл `~/.config/waybar/config` и добавьте:
```json
{
  "layer": "top",
  "position": "top",
  "modules-left": ["sway/workspaces", "sway/mode"],
  "modules-center": ["sway/window"],
  "modules-right": ["pulseaudio", "network", "clock", "tray"],
  "clock": {
    "format": "{:%H:%M}"
  }
}
```

## 2. Настройка цветовой темы

### Создание стилей
Откройте `~/.config/waybar/style.css` и добавьте:
```css
* {
  font-family: "Fira Code", "Font Awesome 6 Free";
  font-size: 12px;
}

window#waybar {
  background: #1e1e2e;  /* Цвет фона */
  color: #cdd6f4;      /* Цвет текста */
}

#workspaces button.active {
  color: #f5c2e7;      /* Цвет активного рабочего пространства */
}

#clock {
  background: #585b70;
  padding: 0 10px;
  border-radius: 5px;
}
```

### Основные CSS-переменные
Для удобства управления цветами:
```css
@define-color background #1e1e2e;
@define-color text      #cdd6f4;
@define-color accent    #f5c2e7;
@define-color warning   #f38ba8;
```

## 3. Интеграция с Dotfiles

### Перенос конфигов в репозиторий
```bash
mkdir -p ~/dotfiles/config/waybar
cp ~/.config/waybar/* ~/dotfiles/config/waybar/
```

### Создание симлинков
```bash
rm -rf ~/.config/waybar
ln -s ~/dotfiles/config/waybar ~/.config/waybar
```

## 4. Дополнительные настройки

### Иконки (Font Awesome)
Пример для модуля громкости:
```json
"pulseaudio": {
  "format": "{volume}% {icon}",
  "format-icons": ["", "", ""]
}
```

### Градиенты
```css
#custom-module {
  background: linear-gradient(90deg, #cba6f7, #f5c2e7);
}
```

## 5. Перезапуск Waybar

### Быстрый перезапуск
```bash
pkill waybar && waybar &
```

### Полная перезагрузка
Для Sway:
```bash
swaymsg reload
```

Для Hyprland:
```bash
hyprctl reload
```

## 6. Устранение проблем

### Waybar не запускается
Проверьте логи:
```bash
waybar -l debug
```

### Проблемы со шрифтами
Установите необходимые шрифты:
```bash
paru -S ttf-firacode-nerd  # Для Arch Linux
```

### Цвета не применяются
Проверьте:
1. Синтаксис CSS
2. Правильность симлинков
3. Наличие всех зависимостей

