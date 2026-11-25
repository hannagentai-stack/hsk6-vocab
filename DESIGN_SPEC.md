# TÀI LIỆU THÔNG SỐ THIẾT KẾ UI/UX (DESIGN SPECIFICATION)
**Dự án:** WebHSK6 — Ứng dụng Web Học Từ Vựng Tiếng Trung HSK 6 (Mobile-First & Desktop)  
**Link File Figma Trực Tiếp:** https://www.figma.com/design/mjyfcBM9dC0Q3oUXQcBKN3  
**Triết lý thiết kế:** Tối giản, thoáng đãng, thân thiện lấy cảm hứng từ trải nghiệm học tập của Duolingo (tập trung 1 tác vụ chính trên mỗi màn hình, ưu tiên thao tác ngón cái một tay trên điện thoại, phản hồi tức thì bằng màu sắc & âm thanh, không sao chép logo/linh vật thương hiệu).

---

## 1. CẤU TRÚC FILE FIGMA
File Figma gồm **3 Page** được tổ chức theo chuẩn Design System & Auto Layout:
1. **`01 · Style Guide & Components` (`node-id=0:1`)**: Bảng biến màu sắc, phân cấp chữ, bo góc, khoảng cách và 7 bộ Component tái sử dụng.
2. **`02 · Mobile Screens (390×844) — Primary` (`node-id=2:2`)**: Bộ màn hình điện thoại thiết kế ưu tiên trước (vùng chạm ngón cái ở nửa dưới màn hình) và luồng Prototype tương tác.
3. **`03 · Desktop Screens (1440×900)` (`node-id=2:3`)**: Bộ màn hình máy tính đồng bộ Component, thanh điều hướng trên cùng, khung học tập trung ở giữa (`max-width: 700px`) và lưới đáp án `2×2`.

---

## 2. HỆ THỐNG DESIGN TOKENS (BIẾN MÀU, CHỮ, KHOẢNG CÁCH)

### 2.1. Bảng màu ngữ nghĩa (Semantic Colors)
| Token Figma | Biến CSS | Mã Hex | Vai trò hiển thị |
|---|---|---|---|
| `color/bg/canvas` | `--bg-canvas` | `#F8FAFC` | Nền tổng thể của trang (sáng dịu, không chói mắt khi học lâu) |
| `color/bg/surface` | `--bg-surface` | `#FFFFFF` | Bề mặt thẻ câu hỏi, thẻ đáp án mặc định, khung cài đặt |
| `color/bg/subtle` | `--bg-subtle` | `#F1F5F9` | Nền thanh chuyển chế độ, thanh tiến độ chưa lấp đầy, huy hiệu số thứ tự |
| `color/brand/primary` | `--color-primary` | `#0EA5E9` | Nút hành động chính ("Bắt đầu học", thanh tiến độ) |
| `color/brand/primary-tint` | `--color-primary-tint` | `#F0F9FF` | Nền thẻ đang chọn, khu vực tải file, nút phụ chủ đạo |
| `color/brand/primary-border` | `--color-primary-border` | `#0284C7` | Viền thẻ đang chọn & gờ nổi khối đáy (3D lip) của nút chính |
| `color/brand/primary-text` | `--color-primary-text` | `#0369A1` | Chữ nhấn chủ đạo, nhãn Pinyin gợi ý |
| `color/state/correct` | `--color-correct` | `#22C55E` | Nút "Tiếp tục" khi trả lời đúng, huy hiệu dấu tích `✓` |
| `color/state/correct-tint` | `--color-correct-tint` | `#DCFCE7` | Nền thẻ đáp án đúng & thanh thông báo phản hồi đúng ở đáy màn hình |
| `color/state/correct-border` | `--color-correct-border` | `#16A34A` | Viền thẻ đáp án đúng & gờ nổi khối đáy nút đúng |
| `color/state/correct-text` | `--color-correct-text` | `#15803D` | Tiêu đề "Chính xác!" và nhãn Pinyin xanh lá |
| `color/state/wrong` | `--color-wrong` | `#EF4444` | Nút "Tiếp tục" khi trả lời sai, huy hiệu dấu chéo `✕` |
| `color/state/wrong-tint` | `--color-wrong-tint` | `#FEE2E2` | Nền thẻ chọn sai & thanh thông báo phản hồi sai |
| `color/state/wrong-border` | `--color-wrong-border` | `#DC2626` | Viền thẻ chọn sai & gờ nổi khối đáy nút sai |
| `color/state/wrong-text` | `--color-wrong-text` | `#B91C1C` | Tiêu đề "Chưa đúng rồi" |
| `color/accent/star` | `--color-star` | `#F59E0B` | Ngôi sao đánh dấu "Từ khó" & huy hiệu gợi ý |
| `color/accent/star-tint` | `--color-star-tint` | `#FEF3C7` | Nền chip "Đã lưu" từ khó & khung hé lộ gợi ý 1 chạm |
| `color/text/primary` | `--text-primary` | `#0F172A` | Chữ Hán, tiêu đề chính, nội dung đáp án |
| `color/text/secondary` | `--text-secondary` | `#64748B` | Chữ phụ, hướng dẫn ngắn, tiến độ phụ |
| `color/border/default` | `--border-default` | `#E2E8F0` | Viền thẻ mặc định (`1.5px` – `2px`) |
| `color/border/strong` | `--border-strong` | `#CBD5E1` | Gờ đáy thẻ mặc định (`3px`) & nút gạt tắt |

