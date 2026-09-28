---
title: "🚀 Tự Động Hóa Tìm Kiếm, Đánh Giá & Giao Tiếp Lead LinkedIn Với AI-Agent - Giải Pháp Sales 24/7"
description: "Workflow này tự động hóa toàn bộ quy trình từ tìm kiếm lead phù hợp (ICP) trên LinkedIn đến gửi tin nhắn tự động, đánh giá lead bằng AI, và quản lý kết nối - tiết kiệm thời gian cho các sếp lên tới 20 giờ/tuần."
slug: "tieu-dong-hoa-linkedin-lead-generation-scoring-communication"
tags: [n8n, automation, sales, ai, marketing, linkedin, google-sheets, openai, no-code]
keywords: [tự động hóa linkedin, tìm kiếm lead linkedin, ai agent n8n, đánh giá lead, tự động gửi tin nhắn linkedin, workflow n8n sales]
---

# 🚀 **Tự Động Hóa Tìm Kiếm, Đánh Giá & Giao Tiếp Lead LinkedIn Với AI-Agent**

## **🔍 Giới Thiệu: Giải Pháp "Tự Động Hóa 100%" Cho Quy Trình Sales LinkedIn**
Hiện nay, các sếp và đội ngũ sales phải mất **gần 20 giờ/tuần** để:
✅ Tìm kiếm lead phù hợp trên LinkedIn theo ICP (Ideal Customer Profile)
✅ Nghiên cứu thông tin chi tiết về công ty và cá nhân (website, bài viết, tin tức)
✅ Đánh giá độ phù hợp của lead (lead scoring)
✅ Gửi tin nhắn tự động và theo dõi kết nối

