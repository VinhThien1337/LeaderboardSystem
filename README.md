> **-------------------------------------------------------**
# LeaderboardSystem Plugin

## Giới Thiệu
**LeaderboardSystem** là plugin Minecraft được phát triển và sở hữu bởi **VinhThien** giúp tạo một hệ thống bảng xếp hạng tuyệt vời bằng gui dễ tiếp cận

**Thông Tin Plugin:**
- **Plugin version:**: 1.0
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

# GUI Settings
gui:
  title: "&6&lLeaderboards"
  size: 54
  click_sound:
    enabled: true
    sound: "UI_BUTTON_CLICK"
    volume: 1.0
    pitch: 1.0
  filler_item:
    enabled: true
    material: "GRAY_STAINED_GLASS_PANE"
    display_name: " "
  border_item:
    enabled: true
    material: "BLACK_STAINED_GLASS_PANE"
    display_name: " "
  close_button:
    enabled: true
    material: "BARRIER"
    display_name: "&c&lClose"
    lore:
      - "&7Click to close the menu."
    slot: 49

# Settings for the specific leaderboard GUIs (the ones that show player heads)
leaderboard_gui:
  click_sound:
    enabled: true
    sound: "BLOCK_NOTE_BLOCK_HAT"
    volume: 1.0
    pitch: 1.2
  # Format for the player heads in the top player view
  top_player_format:
    display_name: "&#55aaff&l{player_name}"
    lore:
      - "&bRank: &e#{rank}"
      - "&b{format}: &e{value}"
  # Items in the bottom row of the leaderboard GUI
  items:
    personal_stats:
      enabled: true
      material: "PLAYER_HEAD"
      display_name: "&e&lYour Stats"
      # {rank}, {value}, and {format} will be replaced with the player's data
      lore:
        - "&7Your Rank: &b{rank}"
        - "&7{format}: &b{value}"
      slot: 48
    refresh_button:
      enabled: true
      material: "SUNFLOWER"
      display_name: "&e&lRefresh"
      lore:
        - "&7Click to refresh the leaderboard."
      slot: 49
    search_button:
      enabled: true
      material: "OAK_SIGN"
      display_name: "&e&lSearch Player"
      lore:
        - "&7Click to search for a player's rank."
      slot: 50
    previous_page_button:
      enabled: true
      material: "ARROW"
      display_name: "&a&lPrevious Page"
      lore:
        - "&7Go to the previous page."
      slot: 45
    next_page_button:
      enabled: true
      material: "ARROW"
      display_name: "&a&lNext Page"
      lore:
        - "&7Go to the next page."
      slot: 53
  search_feedback:
    no_player_sound:
      enabled: true
      sound: "ENTITY_VILLAGER_NO"
      volume: 1.0
      pitch: 1.0
    no_player_actionbar: "&cPlayer not found!"
    cancelled_actionbar: "&eSearch cancelled."
  search_messages:
    prompt_text: "&#aaffaaPlease enter the player's name to search, or type &#ff5555.quit &#aaffaa to cancel."
    leaderboard_key_not_found_error: "&#ff5555Error: Leaderboard key not found."
    player_not_found: "&#ff5555Could not find player '&#ffffff{player_name}&#ff5555' in the {leaderboard_key} leaderboard."
    search_result_header: "&#ffff00--- Search Result ---"
    search_result_player: "&#55ffffPlayer: &#ffffff{player_name}"
    search_result_leaderboard: "&#55ffffLeaderboard: &#ffffff{leaderboard_key}"
    search_result_rank: "&#55ffffRank: &#ffffff#{rank}"
    search_result_score: "&#55ffffScore: &#ffffff{score}"
    search_result_footer: "&#ffff00--------------------"
    conversation_prefix: "&b[Leaderboard] &r"
    search_command_usage: "&cUsage: /lb search <leaderboard> <player>"
    invalid_leaderboard: "&cLeaderboard '{leaderboard_id}' not found."

# --- Leaderboard Definitions ---
# type: INTERNAL_KILLS, INTERNAL_DEATHS, INTERNAL_MOBS_KILLED, INTERNAL_BLOCKS_BROKEN, INTERNAL_BLOCKS_PLACED, PLACEHOLDER
leaderboards:
  kills:
    type: INTERNAL_KILLS
    format: "Kills"
    material: DIAMOND_SWORD
    display_name: "&4&lKills Leaderboard"
    lore:
      - "&7Top player killers."
    slot: 20
  deaths:
    type: INTERNAL_DEATHS
    format: "Deaths"
    material: BONE
    display_name: "&c&lDeaths Leaderboard"
    lore:
      - "&7Most frequent deaths."
    slot: 21
  mobs_killed:
    type: INTERNAL_MOBS_KILLED
    format: "Mob Kills"
    material: ZOMBIE_HEAD
    display_name: "&5&lMobs Killed Leaderboard"
    lore:
      - "&7Top mob slayers."
    slot: 22
  blocks_broken:
    type: INTERNAL_BLOCKS_BROKEN
    format: "Blocks Broken"
    material: IRON_PICKAXE
    display_name: "&3&lBlocks Broken Leaderboard"
    lore:
      - "&7Most blocks destroyed."
    slot: 23
  blocks_placed:
    type: INTERNAL_BLOCKS_PLACED
    format: "Blocks Placed"
    material: GRASS_BLOCK
    display_name: "&2&lBlocks Placed Leaderboard"
    lore:
      - "&7Most blocks placed."
    slot: 24
  money:
    type: PLACEHOLDER
    placeholder: "%vault_eco_balance_fixed%"
    format: "Money"
    material: GOLD_INGOT
    display_name: "&a&lMoney Leaderboard"
    lore:
      - "&7Richest players on the server."
    slot: 30
  jumps:
    type: PLACEHOLDER
    placeholder: "%statistic_jump%"
    format: "Jumps"
    material: RABBIT_FOOT
    display_name: "&e&lJumps Leaderboard"
    lore:
      - "&7Players who jump the most."
    slot: 32

```

> **-------------------------------------------------------**