### 2.2. Hệ thống chữ (Typography Scale)
- **Font chữ Hán (Hanzi):** `'Noto Sans SC', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif` — nét chữ rõ ràng, dễ phân biệt các chữ HSK 6 nhiều nét (như `暧昧`, `兢兢业业`, `囊括`).
- **Font giao diện, Pinyin & Tiếng Việt:** `'Inter', 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif` — hỗ trợ trọn vẹn dấu thanh điệu Pinyin (`ā á ǎ à`, `ǖ ǘ ǚ ǜ`) và dấu tiếng Việt không bị lệch dòng.

| Style Figma | Font Family | Trọng lượng | Cỡ chữ (Mobile / Desktop) | Line Height | Ứng dụng |
|---|---|---|---|---|---|
| `Hanzi/Hero` | Noto Sans SC | Bold (`700`) | `48px` / `54px` | `60px` / `66px` | Chữ Hán chính ở màn hình câu hỏi Trung → Việt |
| `Hanzi/Card` | Noto Sans SC | Bold (`700`) | `24px` / `26px` | `32px` / `36px` | 4 thẻ đáp án chữ Hán ở chế độ Việt → Trung |
| `Hanzi/Inline` | Noto Sans SC | Bold (`700`) | `18px` – `20px` | `26px` | Chữ Hán trong thanh phản hồi & danh sách từ sai |
| `Pinyin/Large` | Inter | SemiBold (`600`) | `18px` – `20px` | `26px` – `28px` | Pinyin hiển thị ngay khi chọn đúng hoặc gợi ý |
| `Heading/H1` | Inter | Bold (`700`) | `22px` – `26px` | `30px` – `34px` | Tiêu đề trang chủ & màn hình kết quả |
| `Body/Button` | Inter | Bold (`700`) | `16px` | `22px` | Nhãn trên nút hành động chính / phụ |
| `Body/Option` | Inter | SemiBold (`600`) | `15px` – `16px` | `22px` | Nghĩa tiếng Việt trên 4 thẻ đáp án |
| `Body/Caption` | Inter | Medium (`500`) | `13px` | `18px` | Chú thích định dạng file, bộ đếm phụ |

