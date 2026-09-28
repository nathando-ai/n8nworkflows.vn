---
title: "🚀 Tự Động Hóa Báo Cáo Tin Tức Hàng Ngày UPSC Từ The Hindu Với Gemini AI & Google Sheets"
description: "Workflow tự động hóa thu thập, phân tích và tổng hợp tin tức UPSC từ The Hindu hàng ngày, sử dụng trí tuệ nhân tạo Gemini để lọc nội dung quan trọng, tạo tóm tắt và lưu vào Google Sheets. Giúp các sĩ tử UPSC tiết kiệm thời gian lên đến 5-6 tiếng/tháng và giảm thiểu sai sót trong học tập."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-upsc-the-hindu-gemini-ai"
tags: [n8n, automation, no-code, ai, google-sheets, upsc, gemini-ai, content-creation]
keywords: [tự động hóa upsc, gemini ai, google sheets automation, tin tức hàng ngày upsc, the hindu automation, workflow no-code, ai agent upsc]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Hàng Ngày UPSC Từ The Hindu Với Gemini AI**

Hàng ngày, các sĩ tử UPSC phải mất **3-5 tiếng** để đọc, tóm tắt và phân loại tin tức từ các báo như *The Hindu*, *Indian Express* hoặc *Economic Times*. Nhưng với **workflow này**, các sếp sẽ được tự động hóa **tất cả quá trình** – từ thu thập tin tức đến phân tích, tóm tắt và lưu trữ vào Google Sheets, chỉ trong **vài giây mỗi ngày**!

Workflow này không chỉ tiết kiệm thời gian mà còn **tăng độ chính xác** khi sử dụng **Google Gemini AI** để lọc ra **5-6 tin tức quan trọng nhất** liên quan đến UPSC, đồng thời tự động tạo **tóm tắt ngắn gọn** và đánh giá **tầm quan trọng** của mỗi tin.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Giảm **3-5 tiếng/tháng** cho việc đọc và tóm tắt tin tức.
✅ **Tin tức chính xác**: Gemini AI lọc ra **chỉ những tin quan trọng nhất** cho UPSC.
✅ **Tóm tắt tự động**: AI tạo **tóm tắt ngắn gọn** và đánh giá **tầm quan trọng** của mỗi tin.
✅ **Lưu trữ hệ thống**: Dữ liệu được tự động ghi vào **Google Sheets** với cấu trúc rõ ràng.
✅ **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động hàng ngày.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Google Gemini API Key** (để sử dụng AI phân tích tin tức).
- **Tài khoản Google Sheets** (để lưu trữ báo cáo hàng ngày).
- **Thời gian cài đặt**: ~30 phút (chỉ cần cấu hình 1 lần).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/9872) (hoặc sử dụng link trên canvas).
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **11 node** quan trọng, trong đó **3 node cần cấu hình kỹ lưỡng**:

#### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy hàng ngày)**
- **Thời gian mặc định**: **7h sáng** (có thể điều chỉnh theo nhu cầu).
- **Lưu ý**: Đảm bảo **Google Sheets** đã được kết nối và **API Key Gemini** đã được thêm vào **Credentials**.

#### **🔹 Node 2: Google Gemini Chat Model (AI Phân Tích Tin Tức)**
- **Yêu cầu**:
  - **Credentials**: Thêm **Google Gemini API Key** vào **Credentials** của n8n.
  - **Prompt mặc định**:
    ```json
    "Analyze this news article for UPSC relevance. Extract:
    1. Brief Summary (max 100 words)
    2. What is important for UPSC (Governance, Economy, IR, etc.)
    3. Key Points to Remember"
    ```
  - **Lưu ý**: Nếu muốn **cải thiện chất lượng phân tích**, các sếp có thể **tùy chỉnh prompt** để phù hợp với chủ đề UPSC cụ thể (ví dụ: **Yojana, PRS India, PIB**).

