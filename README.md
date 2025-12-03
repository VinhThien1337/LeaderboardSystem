> **-------------------------------------------------------**
# LeaderboardSystem Plugin

## Giới Thiệu
**LeaderboardSystem** là plugin Minecraft được phát triển và sở hữu bởi **VinhThien** giúp tạo một hệ thống bảng xếp hạng tuyệt vời bằng gui dễ tiếp cận

**Thông Tin Plugin:**
- **Plugin version:**: 1.1
- **Author:**: VinhThien
- **Tương thích**: Spigot/Paper 

---

## Danh Sách Lệnh

### Lệnh Quảng Lý Dành Cho Admin
```bash
/leaderboardsystem help                    # Xem các lệnh của plugin
/leaderboardsystem reload                  # Load lại toàn bộ cấu hình
/leaderboardsystem version                 # Xem phiên bản plugin
```

### **Lệnh Admin - Quản Lý Crate**
```bash
/leaderboard                   # Mở gui bảng xếp hạng
/leaderboard search <leaderboard> <tên_người_chơi>                   # Tìm kiếm thông số người chơi
```

## **Hệ Thống Permissions Chi Tiết**

### **User Permissions** 
| Permission | Mô tả |
|------------|-------|
| `leaderboard.use` | Mở gui bảng xếp hạng |
| `leaderboard.reload` | Reload toàn bộ cấu hình |
| `leaderboard.help` | Sử dụng lệnh help | Default |
| `leaderboard.version` | Xem phiên bản plugin |
| `leaderboard.*` | Toàn bộ quyền của plugin |

## ⚙️ Cấu Hình

