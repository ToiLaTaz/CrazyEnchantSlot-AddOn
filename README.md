# CrazyEnchantSlot-AddOn

> **Hiển thị số slot enchant còn lại trên item - Add-on cho CrazyEnchantments**

![Version](https://img.shields.io/badge/version-1.0.1-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Java](https://img.shields.io/badge/java-21+-orange)
![Minecraft](https://img.shields.io/badge/minecraft-1.21+-blueviolet)

---

## 📌 Tổng Quan

Plugin này thêm tính năng hiển thị **số slot enchant còn lại** trực tiếp trên lore của item khi player cầm item có enchant từ **CrazyEnchantments**.

### ✨ Tính Năng

- 🎁 Tự động hiển thị số slot còn lại trên lore item
- ∞ Phát hiện enchant vô hạn (∞)
- 🔴 Thông báo khi full slot
- 🎨 Tùy chỉnh hoàn toàn tin nhắn
- 📊 PlaceholderAPI support (8 placeholder)
- ⚡ Nhẹ & nhanh - chỉ 22 KB
- 🔧 Dễ cấu hình

---

## 📥 Cài Đặt

### Yêu Cầu
- **Java**: 21 trở lên
- **Server**: Paper 1.21.3+ hoặc Folia
- **Plugin**: CrazyEnchantments
- **Optional**: PlaceholderAPI

### Bước Cài Đặt

1. **Download** file `CrazyEnchantSlot-AddOn.jar`
2. **Copy** vào folder `plugins/`
3. **Restart** server
4. ✅ Plugin tự động tạo config

```bash
# Sau restart, check console
[CrazyEnchantSlot-AddOn] ✓ CrazyEnchantSlot-AddOn enabled successfully!
```

---

## ⚙️ Cấu Hình

File config: `plugins/CrazyEnchantSlot-AddOn/config.yml`

```yaml
Settings:
  # Bật/Tắt plugin
  Enabled: true

  # Hiển thị lore trên item
  ShowSlotLore: true

  # Debug mode (xem log chi tiết)
  Debug: false

Messages:
  # Khi còn slot
  # %space% = số slot còn lại
  SlotLore: "&7Còn có thể enchant: &e%space% enchant"

  # Khi vô hạn slot
  SlotLoreInfinite: "&7Còn có thể enchant: &e∞"

  # Khi full slot
  SlotLoreMaxReached: "&cBạn không thể enchant thêm!"

  # Reload success
  ReloadSuccess: "&8[&aCrazyEnchantSlot-AddOn&8]: &aConfiguration reloaded successfully!"

  # Error messages
  NoPermission: "&cYou do not have permission to use this command."
  InvalidCommand: "&cUsage: /ceaddon reload"
```

### Tùy Chỉnh Tin Nhắn

- `&c` = đỏ, `&e` = vàng, `&a` = xanh lá, `&7` = xám, `&b` = xanh nước

### Built-in Placeholder trong Lore

Có thể sử dụng trực tiếp trong lore config (không cần PlaceholderAPI):

| Placeholder | Ý Nghĩa |
|------------|---------|
| `%space%` | Slot còn lại |
| `%hientai%` | Số enchant hiện tại |
| `%toida%` | Tổng slot tối đa |

**Ví dụ:**
```yaml
SlotLore: "&7[%hientai%/%toida%] &eỊ còn %space% slot"
# Output: [3/8] Ị còn 5 slot
```

---

## 🎮 Cách Sử Dụng

### Xem Lore

Khi cầm item CrazyEnchant lên tay → Lore tự động hiển thị:

```
[Item Name]
[Original Lore...]
Còn có thể enchant: 5 enchant
```

### Lệnh

```bash
# Reload config (không cần restart)
/ceaddon reload

# Check trạng thái plugin
/ceaddon check
```

### Quyền Hạn

| Quyền | Mô Tả |
|------|-------|
| `ceaddon.reload` | Reload config |
| `ceaddon.check` | Check status |

---

## 📊 PlaceholderAPI

**Chỉ hoạt động với PlaceholderAPI** - Sử dụng trong plugin khác (scoreboards, nametags, actionbar, etc.):

⚠️ **Không thể dùng trong lore item!** Dùng **Built-in Placeholder** ở trên để sửa lore.

### Placeholder Hiện Tại

| Placeholder | Giá Trị | Ví Dụ |
|------------|--------|-------|
| `%ceaddon_slots%` | Slot còn lại | `5` |
| `%ceaddon_hientai%` | Số enchant hiện tại | `3` |
| `%ceaddon_toida%` | Tổng slot tối đa | `8` |
| `%ceaddon_max_slots%` | Max từ API | `10` |
| `%ceaddon_base_slots%` | Base slots | `10` |
| `%ceaddon_slot_crystal_adjustment%` | Giảm slot (crystal) | `-2` |
| `%ceaddon_bypass_limit%` | Có bypass permission | `false` |
| `%ceaddon_current_enchants%` | Số enchant hiện tại | `3` |

### Ví Dụ Sử Dụng (PlaceholderAPI)

```
# Trên actionbar
/msg %player% [%ceaddon_hientai%/%ceaddon_toida%] slots

# Trên bảng thông tin
Slots: %ceaddon_hientai%/%ceaddon_toida%

# Format đẹp
[%ceaddon_hientai%/%ceaddon_toida%] ≫ %ceaddon_slots% còn lại
```

---

## 🎯 Sự Khác Nhau

| Loại | Nơi Dùng | Cách Dùng |
|------|----------|----------|
| **Built-in** | Lore item config | `%space%` `%hientai%` `%toida%` |
| **PlaceholderAPI** | Scoreboards, Chat, Actionbar, etc. | `%ceaddon_slots%` `%ceaddon_hientai%` |

---

## 🔍 Cách Hoạt Động

1. **Khi cầm item** (ấn phím 1-9)
   - Plugin kiểm tra item có enchant CrazyEnchant không
   - Nếu có → Tính số slot còn lại
   - Cập nhật lore tự động

2. **Khi click inventory**
   - Tương tự như cầm item
   - Update sau 1 tick

3. **Hiển thị lore dựa trên tình huống:**

| Tình huống | Lore Hiển Thị |
|-----------|-------|
| Còn 5 slot | `Còn có thể enchant: 5 enchant` |
| Full slot (0) | `Bạn không thể enchant thêm!` |
| Vô hạn slot | `Còn có thể enchant: ∞` |
| Không có enchant | Không hiển thị |

---

## ❓ Hỏi & Đáp

### Q: Plugin làm chậm server không?
**A:** Không. Plugin chỉ hoạt động khi player cầm/click item, rất nhẹ (22 KB).

### Q: Tại sao lore không cập nhật?
**A:**
- Kiểm tra `ShowSlotLore: true` trong config
- Kiểm tra item có CrazyEnchant không (dùng `/ce check`)
- Restart server sau khi sửa config

### Q: Có thể tùy chỉnh lore không?
**A:** Có! Edit file `config.yml` phần `Messages` rồi dùng `/ceaddon reload`.

### Q: PlaceholderAPI bắt buộc không?
**A:** Không! PlaceholderAPI là tùy chọn. Plugin vẫn hoạt động bình thường mà không cần.

### Q: Có thể hiển thị định dạng khác không?
**A:** Có! Chỉnh `SlotLore` trong config, ví dụ:
```yaml
SlotLore: "[%hientai%/%toida%] &eỊ %space% slot"
SlotLore: "Enchant: %space%"
SlotLore: "&7Progress: %hientai%/%toida%"
```

### Q: Tại sao `%ceaddon_hientai%` không hoạt động trong lore?
**A:** PlaceholderAPI không parse placeholder trong lore item. Hãy dùng **built-in placeholder**:
- ❌ Sai: `SlotLore: "%ceaddon_hientai%/%ceaddon_toida%"`
- ✅ Đúng: `SlotLore: "%hientai%/%toida%"`

---

## 🐛 Xử Lý Vấn Đề

### Lore không hiển thị

```
1. Dùng /ceaddon check
   - Kiểm tra plugin đã load
   - Kiểm tra item info

2. Check config
   - ShowSlotLore: true ?
   - Item có CrazyEnchant ?

3. Bật debug mode
   Settings.Debug: true
   /ceaddon reload

4. Check console
   - Có error message gì không?
```

### Plugin không load

```
1. Kiểm tra CrazyEnchantments đã install
   /plugins

2. Kiểm tra Java version
   java -version
   Cần Java 21+

3. Check console
   Có thông báo lỗi gì không?

4. Restart server
   /stop
```

---

## 📋 Yêu Cầu Hệ Thống

| Yêu Cầu | Chi Tiết |
|---------|---------|
| **Java** | 21 trở lên |
| **Minecraft** | 1.21+ |
| **Server** | Paper 1.21.3+ hoặc Folia |
| **Plugin** | CrazyEnchantments (bắt buộc) |
| **Optional** | PlaceholderAPI |
| **Dung lượng** | 22 KB |

---

## 📝 Ví Dụ Config

### Config Tiếng Việt

```yaml
Settings:
  Enabled: true
  ShowSlotLore: true
  Debug: false

Messages:
  # Built-in placeholder: %space%, %hientai%, %toida%
  SlotLore: "&7[%hientai%/%toida%] &a%space% slot"
  SlotLoreInfinite: "&7Enchant: &a∞"
  SlotLoreMaxReached: "&c⚠ Không thể enchant thêm!"
  ReloadSuccess: "&a✓ Reload thành công!"
  NoPermission: "&c✗ Bạn không có quyền!"
  InvalidCommand: "&cSử dụng: /ceaddon reload"
```

### Config Tiếng Anh

```yaml
Settings:
  Enabled: true
  ShowSlotLore: true
  Debug: false

Messages:
  # Built-in placeholder: %space%, %hientai%, %toida%
  SlotLore: "&7[%hientai%/%toida%] &aSlots: %space%"
  SlotLoreInfinite: "&7Slots: &a∞"
  SlotLoreMaxReached: "&c⚠ Slots Full!"
  ReloadSuccess: "&a✓ Reloaded!"
  NoPermission: "&c✗ No permission!"
  InvalidCommand: "&cUsage: /ceaddon reload"
```

---

## 🎯 Tips & Tricks

### 1. Hiển thị format "số/tối đa"

```yaml
SlotLore: "&7[%hientai%/%toida%] Còn: &e%space%"
# Output: [3/8] Còn: 5
```

### 2. Sử dụng với PlaceholderAPI

Tạo actionbar cho player:

```
Enchant: [%ceaddon_hientai%/%ceaddon_toida%]
```

### 3. Tắt tạm thời

```yaml
ShowSlotLore: false
/ceaddon reload
# Lore sẽ không hiển thị
```

### 4. Debug mode

```yaml
Debug: true
/ceaddon reload

# Xem chi tiết trong console
# Giúp troubleshoot vấn đề
```

---

## 📞 Hỗ Trợ

- **Lỗi?** Check console bằng `/ceaddon check`
- **Câu hỏi?** Bật `Debug: true` để xem log
- **Gợi ý?** Tùy chỉnh `config.yml` theo ý

---

## 📄 License

MIT License 
---

## 🔗 Liên Quan

- **CrazyEnchantments**: [https://docs.crazycrew.us/](https://docs.crazycrew.us/)
- **Paper**: [https://papermc.io/](https://papermc.io/)
- **PlaceholderAPI**: [https://docs.extendedclip.com/placeholderapi/](https://docs.extendedclip.com/placeholderapi/)

---