### 2.3. Khoảng cách, Bo góc & Hiệu ứng nổi khối (Spacing, Radius & Tactile Elevation)
- **Thang khoảng cách (`Layout`):** `xs: 4px`, `sm: 8px`, `md: 12px`, `lg: 16px`, `xl: 20px`, `2xl: 24px`, `3xl: 32px`.
- **Bo góc (`Radius`):**
  - `radius/sm`: `10px` (ô số thứ tự `1–4` trong thẻ đáp án)
  - `radius/md`: `14px` (nút chọn chặng `10 / 20 / 50 từ`)
  - `radius/lg`: `16px` (nút chính & thẻ đáp án)
  - `radius/xl`: `20px` – `24px` (khung câu hỏi chính, khu vực tải file, thanh phản hồi đáy)
  - `radius/full`: `999px` (thanh tiến độ, chip Nghe / Gợi ý / Từ khó)
- **Hiệu ứng gờ nổi xúc giác (Tactile 3D Lip — không làm rối mắt):**
  - Thẻ đáp án mặc định & nút phụ: `box-shadow: 0 3px 0 #CBD5E1` (khi nhấn giữ dịch xuống `translateY(2px)` giảm bóng còn `0 1px 0`).
  - Nút chính (`Primary`): `box-shadow: 0 4px 0 #0284C7`.
  - Nút/thẻ Đúng (`Correct`): `box-shadow: 0 4px 0 #16A34A`.
  - Nút/thẻ Sai (`Wrong`): `box-shadow: 0 4px 0 #DC2626`.

---

## 3. ĐẶC TẢ CÁC COMPONENT TÁI SỬ DỤNG (PAGE 1)

1. **`Button` (`id: 4:78`)** — 4 biến thể (`Primary`, `Success`, `Danger`, `Secondary`):
   - Kích thước chuẩn Mobile: rộng `100%` (`342px` trong khung `390px` có lề ngang `24px`), **cao cố định `54px`** (đảm bảo chuẩn vùng chạm ngón cái `≥ 48px`), `padding: 0 20px`, `border-radius: 16px`.
2. **`AnswerCard` (`id: 4:111`)** — 8 biến thể (`Mode = Viet | Hanzi` × `State = Default | Selected | Correct | Wrong`):
   - Auto Layout `HORIZONTAL`, căn giữa trục phụ, `min-height: 58px`, `padding: 14px 16px`, `gap: 12px`, `border-radius: 16px`, viền `2px`.
   - Bên trái là `Option Badge` (`30×30px`, bo góc `10px`) hiển thị `1, 2, 3, 4` ở trạng thái mặc định/đã chọn, tự đổi thành `✓` (nền xanh `#22C55E`) khi đúng hoặc `✕` (nền đỏ `#EF4444`) khi sai.
3. **`ProgressBar` (`id: 4:112`)**:
   - Auto Layout `HORIZONTAL`, `gap: 12px`, gồm nút thoát `✕` (`24×24px`, vùng chạm `40×40px`) + thanh rãnh bo tròn cao `12px` (`#E2E8F0`, phần hoàn thành `#0EA5E9` chuyển mượt `width`) + bộ đếm câu `6/20`.
4. **`ModeSwitch` (`id: 4:128`)** — 2 biến thể (`ZH-to-VI`, `VI-to-ZH`):
   - Thanh chuyển nhanh dạng Segmented Control cao `42px`, nền `#F1F5F9`, `padding: 4px`, bo góc `12px`; tab đang chọn có nền trắng `#FFFFFF` chữ `#0369A1` in đậm. Đặt ngay đầu màn hình câu hỏi để đổi qua lại **Trung → Việt** và **Việt → Trung** chỉ với 1 chạm.
5. **`ActionChip` (`id: 4:146`)** — 4 biến thể (`Audio`, `Hint`, `StarOff`, `StarOn`):
   - Nút tròn dài mảnh (`height: 34px`, `padding: 8px 12px`, `gap: 6px`, `border-radius: 999px`) đặt gọn trong khung câu hỏi:
     - `🔊 Nghe`: đọc từ tiếng Trung bằng Web Speech API.
     - `💡 Gợi ý`: mở Pinyin (chế độ Trung → Việt) hoặc ký tự chữ Hán đầu tiên (chế độ Việt → Trung).
     - `⭐ Từ khó / Đã lưu`: đánh dấu từ HSK 6 khó nhớ vào bộ lọc riêng trong `localStorage`.
