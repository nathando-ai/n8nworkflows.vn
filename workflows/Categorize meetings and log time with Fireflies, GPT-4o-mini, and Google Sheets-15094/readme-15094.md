---
title: "🤖 **Tự Động Hóa Phân Loại Cuộc Hỏi & Đáp với Fireflies + GPT-4o-mini + Google Sheets (Không Cần Code!)**"
description: "Giải pháp tự động hóa phân loại cuộc họp từ Fireflies sang Google Sheets với AI GPT-4o-mini, tiết kiệm thời gian quản lý và phân tích dữ liệu hiệu quả. Hỗ trợ doanh nghiệp theo dõi tất cả cuộc họp theo danh mục (Sales, Client, Internal...) chỉ trong vài giây sau khi kết thúc."
slug: "tu-dong-hoa-phan-loai-cuoc-hop-fireflies-gpt-4o-mini-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, fireflies, google-sheets, gpt-4o-mini, workflow-ai]
keywords: [n8n workflow tự động hóa cuộc họp, phân loại cuộc họp với AI, Fireflies + GPT-4o-mini, tự động hóa quản lý cuộc họp, Google Sheets tự động hóa, AI categorization]
---

# 🚀 **Tự Động Hóa Phân Loại Cuộc Hỏi & Đáp với Fireflies + GPT-4o-mini + Google Sheets**

## **🔥 Nỗi Đau Của Các Sếp Khi Quản Lý Cuộc Hỏi Thường Xuyên**
Hàng ngày, các sếp và nhân viên phải mất **thời gian quý báu** để:
- **Lắng nghe và ghi chú** từng cuộc họp dài hàng giờ.
- **Phân loại thủ công** cuộc họp vào danh mục (Sales, Client, Internal, HR, Product, Finance, Other...) để phân tích sau.
- **Tìm kiếm và tổng hợp** dữ liệu từ nhiều cuộc họp để báo cáo cho lãnh đạo.
- **Đối mặt với rủi ro** quên ghi chú hoặc ghi nhầm thông tin quan trọng.

**Kết quả?** Thời gian bị "chôn vùi" trong công việc thủ công, dữ liệu phân tán, khó theo dõi tiến độ và hiệu quả của các cuộc họp.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% Không Cần Code!**
Với **n8n**, bạn có thể **tự động hóa toàn bộ quy trình** từ khi cuộc họp kết thúc đến khi dữ liệu được phân loại và lưu trữ sẵn trên **Google Sheets**. Cụ thể:
✅ **Fireflies** tự động ghi âm và chuyển ngữ văn bản cuộc họp.
✅ **GPT-4o-mini** phân loại cuộc họp vào danh mục chính xác (Sales, Client, Internal, HR, Product, Finance, Other) **với độ tin cậy cao**.
✅ **Google Sheets** tự động lưu trữ tất cả thông tin (danh mục, thời gian, người tham gia, lý do phân loại) **một cách hệ thống**.
✅ **Báo cáo tự động** sau vài tuần, bạn có thể **lọc theo danh mục** để xem tất cả cuộc họp Sales, Internal, hoặc Product chỉ trong vài giây.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, không lag)
:::

---

## **🎯 Kết Quả Các Sếp Nhận Được**
### **💰 Tiết Kiệm Thời Gian**
- **Không cần ghi chú thủ công** sau mỗi cuộc họp.
- **Phân loại tự động** trong vài giây thay vì mất **10-30 phút** mỗi cuộc họp.

### **📊 Dữ Liệu Chính Xác & Hệ Thống Hóa**
- **Không sai sót** do phân loại thủ công.
- **Tất cả cuộc họp** được lưu trữ trên **Google Sheets** với **thông tin đầy đủ** (danh mục, thời gian, người tham gia, lý do phân loại).

### **📈 Tối Ưu Quá Trình Quyết Định**
- **Lọc nhanh** theo danh mục (Sales, Client, Internal...) để **phân tích hiệu quả**.
- **Báo cáo tự động** sau mỗi tuần/month để **đánh giá tiến độ** của đội nhóm.

