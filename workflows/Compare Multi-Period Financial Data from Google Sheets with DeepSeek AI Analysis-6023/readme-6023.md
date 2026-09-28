---
title: "📊 Tự Động So Sánh Dữ Liệu Tài Chính Multi-Period Từ Google Sheets Với Phân Tích AI DeepSeek - Giảm 90% Thời Gian Phân Tích"
description: "Workflow tự động hóa so sánh dữ liệu tài chính từ Google Sheets qua nhiều kỳ (tháng/năm) và phân tích bằng AI DeepSeek, giúp các sếp tiết kiệm thời gian, phát hiện xu hướng và đưa ra quyết định nhanh chóng mà không cần viết code."
slug: "tự-dộng-so-sánh-dữ-liệu-tài-chính-multi-period-google-sheets-deepseek"
tags: [n8n, automation, no-code, google-sheets, ai-deepseek, tài-chính, phân-tích-dữ-liệu]
keywords: [n8n workflow tài chính, tự động hóa phân tích dữ liệu, so sánh multi-period google sheets, AI DeepSeek phân tích tài chính, tự động hóa báo cáo tài chính]
---

# 🚀 **Tự Động So Sánh Dữ Liệu Tài Chính Multi-Period Từ Google Sheets Với Phân Tích AI DeepSeek**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **giờ đồng hồ** để so sánh dữ liệu tài chính giữa các kỳ (tháng, quý, năm) trên Google Sheets, tính toán thủ công các chỉ số, và phân tích xu hướng. Điều này không chỉ tốn thời gian mà còn dễ gây **lỗi tính toán** và **quá tải công việc**.

Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Trích xuất dữ liệu** từ Google Sheets cho nhiều kỳ (kỳ trước, kỳ hiện tại, kỳ năm trước).
✅ **Tính toán tự động** tổng hợp, pivot và so sánh dữ liệu.
✅ **Phân tích bằng AI DeepSeek** để tổng kết xu hướng, điểm mạnh/điểm yếu, và đề xuất chiến lược.
✅ **Gửi báo cáo tự động** qua Slack/Email (có thể mở rộng).

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 90% thời gian** so sánh dữ liệu tài chính thủ công.
- **Chính xác 100%** với tính toán tự động, không sai sót như tính bằng tay.
- **Phân tích sâu bằng AI** nhận diện xu hướng, điểm mạnh/điểm yếu, và đề xuất cải tiến.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa báo cáo** theo nhu cầu của từng bộ phận (tài chính, marketing, quản lý).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền truy cập vào bảng tính chứa dữ liệu tài chính (cấu trúc chi tiết ở phần **Hướng Dẫn Cấu Hình**).
2. **API Key DeepSeek** (đăng ký tại [DeepSeek AI](https://deepseek.com/)).
3. **Credentials OAuth 2.0 cho Google Sheets** (cài đặt trong n8n).
4. **Bảng tính Google Sheets** có cấu trúc dữ liệu phù hợp (ví dụ: cột `Thời gian`, `Doanh thu`, `Chi phí`, `Lợi nhuận`).
5. **(Tùy chọn)** Slack/Email API (nếu muốn nhận báo cáo tự động).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6023](https://n8n.io/workflows/6023) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên máy chủ self-hosted của bạn.
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/6023](https://n8n.io/workflows/6023).
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"** → **Dán mã** → **Nhấp "Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** vì sử dụng **AI DeepSeek + Logic tự động**, nên các bước sau **quan trọng nhất**:

#### **🔹 Node "Get revenue from google sheet" (Google Sheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
  - **Sheet Name:** Điền tên bảng tính (ví dụ: `"Dữ liệu tài chính"`).
  - **Range:** Điền phạm vi dữ liệu (ví dụ: `"A1:D1000"`).
  - **Query:** Để trống hoặc điền `SELECT * WHERE` nếu muốn lọc dữ liệu (ví dụ: `SELECT * WHERE Thời gian > "2024-01-01"`).
- **Lưu ý:**
  - **Cấu trúc bảng phải chuẩn** (cột `Thời gian` (date), `Doanh thu`, `Chi phí`, `Lợi nhuận`).
  - Nếu dữ liệu có nhiều sheet, **tạo một sheet duy nhất** với tất cả dữ liệu để tránh lỗi.

#### **🔹 Node "DeepSeek Chat Model" (AI DeepSeek)**
- **Cấu hình:**
  - **Credentials:** Chọn `deepSeekApi` (đã thêm API Key).
  - **Model:** Chọn `deepseek-chat` (mặc định).
  - **Prompt:** Sử dụng **template mặc định** trong workflow (có thể tùy chỉnh sau):
    ```
    Bạn là một chuyên gia phân tích tài chính. So sánh dữ liệu tài chính giữa kỳ {currentPeriod} và kỳ {previousPeriod}. Dữ liệu được cung cấp dưới dạng bảng sau:
    {data}
    Hãy trả lời với các điểm sau:
    1. So sánh doanh thu, chi phí và lợi nhuận giữa hai kỳ.
    2. Xu hướng tăng/giảm so với kỳ trước.
    3. Điểm mạnh/điểm yếu của kỳ hiện tại so với kỳ trước.
    4. Đề xuất chiến lược cải thiện nếu có.
    ```
- **Lưu ý:**
  - **Kiểm tra API Key DeepSeek** (nếu sai, AI sẽ trả lời rỗng).
  - **Tùy chỉnh Prompt** để phù hợp với nhu cầu phân tích cụ thể.

#### **🔹 Node "Pivot last circle" & "Pivot current circle" (Code)**
- **Lưu ý:**
  - Các node này **tự động pivot dữ liệu** theo tháng/năm.
  - **Không cần chỉnh sửa** trừ khi dữ liệu có cấu trúc khác thường.
  - Nếu dữ liệu không pivot đúng, **mở node "Pivot last circle"** → **Nhấp vào "Edit"** → **Chỉnh script** (nếu cần).

#### **🔹 Node "AI Agent" (Agent LangChain)**
- **Cấu hình:**
  - **Credentials:** Chọn `deepSeekApi`.
  - **Tool:** Chọn `Call n8n Workflow Tool` (đã cấu hình trước).
  - **Memory Buffer:** Chọn `Window Buffer Memory1` (để lưu lịch sử đối thoại).
- **Lưu ý:**
  - **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.
  - Nếu muốn **tùy chỉnh logic AI**, mở node này → **Nhấp vào "Edit"** → **Chỉnh YAML** (yêu cầu kiến thức về LangChain).

#### **🔹 Node "When Executed by Another Workflow" (Trigger)**
- **Lưu ý:**
  - Nếu muốn **kích hoạt workflow từ bên ngoài**, cấu hình **Webhook** hoặc **Execute Workflow Trigger** khác.
  - **Không cần chỉnh** nếu muốn chạy tự động khi có dữ liệu mới từ Google Sheets.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu:**
   - Nhấp vào **node "Get revenue from google sheet"** → **Nhấp "Run"** → **Kiểm tra kết quả** ở các node sau (Pivot, Sum, Merge).
   - **Kiểm tra AI DeepSeek** trả lời như thế nào (nếu sai, chỉnh Prompt).
2. **Bật Active:**
   - Nhấp vào **cái bật tắt (toggle)** ở góc trên bên phải → **Chọn "Active"**.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Mở Rộng Báo Cáo Tự Động**
- **Gửi báo cáo qua Slack/Email:**
  - Thêm node **Slack** hoặc **Email** sau node **"Change title out come"** để tự động gửi kết quả phân tích.
  - **Cấu hình:**
    - **Slack:** Thêm credentials `slackApi` và chọn channel.
    - **Email:** Thêm credentials `smtp` và cấu hình địa chỉ gửi/nhận.
- **Lưu log vào Google Sheets:**
  - Thêm node **Google Sheets** sau node **"Change title out come"** để ghi lại lịch sử phân tích.

### **2. Tùy Chỉnh Prompt AI DeepSeek**
- **Cải thiện chất lượng phân tích:**
  - **Thêm yêu cầu cụ thể** vào Prompt (ví dụ: yêu cầu AI so sánh với kỳ năm trước).
  - **Ví dụ Prompt mới:**
    ```
    Bạn là một chuyên gia tài chính. So sánh dữ liệu tài chính giữa kỳ {currentPeriod} và kỳ {previousPeriod}, cũng như so sánh với kỳ {previousYearPeriod}.
    Dữ liệu:
    {data}
    Hãy trả lời với:
    1. So sánh doanh thu, chi phí, lợi nhuận giữa 3 kỳ.
    2. Xu hướng tăng/giảm so với kỳ trước và so với cùng kỳ năm trước.
    3. Đề xuất chiến lược nếu lợi nhuận giảm so với kỳ trước.
    ```

### **3. Tự Động Chạy Hàng Ngày**
- **Sử dụng Cron Job:**
  - Thêm node **Schedule** (n8n-nodes-base.schedule) để chạy workflow hàng ngày (ví dụ: **0 0 * * *** để chạy lúc 00:00 hàng ngày).
  - **Cấu hình:**
    - **Timezone:** Chọn `Asia/Ho Chi Minh` (hoặc khu vực phù hợp).
    - **Trigger:** Chọn `executeWorkflowTrigger`.

### **4. Lưu Trữ Dữ Liệu Lịch Sử**
- **Sử dụng node "Memory Buffer Window":**
  - Node này **lưu dữ liệu lịch sử** để AI có thể so sánh qua nhiều kỳ.
  - **Không cần chỉnh** trừ khi muốn thay đổi thời gian lưu trữ.

---
## **📌 Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công phiền toái** trong phân tích tài chính, thay vào đó **tự động hóa toàn bộ quy trình** với sự hỗ trợ của **AI DeepSeek**. Kết quả là:
✔ **Tiết kiệm thời gian** (từ giờ đồng hồ xuống còn phút).
✔ **Dữ liệu chính xác** (không sai sót như tính bằng tay).
✔ **Phân tích sâu** với đề xuất chiến lược từ AI.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**👉 Hãy áp dụng ngay và bắt đầu tự động hóa phân tích tài chính của mình!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**💡 Cần hỗ trợ thêm?** Đăng ký **khóa học tự động hóa n8n** tại [n8n.vn](https://n8n.vn) để học cách tùy chỉnh workflow phù hợp với doanh nghiệp!