6. **`FeedbackBanner` (`id: 4:169`)** — 2 biến thể (`Correct`, `Wrong`):
   - Khung thông báo trượt lên từ cạnh dưới màn hình (`border-radius: 24px 24px 0 0` trên Mobile), `padding: 18px 24px 24px`, `gap: 14px`.
   - Khi **Đúng**: nền `#DCFCE7`, viền `#16A34A`, hiện tiêu đề *"Chính xác! 🎉"*, dòng nổi bật **`Chữ Hán · Pinyin`** kèm nghĩa tiếng Việt và nút **"Tiếp tục"** xanh lá.
   - Khi **Sai**: nền `#FEE2E2`, viền `#DC2626`, hiện tiêu đề *"Chưa đúng rồi"*, báo rõ đáp án đúng kèm **`Pinyin`** để người học ghi nhớ ngay trước khi bấm **"Tiếp tục"** màu đỏ.
7. **`UploadZone` (`id: 4:170`)**:
   - Auto Layout `VERTICAL` căn giữa, `padding: 28px 20px`, viền nét đứt `2px dashed #0284C7`, nền `#F0F9FF`, bo góc `20px`. Hỗ trợ chạm chọn file trên điện thoại hoặc kéo-thả trên máy tính cho `.pdf`, `.xlsx`, `.csv`, `.txt`.

---

## 4. CẤU TRÚC TỪNG MÀN HÌNH (MOBILE 390×844 & DESKTOP 1440×900)

