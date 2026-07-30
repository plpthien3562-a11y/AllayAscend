# AllayAscend 1.5.0
## Cẩm nang toàn tập — Lối chơi · Cơ chế · Chiến lược · Quản trị

> **Plugin RPG progression** dành cho server Paper/Purpur **1.20.6+**, gắn kinh tế **Điểm** qua soft-hook **AllayScore**.  
> Thiết kế retention hardcore: **đường & node sống sót sau chết**; Điểm, streak, heat, risk **đốt khi chết**.  
> Bản quyền: MIT · AllayMC © 2026

---

## Mục lục

1. [Triết lý thiết kế](#1-triết-lý-thiết-kế)
2. [Cài đặt & phụ thuộc](#2-cài-đặt--phụ-thuộc)
3. [Bắt đầu trong 5 phút](#3-bắt-đầu-trong-5-phút)
4. [Hệ Điểm & chết](#4-hệ-điểm--chết)
5. [Bốn con đường (Path)](#5-bốn-con-đường-path)
6. [Cây 12 node — full table](#6-cây-12-node--full-table)
7. [Hợp đồng ngày / tuần](#7-hợp-đồng-ngày--tuần)
8. [Huyết ước (Blood Risk)](#8-huyết-ước-blood-risk)
9. [Thử thách chết người (Ordeal)](#9-thử-thách-chết-người-ordeal)
10. [Truy nã (Bounty) & chống farm](#10-truy-nã-bounty--chống-farm)
11. [Kỹ năng chủ động](#11-kỹ-năng-chủ-động)
12. [Nhiệt (Heat) · Prestige · Season](#12-nhiệt-heat--prestige--season)
13. [Lớp RPG sâu (1.5.0)](#13-lớp-rpg-sâu-150)
14. [GUI · Lệnh · Quyền](#14-gui--lệnh--quyền)
15. [Echo & vòng lặp “muốn chơi tiếp”](#15-echo--vòng-lặp-muốn-chơi-tiếp)
16. [Chiến lược chơi tối ưu](#16-chiến-lược-chơi-tối-ưu)
17. [Cân bằng kinh tế & chống lạm phát](#17-cân-bằng-kinh-tế--chống-lạm-phát)
18. [Hiệu năng (TPS)](#18-hiệu-năng-tps)
19. [Cấu hình đầy đủ](#19-cấu-hình-đầy-đủ)
20. [Admin toolkit](#20-admin-toolkit)
21. [FAQ · Troubleshooting](#21-faq--troubleshooting)
22. [Changelog ý tưởng 1.5.0](#22-changelog-ý-tưởng-150)

---

## 1. Triết lý thiết kế

AllayAscend **không** thay thế PvP gear hay rank AllayScore. Nó là **lớp danh tính dài hạn**:

| Trục | Mất khi chết? | Ý nghĩa |
|------|----------------|---------|
| Path + unlocked nodes | **Không** | “Tôi là ai trên server” |
| Điểm AllayScore | **Có** (do AllayScore) | Power curve chính, rủi ro thật |
| Contract streak | **Có** | Phạt AFK / death-careless |
| Heat | **Có** | Bonus risk tạm thời |
| Blood Risk stake | **Có** | High-roll, high-pain |
| Season points | **Thuế %** khi chết | Soft progress mùa |
| Prestige | **Không** | Đầu tư dài |
| Mastery / Title / Relics / Discoveries | **Không** | Chiều sâu sưu tầm |

**Mục tiêu cảm xúc:** mỗi session có mục tiêu rõ (contract / node / bounty / ordeal), mỗi cái chết **đau nhưng không xóa identity**, mỗi chiến thắng **đẩy bạn tới bước kế tiếp** (Echo).

---

## 2. Cài đặt & phụ thuộc

### Yêu cầu
- Paper / Purpur **1.20.6+** (API potion/attribute hiện đại)
- Java **21**
- Plugin **AllayScore** (softdepend — bắt buộc để trừ/cộng Điểm)

### Cài
1. Build: `mvn clean package`
2. Copy JAR vào `plugins/`
3. Đảm bảo AllayScore đã bật trước hoặc cùng lúc
4. Restart / `/aa reload`
5. Lần đầu plugin tạo `config.yml`, `messages.yml`, `progress.yml`

### Kiểm tra hook
Log khi enable thành công:
```text
AllayScore hooked — Điểm economy live.
AllayAscend 1.5.0 enabled — paths / contracts / risk / ordeal / bounty / skills / rpg-depth.
```
Nếu thấy *offline Điểm stub (0)* → AllayScore chưa hook; mọi spend sẽ fail.

---

## 3. Bắt đầu trong 5 phút

1. Vào game → gõ **`/ascend`** (hoặc `/asc`, `/thienmenh`)
2. Mở **Hướng dẫn** trong GUI (icon sách) — đọc 7 bước
3. **Con đường** → chọn 1 trong 4 (Kiếm / Pháp / Thám / Thủ)
4. Chơi bình thường: đào, giết, đi bộ, câu → **Hợp đồng** tự đếm
5. Khi đủ điều kiện → **Claim** (GUI hoặc `/ascend claim`) — **không tự trả thưởng**
6. Dùng Điểm mở **node** trên cây
7. Khi máu dày và tự tin: **Huyết ước**, **Truy nã**, **Thử thách**

> **Luật vàng:** chưa chọn path thì hầu hết contract **không đếm** (`contracts-rules.require-path: true`).

---

## 4. Hệ Điểm & chết

### Điểm đến từ đâu?
| Nguồn | Ghi chú |
|-------|---------|
| Login bonus | Base 25 + streak ×5 (max 30 ngày) |
| Claim hợp đồng | Có streak %, path bonus %, prestige %, risk mult |
| Bounty / Ordeal thắng | Có trần & decay |
| Combo / Discovery / Mastery | Nhỏ hoặc one-shot |
| Milestone season | Ngưỡng 150 → 2500 |

### Khi chết xảy ra gì?
1. **AllayScore** reset Điểm (message nhắc)
2. **Streak** hợp đồng về 0
3. **Heat** về 0
4. **Risk** đang active: mất stake (đã trừ sẵn)
5. **Season tax** ~30% điểm mùa
6. **Node / path / prestige / mastery / relics** giữ nguyên
7. Trong **Ordeal**: keep inventory + XP (vẫn fail ordeal)
8. Bị **truy nã** và bị đúng hunter giết: keep inventory + XP

---

## 5. Bốn con đường (Path)

Chọn **một lần**. Đổi đường tốn **120 000 Điểm** và **xóa toàn bộ node** đã mở (soft-reset).

| ID lệnh | Tên | Màu | Phong cách |
|---------|-----|-----|-------------|
| `kiem` | Kiếm sĩ | Đỏ | Cận chiến, sát thương, máu chiến |
| `phap` | Pháp sư | Tím | Di chuyển, sinh tồn, tàng hình chu kỳ |
| `tham` | Thám hiểm | Xanh biển | Tốc độ, haste, đào, nhảy |
| `thu` | Thủ hộ | Xanh lá | Resistance, regen, chống chết |

### Kỹ năng chủ động (cần ≥ 3 node)

| Path | Tên | Hiệu ứng | CD mặc định |
|------|-----|----------|--------------|
| Kiếm | **Cuồng nộ** | Strength II + Speed I (~6s) | 120s |
| Pháp | **Dịch chuyển** | Teleport theo hướng nhìn + slow falling | 100s |
| Thám | **Xung kích** | Dash + Speed II ngắn | 80s |
| Thủ | **Củng cố** | Resistance II + Absorption (~5s) | 130s |

Lệnh: `/ascend skill` hoặc click trong GUI.

---

## 6. Cây 12 node — full table

Chi phí là **Điểm**. Buff **passive** pulse định kỳ, **không mất khi chết**.  
Node `p6` (Pháp): **tàng hình 4s mỗi 45s** — không invis vĩnh viễn.

### Kiếm sĩ (`k1`→`k12`)

| ID | Tên | Buff chính | Giá (Điểm) |
|----|-----|------------|------------|
| k1 | Thế Đứng | Speed I | 5 000 |
| k2 | Nhát Chém | Strength I | 15 000 |
| k3 | Máu Lạnh | Resistance I | 35 000 |
| k4 | Bước Chiến | Speed + Strength | 70 000 |
| k5 | Cuồng Chiến | Strength + Speed | 120 000 |
| k6 | Huyết Chiến | Regeneration I | 200 000 |
| k7 | Thiết Giáp | Res + Fire Res | 320 000 |
| k8 | Hung Nộ | Strength + Regen | 480 000 |
| k9 | Tử Chiến | Strength II | 700 000 |
| k10 | Bất Diệt | Res + Regen + Speed | 950 000 |
| k11 | Chiến Thần | Strength II + Speed | 1 300 000 |
| k12 | Vô Địch | Regen + Strength II + Res | 1 800 000 |

### Pháp sư (`p1`→`p12`)

| ID | Tên | Buff chính | Giá |
|----|-----|------------|-----|
| p1 | Minh Nhãn | Night Vision | 5 000 |
| p2 | Bước Ảo | Speed I | 15 000 |
| p3 | Lá Chắn | Resistance I | 35 000 |
| p4 | Hỏa Giáp | Fire Resistance | 70 000 |
| p5 | Thủy Tức | Water Breathing + NV | 120 000 |
| p6 | Không Ảnh | Invis chu kỳ 4s/45s | 200 000 |
| p7 | Thần Tốc | Speed II | 320 000 |
| p8 | Pháp Giáp | Res + Fire | 480 000 |
| p9 | Thần Trí | Speed II + NV | 700 000 |
| p10 | Ảo Ảnh | Speed (+ vẫn có p6 cycle) | 950 000 |
| p11 | Pháp Vực | Res + Fire + Water + NV | 1 300 000 |
| p12 | Chân Pháp | Speed II + Res + Fire + NV | 1 800 000 |

### Thám hiểm (`t1`→`t12`)

| ID | Tên | Buff chính | Giá |
|----|-----|------------|-----|
| t1 | Bước Nhẹ | Speed I | 5 000 |
| t2 | Nhảy Xa | Jump Boost I | 15 000 |
| t3 | Thị Lực | Night Vision | 35 000 |
| t4 | Thợ Mỏ | Haste I | 70 000 |
| t5 | Lữ Khách | Speed + Jump + NV | 120 000 |
| t6 | Thợ Săn Quặng | Haste + Speed | 200 000 |
| t7 | Bóng Đêm | NV + Speed II | 320 000 |
| t8 | Đào Sâu | Haste II | 480 000 |
| t9 | Xuyên Địa | Haste II + Speed | 700 000 |
| t10 | Lữ Hành Gia | Speed II + Jump + NV | 950 000 |
| t11 | Chinh Phục | Haste II + Jump + NV | 1 300 000 |
| t12 | Kẻ Lang Thang | Haste II + Speed II + NV | 1 800 000 |

### Thủ hộ (`h1`→`h12`)

| ID | Tên | Buff chính | Giá |
|----|-----|------------|-----|
| h1 | Khiên Gỗ | Resistance I | 5 000 |
| h2 | Hồi Phục | Regeneration I | 15 000 |
| h3 | Bền Bỉ | Res + Speed | 35 000 |
| h4 | Lửa Không Chạm | Fire Resistance | 70 000 |
| h5 | Thủ Thành | Res + Regen | 120 000 |
| h6 | Giáp Sắt | Resistance II | 200 000 |
| h7 | Bất Khuất | Res + Regen + Fire | 320 000 |
| h8 | Thành Trì | Res II + Speed | 480 000 |
| h9 | Thủ Hộ | Res II + Regen | 700 000 |
| h10 | Bất Tử | Res II + Regen + Fire | 950 000 |
| h11 | Thủ Hộ Tối Thượng | Res II + Regen + Speed | 1 300 000 |
| h12 | Khiên Vĩnh Cửu | Res II + Regen + Fire + Speed | 1 800 000 |

**Tổng ~1 đường:** khoảng **6M+ Điểm** (curve dài nhiều tuần chơi đều).

Mở khóa: GUI cây kỹ năng hoặc `/ascend unlock <id>`.

---

## 7. Hợp đồng ngày / tuần

### Nguyên tắc quan trọng
- Tiến độ **tự đếm** khi đào / giết / đi / câu (và craft nếu config)
- Thưởng **chỉ khi CLAIM** (GUI hoặc lệnh) → chống AFK auto-payout / dupe
- Cần **đã chọn path**
- Creative / Spectator **không đếm**
- Walk: **không** bay, glide, vehicle; có thể chặn bơi; cần on-ground
- Rate-limit action (chống macro spam)

### Streak
- Claim daily liên tiếp ngày → streak +1
- **+4% thưởng / ngày streak**, trần **+40%**
- **Chết = đứt streak**

### Bonus khác trên claim
- Path `contract-bonus-percent` (cộng dồn node)
- Prestige: **+2% / level**
- Risk multiplier nếu đang Blood Contract
- Hard cap 1 claim: **1200 Điểm** (config)

### Bộ hợp đồng mặc định (rút gọn)

**Ngày**

| ID | Tên | Loại | Mục tiêu lượng | Thưởng base |
|----|-----|------|----------------|-------------|
| d_mine | Thợ mỏ | BREAK | 450 block đá/quặng | 42 |
| d_kill | Săn quái | KILL | 90 mob thường | 48 |
| d_travel | Lữ hành | WALK | 16 000 bước | 38 |
| d_fish | Câu cá | FISH | 35 | 45 |
| d_craft | Thợ thủ công | CRAFT | 40 | 40 |

**Tuần**

| ID | Tên | Loại | Lượng | Thưởng |
|----|-----|------|-------|--------|
| w_boss | Săn boss | KILL elite | 28 | 280 |
| w_ore | Khoáng hiếm | BREAK diamond/debris… | 48 | 300 |
| w_travel | Xuyên lục địa | WALK | 80 000 | 260 |

Reset daily/weekly theo lịch local server; progress incomplete bị clear khi sang ngày/tuần mới sau claim marker.

---

## 8. Huyết ước (Blood Risk)

**Ý tưởng:** cược Điểm → hoàn thành **1 hợp đồng (claim)** trong thời gian → nhận thưởng claim **nhân hệ số** + **hoàn stake**.

| Tham số | Mặc định |
|---------|----------|
| Min / Max stake | 800 / 4000 |
| Hệ số | ×1.30 (+ heat bonus nhỏ + prestige) |
| Thời hạn | 480 giây |
| Thua | Chết hoặc hết giờ → **mất stake** (đã trừ lúc vào) |

Cách chơi an toàn: chỉ risk khi contract gần xong và bạn ở vùng an toàn / có kế hoạch claim ngay.

---

## 9. Thử thách chết người (Ordeal)

Trả **phí vào cửa** → sống sót hết thời gian → thưởng (có trần).  
**Chết = mất phí**. Trong ordeal: **keep đồ**, nhưng **cấm** táo vàng / potion / sữa; buff tank (regen, resistance, absorption, strength, fire res…) **bị gỡ định kỳ**.

| Loại | Phí | Thời gian | Thưởng (min–max) |
|------|-----|-----------|------------------|
| Sóng xương | 1200 | 55s | 160–280 |
| Giáng lôi | 1400 | 40s | 180–310 |
| Hơi wither | 1600 | 32s | 200–340 |
| Hút vực | 1800 | 40s | 220–360 |
| Mưa lửa | 1500 | 45s | 190–320 |
| Sương độc | 1300 | 36s | 170–300 |
| Hút hồn | 2000 | 48s | 240–400 |

- Trần thưởng ordeal: **420**
- Cooldown giữa các lần: **300s**
- Cần AllayScore hook; GUI hiện phí / điểm hiện có

**Không phải máy in Điểm** — EV thường âm nếu chơi ẩu; dùng để heat, season, thrill.

---

## 10. Truy nã (Bounty) & chống farm

### Ba loại (ngẫu nhiên khi nhận)

1. **Săn tinh anh** — giết Enderman / Wither Skeleton / Piglin Brute / Ravager / Vindicator (mặc định 6 kill). Mob phải sống ≥ 40 ticks.
2. **Đào sâu** — Deepslate / Diamond Ore / Ancient Debris (mặc định 60 block).
3. **Truy nã người** — 1 player online **đích danh**:
   - Nạn nhân được báo đang bị truy nã
   - Bị **đúng hunter** giết → **không mất đồ & XP**
   - Hunter hoàn thành → thưởng

### Chống clone treo / farm (1.5.0)

| Cơ chế | Mô tả |
|--------|--------|
| Anti-AFK | Mục tiêu phải có activity (di chuyển) trong **45s** |
| Online tối thiểu | Acc vào server &lt; **120s** không làm mục tiêu |
| Combat tối thiểu | Phải damage trước **≥ 3s** mới tính kết liễu |
| Pair cooldown | Cùng cặp người: **3600s** không săn lại |
| Max / ngày | **5** truy nã hoàn thành |
| Decay thưởng | Mỗi lần trong ngày giảm ~**14%** |
| Trần điểm / ngày | **1600** Điểm từ bounty |
| Cooldown nhận | **240s** sau win; fail **150s** |
| Creative | Không đếm |

Phí vào mặc định: **500 Điểm**. Thời hạn: **900s**. Hết giờ = mất phí.

Permission miễn săn: `allayascend.bounty.immune`.

---

## 11. Kỹ năng chủ động

Xem bảng mục 5.  
Điều kiện: path đã chọn, **≥ 3 node**, hết cooldown, `skills.enabled: true`.

---

## 12. Nhiệt (Heat) · Prestige · Season

### Heat (0–100)
- Cộng khi kill / claim / ordeal / bounty
- Decay khi idle (~30s không gain → trừ dần)
- Tăng nhẹ payout risk / một số reward
- **Dump về 0 khi chết**

### Season points
- Nhận từ claim, unlock node, ordeal, bounty, discovery, mastery…
- Dùng mua **Prestige**
- Chết: mất **~30%** (season-tax)

### Prestige
- Cost: **900** season / level (mặc định)
- Max: **10**
- Bonus: **+2%** thưởng hợp đồng / level (vĩnh viễn)
- Không mất khi chết

### Milestone season (tự nhận khi đủ)

| Ngưỡng | Thưởng Điểm |
|--------|-------------|
| 150 | 120 |
| 400 | 280 |
| 800 | 500 |
| 1500 | 900 |
| 2500 | 1500 |

---

## 13. Lớp RPG sâu (1.5.0)

Tất cả chạy **trên event** (kill, unlock, claim, damage) — **không** thêm timer dày → bảo vệ TPS.

### Path Mastery
Mở **đủ 12/12** node của path → **MASTER**:
- Thưởng **2500 Điểm** (config)
- + season, + di vật
- Đánh dấu vĩnh viễn trên hồ sơ

### Danh hiệu (Title)
| Node đã mở | Danh hiệu |
|------------|-----------|
| 0–2 | Tân binh |
| 3–5 | Nhập môn |
| 6–9 | Tinh thông |
| 10–11 | Lão luyện |
| 12 / Mastery | Huyền thoại |

### Kill Combo
- Cửa sổ **4s** giữa 2 kill
- Mỗi mốc ×5: thưởng nhỏ (có giới hạn)
- Chết → combo về 0
- Lưu **max combo** lịch sử

### Khám phá (Discovery)
Lần đầu hạ: Warden, Elder Guardian, Wither, Ender Dragon, Ravager, Piglin Brute, Wither Skeleton, Evoker → Điểm + 1 di vật + season nhỏ.

### Di vật (Relics)
- Rơi từ claim (weekly chắc hơn)
- Đủ **10** tự đổi **40** season points

### Path XP
Tích khi unlock / claim / combo — chỉ số “độ gắn bó” path (hiển thị hồ sơ).

### Clutch
Khi máu rơi xuống **≤ 25% max HP** (sau damage):
- CD **180s**
- Cần ≥ 3 node
- Buff ngắn 3s theo path (Strength/Speed, Invis, Speed III, Res+Regen)

---

## 14. GUI · Lệnh · Quyền

### GUI chính (`/ascend`)
- Con đường (tiến độ X/12)
- Hợp đồng
- Huyết ước
- Thử thách (hiện phí & điểm)
- Truy nã (mô tả loại + đích danh)
- Kỹ năng đường
- Hướng dẫn 7 bước
- Hồ sơ (danh hiệu, mastery, di vật, combo, khám phá…)

### Lệnh người chơi

| Lệnh | Mô tả |
|------|--------|
| `/ascend` · `/asc` · `/thienmenh` | Menu |
| `/ascend path [kiem\|phap\|tham\|thu\|tree]` | Chọn / xem cây |
| `/ascend unlock <id>` | Mở node |
| `/ascend contract` | Xem hợp đồng |
| `/ascend claim [id]` | Nhận thưởng |
| `/ascend stats` | Hồ sơ chat |
| `/ascend risk <số>` | Huyết ước |
| `/ascend prestige [buy]` | Xem / mua prestige |
| `/ascend skill` | Kỹ năng |
| `/ascend bounty` | GUI truy nã |
| `/ascend guide` | Hướng dẫn |
| `/ascend echo` | Echo thủ công |
| `/ascend help` | Trợ giúp |

**Quyền:** `allayascend.use` (default true).

### Admin

| Lệnh | Mô tả |
|------|--------|
| `/aa reload` | Reload config + messages + paths |
| `/aa reset <player>` | Xóa tiến độ 1 người (online) |
| `/aa resetall confirm` | Xóa toàn server |
| `/aa grant <player> <nodeId>` | Cấp node |
| `/aa setpath <player> <KIEM\|…>` | Ép path |

**Quyền:** `allayascend.admin` (default op).

---

## 15. Echo & vòng lặp “muốn chơi tiếp”

Sau path chọn / unlock / claim, plugin hiện **title + subtitle + chat** gợi ý **mục tiêu kế**:
- Node tiếp theo + giá
- Contract dở
- Streak

Actionbar định kỳ (mặc định ~400s) thì thầm lại `lastEcho` — đủ thưa để không spam, đủ đều để session dài vẫn có hướng.

---

## 16. Chiến lược chơi tối ưu

### Tuần 1 (Tân binh)
1. Chọn path khớp lối chơi thật (thợ mỏ → Thám, PvP → Kiếm/Thủ)
2. Claim daily mỗi ngày — **bảo vệ streak**
3. Mở k1–k3 (hoặc tương đương) sớm để skill + bonus contract
4. Tránh ordeal / risk lớn khi Điểm mỏng

### Tuần 2–3
1. Weekly ore/boss khi party
2. Bounty **có chọn lọc** (đừng spam hết 5 lượt nếu EV thấp)
3. Risk chỉ khi 1 contract còn vài % và bạn an toàn
4. Tích season → prestige sớm (+% vĩnh viễn)

### Endgame path
1. Mastery 12/12
2. Prestige 10
3. Sưu tầm discovery + max combo cá nhân
4. Đổi path chỉ khi chắc chắn (phí 120k + mất node)

### PvP / hardcore survival
- Thủ / Kiếm ưu tiên Res + Regen
- Pháp invis chu kỳ để disengage
- Thám kiting + haste đào gear nhanh hơn

---

## 17. Cân bằng kinh tế & chống lạm phát

Thiết kế **daily net thấp**, **phí ordeal/bounty cao**, **thưởng bị siết**:

- Claim cap 1200
- Ordeal max reward 420, phí 1200–2000
- Bounty decay + daily earn cap 1600 + max 5/day
- Risk mult chỉ 1.30 (không phải x2+ dễ vỡ)
- Node đắt dần → sink Điểm khổng lồ
- Death đốt Điểm + streak + heat + season tax

**Farm clone** bị chặn bằng AFK check, combat time, pair CD, entity ticks.

---

## 18. Hiệu năng (TPS)

| Việc | Tần suất |
|------|----------|
| Pulse path buff | 60 ticks |
| Echo actionbar | 8000 ticks |
| Autosave | 6000 ticks (async schedule → save sync) |
| Heat decay | 100 ticks |
| Bounty expire | 200 ticks |
| Contract daily sweep | 1200 ticks |

**Không** có scanner entity toàn map, **không** AI custom nặng.  
Ordeal chỉ spawn local quanh player và cleanup UUID list.  
Combo / discovery / clutch = O(1) trên event.

---

## 19. Cấu hình đầy đủ

File: `plugins/AllayAscend/config.yml`

Các nhóm chính:
- `path-change-cost`
- `risk.*` · `heat.*` · `death.*` · `prestige.*`
- `skills.*` · `login-bonus.*`
- `contracts-rules.*` · `contracts.<id>.*`
- `bounty.*` (gồm anti-farm)
- `ordeal.*` từng loại
- `rpg.*` (mastery, combo, relic, clutch)
- `milestones` list
- `performance.*`

Messages: `messages.yml` (MiniMessage).  
Progress: `progress.yml` (không sửa tay khi server online).

Sau chỉnh: `/aa reload` (path trees + messages + config). Một số timer chỉ đọc lúc enable → restart nếu đổi interval.

---

## 20. Admin toolkit

- Theo dõi inflation: so sánh tốc độ claim vs sink node
- `reset` khi exploit; `resetall` chỉ maintenance season mới
- `grant` / `setpath` cho event / đền bù
- Bật `allayascend.bounty.immune` cho staff nếu cần
- Backup `progress.yml` trước wipe

---

## 21. FAQ · Troubleshooting

**Q: Thử thách không chạy dù đủ điểm?**  
A: Cần AllayScore hook. Bản 1.4.4+ đã fix Attribute max-health crash + refund nếu lỗi. Xem message thiếu điểm / cooldown / economy.

**Q: Contract không tăng?**  
A: Chưa chọn path; đang Creative; walk đang fly/glide; hoặc đã claim hôm đó.

**Q: Truy nã người không tính kill?**  
A: Mục tiêu AFK; combat &lt; 3s; không đúng UUID mục tiêu; hoặc đã hết giờ.

**Q: Đổi path mất hết skill tree?**  
A: Đúng design — fee + soft reset node.

**Q: Invis Pháp vĩnh viễn?**  
A: Không. Chỉ pulse 4s/45s từ node p6.

**Q: Có cần PlaceholderAPI?**  
A: Không bắt buộc cho core 1.5.0.

---

## 22. Changelog ý tưởng 1.5.0

- 12 node / path + GUI tiến độ  
- Ordeal an toàn API + GUI phí rõ  
- Bounty đích danh + keep inv khi bị săn  
- Anti-farm AFK/clone/pair/daily cap/decay  
- RpgDepth: Mastery, Title, Combo, Discovery, Relics, Path XP, Clutch  
- PotionEffectType hiện đại (Paper 1.20.5+)

---

## Phụ lục A — Vòng lặp session mẫu (60–90 phút)

```text
Login → nhận login bonus
→ /ascend xem contract gần xong
→ chơi (mine/kill/travel) 20–40 phút
→ claim daily (+streak)
→ mở 1 node nếu đủ Điểm
→ (optional) bounty 1 lượt nếu an toàn
→ (optional) risk nếu contract còn 1 cái gần done
→ logout khi còn streak, không liều death vô ích
```

## Phụ lục B — Thuật ngữ nhanh

| Thuật ngữ | Nghĩa |
|-----------|--------|
| Path | Con đường RPG cố định |
| Node | Ô skill tree, cost Điểm |
| Điểm | Currency AllayScore |
| Claim | Nhận thưởng contract thủ công |
| Streak | Chuỗi ngày claim daily |
| Heat | Nhiệt tạm, boost nhẹ |
| Risk / Huyết ước | Cược Điểm vào claim |
| Ordeal | Thử thách sống sót có phí |
| Bounty / Truy nã | Mục tiêu có thời hạn |
| Season | Điểm mùa → Prestige |
| Mastery | Full 12 node |
| Relic | Di vật đổi season |
| Clutch | Buff khi suýt chết |
| Echo | Gợi ý mục tiêu tiếp |

---

*Tài liệu này mô tả hành vi mặc định AllayAscend **1.5.0** theo source. Số liệu có thể đổi theo `config.yml` server của bạn.*

**AllayAscend** — *Commit to a path. Survive the score. Ascend.*
