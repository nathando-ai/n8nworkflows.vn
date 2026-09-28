---
title: "🕋 **Tự Động Hóa Lịch Sử Cầu Nguyện & Nhắc Nhở Nghiêm Câm (Ayamul Bidh) Hàng Ngày Trên Google Calendar - N8n**"
description: "Workflow tự động hóa 100% không code giúp các sếp lập lịch cầu nguyện 5 thời khắc, nhắc nhở nghiêm câm Ayamul Bidh (13-15 Hijri) và các lời doa hàng ngày trên Google Calendar, dựa trên vị trí địa lý và API Aladhan chính xác. Giúp tăng cường kỷ luật ibadah hàng ngày mà không tốn thời gian thủ công."
slug: "tieu-dong-hoa-lich-su-cau-nguyen-nhac-nhom-ayamul-bidh"
tags: [n8n, automation, google-calendar, islamic-productivity, api-aladhan, no-code]
keywords: [tự động hóa n8n, lịch cầu nguyện hàng ngày, nhắc nhở nghiêm câm ayamul bidh, google calendar islam, api aladhan, tự động hóa ibadah]
---

# 🕋 **Tự Động Hóa Lịch Sử Cầu Nguyện & Nhắc Nhở Nghiêm Câm (Ayamul Bidh) Hàng Ngày Trên Google Calendar**

## 🔥 **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp có lẽ đã từng gặp phải tình trạng:
- **Quên thời gian cầu nguyện** giữa công việc bận rộn, dẫn đến mất thời gian quý báu cho ibadah.
- **Khó nhớ ngày nghiêm câm Ayamul Bidh** (13, 14, 15 Hijri), khiến các sếp bỏ lỡ cơ hội tăng thêm phước lành.
- **Phải thủ công cập nhật lịch hàng ngày**, tốn thời gian và dễ xảy ra lỗi.

