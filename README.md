<div align="center">

# ⚔️ AllayAscend

### Plugin RPG Progression cho Paper 1.20+ — mở rộng hệ **Điểm (AllayScore)**

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Paper](https://img.shields.io/badge/Paper-1.20.x-green)
![Java](https://img.shields.io/badge/Java-21-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)
![Status](https://img.shields.io/badge/status-hardcore%20survival-red)

**9 Con Đường · 36 Node kỹ năng · Thiên Mệnh · Blood Contract · Ordeal · Boss Event · Truy Nã · Mùa Giải**

</div>

---

## 📖 Giới thiệu

**AllayAscend** là plugin RPG progression sống-chết dành cho server sinh tồn hardcore, gắn trực tiếp vào nền kinh tế **Điểm** của **AllayScore**. Đây không phải một plugin "cày cho vui" — mọi hệ thống được thiết kế xoay quanh một triết lý duy nhất:

> **Danh hiệu (Path + Node) là vĩnh viễn. Của cải (Điểm, streak, cược) là tạm thời và sẽ mất khi bạn chết.**

Member chọn 1 trong 9 con đường tu luyện, mở dần cây kỹ năng 36 node bằng Điểm, hoàn thành Thiên Mệnh mỗi ngày để kiếm thêm Điểm, và có thể mạo hiểm với Blood Contract, Ordeal sinh tử, Boss Event cộng đồng, hoặc bị treo thưởng Truy Nã. Tất cả được cân bằng chặt để chống lạm phát và giữ chân người chơi trong dài hạn (~1 tháng/đường, mùa giải reset định kỳ).

### Vì sao chọn AllayAscend?

- 🔒 **Rủi ro thật** — chết mất Điểm, mất streak, mất tiền cược. Chỉ path/node là an toàn.
- 📈 **Curve dài hơi** — tổng chi phí một con đường ~3.5 triệu Điểm, chống việc "full trong 1 ngày".
- 🎯 **Cá nhân hoá** — Thiên Mệnh mỗi ngày được gán riêng theo path & tiến độ, không node → thưởng cao hơn để cân bằng người mới/cũ.
- 🎲 **Nhiều lối chơi rủi ro** — Risk (Blood Contract), Ordeal (thử thách chết người), Bounty (bị/đi săn người chơi).
- 👑 **Sự kiện cộng đồng** — Boss Event admin điều khiển, scale ngẫu nhiên 2×–7×.
- ⚙️ **Hiệu năng-first** — toàn bộ hệ thống event-driven, không thêm timer nặng gây tụt TPS.

---

## 📑 Mục lục

1. [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
2. [Cài đặt](#-cài-đặt)
3. [Build từ source](#-build-từ-source)
4. [Bắt đầu nhanh (cho member)](#-bắt-đầu-nhanh-cho-member)
5. [Hệ thống Điểm & những gì mất khi chết](#-hệ-thống-điểm--những-gì-mất-khi-chết)
6. [9 Con đường (Path)](#-9-con-đường-path)
7. [Cây kỹ năng — 36 Node](#-cây-kỹ-năng--36-node)
8. [Thiên Mệnh & Claim](#-thiên-mệnh--claim)
9. [Blood Contract (Risk)](#-blood-contract-risk)
10. [Ordeal — Thử thách sinh tử](#-ordeal--thử-thách-sinh-tử)
11. [Boss Event](#-boss-event)
12. [Truy Nã (Bounty)](#-truy-nã-bounty)
13. [Mảnh — Huy Hiệu — Nâng Cấp Trang Bị](#-hệ-thống-mảnh--huy-hiệu--nâng-cấp-trang-bị)
14. [Giờ Vàng Vắng — Tinh Hồn Cô Độc](#-giờ-vàng-vắng--tinh-hồn-cô-độc)
15. [Mùa giải (Season) & Prestige](#-mùa-giải-season--prestige)
16. [Danh sách lệnh đầy đủ](#-danh-sách-lệnh-đầy-đủ)
17. [Permissions](#-permissions)
18. [Tham chiếu Config](#-tham-chiếu-config)
19. [Cấu trúc mã nguồn](#-cấu-trúc-mã-nguồn)
20. [FAQ / Câu hỏi thường gặp](#-faq--câu-hỏi-thường-gặp)
21. [Đóng góp (Contributing)](#-đóng-góp-contributing)
22. [License](#-license)

---

## 🧩 Yêu cầu hệ thống

| Thành phần | Yêu cầu |
|---|---|
| Server | PaperMC **1.20.x** (khuyến nghị 1.20.6) |
| Java | **21** trở lên |
| Phụ thuộc mềm (softdepend) | **AllayScore** — bắt buộc để có kinh tế Điểm hoạt động |
| Tuỳ chọn | **AllayShop** — để dùng `/shop` cho các vật phẩm liên quan |

> ⚠️ Không có AllayScore, plugin vẫn load được nhưng **toàn bộ hệ Điểm sẽ không hoạt động** — hãy luôn cài AllayScore trước.

---

## 📦 Cài đặt

1. Cài **AllayScore** trước tiên (nền kinh tế Điểm).
2. Tải `AllayAscend.jar` (build sẵn hoặc tự build — xem mục dưới) và thả vào thư mục `plugins/`.
3. Khởi động lại (restart, không dùng `/reload`) server.
4. File cấu hình sẽ tự sinh tại `plugins/AllayAscend/config.yml` và `messages.yml` — chỉnh sửa theo nhu cầu server rồi `/aa reload`.
5. (Tuỳ chọn) Cài thêm **AllayShop** nếu muốn tích hợp `/shop`.

---

## 🛠️ Build từ source

```bash
git clone <repo-url>
cd AllayAscend
mvn -q clean package
```

File jar hoàn chỉnh sẽ nằm tại:

```
target/AllayAscend.jar
```

Dự án dùng Maven, biên dịch bằng **Java 21**, phụ thuộc `paper-api 1.20.6-R0.1-SNAPSHOT` (scope `provided`, lấy từ repo Maven của PaperMC).

---

## 🚀 Bắt đầu nhanh (cho member)

```
1. Farm XP như bình thường → đổi ra Điểm (AllayScore)
2. Gõ /ascend → chọn 1 trong 9 Path
3. Mở khoá node trên cây kỹ năng (GUI 3 trang, 12 node/trang)
4. Hoàn thành Thiên Mệnh hằng ngày → /ascend claim để nhận thưởng
5. (Khi đã quen) thử Risk / Ordeal / Boss Event / Bounty để kiếm nhanh hơn — nhưng rủi ro cao hơn
```

### 3 điều bắt buộc phải nhớ

1. `/ascend` mở menu chính — mọi thứ đều bắt đầu từ đây.
2. Thiên Mệnh hoàn thành **không tự động** trả thưởng — bạn **phải `/ascend claim`**.
3. Chết sẽ mất **Điểm và streak**, nhưng **không** mất Path hay node đã mở khoá.

---

## 💀 Hệ thống Điểm & những gì mất khi chết

| ❌ Mất khi chết | ✅ Giữ khi chết |
|---|---|
| Điểm AllayScore + Rank | Path đã chọn + toàn bộ node đã mở |
| Streak Thiên Mệnh (đứt chuỗi) | Prestige (cấp độ vượt mùa) |
| Tiền cược đang treo trong Blood Contract | — |
| Phí đã đóng khi đang chơi Ordeal | — |
| Heat (điểm "nóng" tích luỹ) | — |

**Bảo hiểm chết** (`/ascend insurance`): đổi **1 Mảnh Nâng Level** để kích hoạt — lần chết tiếp theo bạn **giữ nguyên đồ đạc**, chỉ mất **70% Điểm** thay vì mất trắng.

---

## 🛤️ 9 Con đường (Path)

Mỗi người chỉ chọn **1 Path** tại một thời điểm. Muốn đổi sang path khác, bạn phải trả `path-change-cost` (mặc định **120.000 Điểm**) và toàn bộ node hiện tại sẽ **reset về 0**.

| Lệnh chọn | Tên | Phong cách chơi | Skill chủ động (`/ascend skill`) |
|---|---|---|---|
| `/ascend path kiem` | **Kiếm sĩ** | Cận chiến, sát thương & sức bền | Cuồng Nộ — Strength + Speed ngắn hạn |
| `/ascend path phap` | **Pháp sư** | Di chuyển, hiệu ứng & sinh tồn | Dịch Chuyển — blink + slow falling |
| `/ascend path tham` | **Thám hiểm** | Tốc độ, đào quặng & cơ động | Xung Kích — dash + Speed |
| `/ascend path thu` | **Thủ hộ** | Phòng thủ, hồi phục & chống chết | Củng Cố — Resistance + Absorption |
| `/ascend path cung` | **Cung thủ** | Tầm xa, tốc độ kéo cung & cơ động | Mưa Tên — Speed + Jump Boost |
| `/ascend path linh` | **Linh hồn** | Hấp thụ, Night Vision & kháng hiệu ứng | Lớp Hồn — Invisibility ngắn + Resistance |
| `/ascend path cong` | **Công binh** | Đào, craft, Haste & tiện ích | Xung Công — Haste + Speed |
| `/ascend path doc` | **Độc sư** | Poison, kiểm soát & bền bỉ | Nọc Độc — Speed + Resistance |
| `/ascend path hoa` | **Hỏa thần** | Lửa, sức mạnh bùng nổ & áp lực | Bùng Cháy — Strength + Fire Resistance |

> Skill chủ động yêu cầu **≥ 3 node đã mở** và có cooldown riêng theo `skills.*` trong config (60–130 giây tuỳ path).

---

## 🌳 Cây kỹ năng — 36 Node

- Mỗi path có **36 node**, chia thành **3 trang GUI × 12 node/trang**.
- Giá node tăng theo cấp số nhân: `4500 × 1.28^(n-1)` Điểm.
- Buff passive **nhẹ** (Speed / Night Vision / Haste / Strength / Resistance / Regeneration / Fire Resistance) — không stack máu bẩn hay phá cân bằng PvP.
- Tại mốc **node 12** và **node 24** có **nhánh rẽ A/B** — chỉ được chọn **một trong hai**.
- Các node phía sau nhánh rẽ yêu cầu đã mở **một trong hai nhánh** (điều kiện OR, không cần cả hai).

### Bảng giá tham khảo

| Tầng | Giá (Điểm) |
|---|---|
| T1 | 4,500 |
| T2 | 5,800 |
| T3 | 7,400 |
| T5 | 12,100 |
| T8 | 25,300 |
| T12 (nhánh) | 68,000 |
| T18 | 299,100 |
| T24 (nhánh) | 1,315,400 |
| T30 | 5,785,000 |
| T36 (Master) | ~8,000,000 |

> 💰 Tổng chi phí hoàn thành trọn vẹn một Path (36 node) ước tính **~3.5 triệu Điểm**, thiết kế để mất khoảng **1 tháng** cày liên tục — chống việc max hoá trong vài ngày.

### Chi tiết 9 Path — chu kỳ buff & id node

<details>
<summary><b>Kiếm sĩ</b> (<code>k1</code>–<code>k36</code>, nhánh <code>k12a/b</code>, <code>k24a/b</code>)</summary>

- Chu kỳ buff xoay theo tầng: `Speed → Strength → Resistance → Regeneration → Fire Resistance`
- Trang 1 (T1–12): Thế Đứng, Nhát Chém, Máu Lạnh, Bước Chiến, Cuồng Chiến, Huyết Chiến, Thiết Giáp, Huyết Nộ, Chí Tôn, Bá Vương, Vô Song, Master Kiếm
- Trang 2 & 3: cùng bộ tên, hậu tố ·2 và ·3
</details>

<details>
<summary><b>Pháp sư</b> (<code>p1</code>–<code>p36</code>, nhánh <code>p12a/b</code>, <code>p24a/b</code>)</summary>

- Chu kỳ buff: `Night Vision → Speed → Resistance → Fire Resistance → Regeneration`
- Trang 1: Khởi Linh, Dịch Tầng, Lớp Khiên, Tàng Ảnh, Hồi Lực, Pháp Trận, Hộ Thể, Không Ảnh, Đại Pháp, Chân Sư, Pháp Thần, Master Pháp
</details>

<details>
<summary><b>Thám hiểm</b> (<code>t1</code>–<code>t36</code>, nhánh <code>t12a/b</code>, <code>t24a/b</code>)</summary>

- Chu kỳ buff: `Speed → Jump Boost → Fast Digging → Night Vision → Resistance`
- Trang 1: Lữ Khách, Bước Nhảy, Tay Đào, Đêm Rừng, Xuyên Sơn, Tốc Hành, Thám Sâu, Địa Đạo, Chinh Phục, Thiên Lý, Vô Tận, Master Thám
</details>

<details>
<summary><b>Thủ hộ</b> (<code>h1</code>–<code>h36</code>, nhánh <code>h12a/b</code>, <code>h24a/b</code>)</summary>

- Chu kỳ buff: `Resistance → Regeneration → Fire Resistance → Speed → Resistance`
- Trang 1: Thế Thủ, Lớp Da, Hồi Phục, Chống Cháy, Khiên Sống, Bất Khuất, Thành Lũy, Huyết Thủ, Bất Diệt, Thủ Thần, Vách Sắt, Master Thủ
</details>

<details>
<summary><b>Cung thủ</b> (<code>c1</code>–<code>c36</code>, nhánh <code>c12a/b</code>, <code>c24a/b</code>)</summary>

- Chu kỳ buff: `Speed → Night Vision → Jump Boost → Strength → Resistance`
- Trang 1: Tư Thế, Mắt Diều, Bước Nhảy, Tên Nhanh, Sát Thủ, Kình Xạ, Tinh Mắt, Cung Thánh, Thần Xạ, Siêu Việt, Chí Tôn Cung, Master Cung
</details>

<details>
<summary><b>Linh hồn</b> (<code>l1</code>–<code>l36</code>, nhánh <code>l12a/b</code>, <code>l24a/b</code>)</summary>

- Chu kỳ buff: `Night Vision → Resistance → Regeneration → Speed → Fire Resistance`
- Trang 1: Khởi Linh, Lớp Hồn, Hấp Thụ, Bóng Đêm, Huyết Ảnh, Linh Giáp, Hồn Bất Diệt, Dạ Hành, Linh Vực, Thần Hồn, Vô Ảnh, Master Linh
</details>

<details>
<summary><b>Công binh</b> (<code>g1</code>–<code>g36</code>, nhánh <code>g12a/b</code>, <code>g24a/b</code>)</summary>

- Chu kỳ buff: `Fast Digging → Speed → Night Vision → Resistance → Fire Resistance`
- Trang 1: Thợ Mới, Xách Ba Lô, Tay Nghề, Đào Sâu, Nhánh Đào, Nhánh Xây, Kỹ Sư, Thợ Cả, Siêu Đào, Công Xưởng, Đại Công, Master Công
</details>

<details>
<summary><b>Độc sư</b> (<code>d1</code>–<code>d36</code>, nhánh <code>d12a/b</code>, <code>d24a/b</code>)</summary>

- Chu kỳ buff: `Resistance → Speed → Night Vision → Regeneration → Fire Resistance`
- Trang 1: Nọc Độc, Lớp Da, Bóng Rừng, Hấp Thụ, Nhánh Độc, Nhánh Kiểm, Độc Vực, Tê Liệt, Huyết Nọc, Độc Thần, Vô Độc, Master Độc
</details>

<details>
<summary><b>Hỏa thần</b> (<code>f1</code>–<code>f36</code>, nhánh <code>f12a/b</code>, <code>f24a/b</code>)</summary>

- Chu kỳ buff: `Fire Resistance → Strength → Speed → Resistance → Regeneration`
- Trang 1: Tia Lửa, Lớp Than, Bùng Nổ, Hỏa Giáp, Nhánh Lửa, Nhánh Nổ, Diễm Long, Thiêu Đốt, Hỏa Thần, Dung Nham, Thiên Hỏa, Master Hỏa
</details>

---

## 📜 Thiên Mệnh & Claim

Hệ thống nhiệm vụ cá nhân thay thế cho "hợp đồng" kiểu cũ — **adaptive** theo tiến độ mỗi người.

- Mỗi ngày nhận **3 Thiên Mệnh** + **1 nhiệm vụ tuần**, gán riêng theo path và sức mạnh hiện tại.
- Có niche **underdog**: thưởng thêm cho hành động mạo hiểm như giết quái khi máu thấp, sống sót sau đòn chí mạng.
- **Càng ít node đã mở → thưởng càng cao** (tối đa nhân **~1.75×**) để bù cho người mới.
- **Từ 24 node trở lên** áp dụng "soft tax" — thưởng giảm dần vì đã đủ mạnh.
- Tiến độ tự động đếm khi bạn chơi bình thường, nhưng **bắt buộc gõ `/ascend claim`** để thực sự nhận Điểm.
- Không tính tiến độ khi: đang ở Creative, đang bay, đang ngồi xe, hoặc **chưa chọn Path**.
- **Chết sẽ làm đứt streak** Thiên Mệnh.

Ví dụ nhiệm vụ ngày (`config.yml → contracts`):

| ID | Tên | Loại | Số lượng | Thưởng | Tuần? |
|---|---|---|---|---|---|
| `d_mine` | Thợ mỏ | Đào khoáng | 450 | 42 Điểm | Không |
| `d_kill` | Săn quái | Giết mob | 90 | 48 Điểm | Không |
| `d_travel` | Lữ hành | Di chuyển | 16,000 block | 38 Điểm | Không |
| `d_fish` | Câu cá | Câu bất kỳ | 35 | 45 Điểm | Không |
| `d_craft` | Thợ thủ công | Craft bất kỳ | 40 | 40 Điểm | Không |
| `w_boss` | Săn boss | Giết mob tinh anh | 28 | 280 Điểm | **Có** |
| `w_ore` | Khoáng hiếm | Đào Diamond/Ancient Debris/Emerald | 48 | 300 Điểm | **Có** |
| `w_travel` | Xuyên lục địa | Di chuyển | 80,000 block | 260 Điểm | **Có** |

---

## 🩸 Blood Contract (Risk)

```
/ascend risk <số_điểm>
```

- Cược một lượng Điểm (tối thiểu **500**, tối đa **4,000**) rằng bạn sẽ **claim được ít nhất 1 Thiên Mệnh** trong thời gian giới hạn (**mặc định 600 giây**).
- **Thắng:** nhận lại tiền cược **+ thưởng ×1.5** (hệ số `reward-multiplier`), cộng thêm bonus nếu Heat cao (`heat-bonus: 0.10`).
- **Thua** (chết hoặc hết giờ chưa claim): **mất trắng tiền cược**.

---

## ⚔️ Ordeal — Thử thách sinh tử

Thử thách solo có thể khiến bạn chết, trả phí vào bằng Điểm để tham gia.

| Ordeal | Ý tưởng | Phí vào | Thời lượng | Thưởng (nếu thắng) |
|---|---|---|---|---|
| Sóng Xương (`bone_wave`) | Đợt quái dồn dập | 500 | 45s | 850–1,100 |
| Giáng Lôi (`thunder`) | Sét đánh liên tục | 600 | 35s | 1,000–1,300 |
| Hơi Wither (`wither_breath`) | Wither Effect + đói | 700 | 30s | 1,150–1,500 |
| Void Pull (`void_pull`) | Hút xuống vực | 800 | 36s | 1,300–1,700 |
| Blaze Rain (`blaze_rain`) | Mưa lửa Blaze | 650 | 40s | 1,100–1,400 |
| Poison Fog (`poison_fog`) | Sương độc | 550 | 32s | 950–1,250 |
| Soul Drain (`soul_drain`) | Rút hồn | 900 | 42s | 1,450–1,900 |

- **Thắng:** thưởng luôn **lãi ròng tối thiểu 200 Điểm** so với phí đã đóng (`min-net-profit` — được ép cứng trong code, không thể lỗ khi thắng).
- **Thua:** mất phí vào; đồ đạc có thể giữ hoặc mất tuỳ từng loại ordeal.
- Trong lúc Ordeal đang diễn ra: bị hạn chế dùng táo vàng / potion hồi máu (theo config).
- Cooldown giữa các lần chơi Ordeal: **120 giây**.

---

## 👑 Boss Event

| Lệnh | Ai dùng | Chức năng |
|---|---|---|
| `/ascend bs` | Admin | Đặt **1** điểm spawn boss (đặt mới sẽ ghi đè điểm cũ) |
| `/ascend bf <phút>` | Admin | Bắt đầu trận Boss, **bắt buộc** truyền số phút giới hạn |
| `/ascend join` | Member | Trả phí vào, được dịch chuyển đến khu vực Boss |

- Boss là một mob thù địch **ngẫu nhiên** (Ravager, Warden, Illusioner, …) được scale sức mạnh từ **2× đến 7×**, cùng buff sát thương/tốc độ mạnh.
- Hết giờ mà chưa hạ được boss → boss biến mất, coi như **thất bại**, người tham gia **mất phí** đã đóng.
- Người chơi **không `/ascend join`** sẽ không bị Boss tấn công.
- **Thắng:** tất cả người còn sống và đã gây sát thương đều nhận Điểm.
- **Mảnh Nâng Level** chỉ dành cho người **kết liễu boss** (hoặc người gây damage cao nhất).

Cửa sổ chờ mặc định sau khi admin đặt spawn (`/ascend bs`) là **72 giờ** trước khi lịch bị coi là hết hạn.

---

## 🎯 Truy Nã (Bounty)

- Người chơi mạnh/đào sâu/elite có thể bị treo thưởng để bị **truy nã bởi người chơi khác**.
- Nạn nhân sẽ được **thông báo tên hunter** đang treo lệnh săn mình.
- Sống sót hết thời gian (**900 giây**) → nhận thưởng sống sót, có chống AFK và giới hạn thưởng theo ngày.
- Nếu bị hunter giết: **giữ nguyên đồ đạc**, nhưng mất **50% Điểm**.
- Cơ chế chống clone/farm: kiểm tra AFK, thời gian giao chiến tối thiểu, cooldown cặp đấu (pair cooldown) 1 giờ.

---

## ⚒️ Hệ thống Mảnh — Huy Hiệu — Nâng Cấp Trang Bị

Đây là chuỗi nguyên liệu đầy đủ: **Mảnh (Shard)** → **Huy Hiệu (Badge)** → **Mảnh Nâng Level** → **Nâng cấp trang bị**. Toàn bộ vật phẩm chống dupe bằng UID gắn trong NBT.

### 1️⃣ Mảnh (Shard) — 4 loại, rơi từ Giờ Vàng Vắng

| Loại | Tên hiển thị | Vật phẩm | Màu | Nguồn rơi | Số mảnh cần để ghép **1 Huy hiệu** cùng loại |
|---|---|---|---|---|---|
| `hunt` | Mảnh Huyết Ảnh | Amethyst Shard | 🔴 Đỏ | Combo kill ≥30 (bội số 30) trên quái tinh anh whitelist | **6** |
| `mine` | Mảnh Địa Mạch | Raw Gold | 🟡 Vàng | Đào Kim Cương / Ancient Debris / Emerald / Nether Gold | **8** |
| `fate` | Mảnh Thiên Cơ | Prismarine Shard | 🟣 Tím | Claim Thiên Mệnh (ngày hoặc tuần) | **5** |
| `trial` | Mảnh Thí Luyện | Magma Cream | 🔵 Lam | Thắng Ordeal | **10** |

- Mỗi loại mảnh chỉ rơi từ **đúng nguồn tương ứng** — ví dụ Mảnh Địa Mạch chỉ rơi khi đào khoáng hiếm, không rơi khi giết quái.
- Điều kiện rơi chung: phải đang trong **Giờ Vàng Vắng** (xem mục bên dưới), có trần rơi mỗi ngày, và tỉ lệ nhân theo loại hành động (`quiet-bonus.mult.*`).

### 2️⃣ Ghép Mảnh → Huy Hiệu

Có 2 cách ghép, tự động không cần bàn craft:

- **Ném xuống đất gần nhau**: ném đủ số mảnh **cùng loại** (theo bảng trên) sát cạnh nhau → tự động gộp thành 1 Huy hiệu.
- **Lệnh gộp nhanh**: `/ascend essence craft` — tự động ghép **toàn bộ** mảnh đủ điều kiện đang có trong túi đồ (không cần thả ra đất).

### 3️⃣ Huy Hiệu (Badge) — 3 công dụng

Huy hiệu có 4 loại tương ứng 4 loại mảnh (Huyết Ảnh / Địa Mạch / Thiên Cơ / Thí Luyện), thể hiện bằng Red Dye / Gold Nugget / Purple Dye / Cyan Dye.

**a) Dùng trực tiếp lấy hiệu ứng tức thời** — chuột phải huy hiệu trên tay, hoặc gõ `/ascend essence <hunt|mine|fate|trial>` (tiêu **1 huy hiệu**/lần):

| Loại | Hiệu ứng khi dùng |
|---|---|
| Huyết Ảnh | Strength II + Speed I, 12 giây |
| Địa Mạch | Haste II, 15 giây |
| Thiên Cơ | **+250 Điểm** ngay lập tức |
| Thí Luyện | Resistance I + Absorption I, 12 giây |

**b) Ghép thành Mảnh Nâng Level** — cần **5 huy hiệu** (loại bất kỳ, gộp chung không phân biệt loại) → ra **1 Mảnh Nâng Level**. Ghép bằng cách ném 5 huy hiệu gần nhau xuống đất, hoặc `/ascend essence craft`.

**c) Dùng để khoá path nâng cấp cho Cung / Nỏ / Trident** — xem mục 5 bên dưới (đây là công dụng quan trọng nhất của huy hiệu ở giai đoạn cuối game).

### 4️⃣ Nâng cấp trang bị thường bằng Mảnh Nâng Level

Áp dụng cho: **giáp & vũ khí Kim Cương/Netherite**, **Khiên (Shield)**, **Spear**.

1. Ném **Mảnh Nâng Level** xuống đất cạnh trang bị muốn nâng.
2. Số mảnh cần theo cấp: **L1 = 1 · L2 = 3 · L3 = 5 · L4 = 8 · L5 = 12**, từ L6 trở đi mỗi cấp **+5 mảnh** (tối đa **Level 25**).
3. Enchant được gán **cố định theo cấp độ** — không cộng dồn/enchant thêm từ bàn phù phép, không dùng được Mending.
4. Mỗi lần nâng cấp **hồi 50% độ bền đã hao mòn**.
5. Enchant theo loại trang bị (tăng dần theo level, có trần):

| Loại trang bị | Enchant chính |
|---|---|
| Kiếm / Rìu | Sharpness (tối đa V), Unbreaking từ Lv8 |
| Giáp (mũ/áo/quần/giày) | Protection (tối đa IV), Unbreaking từ Lv8 |
| Cuốc / Xẻng / Cuốc chim | Efficiency (tối đa V), Unbreaking từ Lv5 |
| Khiên | Unbreaking (tối đa III), Thorns từ Lv10 |
| Spear | Sharpness/Impaling (tối đa V), Unbreaking, Knockback từ Lv8 |

### 5️⃣ Nâng cấp Cung / Nỏ / Trident bằng Huy Hiệu — khoá 1 đường vĩnh viễn

Ba loại vũ khí tầm xa này **không nâng bằng Mảnh Nâng Level** mà dùng **Huy hiệu**, và có luật riêng biệt:

- Lần nâng cấp **đầu tiên** sẽ **khoá vĩnh viễn** vũ khí theo **đúng 1 loại huy hiệu** dùng để nâng — từ đó về sau chỉ nâng tiếp được bằng loại đó, không thể đổi.
- Số huy hiệu cần cho level kế tiếp: **5 + (level hiện tại) × 5** — tức Lv1 cần 5, Lv2 cần 10, Lv3 cần 15... tăng dần đều.
- Mỗi loại huy hiệu cho một hướng enchant khác nhau trên Cung/Nỏ/Trident:

| Huy hiệu khoá | Phong cách | Ví dụ enchant nổi bật |
|---|---|---|
| Huyết Ảnh | Sát thương & knockback | Power/Impaling cao, Punch, Flame ở level cao |
| Địa Mạch | Bền bỉ & tiện ích | Unbreaking cao, Infinity (Cung), Loyalty (Trident) |
| Thiên Cơ | Hiệu ứng đặc biệt | Flame sớm, Multishot (Nỏ), Channeling (Trident) |
| Thí Luyện | Kiểm soát & bền | Punch/Piercing cân bằng + Unbreaking |

> ⚠️ Nếu ném nhầm huy hiệu khác loại với loại đã khoá cạnh vũ khí, hệ thống sẽ **từ chối** và báo lỗi — không tiêu hao huy hiệu.

### 6️⃣ Nâng cấp Mace — đặc biệt nhất

Mace yêu cầu **cả hai nguyên liệu cùng lúc**: **1 Mảnh Nâng Level + đủ cả 4 loại Huy hiệu** (tối thiểu 1 mỗi loại) ném gần nhau xuống đất.

- Mỗi lần nâng chỉ tốn **đúng 1 mảnh mỗi loại nguyên liệu** (1 Mảnh Nâng Level + 1 huy hiệu/loại), không nhân theo level.
- Mace có **skill on-hit theo mốc level** (chỉ kích hoạt khi đánh trúng, cooldown 2.5 giây, hoàn toàn event-driven — không chạy tick nền nên không ảnh hưởng TPS):

| Mốc Level | Hiệu ứng khi đánh trúng |
|---|---|
| Lv1–4 | Hất văng nhẹ |
| Lv5–9 | Chấn động, gây sát thương lan sang ≤3 mob gần đó |
| Lv10–14 | Làm chậm (Slowness) mục tiêu |
| Lv15–19 | Cộng thêm sát thương phụ |
| Lv20–25 | Hất mạnh + chấn động lan sang ≤5 mob gần đó |

### 7️⃣ Bảo hiểm chết

`/ascend insurance` — đổi **1 Mảnh Nâng Level** để nhận **1 lượt bảo hiểm chết**: lần chết kế tiếp bạn **giữ nguyên đồ đạc**, chỉ mất **70% Điểm** thay vì mất trắng.

---

## 🌙 Giờ Vàng Vắng — Tinh Hồn Cô Độc

Cơ chế thưởng cho việc chơi vào giờ vắng người — vật phẩm hiếm chỉ rơi khi server **ít online**.

- Chỉ rơi khi số người online **≤ 12**.
- Chỉ rơi từ các mob tinh anh nhất định: Enderman, Wither Skeleton, Piglin Brute, Evoker, Vindicator, Ravager, Warden, Elder Guardian, Blaze, Guardian, Phantom, Shulker, Hoglin — **không** rơi từ zombie/skeleton thường.
- Tỷ lệ rơi cơ bản theo số người online: solo ~1.2%, duo ~1.1%, từ 3 người trở lên giảm dần theo mỗi người thêm vào (chống lạm phát).
- Trần rơi tối đa mỗi người/ngày: **6 mảnh**.
- Hệ số nhân theo hành động: giết quái thường ×0.35, quái tinh anh ×1.4, đào quặng ×1.1, Thiên Mệnh ×0.9, Thiên Mệnh tuần ×1.6, Ordeal ×1.3.
- Có thông báo broadcast định kỳ mỗi **240 giây** khi tính năng đang bật.

---

## 🏆 Mùa giải (Season) & Prestige

```yaml
season:
  length-weeks: 3          # có thể chỉnh
  keep-score-percent: 50   # giữ 50% Điểm khi sang mùa
  reset-path: true         # reset Path + toàn bộ node
```

- Khi mùa giải kết thúc: **Path và node bị reset**, người chơi **online** giữ lại một phần trăm Điểm quy định.
- Admin chủ động chuyển mùa bằng `/aa seasonroll`.
- **Prestige** (`/ascend prestige`): tốn **900 Điểm mùa** để lên cấp, tối đa **level 10**, mỗi cấp cộng thêm **+2%** bonus vĩnh viễn — prestige **không bị mất** dù có reset mùa hay chết.

---

## 🕹️ Danh sách lệnh đầy đủ

### Người chơi

| Lệnh | Mô tả |
|---|---|
| `/ascend` (alias: `/asc`, `/thienmenh`) | Mở menu GUI chính |
| `/ascend path [id]` | Chọn hoặc xem thông tin path hiện tại |
| `/ascend path tree` | Mở cây kỹ năng (GUI 3 trang) |
| `/ascend unlock <id>` | Mở khoá 1 node cụ thể |
| `/ascend fate` | Xem Thiên Mệnh hiện tại |
| `/ascend claim` | Nhận thưởng Thiên Mệnh đã hoàn thành |
| `/ascend risk <điểm>` | Đặt Blood Contract (cược Điểm) |
| `/ascend skill` | Kích hoạt skill chủ động của path |
| `/ascend join` | Tham gia trận Boss Event đang mở |
| `/ascend insurance` (alias: `/ascend baohiem`) | Đổi Mảnh Nâng Level lấy bảo hiểm chết |
| `/ascend essence craft` (alias: `tinhhon`, `hon`, `quiet`) | Tự động ghép hết Mảnh/Huy hiệu đủ điều kiện trong túi |
| `/ascend essence <hunt\|mine\|fate\|trial>` | Tiêu 1 huy hiệu loại tương ứng để nhận buff/Điểm ngay |
| `/ascend prestige` | Prestige lên cấp (tốn Điểm mùa) |
| `/ascend stats` | Xem hồ sơ tiến độ cá nhân |
| `/ascend guide` | Hướng dẫn nhanh trong GUI |

### Admin

| Lệnh | Mô tả |
|---|---|
| `/ascendadmin` (alias: `/aa`) | Lệnh gốc quản trị |
| `/ascend bs` | Đặt điểm spawn Boss |
| `/ascend bf <phút>` | Bắt đầu trận Boss |
| `/ascend bloodmoon` / `/ascend eclipse` | Kích hoạt event thế giới |
| `/aa reload` | Tải lại config |
| `/aa reset <player>` | Reset tiến độ 1 người chơi |
| `/aa resetall confirm` | Xoá toàn bộ tiến độ server (cần xác nhận) |
| `/aa grant <player> <node>` | Cấp node cho người chơi |
| `/aa setpath <player> <PATH>` | Ép path cho người chơi |
| `/aa seasonroll` | Chuyển sang mùa giải mới |

---

## 🔑 Permissions

| Permission | Mặc định | Ý nghĩa |
|---|---|---|
| `allayascend.use` | `true` (mọi người) | Dùng lệnh `/ascend` |
| `allayascend.admin` | `op` | Dùng lệnh `/ascendadmin` (`/aa`) |

---

## ⚙️ Tham chiếu Config

| Key | Ý nghĩa |
|---|---|
| `path-change-cost` | Phí đổi sang path khác (mặc định 120,000) |
| `season.length-weeks` | Độ dài một mùa giải (tuần) |
| `season.keep-score-percent` | % Điểm được giữ lại khi chuyển mùa |
| `quiet-bonus.*` | Toàn bộ cấu hình cơ chế Giờ Vàng Vắng (tỉ lệ rơi, trần/ngày, hệ số nhân) |
| `quiet-bonus.craft.shards.*` | Số mảnh cần để ghép 1 huy hiệu, theo từng loại (hunt/mine/fate/trial) |
| `quiet-bonus.craft.badges-per-frag` | Số huy hiệu cần để ghép 1 Mảnh Nâng Level (mặc định 5) |
| `quiet-bonus.badge-use.fate-score` | Số Điểm nhận khi dùng trực tiếp 1 Huy hiệu Thiên Cơ (mặc định 250) |
| `level-gear.max-level` | Cấp tối đa của trang bị nâng cấp (25) |
| `level-gear.ranged-badges-base` / `ranged-badges-step` | Số huy hiệu cần cho Cung/Nỏ/Trident, tăng dần mỗi cấp |
| `level-gear.redeem.insurance-cost` | Số Mảnh Nâng Level cần cho 1 lượt bảo hiểm chết |
| `risk.min-stake` / `max-stake` | Giới hạn cược Blood Contract |
| `risk.reward-multiplier` | Hệ số thưởng khi thắng Risk |
| `heat.*` | Cấu hình tích/giảm điểm "Heat" |
| `death.season-tax-percent` | % Điểm bị trừ thêm khi chết trong mùa |
| `prestige.season-cost` / `max-level` / `bonus-per-level` | Cấu hình hệ Prestige |
| `skills.*` | Cooldown/duration skill chủ động theo từng path |
| `login-bonus.*` | Thưởng đăng nhập theo streak ngày |
| `contracts-rules.*` | Điều kiện chống gian lận khi làm Thiên Mệnh (AFK, đứng dưới nước, v.v.) |
| `contracts.*` | Danh sách Thiên Mệnh ngày/tuần, số lượng & thưởng |
| `bounty.*` | Toàn bộ cấu hình hệ Truy Nã (thưởng, cooldown, chống clone) |
| `rpg.*` | Cấu hình chiều sâu RPG: combo, discovery, relic, clutch |
| `ordeal.*` | Phí vào, thời lượng, thưởng của từng loại Ordeal |
| `milestones` | Các mốc thưởng theo streak dài hạn |
| `boss.*` | Phí vào, máu, scale, sát thương, thời gian chờ của Boss Event |
| `performance.*` | Chu kỳ tick cho buff path / echo / autosave — chỉnh để tối ưu TPS |

> 📌 File config đầy đủ có **316 dòng**, mỗi mục đều có comment giải thích trực tiếp trong `config.yml` — nên đọc kỹ trước khi chỉnh trên server thật.

---

## 🗂️ Cấu trúc mã nguồn

```
AllayAscend/
├── pom.xml
├── LICENSE
├── README.md
└── src/main/
    ├── java/com/allayascend/
    │   ├── AllayAscend.java              # Main class, đăng ký listener/command/manager
    │   ├── command/
    │   │   ├── AscendCommand.java         # Lệnh /ascend cho member
    │   │   └── AscendAdminCommand.java    # Lệnh /aa cho admin
    │   ├── data/
    │   │   ├── NodeDef.java               # Định nghĩa 1 node kỹ năng
    │   │   ├── PathId.java                # Enum 9 path
    │   │   └── PlayerProgress.java        # Trạng thái tiến độ 1 người chơi
    │   ├── gui/
    │   │   ├── AscendGUI.java             # Render menu & cây kỹ năng
    │   │   └── GuiHolder.java             # Holder phân biệt inventory custom
    │   ├── listener/
    │   │   ├── AscendListener.java        # Sự kiện gameplay (chết, giết, đào, v.v.)
    │   │   └── GuiListener.java           # Click trong GUI
    │   ├── manager/
    │   │   ├── BossEventManager.java      # Logic Boss Event
    │   │   ├── BountyManager.java         # Logic Truy Nã
    │   │   ├── EchoManager.java           # Hiệu ứng "Echo" định kỳ
    │   │   ├── EventCycleManager.java     # Bloodmoon / Eclipse
    │   │   ├── FateManager.java           # Thiên Mệnh (fate contracts)
    │   │   ├── LevelGearManager.java      # Mảnh Nâng Level, bảo hiểm
    │   │   ├── OrdealManager.java         # Logic Ordeal
    │   │   ├── PathManager.java           # Chọn/đổi path, buff theo chu kỳ
    │   │   ├── ProgressStore.java         # Lưu/đọc dữ liệu người chơi
    │   │   ├── QuietBonusManager.java     # Giờ Vàng Vắng
    │   │   ├── RiskManager.java           # Blood Contract
    │   │   ├── RpgDepthManager.java       # Combo, discovery, relic, clutch
    │   │   └── SkillManager.java          # Skill chủ động theo path
    │   └── util/
    │       └── ScoreBridge.java           # Cầu nối API sang AllayScore
    └── resources/
        ├── plugin.yml
        ├── config.yml
        └── messages.yml
```

---

## ❓ FAQ / Câu hỏi thường gặp

**Q: Tôi chưa cài AllayScore thì plugin có chạy không?**
A: Plugin vẫn load (softdepend) nhưng toàn bộ hệ Điểm sẽ không hoạt động đúng. Luôn cài AllayScore trước.

**Q: Đổi path có mất node đã mở không?**
A: Có. Đổi path sẽ **reset toàn bộ node** về 0 và tốn thêm `path-change-cost` Điểm.

**Q: Làm xong Thiên Mệnh mà không thấy nhận Điểm?**
A: Bạn cần gõ `/ascend claim` — tiến độ hoàn thành không tự động trả thưởng.

**Q: Vì sao node của tôi không mở được dù đủ Điểm?**
A: Kiểm tra xem node đó có nằm sau một **nhánh rẽ (12/24)** hay không — bạn cần mở ít nhất một trong hai nhánh trước đó.

**Q: Chết trong Ordeal có mất đồ không?**
A: Tuỳ loại Ordeal — một số giữ đồ, một số không. Xem chi tiết trong bảng Ordeal ở trên hoặc `messages.yml`.

**Q: Bảo hiểm chết dùng được mấy lần?**
A: Mỗi lần kích hoạt (`/ascend insurance`) tốn 1 Mảnh Nâng Level và chỉ có hiệu lực cho **1 lần chết tiếp theo**.

---

## 🤝 Đóng góp (Contributing)

Repo hoan nghênh Pull Request và Issue:

1. Fork repo, tạo branch riêng cho tính năng/fix (`feature/ten-tinh-nang` hoặc `fix/ten-loi`).
2. Giữ nguyên style code hiện có (Java 21, cấu trúc package theo `manager` / `listener` / `gui` / `command`).
3. Test kỹ trên Paper 1.20.x trước khi gửi PR — đặc biệt các thay đổi ảnh hưởng `performance.*` (tránh tụt TPS).
4. Mô tả rõ trong PR: tính năng làm gì, ảnh hưởng config nào, có cần migrate dữ liệu cũ không.
5. Với thay đổi cân bằng số liệu (giá node, thưởng, tỉ lệ rơi...), vui lòng giải thích lý do trong PR để dễ review.

Báo lỗi hoặc đề xuất tính năng: mở **Issue** kèm log server (nếu có) và bước tái hiện lỗi.

---

## 📄 License

MIT © 2026 AllayMC
