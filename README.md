# ⚔️ AllayAscend **1.0.13**

> Plugin RPG gắn **AllayScore (Điểm)** cho **Paper 1.20+**  
> Path + node sống sót qua chết · Điểm / streak / risk cháy khi chết

```
Java 21  ·  Paper 1.20.x  ·  Soft-depend: AllayScore  ·  MIT © 2026 AllayMC
```

```bash
mvn -q clean package
# → target/AllayAscend.jar
```

---

## 📑 Mục lục

| # | Mục |
|---|-----|
| 1 | [Cài đặt](#-cài-đặt) |
| 2 | [Cách chơi nhanh](#-cách-chơi-nhanh) |
| 3 | [Hệ thống Điểm & chết](#-hệ-thống-điểm--chết) |
| 4 | [9 Con đường (Path)](#-9-con-đường-path) |
| 5 | [Đổi path (GUI)](#-đổi-path-nút-gui) |
| 6 | [Cây kỹ năng (36 node)](#-cây-kỹ-năng-36-node) |
| 7 | [Thiên Mệnh & Claim](#-thiên-mệnh--claim) |
| 8 | [Blood Contract (Risk)](#-blood-contract-risk) |
| 9 | [Ordeal](#-ordeal) |
| 10 | [Boss Event](#-boss-event) |
| 11 | [Truy nã (Bounty)](#-truy-nã-bounty) |
| 12 | [**Mảnh Nâng Level · Thuộc tính · Skill**](#-mảnh-nâng-level--thuộc-tính--skill) ⭐ |
| 13 | [Giờ Vàng Vắng](#-giờ-vàng-vắng-quiet-bonus) |
| 14 | [Mùa giải](#-mùa-giải-season) |
| 15 | [Kỹ năng chủ động Path](#-kỹ-năng-chủ-động) |
| 16 | [Luật server trong code](#-luật-server-liên-quan-ascend) |
| 17 | [Lệnh người chơi](#-lệnh-người-chơi) |
| 18 | [Lệnh admin](#-lệnh-admin) |
| 19 | [Config quan trọng](#-config-quan-trọng) |
| 20 | [Changelog 1.0.13](#-changelog-1013) |

---

## 📦 Cài đặt

```
1. Cài AllayScore trước (economy Điểm)
2. Thả AllayAscend.jar vào plugins/
3. Restart server
4. (Tuỳ chọn) AllayShop cho /shop
```

---

## 🎮 Cách chơi nhanh

```
1. Farm XP / chơi → có Điểm (AllayScore)
2. /ascend → chọn 1 Path (GUI)
3. Mở node trên cây (GUI 3 trang × 12)
4. Làm Thiên Mệnh → CLAIM khi xong
5. (Muộn) Risk / Ordeal / Boss / Bounty / Mảnh Level
```

**3 câu nhớ**

| | |
|---|---|
| 1️⃣ | `/ascend` = menu chính |
| 2️⃣ | Thiên Mệnh xong phải **claim** mới có Điểm |
| 3️⃣ | Chết mất **Điểm** · **không mất** node đã mở |

---

## 💀 Hệ thống Điểm & chết

| ❌ Mất khi chết | ✅ Giữ khi chết |
|-----------------|-----------------|
| Điểm AllayScore + Rank | Path + node đã mở |
| Streak Thiên Mệnh | Prestige |
| Tiền cược Risk | — |
| Phí Ordeal (nếu đang chơi) | — |
| Heat | — |

**Bảo hiểm chết** (`/ascend insurance`): đổi **1 Mảnh Nâng Level** → chết **giữ đồ**, chỉ mất **70% Điểm**.

Trong **Boss** đã join hoặc **Ordeal**: giữ đồ theo luật riêng của event.

---

## 🛤️ 9 Con đường (Path)

Chọn **1** path. Mỗi path ~**36 node**, buff passive nhẹ, skill chủ động riêng.

| ID | Tên | Phong cách | Skill (`/ascend skill`) |
|----|-----|------------|-------------------------|
| `kiem` | **Kiếm sĩ** | Cận chiến, ST & sức bền | Cuồng nộ — Strength + Speed |
| `phap` | **Pháp sư** | Di chuyển, hiệu ứng & sinh tồn | Dịch chuyển — blink + slow falling |
| `tham` | **Thám hiểm** | Tốc độ, đào quặng & cơ động | Xung kích — dash + Speed |
| `thu` | **Thủ hộ** | Phòng thủ, hồi phục & chống chết | Củng cố — Resistance + Absorption |
| `cung` | **Cung thủ** | Tầm xa, tốc độ kéo & cơ động | Mưa tên — Speed + Jump |
| `linh` | **Linh hồn** | Hấp thụ, NV & kháng hiệu ứng | Lớp hồn — Invis ngắn + Resistance |
| `cong` | **Công binh** | Đào, craft, Haste & tiện ích | Xung công — Haste + Speed |
| `doc` | **Độc sư** | Poison, kiểm soát & bền bỉ | Nọc độc — Speed + Resistance |
| `hoa` | **Hỏa thần** | Lửa, sức mạnh bùng nổ | Bùng cháy — Strength + Fire Res |

> Skill cần **≥ 3 node** đã mở. Cooldown theo `skills.*`.  
> Buff path refresh định kỳ duration dài — **Night Vision không chớp tắt**.

---

## 🔄 Đổi path (nút GUI)

> **Không còn** lệnh `/ascend path <id>` để chọn / đổi.

```
/ascend → Con đường → nút «Đổi con đường» (góc dưới trái, compass)
       → chọn path mới trong menu 9 ô
```

| Lần | Chi phí |
|-----|---------|
| Lần đầu chọn | **Miễn phí** |
| Đổi sau | `path-change-cost` (mặc định **120.000 Điểm**) + **reset toàn bộ node** |

`/ascend path` chỉ **liệt kê** · `/ascend path tree` xem cây text.

---

## 🌳 Cây kỹ năng (36 node)

- GUI **3 trang × 12** node
- Giá tăng dần: `4500 × 1.28^(n-1)`
- **Nhánh A/B** tại mốc **12** và **24** (chỉ chọn 1)
- Node sau nhánh: cần **một trong hai** (OR)

### Bảng giá tham khảo

| Tầng | Giá (Điểm) | Tầng | Giá (Điểm) |
|------|------------|------|------------|
| T1 | 4.500 | T18 | 299.100 |
| T2 | 5.800 | T24 | 1.315.400 |
| T5 | 12.100 | T30 | 5.775.000 |
| T12 | 68.000 | T36 | 8.000.000 |

---

## 📜 Thiên Mệnh & Claim

Nhiệm vụ **cá nhân**, adaptive theo path & sức.

| | |
|---|---|
| Mỗi ngày | **3** Thiên Mệnh |
| Mỗi tuần | **1** Thiên Mệnh tuần |
| Underdog | Ít node → thưởng cao hơn (tối đa ~**×1.75**) |
| Soft tax | ≥24 node → giảm nhẹ thưởng |
| Claim | **Bắt buộc** click / `/ascend claim` mới nhận Điểm |
| Chết | **Đứt streak** |

Không đếm: Creative / bay / xe / chưa chọn path.

---

## 🩸 Blood Contract (Risk)

```
/ascend risk <số_điểm>   hoặc GUI «Huyết ước»
```

```
Cược Điểm ──► trong thời gian claim 1 Thiên Mệnh
   │
   ├─ Thắng: thưởng × multiplier + hoàn cược
   └─ Chết / hết giờ: mất cược
```

Mặc định: min **500** · max **4000** · duration **600s** · mult ~**1.50**.

---

## ☠️ Ordeal

Thử thách có thể chết. Phí vào bằng Điểm. **Cấm** táo vàng / potion / sữa trong lúc thi.

| Ordeal | Ý tưởng |
|--------|---------|
| Sóng xương | Đợt quái |
| Giáng lôi | Sét |
| Hơi wither | Wither + đói |
| Hút vực | Kéo xuống + levitation |
| Mưa lửa | Fireball + blaze |
| Sương độc | Poison + damage |
| Hút hồn | Wither + hút máu |

- **Thắng:** thưởng > phí (enforce `min-net-profit`)
- **Thua:** mất phí · đồ giữ trong ordeal
- Thoát game giữa chừng: hoàn **50%** phí + cooldown nhẹ

---

## 👹 Boss Event

| Lệnh | Ai | Việc |
|------|-----|------|
| `/ascend bs` | Admin | Đặt **1** spawn (ghi đè cũ) |
| `/ascend bf <phút>` | Admin | Start boss, **bắt buộc** số phút |
| `/ascend join` | Member | Trả phí, tele vào |
| `/ascend bstop` | Admin | Ép dừng |

- Boss = mob thù địch random (Ravager, Warden, …), scale **2–7**
- Hết giờ = boss biến mất = **fail**, join **mất phí**
- Người **không join** không bị Boss đánh
- Thắng: Điểm cho người còn sống + đã gây damage
- **Mảnh Nâng Level** cho người kết liễu (hoặc top damage)

---

## 🎯 Truy nã (Bounty)

- Elite / đào sâu / truy nã player
- Nạn nhân được **báo tên hunter**
- Sống hết giờ → thưởng sống sót (anti-AFK + daily cap)
- Bị hunter giết: **giữ đồ**, mất **50% Điểm**
- Chống clone: AFK check, combat time, pair cooldown

---

## 💎 Mảnh Nâng Level · Thuộc tính · Skill

### Cách nâng

```
1. Ném Mảnh Nâng Level xuống đất cạnh giáp/vũ khí ≥ Kim Cương
   (hoặc craft đúng công thức theo level trên bàn crafting)
2. Enchant cố định theo level — không enchant tay thêm
3. Mỗi lần nâng: hồi 50% độ bền đã mất
4. Chi phí mảnh: L1=1 · L2=3 · L3=5 · L4=8 · L5=12 · …
5. /ascend insurance — 1 mảnh = 1 bảo hiểm chết
6. Gear Ascend: cấm Anvil / Enchant table / Mending
```

### Max level theo loại

| Loại | Max |
|------|-----|
| Vũ khí / giáp / tool (Mảnh Level) | **15** |
| Cung | **5** |
| Nỏ | **3** |
| Trident | **3** |
| Khiên | **3** |
| **Mace Ultra** | **1 bậc** (không hiện Lv) |

### ⚡ Thuộc tính cộng dồn theo Level (1.0.13+)

Mỗi level cộng thêm — **cộng dồn**, hiện rõ trên lore:

| Stat | Công thức | Ví dụ |
|------|-----------|--------|
| **Sát thương** | **+3% / level** | Lv.1 = +3% · Lv.5 = +15% · Lv.15 = +45% |
| **Độ bền** | **+3% / level** (giảm hao) · **trần 60%** | Lv.1 = −3% hao · Lv.10 = −30% · cap 60% |
| **Giáp** | +0.1 Armor + +0.15 Toughness / level | Lv.15 ≈ +1.5 armor · +2.25 toughness |

```
┌─────────────────────────────────────────────────────────┐
│  Diamond Sword Lv.5                                     │
│  ─────────────────────────────────────────────────────  │
│  Cấp độ: 5/15                                           │
│  +15% sát thương  (+3%/level · cộng dồn)               │
│  +15% độ bền      (giảm hao · +3%/level · trần 60%)    │
│  Không enchant thêm · không sửa / Mending               │
└─────────────────────────────────────────────────────────┘
```

**Cách áp dụng kỹ thuật**

| Loại | Cơ chế |
|------|--------|
| Cận chiến (kiếm, rìu, spear, mace, trident) | `AttributeModifier` MULTIPLY trên `ATTACK_DAMAGE` |
| Cung / nỏ / trident (projectile) | Nhân damage trong event khi mũi tên trúng |
| Mọi gear Ascend | `PlayerItemDamageEvent` giảm hao theo % |
| Giáp (nón/áo/quần/giày) | Attribute ARMOR + ARMOR_TOUGHNESS |

> **Gear level cũ** (trước bản 1.0.13) tự nhận thuộc tính khi **login** hoặc **dùng lần đầu** — không mất UID, không cần nâng lại.

Config:

```yaml
level-gear:
  damage-percent-per-level: 3      # % ST mỗi level
  durability-percent-per-level: 3  # % giảm hao mỗi level
  max-level: 15
```

### 🛡️ Khiên level

| Level | Knockback khi đỡ |
|-------|------------------|
| Lv.1 | Nhẹ |
| Lv.2 | Trung bình (~2 block) |
| Lv.3 | Mạnh (~3–4 block) |

### 🗡️ Skill max theo path (signature)

Skill max **chỉ kích** khi:

1. Gear đạt **max level** loại đó  
2. Player đang theo **đúng path** của món signature  

| Path | Gear signature | Skill khi max |
|------|----------------|---------------|
| **Kiếm sĩ** | Kiếm · Mace Ultra | Kiếm: +ST + hất · Mace: % proc hất/chấn + hồi bền + debuff 5s |
| **Độc sư** | Rìu | Poison + slow mục tiêu |
| **Hỏa thần** | Spear | Đốt + ST phụ |
| **Pháp sư** | Hoe | Speed + Slow Falling khi dùng |
| **Công binh** | Cuốc · Xẻng | Haste khi đào |
| **Thủ hộ** | Áo · Quần · Khiên | Absorption + kháng khi bị đánh / đỡ |
| **Linh hồn** | Nón | Invis ngắn + kháng khi bị đánh |
| **Thám hiểm** | Giày · Trident | Giày: Speed + Jump khi bị đánh · Trident max: skill huy hiệu |
| **Cung thủ** | Cung · Nỏ | Skill max theo huy hiệu (Huyết/Địa/Thiên/Thí) |

> Enchant passive dùng được **mọi path**. Skill max **chỉ** đúng path.

### 🔨 Mace Ultra

```
Công thức:  3 Mảnh Level  +  đủ 4 huy hiệu  +  1 mace
Kết quả:    Mace Ultra (không hiện Lv.1)
Enchant:    Density V · Breach IV · Unbreaking III
Skill:      ~28% proc · path Kiếm sĩ · Weakness+Slowness 5s · hồi độ bền đặc biệt
```

### Cung / Nỏ / Trident (huy hiệu)

- Chỉ **1 loại huy hiệu** (khóa path), không trộn
- Lv.1 cần 5 huy hiệu · mỗi level +5
- Huyết = ST · Địa = bền · Thiên = đặc biệt · Thí = kiểm soát

---

## 🌙 Giờ Vàng Vắng (Quiet Bonus)

Chỉ khi server **vắng** (online ≤ `drop-max-online`, mặc định **12**):

```
Mảnh sưu tập (Huyết Ảnh · Địa Mạch · Thiên Cơ · Thí Luyện)
        │
        ├─ ghép mảnh cùng loại → Huy hiệu
        └─ 5 huy hiệu → 1 Mảnh Nâng Level
```

- Rơi từ: tinh anh / đào kim cương·debris / claim fate / thắng ordeal
- R-click huy hiệu → bonus nhỏ (buff / Điểm)
- Hệ số Điểm nhẹ khi server vắng

```
/ascend essence help
/ascend essence craft
```

---

## 📅 Mùa giải (Season)

```yaml
season:
  length-weeks: 3
  keep-score-percent: 50
  reset-path: true
```

- Hết hạn: **reset path**, giữ % Điểm (online)
- Admin: `/aa seasonroll`

---

## ✨ Kỹ năng chủ động

`/ascend skill` hoặc icon trong menu chính.

- Cần path + **≥ 3 node**
- Cooldown theo path (`skills.*`)
- Không stack spam — message khi đang CD

---

## ⚖️ Luật server liên quan Ascend

Các rule **có trong code** (khi plugin bật):

| Rule | Chi tiết |
|------|----------|
| **Đổi path** | Chỉ qua nút GUI «Đổi con đường» |
| **Mending nerf** | Vanilla Mending chỉ hồi **50%** · Gear Ascend **cấm** Mending |
| **Triệt sản Villager** | Villager **không sinh sản** |
| **Night Vision** | Duration dài hơn pulse → **không chớp tắt** |
| **Ordeal** | Cấm táo vàng, potion, sữa, mật ong |

---

## ⌨️ Lệnh người chơi

| Lệnh | Mô tả |
|------|--------|
| `/ascend` | Menu GUI |
| `/ascend path` | Liệt kê 9 path (không chọn) |
| `/ascend path tree` | Cây kỹ năng (text) |
| `/ascend unlock <id>` | Mở node |
| `/ascend fate` | Thiên Mệnh |
| `/ascend claim` | Nhận thưởng fate |
| `/ascend risk <điểm>` | Blood Contract |
| `/ascend skill` | Skill path |
| `/ascend join` | Vào Boss |
| `/ascend insurance` | Đổi mảnh → bảo hiểm |
| `/ascend prestige` | Prestige |
| `/ascend stats` | Hồ sơ |
| `/ascend guide` | Hướng dẫn GUI |
| `/ascend bounty` | Truy nã |
| `/ascend essence` | Sưu tập Giờ Vàng |

---

## 🛠️ Lệnh admin

| Lệnh | Mô tả |
|------|--------|
| `/ascend bs` | Set spawn Boss (1 điểm) |
| `/ascend bf <phút>` | Bắt đầu Boss |
| `/ascend bstop` | Ép dừng Boss |
| `/ascend bloodmoon` / `eclipse` | Event thế giới |
| `/aa reload` | Reload |
| `/aa reset <player>` | Reset 1 người |
| `/aa resetall confirm` | Wipe toàn server |
| `/aa grant <player> <node>` | Cấp node |
| `/aa setpath <player> <PATH>` | Ép path |
| `/aa seasonroll` | Sang mùa mới |

Permission: `allayascend.use` (default true) · `allayascend.admin` (op).

---

## ⚙️ Config quan trọng

| Key | Ý nghĩa | Mặc định |
|-----|---------|----------|
| `path-change-cost` | Phí đổi path (GUI) | 120000 |
| `level-gear.damage-percent-per-level` | **% ST mỗi level** | **3** |
| `level-gear.durability-percent-per-level` | **% giảm hao mỗi level** | **3** |
| `level-gear.max-level` | Max vũ khí/giáp/tool | 15 |
| `level-gear.shield-max-level` | Max khiên | 3 |
| `level-gear.bow-max-level` | Max cung | 5 |
| `season.length-weeks` | Độ dài mùa | 3 |
| `season.keep-score-percent` | % Điểm giữ khi sang mùa | 50 |
| `boss.scale-min` / `scale-max` | Scale boss | 2 / 7 |
| `ordeal.min-net-profit` | Lãi tối thiểu khi thắng ordeal | 200 |
| `risk.*` | Stake / mult / duration | — |
| `quiet-bonus.*` | Giờ Vàng Vắng | — |
| `performance.path-buff-interval-ticks` | Chu kỳ refresh buff path | 100 |

---

## 🆕 Changelog 1.0.13

### Gear Level — thuộc tính thật

- ✅ **+3% sát thương / level** cộng dồn (Attribute melee + event ranged)
- ✅ **+3% độ bền / level** giảm hao (trần 60%)
- ✅ Giáp: +Armor / +Toughness theo level
- ✅ Lore hiển thị rõ `+X% sát thương` · `+X% độ bền`
- ✅ **Gear cũ** tự migrate khi login / dùng — không mất progress
- ✅ Config: `damage-percent-per-level` · `durability-percent-per-level`

### Giữ nguyên

- Path / node / Thiên Mệnh / Risk / Ordeal / Boss / Bounty / Quiet Bonus
- Skill max signature theo 9 path
- Mace Ultra · Khiên knockback · Cung huy hiệu

---

## 📄 License

MIT © 2026 AllayMC