**Workflow này giải quyết tất cả đó!** Với **API Aladhan** và **Google Calendar**, các sếp sẽ có một **lịch cầu nguyện tự động hóa hoàn hảo**, bao gồm:
✅ **5 thời khắc cầu nguyện** (Subuh, Dzuhur, Ashar, Maghrib, Isya) với thời gian chính xác.
✅ **Lời doa Pagi & Petang** (Dhikr sáng & chiều).
✅ **Nhắc nhở nghiêm câm Ayamul Bidh** (ngày 13, 14, 15 Hijri) để tăng phước lành.
✅ **Không trùng lặp sự kiện** (anti-duplicate) để tránh nhầm lẫn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công cập nhật lịch hàng ngày.
- **Chính xác 100%**: Thời gian cầu nguyện được tính toán dựa trên vị trí địa lý và API Aladhan.
- **Nhắc nhở nghiêm câm Ayamul Bidh**: Không bỏ lỡ ngày tăng phước lành.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động hàng ngày, không cần can thiệp.
- **Dễ dàng tùy chỉnh**: Chỉ cần thay đổi vị trí thành phố, workflow vẫn hoạt động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (đã kết nối với n8n).
2. **API Key Aladhan** (sẽ được tự động gọi trong workflow).
3. **Thời gian zone** được thiết lập là **Asia/Jakarta** (hoặc tương đương với vị trí của các sếp).
4. **Vị trí địa lý** (thành phố và quốc gia) của các sếp (ví dụ: Hà Nội, Việt Nam).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Cách 1: Import từ file JSON
1. Tải file workflow từ [n8n.io/workflows/15101](https://n8n.io/workflows/15101).
2. Trên giao diện n8n, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create Workflow**.

# Cách 2: Copy/Paste JSON
1. Mở n8n Editor → Nhấn **Create Workflow**.
2. Chọn **Import** → **Paste JSON**.
3. Dán toàn bộ mã JSON từ [n8n.io/workflows/15101](https://n8n.io/workflows/15101) vào ô.
4. Nhấn **Import**.
```

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **11 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu Hình Schedule Trigger (Lịch Khởi Động)**
- **Node**: `Schedule Trigger`
- **Lưu ý**:
  - Thiết lập **run once daily** (ví dụ: **00:05 AM** để chạy sớm sáng).
  - Đảm bảo **timezone** của n8n là **Asia/Jakarta** (hoặc timezone của vị trí các sếp).

##### **B. Cấu Hình Vị Trí Thành Phố & Quốc Gia**
- **Node**: `Set City and Country`
- **Lưu ý**:
  - Thay đổi giá trị mặc định từ:
    ```json
    city: Bandung
    country: Indonesia
    ```
    thành vị trí của các sếp (ví dụ: `city: Hà Nội`, `country: Việt Nam`).
  - **Kiểm tra chính tả** để tránh lỗi API.

##### **C. Cấu Hình Google Calendar OAuth2**
- **Node**: `Create an event` & `Get Today Event`
- **Lưu ý**:
  1. **Thêm credentials Google Calendar**:
     - Trên n8n, đi đến **Credentials** → **Add New** → Chọn **Google Calendar OAuth2**.
     - Đăng nhập tài khoản Google và cấp quyền cho n8n.
  2. **Chọn calendar** trong node `Create an event`:
     - Mở node `Create an event` → Tab **Credentials** → Chọn tài khoản Google đã kết nối.
     - Trong **Calendar ID**, chọn **calendar** của các sếp (hoặc tạo mới nếu chưa có).
  3. **Kiểm tra quyền**:
     - Đảm bảo tài khoản Google có quyền **thêm và đọc sự kiện** trong calendar.

##### **D. Cấu Hình API Aladhan (Tự Động)**
- **Node**: `Fetch Prayer Data` & `get hijri date`
- **Lưu ý**:
  - Workflow **tự động gọi API Aladhan** dựa trên vị trí đã thiết lập.
  - **Không cần API Key** (API Aladhan miễn phí và không yêu cầu key).

##### **E. Logic Nhắc Nhở Ayamul Bidh (13-15 Hijri)**
- **Node**: `detect ayamul bidh date` (Code Node)
- **Lưu ý**:
  - Node này **kiểm tra ngày Hijri** và thêm sự kiện **nhắc nhở nghiêm câm** nếu ngày là 13, 14, hoặc 15.
  - **Không cần chỉnh sửa** nếu các sếp muốn sử dụng logic mặc định.

##### **F. Anti-Duplicate (Tránh Trùng Lặp Sự Kiện)**
- **Node**: `IF Event Do not Exist` & `Get Today Event`
- **Lưu ý**:
  - Workflow **so sánh sự kiện mới** với sự kiện đã tồn tại trong ngày.
  - **Chỉ tạo sự kiện mới** nếu không có sự kiện tương tự trong Google Calendar.
  - **Kiểm tra** node `Get Today Event` để đảm bảo nó lấy được danh sách sự kiện hiện tại.

#### 3. **Kích Hoạt ⚡️**
1. **Test Run** (Kiểm tra dữ liệu mẫu):
   - Nhấn **Run Workflow** để kiểm tra nếu workflow chạy đúng.
   - Kiểm tra **Google Calendar** xem có sự kiện mới được tạo không.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, nhấn **Activate** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi Nhắc Nhở qua Telegram/WhatsApp**:
   - Thêm node **Telegram Bot** hoặc **WhatsApp Business API** để gửi thông báo khi gần đến thời gian cầu nguyện.
2. **Lưu Log Hoạt Động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử sự kiện đã tạo.
3.. **Hỗ Trợ Nhiều Người Dùng**:
   - Sử dụng **Google Sheets** để lưu danh sách người dùng và chạy workflow cho từng người.
4. **Thêm Nhạc Nhắc Nhở**:
   - Kết nối với **YouTube API** để phát nhạc nhắc nhở (ví dụ: Adhan).
5. **Tích Hợp AI Đọc Doa**:
   - Sử dụng **LLM Node** (như n8n-nodes-ai) để đọc lời doa Pagi/Petang bằng giọng nói.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa ibadah hàng ngày** mà không tốn thời gian thủ công. Với **Google Calendar** và **API Aladhan**, các sếp sẽ **không bao giờ quên thời gian cầu nguyện** và **không bỏ lỡ ngày nghiêm câm Ayamul Bidh**.

**Hãy áp dụng ngay và bắt đầu cuộc sống ibadah hiệu quả hơn!** 🌙✨

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📌 Lưu ý cuối cùng**:
- Nếu workflow không hoạt động, hãy kiểm tra:
  - **Credentials Google Calendar** có đúng không?
  - **Vị trí thành phố** có chính xác không?
  - **Timezone** của n8n có phù hợp không?
- **Không cần lo lắng về API Aladhan** vì nó miễn phí và không yêu cầu key!