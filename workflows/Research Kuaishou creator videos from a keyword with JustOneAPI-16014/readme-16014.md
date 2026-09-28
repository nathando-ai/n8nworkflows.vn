---
title: "🔍 Tự Động Hoá Nghiên Cứu Video Creator Kuaishou Từ Từ Khóa Với JustOneAPI (N8n)"
description: "Workflow tự động hóa tìm kiếm và phân tích video của các creator Kuaishou từ từ khóa cụ thể, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và phát hiện ra nội dung viral tiềm năng. Kết quả được xuất dưới dạng danh sách video chi tiết, sẵn sàng cho phân tích sâu hơn."
slug: "tu-dong-hoa-nghien-cuu-video-creator-kuaishou"
tags: [n8n, automation, market-research, justoneapi, kuaishou]
keywords: [n8n workflow nghiên cứu thị trường, tự động hóa tìm kiếm creator Kuaishou, JustOneAPI với n8n, phân tích video viral, tự động hóa no-code]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Video Creator Kuaishou Từ Từ Khóa Với JustOneAPI**

### **Giải Phẫu Nỗi Đau Của Các Sếp**
Các sếp marketing hay nghiên cứu thị trường thường phải **tốn nhiều thời gian thủ công** để:
- Tìm kiếm creator Kuaishou phù hợp với từ khóa nghiên cứu (ví dụ: "ẩm thực", "du lịch", "game").
- Lấy danh sách video của họ để phân tích nội dung, xu hướng, hoặc đối thủ cạnh tranh.
- Lọc và tổng hợp dữ liệu một cách hiệu quả trong Excel hoặc Google Sheets.

**Workflow này tự động hóa toàn bộ quá trình** bằng cách kết hợp **JustOneAPI** (API mạnh mẽ cho Kuaishou) và **n8n** (tự động hóa no-code), giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
✅ **Nhận dữ liệu chính xác** từ API chính thức (không phải web scraping rủi ro).
✅ **Cập nhật động** khi cần thay đổi từ khóa hoặc yêu cầu mới.
✅ **Xuất kết quả sẵn sàng phân tích** dưới dạng danh sách video chi tiết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị giới hạn bởi phiên bản miễn phí, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Danh sách video creator** được tự động lấy từ Kuaishou theo từ khóa (ví dụ: "ẩm thực", "du lịch").
- **Cấu trúc dữ liệu sạch** (ID video, tiêu đề, thời lượng, ngày upload, link xem).
- **Không cần code** – chỉ cần cấu hình API và từ khóa.
- **Hoạt động liên tục** – không giới hạn bởi phiên bản miễn phí của n8n.
- **Dễ mở rộng** – có thể kết hợp với Slack/Telegram để báo cáo kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản JustOneAPI**:
   - Đăng ký tại [JustOneAPI](https://www.justoneapi.com/) và lấy **API Key**.
   - Chọn gói phù hợp (gói free có giới hạn request).
   - **Lưu ý**: API Key này sẽ được sử dụng trong workflow, **không chia sẻ cho người khác**.

2. **Tài khoản Kuaishou Developer** (nếu cần):
   - JustOneAPI là wrapper cho API chính thức của Kuaishou, nên **không cần đăng ký tài khoản Kuaishou riêng** (trừ khi muốn kiểm tra thủ công).

3. **Dữ liệu đầu vào**:
   - Từ khóa nghiên cứu (ví dụ: "ẩm thực", "du lịch", "game").
   - (Tùy chọn) Các tham số bổ sung như số lượng kết quả trả về, thời gian upload (ví dụ: video trong 30 ngày gần nhất).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io/workflows/16014](https://n8n.io/workflows/16014) (chọn "Download JSON").
  2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Mở file JSON từ link trên và **copy toàn bộ nội dung**.
  2. Trên n8n Editor, nhấn **"Import"** → **"Paste JSON"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **9 node chính**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node "Prepare API and Research Fields" (Set)**
- **Cấu hình**:
  - Thay đổi giá trị của `keyword` thành từ khóa nghiên cứu của các sếp (ví dụ: `"ẩm thực"`).
  - Cấu hình `apiKey` bằng **API Key của JustOneAPI** (đã lấy ở bước chuẩn bị).
  - Tham số `baseUrl` (nếu cần thay đổi, mặc định là `https://api.justoneapi.com`).

##### **B. Node "Search Kuaishou Users by Keyword" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.justoneapi.com/kuaishou/search/users`.
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer <API_KEY_CỦA_JUSTONEAPI>
    ```
  - **Body (JSON)**:
    ```json
    {
      "keyword": "{{ $node["Prepare API and Research Fields"].json["keyword"] }}",
      "limit": 20  // Số lượng kết quả trả về (tùy chỉnh)
    }
    ```

##### **C. Node "If User ID Exists" (If)**
- **Lưu ý**:
  - Node này **lọc bỏ user ID trống hoặc không hợp lệ** trước khi lấy video.
  - Nếu kết quả không có user ID nào, workflow sẽ **dừng ở đây** (không gây lỗi).

##### **D. Node "Fetch User Video List from Kuaishou" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.justoneapi.com/kuaishou/user/videos`.
  - **Headers** (giống như node trước):
    ```
    Authorization: Bearer <API_KEY_CỦA_JUSTONEAPI>
    ```
  - **Body (JSON)**:
    ```json
    {
      "user_id": "{{ $node["Extract User IDs from Search Results"].json["user_id"] }}",
      "limit": 50  // Số lượng video lấy cho mỗi creator
    }
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** và nhập từ khóa mẫu (ví dụ: `"ẩm thực"`).
   - Kiểm tra kết quả trong node **"Output Final Creator Video List"** (Set).
   - **Kiểm tra lỗi**: Nếu có lỗi API, kiểm tra lại `API Key` và `keyword`.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để **báo cáo kết quả tự động** khi workflow hoàn thành.
   - Ví dụ: Gửi danh sách video mới nhất vào kênh Slack của team.

2. **Lưu log vào Google Sheets/Excel**:
   - Thêm node **Google Sheets** để **ghi lại lịch sử nghiên cứu** (từ khóa, ngày lấy, số lượng video).
   - Cấu hình sheet với các cột: `Từ khóa`, `Ngày lấy`, `Số video`, `Link video`.

3. **Tự động cập nhật định kỳ**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** (n8n Pro) để chạy workflow **hàng ngày/tuần**.
   - Ví dụ: Cập nhật video mới của creator "ẩm thực" vào mỗi thứ 2.

4. **Phân tích dữ liệu với Python (nếu cần)**:
   - Sử dụng node **Code** để **lọc video theo tiêu chí** (ví dụ: video có view > 100K).
   - Sau đó xuất ra **CSV** hoặc **Google Data Studio** để visual hóa.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công** trong nghiên cứu thị trường Kuaishou, giúp:
✔ **Tìm kiếm creator** nhanh chóng từ từ khóa.
✔ **Lấy video chi tiết** mà không cần scrape.
✔ **Tự động hóa hoàn toàn** với n8n (không cần code).

**Hành động ngay**:
1. **Import workflow** và cấu hình API Key.
2. **Test với từ khóa mẫu** (ví dụ: `"du lịch"`).
3. **Mở rộng** bằng cách kết hợp với Slack/Google Sheets.

**Cần hỗ trợ?**
- Trên n8n.io có **community hỗ trợ** [tại đây](https://community.n8n.io/).
- Các sếp có thể **customize workflow** theo nhu cầu riêng (ví dụ: lấy video theo thời gian, lọc theo tag).

---
**🚀 Chúc các sếp thành công với chiến dịch nghiên cứu thị trường của mình!** 🚀