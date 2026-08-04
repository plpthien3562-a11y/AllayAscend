# ⚔️ AllayAscend **1.0.20**

> Plugin RPG gắn **AllayScore (Điểm)** cho **Paper 1.20+**  
> Path + node sống sót qua chết · Điểm / streak / risk cháy khi chết  
> Gear level bằng **kết liễu Boss** · skill giáp = kháng / phản / thoát chết (không buff)

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
| 6 | [Cây kỹ năng](#-cây-kỹ-năng-36-node) |
| 7 | [Thiên Mệnh](#-thiên-mệnh--claim) |
| 8 | [Risk / Ordeal / Bounty](#-risk--ordeal--bounty) |
| 9 | [Boss Event](#-boss-event) |
| 10 | [**Nâng Level Gear**](#-nâng-level-gear-boss--thuộc-tính--skill) ⭐ |
| 11 | [Skill path (vũ khí & giáp)](#-skill-max--chỉ-đúng-path) |
| 12 | [Giờ Vàng Vắng](#-giờ-vàng-vắng) |
| 13 | [Lệnh](#-lệnh) |
| 14 | [Config](#-config-quan-trọng) |
| 15 | [Changelog](#-changelog) |

---

## 📦 Cài đặt

```
1. Cài AllayScore trước (economy Điểm)
2. Thả AllayAscend.jar vào plugins/
3. Restart server
```

---

## 🎮 Cách chơi nhanh

```
1. Có Điểm (AllayScore) → /ascend → chọn Path
2. Mở node trên cây (GUI 3 trang)
3. Thiên Mệnh → CLAIM khi đủ
4. Boss Event → kết liễu để nâng level gear đang cầm / mặc
5. (Tuỳ) Risk · Ordeal · Bounty · Prestige
```

| | |
|---|---|
| 1️⃣ | `/ascend` = menu chính |
| 2️⃣ | Thiên Mệnh xong phải **claim** mới có Điểm |
| 3️⃣ | Chết mất **Điểm** · **không mất** node / level gear trên item |

---

## 💀 Hệ thống Điểm & chết

| ❌ Mất khi chết | ✅ Giữ khi chết |
|-----------------|-----------------|
| Điểm AllayScore | Path + node đã mở |
| Streak Thiên Mệnh | Prestige |
| Risk / heat / phí Ordeal | Level trên **item** (NBT) |

**Bảo hiểm chết** (`/ascend insurance`): đổi 1 Cục Netherite → chết **giữ đồ**, mất ~70% Điểm.

Boss đã join / Ordeal: giữ đồ theo luật event.

---

## 🛤️ 9 Con đường (Path)

Chọn **1** path. ~36 node, buff passive, skill chủ động (`/ascend skill`, cần ≥3 node).

| ID | Tên | Skill chủ động |
|----|-----|----------------|
| `kiem` | Kiếm sĩ | Cuồng nộ — Strength + Speed |
| `phap` | Pháp sư | Dịch chuyển — blink |
| `tham` | Thám hiểm | Xung kích — dash |
| `thu` | Thủ hộ | Củng cố — Resistance + Absorption |
| `cung` | Cung thủ | Mưa tên — Speed + Jump |
| `linh` | Linh hồn | Lớp hồn — Invis + Resistance |
| `cong` | Công binh | Xung công — Haste + Speed |
| `doc` | Độc sư | Nọc độc — Speed + Resistance |
| `hoa` | Hỏa thần | Bùng cháy — Strength + Fire Res |

---

## 🔄 Đổi path (nút GUI)

> **Không** dùng lệnh để chọn path.

```
/ascend → Con đường → «Đổi con đường» → chọn path mới
```

| Lần | Chi phí |
|-----|---------|
| Lần đầu | Miễn phí |
| Đổi sau | `path-change-cost` (mặc định **120.000 Điểm**) + **reset node** |

---

## 🌳 Cây kỹ năng (36 node)

- GUI **3 trang × 12** · giá tăng dần  
- Nhánh A/B tại mốc 12 và 24 (chỉ chọn 1)  
- Buff path **không mất khi chết**

---

## 📜 Thiên Mệnh & Claim

| | |
|---|---|
| Ngày | 3 fate · Tuần | 1 fate |
| Underdog | Ít node → thưởng cao hơn (tối đa ~×1.75) |
| Soft tax | ≥24 node → giảm nhẹ thưởng |
| Claim | **Bắt buộc** click / `/ascend claim` |
| Chết | **Đứt streak** |

---

## 🩸 Risk · Ordeal · Bounty

**Blood Contract (`/ascend risk`)**  
Cược Điểm → claim 1 Thiên Mệnh trong thời gian. Thắng: hệ số + hoàn cược. Chết/hết giờ: mất cược.

**Ordeal**  
Thử thách có phí · cấm táo vàng / potion / sữa. Thắng lãi tối thiểu (`min-net-profit`). Thoát game: hoàn 50%.

**Truy nã**  
Elite / đào / săn player. Nạn nhân bị hunter giết: **giữ đồ**, mất 50% Điểm.

---

## 👹 Boss Event

| Lệnh | Ai | Việc |
|------|-----|------|
| `/ascend bs` | Admin | Đặt 1 spawn |
| `/ascend bf <phút>` | Admin | Start (1–180 phút) |
| `/ascend join` | Member | Trả phí, tele vào |
| `/ascend bstop` | Admin | Ép dừng |

- Boss random (Ravager, Warden, …), scale **2–7**
- **BossBar** máu realtime cho người đã join
- HP ≤ **20%** → **bão sét 3s** giáng quanh người tham chiến (**1 lần / fight**)
- Kết liễu (`getKiller`) → **tiến trình level gear** (cầm + giáp mặc)
- Hết giờ = fail, mất phí join · người không join không bị boss đánh

```yaml
boss:
  enrage-hp-percent: 0.20
  storm-duration-seconds: 3
  storm-interval-ticks: 8
```

---

## 💎 Nâng Level Gear (Boss) · Thuộc tính · Skill

### Cách nâng — chỉ kết liễu Boss

> **Không** craft · **không** ném đất · **không** click túi để nâng level.  
> Admin: `/ascend up <level>` (cầm item tay chính, `allayascend.admin`).

| Gear | Cộng tiến trình |
|------|-----------------|
| Kiếm / rìu / spear / tool | Kết liễu Boss khi **cầm** |
| **Giáp** (nón/áo/quần/giày) | Kết liễu Boss khi **đang mặc** — **cùng công thức** kiếm |
| Cung / nỏ / trident | Kết liễu bằng **projectile** (đúng người bắn) |
| Mace | Cầm mace → thanh tiến trình → **Ultra** (mặc định **12** boss) |
| **Khiên** | **Đỡ đòn Boss** (+1 tiến trình mỗi lần đỡ) |

**Công thức** (`level-gear.boss-progress`):

```
cần = base + level × step
mặc định base=1 · step=2
→ Lv0→1: 1 · Lv1→2: 3 · Lv2→3: 5 · Lv3→4: 7 …
```

Tiến độ lưu **NBT `boss_progress`** trên item + thanh `[■■■□□]` trên lore.

```
Diamond Sword / Chestplate Lv.1 · cần 3 boss → Lv.2
  Tiến độ Boss → Lv.2: 2/3
  [■■■■■■□□□□]
```

### Max level

| Loại | Max |
|------|-----|
| Vũ khí cận / giáp / tool | **15** |
| Cung | **5** |
| Nỏ · Trident · Khiên | **3** |
| Mace Ultra | **1 bậc** |

### Thuộc tính mỗi level

| Stat | Công thức |
|------|-----------|
| Sát thương (vũ khí) | **+3% / level** cộng dồn |
| Độ bền | **+3% / level** giảm hao · trần **60%** |
| Giáp | **+0.25 Armor** + **+0.20 Toughness** / level |
| Xuyên giáp | Từ **Lv.10** (gear max 15): +2% / level |

### Enchant giáp mỗi level

- **Protection** = `min(4, level)` — mỗi level +1 (tới 4)
- Unbreaking tăng theo level
- Phụ: Projectile / Blast / Fire Protection · Thorns (Lv≥10)
- Giày: Feather Falling · Depth Strider · Nón: Respiration · Aqua Affinity

### Khiên knockback

| Level | Khi đỡ |
|-------|--------|
| 1 | Nhẹ |
| 2 | ~2 block |
| 3 | ~3–4 block |

---

## 🗡️ Skill max — chỉ đúng PATH

Điều kiện chung:

1. Item đạt **max level** loại đó  
2. Player theo **đúng path** signature  

Enchant passive dùng được **mọi path**. Skill max **chỉ** đúng path.

### Vũ khí / tool

| Path | Gear | Skill |
|------|------|--------|
| **Kiếm sĩ** | Kiếm max | +ST + hất khi đánh |
| **Kiếm sĩ** | **Mace Ultra** | ~28% proc: hất + chấn ≤4 mob + hồi bền · Weakness+Slow 5s |
| **Độc sư** | Rìu max | Poison + Slow mục tiêu |
| **Hỏa thần** | Spear max | Đốt + ST phụ |
| **Pháp sư** | Hoe max | Speed + Slow Falling khi dùng |
| **Công binh** | Cuốc / Xẻng max | Haste khi đào |
| **Cung thủ** | Cung / Nỏ max | Skill projectile (theo hệ nếu có) |
| **Thám hiểm** | Trident max | Skill projectile |

### Giáp — không buff potion (1.0.20)

Xử lý trực tiếp trên **đòn đánh** (giảm dame / phản / thoát chết):

| Path | Gear max | Hiệu ứng |
|------|----------|----------|
| **Thủ hộ** | Áo · Quần · Khiên | **−15% dame nhận** + **phản 12%** lên attacker |
| **Linh hồn** | Nón | **12%** né mạnh → đòn đó còn **30%** dame |
| **Thám hiểm** | Giày | **8%** thoát chết (còn **1 máu**, CD **45s**) |

```yaml
level-gear:
  armor-skill:
    reduce-percent: 0.15
    reflect-percent: 0.12
    phase-chance: 0.12
    clutch-chance: 0.08
    clutch-cd-ms: 45000
```

Sai path → chỉ còn enchant + attribute, **không** skill giáp.

### Mace Ultra

```
Cách: cầm Mace kết liễu đủ boss (mặc định 12) → Ultra
Enchant: Density V · Breach IV · Unbreaking III
Skill: path Kiếm sĩ · % proc · debuff 5s · hồi độ bền
```

---

## 🌙 Giờ Vàng Vắng

Khi server **vắng** (online ≤ `drop-max-online`):

- Rơi **Cục Kim Cương** sưu tập (Huyết / Địa / Thiên / Thí) — NBT
- Ghép: `/ascend essence craft` hoặc click trong túi
- Huy hiệu = `NETHERITE_INGOT` + NBT · R-click dùng buff nhỏ
- 5 huy hiệu → 1 **Cục Netherite · Nâng Level** (bảo hiểm / redeem)

> Cục custom **không đặt** xuống đất (mất NBT).  
> **Level gear không** dùng cục để nâng nữa — chỉ Boss kill.

---

## 📅 Mùa giải

```yaml
season:
  length-weeks: 3
  keep-score-percent: 50
  reset-path: true
```

Admin: `/aa seasonroll`

---

## ⌨️ Lệnh

### Người chơi

| Lệnh | Mô tả |
|------|--------|
| `/ascend` | Menu GUI |
| `/ascend path` / `path tree` | Liệt kê / cây text |
| `/ascend unlock <id>` | Mở node |
| `/ascend fate` · `claim` | Thiên Mệnh |
| `/ascend risk <điểm>` | Blood Contract |
| `/ascend skill` | Skill path chủ động |
| `/ascend join` | Vào Boss |
| `/ascend insurance` | Bảo hiểm chết |
| `/ascend prestige` · `stats` · `guide` · `bounty` | — |
| `/ascend essence` | Sưu tập Giờ Vàng |

### Admin (`allayascend.admin`)

| Lệnh | Mô tả |
|------|--------|
| `/ascend up [level]` | Set level **item tay chính** (Mace → Ultra) |
| `/ascend bs` | Set spawn Boss |
| `/ascend bf <phút>` | Bắt đầu Boss |
| `/ascend bstop` | Ép dừng Boss |
| `/aa reload` · `reset` · `resetall confirm` | — |
| `/aa grant` · `setpath` · `seasonroll` | — |

Permission: `allayascend.use` (default true) · `allayascend.admin` (op).

---

## ⚙️ Config quan trọng

| Key | Ý nghĩa | Mặc định |
|-----|---------|----------|
| `path-change-cost` | Phí đổi path | 120000 |
| `level-gear.boss-progress.base` / `step` | Boss kills mỗi bậc | 1 / 2 |
| `level-gear.mace-ultra-kills` | Boss → Mace Ultra | 12 |
| `level-gear.damage-percent-per-level` | % ST / level | 3 |
| `level-gear.durability-percent-per-level` | % giảm hao / level | 3 |
| `level-gear.armor-pen-start-level` | Bắt đầu xuyên giáp | 10 |
| `level-gear.armor-skill.*` | Kháng / phản / né / thoát chết | xem trên |
| `boss.enrage-hp-percent` | Ngưỡng bão sét | 0.20 |
| `boss.storm-duration-seconds` | Thời gian bão | 3 |
| `ordeal.min-net-profit` | Lãi tối thiểu Ordeal | 200 |
| `quiet-bonus.drop-max-online` | Trần online để rơi mảnh | 12 |

---

## ⚖️ Luật trong code

| Rule | Chi tiết |
|------|----------|
| Đổi path | Chỉ nút GUI «Đổi con đường» |
| Mending | Vanilla 50% · Gear Ascend **cấm** |
| Villager | Không sinh sản |
| Ordeal | Cấm táo vàng, potion, sữa |
| Nâng gear | **Chỉ** Boss kill (+ admin `/ascend up`) |

---

## 🆕 Changelog

### 1.0.20 — Skill giáp phòng thủ thật
- Thủ hộ: −% dame + phản %
- Linh hồn: tỉ lệ né mạnh (−70% đòn)
- Thám hiểm: tỉ lệ thoát chết (1 máu, CD)
- Bỏ buff potion từ skill giáp

### 1.0.19 — Skill giáp path + README
### 1.0.18 — Giáp boss kills như kiếm · Protection +1/level · Armor/Toughness
### 1.0.17 — `/ascend up [level]` admin
### 1.0.16 — BossBar + bão sét HP≤20%
### 1.0.15 — Nâng level chỉ bằng kết liễu Boss · NBT tiến độ
### 1.0.14 — Cục Netherite / Kim Cương NBT (Quiet Bonus)
### 1.0.13 — +3% ST / độ bền theo level · attribute giáp

---

## 📄 License

MIT © 2026 AllayMC