### config.yml
```yaml
# Leaderboard System Configuration

# --- General Settings ---

# Plugin language: 'en' (English) or 'vi' (Vietnamese).
# Loads messages from messages/messages_xx.yml.
language: "en"

# How often player stats are updated in the database (in ticks).
# 20 ticks = 1 second, 1200 ticks = 1 minute.
update_interval: 1200 # Default: 60 seconds

# --- Sound Settings ---
sound:
  # Sound played when clicking GUI items.
  click_sound:
    enabled: true # Enable/disable this sound.
    sound: "UI_BUTTON_CLICK" # Bukkit Sound enum name.
    volume: 1.0 # 0.0 to 1.0
    pitch: 1.0 # 0.0 to 2.0
  # Sound played when search fails or is cancelled.
  search_feedback:
    no_player_sound:
      enabled: true
      sound: "ENTITY_VILLAGER_NO"
      volume: 1.0
      pitch: 1.0

# --- Automatic Number Formatting (e.g., 1,234,567 -> 1.23M) ---
automatic_format:
  # Suffixes for large numbers.
  number_formatter:
    thousands: k
    millions: M
    billions: B
    trillions: T
    quadrillions: Q
  # Leaderboards to apply automatic number formatting.
  # 'key' must match a leaderboard ID. 'placeholder' is the PAPI placeholder to format.
  format_list:
    money:
      placeholder: "%vault_eco_balance_fixed%" # PAPI placeholder for the raw number.
      number_formatter: true # Enable/disable formatting for this leaderboard.

# --- Main GUI Settings ---
gui:
  # Title of the main GUI. Supports color codes.
  title: "&8ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅѕ"
  # Size of the main GUI (must be a multiple of 9).
  size: 45
  # Border items for the GUI.
  border_item:
    enabled: true # Enable/disable border items.
    material: "LIGHT_GRAY_STAINED_GLASS_PANE" # Bukkit Material name.
    display_name: " " # Use " " for an empty name.
    lore: [] # Lore lines for the border item.
    # List of slots for border items. Can be single numbers (e.g., 0, 1) or ranges (e.g., 0-8).
    # Example for a 45-slot GUI (5 rows):
    # Top row: 0-8, Bottom row: 36-44, Sides: 9, 17, 18, 26, 27, 35
    slots: "[0-8, 36-44, 9, 17, 18, 26, 27, 35]"
  # Close button for the main GUI.
  close_button:
    enabled: true
    material: "BARRIER"
    display_name: "&#ff0000&lᴄʟᴏѕᴇ"
    lore:
      - "&fClick to close the menu"
    slot: 40 # The slot where the close button will appear.

# --- Specific Leaderboard GUI Settings ---
leaderboard_gui:
  # Format for player heads displayed in the leaderboard list.
  # {player_name}, {rank}, {value}, {format} are replaced.
  top_player_format:
    display_name: "&#b3ff00{player_name}"
    lore:
        - "&f{format}: &7{value} &#b3ff00(#{rank})"
  # Control items in the specific leaderboard GUI.
  items:
    # Player's own statistics button.
    personal_stats:
      enabled: true
      material: "PLAYER_HEAD"
      display_name: "&#b3ff00%player_name%" # %player_name% is a PlaceholderAPI placeholder.
      lore:
        - "&f{format}: &7{value} &#b3ff00(#{rank})"
      slot: 48 # Slot for the button.
    # Refresh button.
    refresh_button:
      enabled: true
      material: "BELL"
      display_name: "&#b3ff00ʀᴇꜰʀᴇѕʜ"
      lore:
        - "&fClick to refresh!"
      slot: 49
    # Search button (opens SignGUI).
    search_button:
      enabled: true
      material: "OAK_SIGN"
      display_name: "&#b3ff00ѕᴇᴀʀᴄʜ"
      lore:
        - "&fClick to search for players"
      slot: 50
      # SignGUI settings:
      sign-type: "OAK_SIGN" # Material of the sign.
      sign-input-line: 1 # Line number (1-4) for player input.
      sign-gui: # Lines displayed on the sign.
        - ""
        - "↑↑↑↑↑↑↑↑↑↑↑↑"
        - "Search"
        - ""
    # Previous page button.
    previous_page_button:
      enabled: true
      material: "ARROW"
      display_name: "&#b3ff00ᴘʀᴇᴠɪᴏᴜѕ"
      lore:
        - "&fClick to go to the previous page"
      slot: 45
    # Next page button.
    next_page_button:
      enabled: true
      material: "ARROW"
      display_name: "&#b3ff00ɴᴇхᴛ"
      lore:
        - "&fClick to go to the next page"
      slot: 53
  # Feedback sounds for search.
  search_feedback:
    no_player_sound:
      enabled: true
      sound: "ENTITY_VILLAGER_NO"
      volume: 1.0
      pitch: 1.0

# --- Leaderboard Definitions ---
# Define each leaderboard. Each needs a unique key.
leaderboards:
  kills:
    title: "&8ᴍᴏѕᴛ ᴋɪʟʟѕ (Page {page})" # GUI title for this leaderboard. {page} is replaced.
    type: INTERNAL_KILLS # Statistic type: INTERNAL_*, PLACEHOLDER.
    format: "Kills" # Short name for statistic, used in messages.
    material: MACE # Icon material.
    display_name: "&#b3ff00&lᴋɪʟʟѕ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ" # Display name in main GUI.
    lore:
      - "&fClick to view the kills leaderboard"
    slot: 19 # Slot in main GUI.
  deaths:
    title: "&8ᴍᴏѕᴛ ᴅᴇᴀᴛʜѕ (Page {page})"
    type: INTERNAL_DEATHS
    format: "Deaths"
    material: SKELETON_SKULL
    display_name: "&#b3ff00&lᴅᴇᴀᴛʜѕ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the deaths leaderboard"
    slot: 20
  money:
    title: "&8ᴍᴏѕᴛ ᴍᴏɴᴇʏ (Page {page})"
    type: PLACEHOLDER
    placeholder: "%vault_eco_balance_fixed%" # Required for PLACEHOLDER type.
    format: "Money"
    material: EMERALD
    display_name: "&#b3ff00&lᴍᴏɴᴇʏ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the money leaderboard"
    slot: 21
  blocks_broken:
    title: "&8ᴍᴏѕᴛ ʙʟᴏᴄᴋѕ ʙʀᴏᴋᴇɴ (Page {page})"
    type: INTERNAL_BLOCKS_BROKEN
    format: "Blocks Broken"
    material: COBBLESTONE
    display_name: "&#b3ff00&lʙʟᴏᴄᴋѕ ʙʀᴏᴋᴇɴ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the blocks broken leaderboard"
    slot: 22
  blocks_placed:
    title: "&8ᴍᴏѕᴛ ʙʟᴏᴄᴋѕ ᴘʟᴀᴄᴇᴅ (Page {page})"
    type: INTERNAL_BLOCKS_PLACED
    format: "Blocks Placed"
    material: STONE
    display_name: "&#b3ff00&lʙʟᴏᴄᴋѕ ᴘʟᴀᴄᴇᴅ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the blocks placed leaderboard"
    slot: 23
  mobs_killed:
    title: "&8ᴍᴏѕᴛ ᴍᴏʙѕ ᴋɪʟʟᴇᴅ (Page {page})"
    type: INTERNAL_MOBS_KILLED
    format: "Mob killed"
    material: ZOMBIE_HEAD
    display_name: "&#b3ff00&lᴍᴏʙѕ ᴋɪʟʟᴇᴅ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the mobs killed leaderboard"
    slot: 24
  playtime:
    title: "&8ᴍᴏѕᴛ ᴘʟᴀʏᴛɪᴍᴇ (Page {page})"
    type: INTERNAL_PLAYTIME
    format: "Playtime"
    material: CLOCK
    display_name: "&#b3ff00&lᴘʟᴀʏ ᴛɪᴍᴇ ʟᴇᴀᴅᴇʀʙᴏᴀʀᴅ"
    lore:
      - "&fClick to view the playtime leaderboard"
    slot: 25

```

> **-------------------------------------------------------**