### **🔒 An Toàn & Linh Hoạt**
- **Không cần code** – chỉ cần **cấu hình** và chạy.
- **Hoạt động liên tục** 24/7 trên VPS riêng.

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Fireflies** (để lấy **API Key** và **Webhook URL**).
✔ **Tài khoản OpenAI** (để sử dụng **GPT-4o-mini**, cần **API Key**).
✔ **Tài khoản Google** (để kết nối **Google Sheets** và tạo **OAuth2 credential**).
✔ **Google Sheet** mới với **tab "Meeting Categories"** và các cột sau:
   - **Date** (Ngày cuộc họp)
   - **Meeting Title** (Tiêu đề cuộc họp)
   - **Category** (Danh mục: Sales, Client, Internal, HR, Product, Finance, Other)
   - **Confidence** (Độ tin cậy: High/Medium/Low)
   - **Reason** (Lý do phân loại)
   - **Duration (min)** (Thời gian cuộc họp)
   - **Participants** (Người tham gia)
   - **Keywords** (Từ khóa quan trọng)
   - **Fireflies URL** (Link ghi âm)
   - **Logged At** (Thời gian ghi lại)

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15094](https://n8n.io/workflows/15094).
2. **Nhấn nút "Import"** trên n8n Editor.
3. **Chọn file JSON** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/15094](https://n8n.io/workflows/15094).
2. Trên **n8n Editor**, nhấn **"Import"** → **"Paste JSON"** và dán vào.
3. Nhấn **"Import"** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node 1: Webhook — Fireflies Transcript Done**
- **Không cần chỉnh sửa**, chỉ cần **bật Active** sau khi import.
- **URL Webhook** sẽ được sử dụng trong **Fireflies** (hướng dẫn ở phần sau).

#### **🔹 Node 2: Set — Config Values**
- **Thay thế các giá trị sau**:
  ```json
  {
    "YOUR_FIREFLIES_API_KEY": "api_key_của_bạn_trong_Fireflies",
    "YOUR_GOOGLE_SHEET_ID": "id_sheet_google_của_bạn",
    "sheetTabName": "Meeting Categories"
  }
  ```
- **Lấy `YOUR_FIREFLIES_API_KEY`**:
  1. Mở **Fireflies** → **Settings** → **Developer Settings**.
  2. Copy **API Key** và dán vào.
- **Lấy `YOUR_GOOGLE_SHEET_ID`**:
  1. Mở **Google Sheets** → **Chia sẻ** → **Liên kết chia sẻ**.
  2. Trong URL, phần `d/...` là **Sheet ID** (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).

#### **🔹 Node 3: HTTP — Fetch Transcript**
- **Không cần chỉnh sửa**, workflow sẽ tự động lấy dữ liệu từ Fireflies.

#### **🔹 Node 4: Code — Extract Meeting Data**
- **Không cần chỉnh sửa**, node này **tự động xử lý** dữ liệu từ Fireflies.

#### **🔹 Node 5: AI Agent — Categorize Meeting**
- **Không cần chỉnh sửa**, nhưng **đảm bảo**:
  - **GPT-4o-mini** đã được **kết nối** với **OpenAI credential** (hướng dẫn ở phần sau).
  - **Temperature** đã được đặt là **0.1** (để phân loại chính xác).

#### **🔹 Node 6: OpenAI — GPT-4o-mini Model**
- **Kết nối OpenAI credential**:
  1. Trên **n8n Editor**, nhấn **"Add"** → **"OpenAI"** → **"Add"** (nếu chưa có).
  2. Nhập **API Key** từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys).
  3. Chọn **model: gpt-4o-mini**.

#### **🔹 Node 7: Parser — Structured Category Output**
- **Không cần chỉnh sửa**, node này **bắt buộc** để đảm bảo **dữ liệu phân loại có cấu trúc**.

#### **🔹 Node 8: Code — Prepare Sheet Row**
- **Không cần chỉnh sửa**, node này **tự động thêm emoji** cho độ tin cậy (🟢 High, 🟡 Medium, 🔴 Low).

