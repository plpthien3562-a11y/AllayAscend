# AllayAscend 1.0.12

Plugin RPG gắn **AllayScore (Điểm)** cho Paper 1.20+.

- **Path + node** sống sót qua chết (identity dài hạn)
- **Điểm / streak / risk / ordeal entry** mất khi chết hoặc fail
- Soft-depend: **AllayScore**

```bash
mvn -q clean package
# jar: target/AllayAscend.jar
```

Java **21** · Paper **1.20.x** · MIT © 2026 AllayMC

---

## Mục lục wiki (thành viên)

1. [Cài đặt](#cài-đặt)
2. [Cách chơi nhanh](#cách-chơi-nhanh)
3. [Hệ thống Điểm & chết](#hệ-thống-điểm--chết)
4. [9 Con đường (Path)](#9-con-đường-path)
5. [Đổi path (nút GUI)](#đổi-path-nút-gui)
6. [Cây kỹ năng (36 node)](#cây-kỹ-năng-36-node)
7. [Thiên Mệnh & Claim](#thiên-mệnh--claim)
8. [Blood Contract (Risk)](#blood-contract-risk)
9. [Ordeal](#ordeal)
10. [Boss Event](#boss-event)
11. [Truy nã (Bounty)](#truy-nã-bounty)
12. [Mảnh Nâng Level & Bảo hiểm](#mảnh-nâng-level--bảo-hiểm)
13. [Giờ Vàng Vắng (Quiet Bonus)](#giờ-vàng-vắng-quiet-bonus)
14. [Mùa giải (Season)](#mùa-giải-season)
15. [Kỹ năng chủ động](#kỹ-năng-chủ-động)
16. [Luật server liên quan Ascend](#luật-server-liên-quan-ascend)
17. [Lệnh người chơi](#lệnh-người-chơi)
18. [Lệnh admin](#lệnh-admin)
19. [Config quan trọng](#config-quan-trọng)

---

## Cài đặt

1. Cài **AllayScore** trước (economy Điểm).
2. Thả `AllayAscend.jar` vào `plugins/`.
3. Restart server.
4. (Tuỳ chọn) AllayShop cho `/shop`.

---

## Cách chơi nhanh

```
1. Farm XP / chơi → có Điểm (AllayScore)
2. /ascend → chọn 1 Path (GUI)
3. Mở node trên cây (GUI 3 trang × 12)
4. Làm Thiên Mệnh → CLAIM khi xong
5. (Muộn) Risk / Ordeal / Boss / Bounty / Mảnh Level
```

**3 câu nhớ:**

1. `/ascend` = menu chính
2. Thiên Mệnh xong phải **claim** mới có Điểm thưởng
3. Chết mất **Điểm**, **không mất** node đã mở

---

## Hệ thống Điểm & chết

| Mất khi chết | Giữ khi chết |
|--------------|--------------|
| Điểm AllayScore + Rank | Path + node đã mở |
| Streak Thiên Mệnh | Prestige |
| Tiền cược Risk | — |
| Phí Ordeal (nếu đang chơi) | — |
| Heat | — |

**Bảo hiểm chết** (`/ascend insurance`): đổi 1 **Mảnh Nâng Level** → chết **giữ đồ**, chỉ mất **70% Điểm**.

Trong **Boss** đã join hoặc **Ordeal**: giữ đồ theo luật riêng của event.

---

## 9 Con đường (Path)

Chọn **1** path. Mỗi path có ~**36 node**, buff passive nhẹ, skill chủ động riêng.

| ID | Tên | Phong cách | Skill (`/ascend skill`) |
|----|-----|------------|-------------------------|
| `kiem` | **Kiếm sĩ** | Cận chiến, sát thương & sức bền | Cuồng nộ — Strength + Speed |
| `phap` | **Pháp sư** | Di chuyển, hiệu ứng & sinh tồn | Dịch chuyển — blink + slow falling |
| `tham` | **Thám hiểm** | Tốc độ, đào quặng & cơ động | Xung kích — dash + Speed |
| `thu` | **Thủ hộ** | Phòng thủ, hồi phục & chống chết | Củng cố — Resistance + Absorption |
| `cung` | **Cung thủ** | Tầm xa, tốc độ kéo & cơ động | Mưa tên — Speed + Jump |
| `linh` | **Linh hồn** | Hấp thụ, Night Vision & kháng hiệu ứng | Lớp hồn — Invis ngắn + Resistance |
| `cong` | **Công binh** | Đào, craft, Haste & tiện ích | Xung công — Haste + Speed |
| `doc` | **Độc sư** | Poison, kiểm soát & bền bỉ | Nọc độc — Speed + Resistance |
| `hoa` | **Hỏa thần** | Lửa, sức mạnh bùng nổ & áp lực | Bùng cháy — Strength + Fire Resistance |

Skill cần **≥ 3 node** đã mở. Cooldown theo config `skills.*`.

Buff path (Speed / NV / Haste / Strength / Resistance / Regen / FireRes) được **refresh định kỳ** với duration dài — **không chớp tắt** Night Vision.

---

## Đổi path (nút GUI)

> **Không còn lệnh** `/ascend path <id>` để chọn / đổi path.

**Cách đổi:**

1. `/ascend` → **Con đường** (mở cây kỹ năng)
2. Bấm nút **Đổi con đường** (góc dưới trái, slot compass)
3. Chọn path mới trong menu 9 ô

**Chi phí:** `path-change-cost` (mặc định **120.000 Điểm**) + **reset toàn bộ node** đã mở.

Lần đầu chọn path: miễn phí. `/ascend path` chỉ **liệt kê** path hoặc `/ascend path tree` xem cây text.

---

## Cây kỹ năng (36 node)

- GUI **3 trang × 12** node.
- Giá tăng dần (công thức tham khảo `4500 × 1.28^(n-1)`).
- **Nhánh A/B** tại mốc **12** và **24** (chỉ chọn 1).
- Node sau nhánh cần **một trong hai** nhánh (OR).

### Bảng giá tham khảo

| Tầng | Giá (Điểm) |
|------|------------|
| T1 | 4,500 |
| T2 | 5,800 |
| T5 | 12,100 |
| T12 | 68,000 |
| T18 | 299,100 |
| T24 | 1,315,400 |
| T30 | 5,775,000 |
| T36 | 8,000,000 |

Mỗi path có chu kỳ buff riêng (xoay theo tầng) và prefix node (`k1`…`k36`, `p1`…, `t1`…, `h1`…, `c1`…, `l1`…, `g1`…, `d1`…, `f1`…).

---

## Thiên Mệnh & Claim

Nhiệm vụ **cá nhân**, adaptive theo path & sức.

- Mỗi ngày **3 Thiên Mệnh** + **1 tuần**.
- Niche underdog: ít node → thưởng cao hơn (tối đa ~**x1.75**); ≥24 node → soft tax.
- Tiến độ tự đếm · **phải claim** mới nhận Điểm.
- Creative / bay / xe / chưa path → không đếm.
- Chết → **đứt streak**.

Mở: `/ascend` → Thiên Mệnh, hoặc `/ascend fate` · nhận: click item sẵn sàng hoặc `/ascend claim`.

---

## Blood Contract (Risk)

```
/ascend risk <số_điểm>
```

hoặc GUI **Huyết ước**.

- Cược Điểm → trong thời gian phải **claim 1 Thiên Mệnh**.
- Thắng: thưởng × multiplier + **hoàn cược**.
- Chết / hết giờ: **mất cược**.

Mặc định: min 500 · max 4000 · duration 600s · mult ~1.50.

---

## Ordeal

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

- **Thắng:** thưởng > phí (code ép lãi tối thiểu `min-net-profit`).
- **Thua:** mất phí; đồ giữ trong ordeal.
- Thoát game giữa ordeal: hoàn **50%** phí + cooldown nhẹ.

---

## Boss Event

| Lệnh | Ai | Việc |
|------|-----|------|
| `/ascend bs` | Admin | Đặt **1** spawn (ghi đè cũ) |
| `/ascend bf <phút>` | Admin | Start boss, **bắt buộc** số phút |
| `/ascend join` | Member | Trả phí, tele vào |
| `/ascend bstop` | Admin | Ép dừng |

- Boss = mob thù địch random (Ravager, Warden, …), scale **2–7**.
- Hết giờ: boss biến mất = **fail**, join **mất phí**.
- Người **không join** không bị Boss đánh.
- Thắng: Điểm cho người còn sống + đã gây damage.
- **Mảnh Nâng Level** cho người kết liễu (hoặc top damage).

---

## Truy nã (Bounty)

- Elite / đào sâu / truy nã player.
- Nạn nhân được **báo tên hunter**.
- Sống hết giờ → thưởng sống sót (anti-AFK + daily cap).
- Bị hunter giết: **giữ đồ**, mất **50% Điểm**.
- Chống clone: AFK check, combat time, pair cooldown.

---

## Mảnh Nâng Level & Bảo hiểm

1. Ném **Mảnh** xuống đất cạnh giáp/vũ khí ≥ Kim Cương (hoặc craft theo level).
2. Nâng Level: enchant **cố định theo level**, **không enchant tay** thêm.
3. Mỗi lần nâng: **hồi 50% độ bền đã mất**.
4. L1=1 mảnh · L2=3 · L3=5 · L4=8 · L5=12…
5. `/ascend insurance` — 1 mảnh = 1 bảo hiểm chết.
6. Gear Ascend: **không Anvil / Enchant table / Mending / Mend**.
7. **Khiên** tối đa **Lv.3** (Mảnh Level):
   - Lv.1 — đỡ đòn: knockback **nhẹ**
   - Lv.2 — đỡ đòn: knockback **trung bình** (~2 block)
   - Lv.3 — đỡ đòn: knockback **mạnh** (~3–4 block)






### Gear level & skill max theo **9 path** (công bằng)

**Max level**

| Loại | Max |
|------|-----|
| Vũ khí / giáp / tool (Mảnh Level) | **15** |
| Cung | **5** |
| Nỏ | **3** |
| Trident | **3** |
| Khiên | **3** |
| **Mace Ultra** | **1 bậc** (không hiện Lv) |

**Skill max — mỗi path có món signature**

| Path | Gear signature | Skill khi max |
|------|----------------|---------------|
| **Kiếm sĩ** | Kiếm · Mace Ultra | Kiếm: +ST + hất · Mace: % proc hất/chấn + hồi bền + debuff 5s |
| **Độc sư** | Rìu | Poison + slow mục tiêu |
| **Hỏa thần** | Spear | Đốt + ST phụ |
| **Pháp sư** | Hoe | Speed + Slow Falling khi dùng (đào/cày) |
| **Công binh** | Cuốc · Xẻng | Haste khi đào |
| **Thủ hộ** | Áo · Quần · Khiên | Absorption + kháng khi bị đánh / đỡ |
| **Linh hồn** | Nón | Invis ngắn + kháng khi bị đánh |
| **Thám hiểm** | Giày · Trident | Giày: Speed + Jump khi bị đánh · Trident max: skill huy hiệu |
| **Cung thủ** | Cung · Nỏ | Skill max theo huy hiệu khóa (Huyết/Địa/Thiên/Thí) |

> Skill max **chỉ** kích khi player đang theo **đúng path** của món đó. Enchant passive vẫn dùng được mọi path.

### Mace Ultra

- Tên **Mace Ultra** (không hiện Lv.1)
- Công thức: **3 Mảnh Level + đủ 4 huy hiệu** + 1 mace
- Full **Density V · Breach IV · Unbreaking III**
- Skill ~28% proc · path **Kiếm sĩ** · Weakness+Slowness **5s** · hồi độ bền đặc biệt


## Giờ Vàng Vắng (Quiet Bonus)

Chỉ khi server **vắng** (online ≤ `drop-max-online`, mặc định 12):

- Rơi mảnh sưu tập từ tinh anh / đào / fate / ordeal
- Ghép: mảnh → huy hiệu → Mảnh Level
- R-click huy hiệu để dùng bonus nhỏ
- Hệ số Điểm nhẹ khi server vắng

Xem: `/ascend essence help` hoặc icon **Sưu tập Giờ Vàng** trong menu.

---

## Mùa giải (Season)

```yaml
season:
  length-weeks: 3
  keep-score-percent: 50
  reset-path: true
```

- Hết hạn: **reset path**, giữ % Điểm (online).
- Admin: `/aa seasonroll`.

---

## Kỹ năng chủ động

`/ascend skill` hoặc icon trong menu chính.

- Cần path + ≥ 3 node
- Cooldown theo path (config `skills.*`)
- Không stack spam — message khi đang CD

---

## Luật server liên quan Ascend

Các rule này **có trong code plugin** (áp dụng khi plugin bật):

| Rule | Chi tiết |
|------|----------|
| **Đổi path** | Chỉ qua nút GUI «Đổi con đường». Lệnh `/ascend path <id>` **không** đổi path. |
| **Mending nerf** | Mending vanilla chỉ hồi **50%** độ bền so với gốc (chậm ~2×). Gear Ascend: **cấm** Mending. |
| **Triệt sản Villager** | Villager **không sinh sản** (breed / love mode bị hủy). |
| **Night Vision** | Buff path NV duration dài hơn chu kỳ pulse → **không chớp tắt**. |
| **Ordeal** | Cấm táo vàng, potion, sữa, mật ong trong lúc thử thách. |

---

## Lệnh người chơi

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

## Lệnh admin

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

## Config quan trọng

| Key | Ý nghĩa |
|-----|---------|
| `path-change-cost` | Phí đổi path (GUI) |
| `season.length-weeks` | Độ dài mùa |
| `season.keep-score-percent` | % Điểm giữ khi sang mùa |
| `boss.schedule-window-hours` | Cửa sổ sau `/bs` (mặc định 72) |
| `boss.scale-min` / `scale-max` | Scale boss |
| `ordeal.min-net-profit` | Lãi tối thiểu khi thắng ordeal |
| `risk.*` | Stake / mult / duration |
| `quiet-bonus.*` | Giờ Vàng Vắng |
| `performance.path-buff-interval-ticks` | Chu kỳ refresh buff path |

---

## License

MIT © 2026 AllayMC
