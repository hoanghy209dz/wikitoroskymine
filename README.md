# 📖 Hướng Dẫn Sử Dụng ToroSkymine

> Plugin SkyMine được yêu cầu bởi chế hai ngân .
> Lưu ý giúp Hy là luôn chỉnh chance của mọi thứ là 100% nhé , chance của rank cúp addloot

---

## 🔐 Quyền Hạn

| Quyền | Mô tả |
|-------|-------|
| `toroskymine.admin` | Quyền sử dụng tất cả commands |
| `toroskymine.mine` | Quyền đào trong vùng mỏ |
| `toroskymine.bonus.vip` | Bonus VIP: x100.0 chance, +1 items |
| `toroskymine.bonus.mvp` | Bonus MVP: x100.0 chance, +2 items |
| `toroskymine.bonus.legend` | Bonus Legend: x100.0 chance, +3 items |
| `toroskymine.bonus.vidu` | Bonus vidu: x100.0 chance, +4 items |
Tuỳ chỉnh trong config nhé
---

## 🛠️ Commands Cơ Bản

### 1. Lấy Selection Wand
```
/skymine wand
```
Nhận cây rìu vàng để chọn vùng.

### 2. Chọn Vùng
- **Click trái** vào block → Đặt điểm 1
- **Click phải** vào block → Đặt điểm 2

### 3. Tạo Vùng Mỏ
```
/skymine create <tên_vùng>
```
**Ví dụ:** `/skymine create mine1`

### 4. Xóa Vùng Mỏ
```
/skymine delete <tên_vùng>
```

### 5. Xem Thông Tin Vùng
```
/skymine info <tên_vùng>
```
Hiển thị: tọa độ, tool yêu cầu, drops, % đã đào, v.v.

### 6. Danh Sách Vùng
```
/skymine list
```

### 7. Reload Config
```
/skymine reload
```

---

## ⛏️ Cấu Hình Drop Items

### Xem MMOItems Types
```
/skymine types
```

### Xem Items Theo Type
```
/skymine items <type>
```
**Ví dụ:** `/skymine items MATERIAL`

### Nhận Item Test
```
/skymine give <type> <id>
```
**Ví dụ:** `/skymine give MATERIAL DIAMOND_ORE`

### Thêm Drop Vào Vùng
```
/skymine adddrop <zone> <type> <id> <chance%> <amount>
```
**Ví dụ:** `/skymine adddrop mine1 MATERIAL DIAMOND_ORE 100.0 1`
→ 100% chance drop 1 Diamond Ore

### Xóa Tất Cả Drops
```
/skymine cleardrop <zone>
```

---

## 💎 Tool Bonus (Tăng Drop Theo Tool)

### Thêm Bonus
```
/skymine addbonus <zone> <tool_type> <tool_id> <chance_x> <amount_bonus>
```
**Ví dụ:** `/skymine addbonus mine1 TOOL DIAMOND_PICKAXE 100.0 1`
→ Dùng Diamond Pickaxe: chance 100%, amount +1

### Xóa Tất Cả Bonus
```
/skymine clearbonus <zone>
```

---

## 🔄 Cấu Hình Regeneration ( Không cần chỉnh gì vì mặc định tất cả vùng đều 80% , 5 phút muốn chỉnh thì vào config )

### Trigger Regen Thủ Công
```
/skymine regen <zone>
```

### Thay Đổi Tốc Độ Regen
```
/skymine setspeed <zone> <slow|normal|fast>
```

### Cấu Hình Trong zones.yml
```yaml
regen:
  percent: 80.0        # Auto-regen khi đào 80%
  timer-minutes: 5     # Auto-regen sau 5 phút không đào
  speed: NORMAL        # SLOW / NORMAL / FAST
```

---

## 📊 Cách Tính Bonus

### Công Thức:
```
Final Chance = Base × Tool_Chance × Perm_Chance
Final Amount = Base + Tool_Bonus + Perm_Bonus
```

### Ví Dụ:
| Nguồn | Chance | Amount |
|-------|--------|--------|
| Drop gốc | 100% | 1 |
| Tool Bonus | 100% | +1 |
| Perm Bonus (MVP) | 100% | +2 |
| **Tổng** | **300%** | **4 items** |

---

## ⚙️ Config.yml Quan Trọng

```yaml
# Bật/tắt debug log
debug: false

# Mặc định cho vùng mới
regen-defaults:
  percent: 80.0
  timer-minutes: 5
  speed: NORMAL

# Quyền bonus
permission-bonuses:
  - permission: "toroskymine.bonus.legend"
    chance-multiplier: 2.0
    amount-bonus: 3
  - permission: "toroskymine.bonus.mvp"
    chance-multiplier: 1.5
    amount-bonus: 2
  - permission: "toroskymine.bonus.vip"
    chance-multiplier: 1.2
    amount-bonus: 1
```

---

## 📁 Cấu Trúc zones.yml

```yaml
zones:
  mine1:
    world: world
    min: {x: 100, y: 60, z: 100}
    max: {x: 150, y: 80, z: 150}
    required-tool:
      type: "*"
      id: "*"
    regen:
      percent: 80.0
      timer-minutes: 5
      speed: NORMAL
    state:
      mined-blocks: 150
      last-mine-time: 1738856785000
    drops:
      - {type: MATERIAL, id: DIAMOND_ORE, chance: 25.0, amount: 1}
    tool-bonuses:
      - {tool-type: TOOL, tool-id: DIAMOND_PICKAXE, chance-multiplier: 1.5, amount-bonus: 1}
```

---

## ❓ FAQ

**Q: Vùng không regen sau khi đào hết?**
A: Kiểm tra `/skymine info <zone>` xem % đã đào. Server restart giờ sẽ giữ lại trạng thái.

**Q: Đào nhưng không hoạt động không rơi ra gì cả?**
A: Kiểm tra MMOItems đã cài và item type/id có đúng không bằng `/skymine types` và `/skymine items`.

---

> 📅 **Cập nhật lần cuối:** 2026-02-06