**Workflow này tự động hóa toàn bộ quy trình trên bằng AI + n8n, giúp các sếp:**
- **Tiết kiệm 80% thời gian** so với làm thủ công
- **Tăng chất lượng lead** với phân tích sâu bằng AI (OpenAI)
- **Tự động gửi tin nhắn** sau khi kết nối thành công
- **Hoạt động 24/7** mà không cần can thiệp

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tìm kiếm lead tự động** theo ICP với AI-Agent chuyển mô tả ICP thành bộ lọc LinkedIn.
- **Nghiên cứu lead chi tiết** (website, bài viết, tin tức công ty) bằng AI.
- **Đánh giá lead** (lead scoring) dựa trên độ phù hợp với sản phẩm/dịch vụ.
- **Gửi tin nhắn tự động** sau khi kết nối thành công (không cần manual).
- **Quản lý kết nối** (theo dõi phản hồi và gửi tin nhắn theo lịch).
- **Lưu trữ dữ liệu** trên Google Sheets với định dạng chuyên nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn** (để kết nối và gửi tin nhắn).
2. **API Key của Horizon Datawave** ([hdwLinkedin](https://horizondatawave.ai/)) để tìm kiếm và quản lý lead.
3. **Tài khoản Google Sheets** (để lưu trữ lead và dữ liệu phân tích).
4. **API Key OpenAI** (để sử dụng AI trong việc đánh giá lead và tổng hợp thông tin).
5. **Mô tả ICP (Ideal Customer Profile)** của doanh nghiệp (cần nhập vào AI-Agent để tạo bộ lọc).

---
:::note[LƯU Ý]
- **Không cần code** – workflow đã sẵn sàng, chỉ cần cấu hình API và nhập dữ liệu.
- **Không giới hạn số lead** (nhưng tuân thủ chính sách LinkedIn về số kết nối/tuần).
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/3490](https://n8n.io/workflows/3490).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Import All** để thêm workflow vào dự án.

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Import from JSON** → Dán JSON từ file.
3. Nhấn **Import** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình API & Credentials**
Workflow sử dụng **5 loại credentials chính**:
| **Credentials**       | **Địa chỉ cấu hình** | **Lưu ý** |
|----------------------|----------------------|-----------|
| `openAiApi`          | `Settings > Credentials > Add OpenAI` | Nhập API Key từ OpenAI. |
| `googleSheetsOAuth2Api` | `Settings > Credentials > Add Google Sheets` | Cấu hình OAuth 2.0 từ Google Cloud. |
| `hdwLinkedinApi`     | `Settings > Credentials > Add HDW LinkedIn` | Nhập API Key từ [Horizon Datawave](https://horizondatawave.ai/). |

#### **🔹 Cấu hình AI-Agent (ICP → Bộ lọc LinkedIn)**
1. Tìm node **"AI Agent: ICP -> LinkedIn search filters"**.
2. **Nhập mô tả ICP** của doanh nghiệp (ví dụ: *"Công ty SaaS tại Việt Nam, doanh thu > 500 triệu/tháng, sử dụng AWS"*).
3. **Cấu hình prompt** để AI tạo bộ lọc chính xác (ví dụ: tìm kiếm từ khóa như "AI", "cloud", "tăng trưởng").

#### **🔹 Cấu hình Google Sheets**
1. Tạo **1 bảng Google Sheets** mới với các sheet sau (workflow sẽ tự tạo):
   - `Leads` (lưu lead tìm được)
   - `Company Data` (thông tin công ty)
   - `Lead Scoring` (điểm đánh giá lead)
   - `Messages` (lịch sử tin nhắn)
2. **Chia sẻ bảng với n8n** bằng cách:
   - Nhấn **Share** → Chọn **Anyone with the link** → Nhập email `n8n@example.com`.
   - Copy **link share** và dán vào **Google Sheets Credentials** trong n8n.

#### **🔹 Cấu hình LinkedIn & Tin nhắn tự động**
1. Tìm node **"HDW LinkedIn Send Message"**.
2. **Chỉnh sửa tin nhắn mẫu** (ví dụ:
   > *"Xin chào [Tên], tôi là [Tên của bạn] từ [Tên công ty]. Tôi thấy công ty của bạn đang phát triển mạnh trong lĩnh vực [lĩnh vực]. Có thể trao đổi về [sản phẩm/dịch vụ] không?"*).
3. **Cấu hình lịch gửi tin nhắn** trong node **"Schedule Trigger"** (ví dụ: gửi sau 3 ngày kết nối).

#### **🔹 Cấu hình Lead Scoring**
1. Tìm node **"Company Score Analysis"** (OpenAI).
2. **Chỉnh sửa prompt** để AI đánh giá lead dựa trên:
   - Độ phù hợp với ICP.
   - Tần suất bài viết liên quan đến sản phẩm.
   - Tin tức công ty (tăng trưởng, hợp tác mới...).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấn **Run Workflow** và chọn **When clicking ‘Test workflow’** (Manual Trigger).
   - Nhập **ICP mô tả** vào node AI-Agent.
   - Kiểm tra kết quả trên Google Sheets.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Cài đặt lịch chạy** (ví dụ: chạy hàng ngày lọc lead mới).

---
## **✍️ Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa tìm kiếm lead**
- **Thêm bộ lọc nâng cao** trong AI-Agent:
  - Ví dụ: *"Tìm kiếm lead có vị trí là 'CTO' hoặc 'Giám đốc Marketing' tại Việt Nam và Singapore"*.
- **Sử dụng bộ lọc LinkedIn nâng cao** (ví dụ: giới hạn theo ngành nghề, kích thước công ty).

### **2. Tự động gửi tin nhắn theo lịch**
- **Cấu hình 2 Schedule Trigger**:
  - **Schedule Trigger1**: Gửi yêu cầu kết nối (ví dụ: hàng tuần).
  - **Schedule Trigger2**: Kiểm tra phản hồi và gửi tin nhắn (ví dụ: sau 3 ngày).

### **3. Lưu log hoạt động**
- **Thêm node Google Sheets** để lưu lịch sử:
  ```json
  {
    "name": "Log Activity",
    "type": "googleSheets",
    "credentials": ["googleSheetsOAuth2Api"],
    "keyParameters": {
      "operation": "appendOrUpdate",
      "sheetName": "ActivityLog",
      "range": "A1"
    }
  }
  ```
- **Lưu trữ tin nhắn** vào sheet `Messages` với cột:
  - `Date`, `Lead Name`, `Message`, `Status` (đã gửi/đã trả lời).

### **4. Kết hợp với Slack/Telegram**
- **Thêm node Webhook** để gửi thông báo:
  ```json
  {
    "name": "Slack Notification",
    "type": "webhook",
    "credentials": ["slackWebhook"],
    "keyParameters": {
      "url": "https://hooks.slack.com/services/...",
      "body": {
        "text": "🚀 Lead mới được tìm thấy: {{ $node["HDW LinkedIn SN"].json["name"] }}"
      }
    }
  }
  ```

### **5. Cập nhật ICP định kỳ**
- **Sử dụng node Schedule Trigger** để chạy AI-Agent hàng tháng để cập nhật bộ lọc ICP.

---
## **📌 Kết luận: Bắt đầu tự động hóa ngay!**

Workflow này là **giải pháp hoàn chỉnh** cho các sếp muốn:
✔ **Tìm kiếm lead tự động** theo ICP.
✔ **Nghiên cứu lead chi tiết** bằng AI.
✔ **Đánh giá lead** và ưu tiên giao tiếp.
✔ **Gửi tin nhắn tự động** sau khi kết nối.

**Hành động ngay:**
1. **Import workflow** và cấu hình API.
2. **Nhập mô tả ICP** vào AI-Agent.
3. **Bật Active** và theo dõi kết quả trên Google Sheets.

**🚀 Kết quả:** Tiết kiệm **20 giờ/tuần**, tăng **chất lượng lead**, và **tự động hóa toàn bộ quy trình sales**!

---
**💬 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định 24/7!