#### **🔹 Node 9: Google Sheets — Log Meeting Category**
- **Kết nối Google Sheets OAuth2 credential**:
  1. Trên **n8n Editor**, nhấn **"Add"** → **"Google Sheets"** → **"Add"** (nếu chưa có).
  2. Nhấn **"Connect"** và **đăng nhập Google**.
  3. Chọn **Google Sheet** và **tab "Meeting Categories"**.
  4. **Chọn operation: Append** (để thêm dữ liệu mới).

---

### **3. Kích Hoạt ⚡️**
#### **Bước 1: Bật Workflow**
1. Trên **n8n Editor**, nhấn **"Active"** để **bật workflow**.
2. **Không cần Test Run**, vì workflow sẽ **tự động chạy** khi Fireflies gửi dữ liệu.

#### **Bước 2: Cấu Hình Fireflies**
1. Mở **Fireflies** → **Settings** → **Developer Settings** → **Webhooks**.
2. Nhấn **"Add Webhook"**.
3. **Dán URL Webhook** từ **Node 1** (trong n8n Editor).
4. **Chọn event: "Transcript Done"**.
5. Nhấn **"Save"**.

#### **Bước 3: Test với Cuộc Hỏi Mẫu**
1. **Ghi âm một cuộc họp mẫu** trên Fireflies.
2. Sau khi **transcript hoàn tất**, dữ liệu sẽ tự động:
   - **Lấy từ Fireflies** → **Phân loại bằng GPT-4o-mini** → **Lưu vào Google Sheets**.
3. **Kiểm tra Google Sheets** để xem dữ liệu đã được lưu chưa.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Kết Nối với Slack/Telegram để Báo Lệch**
- **Thêm Node Slack/Telegram** sau **Node 9** để **báo cáo tự động** khi có cuộc họp mới được phân loại.
- **Ví dụ**:
  ```json
  {
    "name": "10. Slack — Notify New Meeting",
    "type": "slack",
    "keyParameters": {
      "message": "📝 Cuộc họp mới được phân loại: {{ $node["9"].json["Category"] }} - {{ $node["9"].json["Meeting Title"] }}"
    }
  }
  ```

### **🔹 Lưu Log Lịch Sử Phân Loại**
- **Thêm Node Google Sheets mới** để **lưu log chi tiết** (thời gian phân loại, người phân loại, AI confidence).
- **Cột mới trong Sheet**:
  - **Logged By**: AI
  - **Confidence Score**: Số liệu chính xác (0-1)

### **🔹 Tự Động Gửi Báo Cáo Tuần/Tháng**
- **Sử dụng Node Schedule** (n8n Pro) để **gửi báo cáo tự động** vào cuối tuần.
- **Ví dụ**:
  ```json
  {
    "name": "11. Schedule — Weekly Report",
    "type": "schedule",
    "keyParameters": {
      "cron": "0 0 * * 0" // Chạy vào thứ Bảy 00:00
    }
  }
  ```
  Sau đó, **kết nối với Node Google Sheets** để **tính tổng cuộc họp theo danh mục**.

### **🔹 Cập Nhật Danh Mục Phân Loại**
- **Thay đổi danh sách danh mục** trong **Node 5 (AI Agent)** nếu cần.
- **Ví dụ**: Thêm **"Marketing"** hoặc **"Legal"** vào danh sách phân loại.

---

## **📌 Kết Luận: Tự Động Hóa Cuộc Hỏi & Đáp Bắt Đầu Từ Hôm Nay!**
Với **workflow này**, các sếp đã **giải phóng thời gian** để tập trung vào **các nhiệm vụ chiến lược** hơn, trong khi **dữ liệu cuộc họp** được **quản lý tự động, chính xác và hệ thống hóa**.

### **🚀 Hành Động Ngay Hôm Nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Fireflies, OpenAI và Google Sheets**.
3. **Bật workflow** và **test với cuộc họp mẫu**.
4. **Theo dõi kết quả** trên Google Sheets sau mỗi cuộc họp!

**💡 Lời Khuyên Cuối Cùng**:
- **Self-host n8n** trên VPS để **không phụ thuộc vào n8n.cloud**.
- **Kết hợp với Slack/Telegram** để **báo cáo tức thời**.
- **Tối ưu hóa danh mục phân loại** theo **cần thiết của doanh nghiệp**.

---
**🔥 Chúc các sếp thành công với quy trình tự động hóa mới!** 🚀