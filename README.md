# AllayAscend 1.0.0

Plugin RPG gắn **AllayScore (Điểm)** cho Paper 1.20+.

- **Path + node** sống sót qua chết (identity dài hạn)
- **Điểm / streak / risk / ordeal entry** mất khi chết hoặc fail
- Soft-depend: **AllayScore**

```bash
mvn -q clean package
# jar: target/AllayAscend.jar
```

---

## Mục lục wiki

1. [Cài đặt](#cài-đặt)
2. [Cách chơi nhanh](#cách-chơi-nhanh)
3. [Hệ thống Điểm & chết](#hệ-thống-điểm--chết)
4. [9 Con đường (Path)](#9-con-đường-path)
5. [Cây kỹ năng (36 node)](#cây-kỹ-năng-36-node)
6. [Hợp đồng & Claim](#hợp-đồng--claim)
7. [Blood Contract (Risk)](#blood-contract-risk)
8. [Ordeal](#ordeal)
9. [Boss Event](#boss-event)
10. [Truy nã (Bounty)](#truy-nã-bounty)
11. [Mảnh Nâng Level & Bảo hiểm](#mảnh-nâng-level--bảo-hiểm)
12. [Mùa giải (Season)](#mùa-giải-season)
13. [Lệnh](#lệnh)
14. [Config quan trọng](#config-quan-trọng)

---

## Cài đặt

1. Cài **AllayScore** trước (economy Điểm).
2. Thả `AllayAscend.jar` vào `plugins/`.
3. Restart server.
4. (Tuỳ chọn) AllayShop cho `/shop`.

Java **21**, Paper **1.20.x**.

---

## Cách chơi nhanh

```
1. Farm XP → có Điểm (AllayScore)
2. /ascend → chọn 1 Path
3. Mở node trên cây (GUI 3 trang)
4. Làm hợp đồng → /ascend claim khi xong
5. (Muộn) Risk / Ordeal / Boss / Bounty
```

**3 câu nhớ:**
1. `/ascend` = menu chính
2. Hợp đồng xong phải **claim** mới có Điểm thưởng
3. Chết mất **Điểm**, **không mất** node đã mở

---

## Hệ thống Điểm & chết

| Mất khi chết | Giữ khi chết |
|--------------|--------------|
| Điểm AllayScore + Rank | Path + node đã mở |
| Streak hợp đồng | Prestige |
| Tiền cược Risk | — |
| Phí Ordeal (nếu đang chơi) | — |
| Heat | — |

Bảo hiểm chết (`/ascend insurance`): đổi 1 **Mảnh Nâng Level** → chết **giữ đồ**, chỉ mất **70% Điểm**.

---

## 9 Con đường (Path)

Chọn **1** path. Đổi path sau tốn `path-change-cost` (config) và **reset node**.

| ID lệnh | Tên | Phong cách | Skill chủ động (`/ascend skill`) |
|---------|-----|------------|----------------------------------|
| `kiem` | **Kiếm sĩ** | Cận chiến, sát thương & sức bền | Cuồng nộ — Strength + Speed ngắn |
| `phap` | **Pháp sư** | Di chuyển, hiệu ứng & sinh tồn | Dịch chuyển — blink + slow falling |
| `tham` | **Thám hiểm** | Tốc độ, đào quặng & cơ động | Xung kích — dash + Speed |
| `thu` | **Thủ hộ** | Phòng thủ, hồi phục & chống chết | Củng cố — Resistance + Absorption |
| `cung` | **Cung thủ** | Tầm xa, tốc độ kéo & cơ động | Mưa tên — Speed + Jump |
| `linh` | **Linh hồn** | Hấp thụ, Night Vision & kháng hiệu ứng | Lớp hồn — Invis ngắn + Resistance |
| `cong` | **Công binh** | Đào, craft, Haste & tiện ích | Xung công — Haste + Speed |
| `doc` | **Độc sư** | Poison, kiểm soát & bền bỉ | Nọc độc — Speed + Resistance |
| `hoa` | **Hỏa thần** | Lửa, sức mạnh bùng nổ & áp lực | Bùng cháy — Strength + Fire Resistance |

Skill cần **≥ 3 node** đã mở. Có cooldown theo config `skills.*`.

---

## Cây kỹ năng (36 node)

- Mỗi path ~**36 node** (GUI **3 trang × 12**).
- Giá tăng dần: tầng 1 ≈ **4.500** Điểm → tầng cao tới hàng triệu.
- Buff passive **nhẹ** (Speed / NV / Haste / Strength / Resistance / Regen / FireRes) — không stack máu bẩn.
- **Nhánh A/B** tại mốc **12** và **24** (chỉ chọn 1).
- Node sau nhánh cần **một trong hai** nhánh (OR).

### Bảng giá tham khảo (công thức `4500 × 1.28^(n-1)`)

| Tầng | Giá (Điểm) |
|------|------------|
| T1 | 4,500 |
| T2 | 5,800 |
| T3 | 7,400 |
| T5 | 12,100 |
| T8 | 25,300 |
| T12 | 68,000 |
| T18 | 299,100 |
| T24 | 1,315,400 |
| T30 | 5,785,000 |
| T36 | 8,000,000 |

### Chi tiết từng Path

#### Kiếm sĩ (`/ascend path kiem`)

- **Ý tưởng:** Cận chiến, sát thương & sức bền
- **Chu kỳ buff:** `SPEED → STRENGTH → RESISTANCE → REGENERATION → FIRE_RESISTANCE` (xoay theo tầng)
- **Skill:** Cuồng nộ — Strength + Speed ngắn
- **Prefix node id:** `k1` … `k36`, nhánh `k12a`/`k12b`, `k24a`/`k24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Thế Đứng, Nhát Chém, Máu Lạnh, Bước Chiến, Cuồng Chiến, Huyết Chiến, Thiết Giáp, Huyết Nộ, Chí Tôn, Bá Vương, Vô Song, Master Kiếm |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Pháp sư (`/ascend path phap`)

- **Ý tưởng:** Di chuyển, hiệu ứng & sinh tồn
- **Chu kỳ buff:** `NIGHT_VISION → SPEED → RESISTANCE → FIRE_RESISTANCE → REGENERATION` (xoay theo tầng)
- **Skill:** Dịch chuyển — blink + slow falling
- **Prefix node id:** `p1` … `p36`, nhánh `p12a`/`p12b`, `p24a`/`p24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Khởi Linh, Dịch Tầng, Lớp Khiên, Tàng Ảnh, Hồi Lực, Pháp Trận, Hộ Thể, Không Ảnh, Đại Pháp, Chân Sư, Pháp Thần, Master Pháp |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Thám hiểm (`/ascend path tham`)

- **Ý tưởng:** Tốc độ, đào quặng & cơ động
- **Chu kỳ buff:** `SPEED → JUMP_BOOST → FAST_DIGGING → NIGHT_VISION → RESISTANCE` (xoay theo tầng)
- **Skill:** Xung kích — dash + Speed
- **Prefix node id:** `t1` … `t36`, nhánh `t12a`/`t12b`, `t24a`/`t24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Lữ Khách, Bước Nhảy, Tay Đào, Đêm Rừng, Xuyên Sơn, Tốc Hành, Thám Sâu, Địa Đạo, Chinh Phục, Thiên Lý, Vô Tận, Master Thám |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Thủ hộ (`/ascend path thu`)

- **Ý tưởng:** Phòng thủ, hồi phục & chống chết
- **Chu kỳ buff:** `RESISTANCE → REGENERATION → FIRE_RESISTANCE → SPEED → RESISTANCE` (xoay theo tầng)
- **Skill:** Củng cố — Resistance + Absorption
- **Prefix node id:** `h1` … `h36`, nhánh `h12a`/`h12b`, `h24a`/`h24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Thế Thủ, Lớp Da, Hồi Phục, Chống Cháy, Khiên Sống, Bất Khuất, Thành Lũy, Huyết Thủ, Bất Diệt, Thủ Thần, Vách Sắt, Master Thủ |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Cung thủ (`/ascend path cung`)

- **Ý tưởng:** Tầm xa, tốc độ kéo & cơ động
- **Chu kỳ buff:** `SPEED → NIGHT_VISION → JUMP_BOOST → STRENGTH → RESISTANCE` (xoay theo tầng)
- **Skill:** Mưa tên — Speed + Jump
- **Prefix node id:** `c1` … `c36`, nhánh `c12a`/`c12b`, `c24a`/`c24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Tư Thế, Mắt Diều, Bước Nhảy, Tên Nhanh, Sát Thủ, Kình Xạ, Tinh Mắt, Cung Thánh, Thần Xạ, Siêu Việt, Chí Tôn Cung, Master Cung |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Linh hồn (`/ascend path linh`)

- **Ý tưởng:** Hấp thụ, Night Vision & kháng hiệu ứng
- **Chu kỳ buff:** `NIGHT_VISION → RESISTANCE → REGENERATION → SPEED → FIRE_RESISTANCE` (xoay theo tầng)
- **Skill:** Lớp hồn — Invis ngắn + Resistance
- **Prefix node id:** `l1` … `l36`, nhánh `l12a`/`l12b`, `l24a`/`l24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Khởi Linh, Lớp Hồn, Hấp Thụ, Bóng Đêm, Huyết Ảnh, Linh Giáp, Hồn Bất Diệt, Dạ Hành, Linh Vực, Thần Hồn, Vô Ảnh, Master Linh |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Công binh (`/ascend path cong`)

- **Ý tưởng:** Đào, craft, Haste & tiện ích
- **Chu kỳ buff:** `FAST_DIGGING → SPEED → NIGHT_VISION → RESISTANCE → FIRE_RESISTANCE` (xoay theo tầng)
- **Skill:** Xung công — Haste + Speed
- **Prefix node id:** `g1` … `g36`, nhánh `g12a`/`g12b`, `g24a`/`g24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Thợ Mới, Xách Ba Lô, Tay Nghề, Đào Sâu, Nhánh Đào, Nhánh Xây, Kỹ Sư, Thợ Cả, Siêu Đào, Công Xưởng, Đại Công, Master Công |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Độc sư (`/ascend path doc`)

- **Ý tưởng:** Poison, kiểm soát & bền bỉ
- **Chu kỳ buff:** `RESISTANCE → SPEED → NIGHT_VISION → REGENERATION → FIRE_RESISTANCE` (xoay theo tầng)
- **Skill:** Nọc độc — Speed + Resistance
- **Prefix node id:** `d1` … `d36`, nhánh `d12a`/`d12b`, `d24a`/`d24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Nọc Độc, Lớp Da, Bóng Rừng, Hấp Thụ, Nhánh Độc, Nhánh Kiểm, Độc Vực, Tê Liệt, Huyết Nọc, Độc Thần, Vô Độc, Master Độc |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

#### Hỏa thần (`/ascend path hoa`)

- **Ý tưởng:** Lửa, sức mạnh bùng nổ & áp lực
- **Chu kỳ buff:** `FIRE_RESISTANCE → STRENGTH → SPEED → RESISTANCE → REGENERATION` (xoay theo tầng)
- **Skill:** Bùng cháy — Strength + Fire Resistance
- **Prefix node id:** `f1` … `f36`, nhánh `f12a`/`f12b`, `f24a`/`f24b`

| Trang GUI | Node (tên gốc lặp theo chu kỳ 12) |
|-----------|----------------------------------|
| 1 (T1–12) | Tia Lửa, Lớp Than, Bùng Nổ, Hỏa Giáp, Nhánh Lửa, Nhánh Nổ, Diễm Long, Thiêu Đốt, Hỏa Thần, Dung Nham, Thiên Hỏa, Master Hỏa |
| 2 (T13–24) | Cùng bộ tên + hậu tố · 2 |
| 3 (T25–36) | Cùng bộ tên + hậu tố · 3 |

---

## Hợp đồng & Claim

- Tiến độ **tự đếm** (đào / giết / đi bộ trên đất / câu / craft).
- **Không tự cộng Điểm** — phải `/ascend claim` hoặc click GUI.
- Creative / bay / xe / chưa chọn path → **không đếm**.
- Chết → **đứt streak**.

---

## Blood Contract (Risk)

```
/ascend risk <số_điểm>
```

- Cược Điểm → trong thời gian phải **claim 1 hợp đồng**.
- Thắng: thưởng × multiplier + hoàn cược.
- Chết / hết giờ: **mất cược**.

---

## Ordeal

Thử thách có thể chết. Phí vào bằng Điểm.

| Ordeal | Ý tưởng |
|--------|---------|
| Sóng Xương | Đợt quái |
| Giáng Lôi | Sét |
| Hơi Wither | Wither + đói |
| Void Pull / Blaze Rain / Poison Fog / Soul Drain | Biến thể khó |

- **Thắng:** thưởng > phí (code ép lãi tối thiểu `min-net-profit`).
- **Thua:** mất phí; đồ có thể được giữ tùy ordeal.
- Trong ordeal: hạn chế táo vàng / potion hồi (config).

---

## Boss Event

| Lệnh | Ai | Việc |
|------|-----|------|
| `/ascend bs` | Admin | Đặt **1** spawn (set mới ghi đè cũ) |
| `/ascend bf <phút>` | Admin | Start boss, **bắt buộc** số phút |
| `/ascend join` | Member | Trả phí, tele vào |

- Boss = mob thù địch **random** (Ravager, Warden, Illusioner, …), scale **2–5**, buff mạnh.
- Hết giờ: boss biến mất = **fail**, join **mất phí**.
- Người **không join** không bị Boss đánh.
- Thắng: Điểm cho người còn sống + đã gây damage.
- **Mảnh Nâng Level chỉ người kết liễu** (hoặc top damage).

---

## Truy nã (Bounty)

- Elite / đào sâu / truy nã player.
- Nạn nhân được **báo tên hunter**.
- Sống hết giờ → thưởng sống sót (anti-AFK + daily cap).
- Bị hunter giết: **giữ đồ**, mất **50% Điểm**.
- Chống clone: AFK check, combat time, pair cooldown.

---

## Mảnh Nâng Level & Bảo hiểm

1. Ném **Mảnh** xuống đất cạnh giáp/vũ khí ≥ Kim Cương.
2. Nâng Level: enchant **cố định theo level**, **không enchant tay** thêm.
3. Mỗi lần nâng: **hồi 50% độ bền đã mất**.
4. L1=1 mảnh · L2=3 · L3=5 · L4=8 · L5=12…
5. `/ascend insurance` — 1 mảnh = 1 bảo hiểm chết.

---

## Mùa giải (Season)

```yaml
season:
  length-weeks: 3          # chỉnh được
  keep-score-percent: 50   # giữ 50% Điểm
  reset-path: true         # reset path + node
```

- Hết hạn: **reset path**, giữ % Điểm (online).
- Admin: `/aa seasonroll`.

---

## Lệnh

### Người chơi
| Lệnh | Mô tả |
|------|--------|
| `/ascend` | Menu GUI |
| `/ascend path [id]` | Chọn / xem path |
| `/ascend path tree` | Cây kỹ năng |
| `/ascend unlock <id>` | Mở node |
| `/ascend contract` | Hợp đồng |
| `/ascend claim` | Nhận thưởng hợp đồng |
| `/ascend risk <điểm>` | Blood Contract |
| `/ascend skill` | Skill path |
| `/ascend join` | Vào Boss |
| `/ascend insurance` | Đổi mảnh → bảo hiểm |
| `/ascend prestige` | Prestige |
| `/ascend stats` | Hồ sơ |
| `/ascend guide` | Hướng dẫn GUI |

### Admin
| Lệnh | Mô tả |
|------|--------|
| `/ascend bs` | Set spawn Boss (1 điểm) |
| `/ascend bf <phút>` | Bắt đầu Boss |
| `/ascend bloodmoon` / `eclipse` | Event thế giới |
| `/aa reload` | Reload |
| `/aa reset <player>` | Reset 1 người |
| `/aa resetall confirm` | Wipe toàn server |
| `/aa grant <player> <node>` | Cấp node |
| `/aa setpath <player> <PATH>` | Ép path |
| `/aa seasonroll` | Sang mùa mới |

---

## Config quan trọng

| Key | Ý nghĩa |
|-----|---------|
| `path-change-cost` | Phí đổi path |
| `season.length-weeks` | Độ dài mùa |
| `season.keep-score-percent` | % Điểm giữ khi sang mùa |
| `boss.schedule-window-hours` | Cửa sổ sau `/bs` (mặc định 72) |
| `boss.scale-min` / `scale-max` | Scale boss 2–5 |
| `ordeal.min-net-profit` | Lãi tối thiểu khi thắng ordeal |
| `contracts-rules.*` | Anti-AFK / claim |

---

## License

MIT © 2026 AllayMC