| Mã màn hình | Tên màn hình | Bố cục Mobile (`390×844` — Ưu tiên ngón cái) | Bố cục Desktop (`1440×900` — Mở rộng thoáng) |
|---|---|---|---|
| **01** | **Trang chủ & Chọn chế độ** (`M01` / `D01`) | Dọc 1 cột (`padding: 20px 24px 28px`): Thanh tiêu đề + nút *Tải file* → Thẻ tiến độ kho 2.500 từ HSK 6 → Chọn chế độ → Hàng 3 nút chặng `10 / 20 / 50 từ` → Tuỳ chọn thứ tự & lọc *Chỉ ôn từ khó ⭐* → Nút **Bắt đầu học ngay** neo ở đáy vùng ngón cái. | Thanh điều hướng trên cao `72px` + Khung trung tâm rộng `640px` bo góc `28px` đặt giữa nền sáng `#F8FAFC`; chia 2 cột gọn cho *Số từ mỗi lượt* và *Lọc từ khó*. |
| **02** | **Tải lên file từ vựng** (`M02` / `D02`) | Dọc 1 cột: Nút quay lại `<` + tiêu đề → `UploadZone` → Thẻ hướng dẫn ngắn gọn (bảng 3 cột hoặc 4 cột có `STT` như file PDF 2.500 từ) kèm bảng ví dụ 3 dòng → Cụm 2 nút đáy: *Tải file mẫu (.csv)* & *Dùng kho 2.500 từ mặc định*. | Khung ngang `860px` chia 2 cột cân đối: Cột trái là `UploadZone` kéo-thả file; Cột phải là hướng dẫn định dạng, bảng mẫu và 2 nút hành động. |
| **03** | **Câu hỏi Trung → Việt** (`M03` / `D03`) | Đầu trang: `ProgressBar` + `ModeSwitch`. Giữa trên: Thẻ câu hỏi trắng chứa 3 `ActionChip` (`Nghe`, `Gợi ý`, `Từ khó`) + chữ Hán cực lớn `48px`. Nửa dưới (Thumb zone): 4 thẻ `AnswerCard` tiếng Việt xếp dọc (`gap: 11px`). | Khung trung tâm rộng `700px`: `ProgressBar` → Thẻ câu hỏi chữ Hán `54px` thoáng rộng → **Lưới `2×2`** gồm 4 thẻ `AnswerCard` (mỗi thẻ rộng `342px`, `gap: 16px`). |
| **04** | **Câu hỏi Việt → Trung** (`M04` / `D04`) | Tương tự `M03`, phần câu hỏi hiển thị nghĩa tiếng Việt in đậm `22px` (kèm huy hiệu vàng hé lộ chữ Hán đầu nếu bấm *Gợi ý*); nửa dưới là 4 thẻ đáp án chữ Hán `24px` rõ nét. | Khung trung tâm `700px` với nghĩa tiếng Việt `26px` và lưới `2×2` hiển thị 4 thẻ chữ Hán cỡ lớn `26px`. |
| **05A / 05B** | **Phản hồi Đúng & Sai** (`M05A/B` / `D05A/B`) | Giữ nguyên ngữ cảnh câu hỏi phía trên (thẻ đáp án đổi màu Xanh lá `✓` hoặc Đỏ `✕`, huy hiệu Pinyin bật sáng ngay dưới chữ Hán khi đúng); đáy màn hình trượt lên `FeedbackBanner` kèm Pinyin & nút **Tiếp tục** ngay dưới ngón cái. | Lưới đáp án đổi trạng thái màu tức thì; sát cạnh dưới màn hình hiện dải `FeedbackBanner` trải ngang toàn màn hình, gom nội dung căn giữa `700px`. |
| **06** | **Kết quả cuối bài** (`M06` / `D06`) | Huy hiệu cúp hoàn thành + Điểm phần trăm → Hàng 3 ô thống kê (`Đúng`, `Làm sai`, `Từ khó ⭐`) → Danh sách tóm tắt các từ vừa làm sai kèm Pinyin → 2 nút đáy: **Ôn lại từ vừa sai** & **Học chặng tiếp theo**. | Thẻ tổng kết trung tâm rộng `680px`, 3 ô thống kê lớn, hàng thẻ từ sai nằm ngang và 2 nút hành động đặt cạnh nhau (`2 cột`). |

---

## 5. LUỒNG TƯƠNG TÁC PROTOTYPE (FLOW CONNECTIONS)
Cả hai trang `02 · Mobile Screens` và `03 · Desktop Screens` đều đã gắn sẵn điểm bắt đầu (`Flow Starting Point`) và hiệu ứng chuyển cảnh `Smart Animate (Ease Out, 220ms)`:
1. **Trang chủ (`01`)** → Bấm *"Tải file"* → Mở **Tải lên file từ vựng (`02`)** → Bấm *"Quay lại / Dùng kho 2.500 từ"* → Trở về **Trang chủ (`01`)**.
2. **Trang chủ (`01`)** → Bấm *"Bắt đầu học ngay"* → Vào **Câu hỏi Trung → Việt (`03`)**.
3. **Câu hỏi Trung → Việt (`03`)** ↔ Bấm thanh `ModeSwitch` ↔ Chuyển tức thì sang **Câu hỏi Việt → Trung (`04`)**.
4. **Màn hình câu hỏi (`03` / `04`)** → Chạm đáp án đúng (#2) → Chuyển sang **Phản hồi Đúng kèm Pinyin (`05A`)**; chạm đáp án sai (#1) → Chuyển sang **Phản hồi Sai (`05B`)**.
5. **Phản hồi Đúng/Sai (`05A` / `05B`)** → Chạm nút *"Tiếp tục"* → Chuyển sang **Kết quả cuối bài (`06`)**.
6. **Kết quả cuối bài (`06`)** → Chạm *"Ôn lại câu vừa sai"* → Quay lại vòng ôn câu hỏi (`03`); chạm *"Học chặng tiếp theo"* → Về **Trang chủ (`01`)** tăng sang chặng kế tiếp.