#### **🔹 Node 3: Google Sheets (Lưu Trữ Báo Cáo)**
- **Yêu cầu**:
  - **Kết nối Google Sheets**:
    - Tạo **một bảng mới** với **5 cột** sau:
      - `Date` (Ngày)
      - `URL` (Link tin tức)
      - `Subject` (Chủ đề)
      - `Brief Summary` (Tóm tắt)
      - `What is Important` (Đánh giá tầm quan trọng)
    - **Chia sẻ bảng** với **n8n** bằng cách:
      1. Mở **Google Sheets** → **Chia sẻ** → Thêm email của **n8n** (nếu self-hosted) hoặc **Google Workspace** (nếu dùng n8n.cloud).
      2. Cấp quyền **Editor** cho **n8n**.
  - **Node "Append row in sheet"** và **"Append row in sheet in Google Sheets1"**:
    - **Chọn sheet và tab** tương ứng.
    - **Kiểm tra cấu trúc dữ liệu** để đảm bảo **các cột khớp** với bảng Google Sheets.

#### **🔹 Node 4: HTML & HTTP Request (Thu thập tin tức từ The Hindu)**
- **Không cần cấu hình** (n8n tự động lấy tin từ trang chủ *The Hindu*).
- **Lưu ý**:
  - Nếu *The Hindu* thay đổi **cấu trúc HTML**, workflow **có thể không hoạt động**.
  - **Giải pháp khắc phục**: Sử dụng **node "Code"** để **cập nhật XPath/CSS Selector** nếu cần.

---
### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **node "Manual Trigger"** → **Execute Workflow** để kiểm tra.
  - Kiểm tra **Google Sheets** xem dữ liệu có được ghi vào không.
- **Bật Active**:
  - Sau khi **test thành công**, chuyển **Schedule Trigger** sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁC TỐT NHẤT ĐỂ TĂNG CƠ HỘI**]
🔹 **Kết nối với Slack/Telegram**:
   - Thêm **node "Webhook"** để nhận **báo cáo hàng ngày** qua Slack/Telegram.
   - **Cách làm**:
     1. Tạo **webhook** trên Slack/Telegram.
     2. Thêm **node "HTTP Request"** sau **Google Sheets** để gửi tin nhắn tự động.

🔹 **Lưu log hoạt động**:
   - Thêm **node "Set"** để lưu **thời gian chạy**, **số tin tức được lọc** và **status** vào Google Sheets.

🔹 **Tùy chỉnh AI theo chủ đề**:
   - Nếu các sếp **chỉ quan tâm đến Economy/IR**, **cập nhật prompt** trong **Google Gemini Chat Model** để AI **lọc tin tức theo chủ đề cụ thể**.

🔹 **Dùng cho nhiều báo**:
   - **Sao chép workflow** và thay đổi **URL của HTTP Request** để thu thập từ *Indian Express* hoặc *Economic Times*.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho:
✔ **Sĩ tử UPSC** muốn **tiết kiệm thời gian** và **tập trung học tập**.
✔ **Trung tâm đào tạo UPSC** muốn **tự động hóa việc tạo tài liệu học tập**.
✔ **Giáo viên/giảng viên** cần **báo cáo tin tức hàng ngày** cho học viên.

**Hành động ngay!**
1. **Cài đặt n8n** trên **VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình Google Sheets + Gemini API**.
3. **Bật Schedule Trigger** và **nhận báo cáo tự động hàng ngày!**

👉 **🎁 Đăng ký VPS TinoHost (Self-hosted n8n) với mã giảm giá: VPSN8N (giảm 39%)** → [Đăng ký ngay](https://tino.vn/vps-n8n?affid=388)
👉 **💡 Nếu cần hỗ trợ cài đặt, comment bên dưới hoặc liên hệ tôi qua [LinkedIn](https://www.linkedin.com/in/pawanautomation)!**

---