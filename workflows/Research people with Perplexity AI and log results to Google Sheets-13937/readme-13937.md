---
title: "🔍 **Tự Động Hoá Nghiên Cứu Người Dùng Với Perplexity AI & Ghi Kết Quả Vào Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa nghiên cứu thông tin cá nhân (tên, công ty, vị trí, ngành nghề...) bằng AI Perplexity và ghi kết quả vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng so sánh thủ công, cập nhật thông tin chính xác và cá nhân hóa."
slug: "tieu-dong-hoa-nghien-cuu-nguoi-dung-perplexity-google-sheets"
tags: [n8n, automation, ai-research, google-sheets, perplexity-ai, no-code-workflow]
keywords: [n8n workflow nghiên cứu người dùng, tự động hóa AI Perplexity, ghi kết quả vào Google Sheets, tự động hóa market research, công cụ nghiên cứu nhân sự]
---

# **🚀 Tự Động Hoá Nghiên Cứu Người Dùng Với Perplexity AI & Google Sheets**

### **💡 Giải Phóng Tay Các Sếp Từ Công Việc Nghiên Cứu Thông Tin Cá Nhân**
Hãy tưởng tượng: Bạn chỉ cần nhập tên một nhân viên cũ hoặc đối thủ cạnh tranh vào Google Sheets, workflow sẽ tự động:
✅ **Tìm kiếm thông tin** về họ trên internet (công ty, vị trí, ngành nghề, mạng xã hội) bằng **Perplexity AI** (mô hình AI mạnh mẽ hơn Google Search).
✅ **Ghi kết quả** vào các cột tương ứng trong bảng (không cần chỉnh sửa thủ công).
✅ **Báo lỗi** nếu AI không tìm thấy thông tin (với cảnh báo Slack tự động).
✅ **Cập nhật trạng thái** từ *Pending* → *Processing* → *Done* (hoặc *Error* nếu có vấn đề).

**Kết quả?** Các sếp **tiết kiệm 10+ giờ/tháng**, tránh sai sót thủ công và có dữ liệu **cập nhật liên tục** mà không cần can thiệp.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Thay vì tra cứu thủ công trên Google, AI làm việc 24/7.
- **Dữ liệu chính xác**: Perplexity AI tổng hợp thông tin từ nhiều nguồn (báo chí, LinkedIn, blog...).
- **Cảnh báo tự động**: Nếu AI không tìm thấy thông tin, Slack sẽ báo ngay (và ghi lỗi vào Google Sheets).
- **Cá nhân hóa**: Thay đổi câu hỏi nghiên cứu chỉ cần chỉnh **Config Tab** (không cần sửa workflow).
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google Sheets** (với quyền chỉnh sửa):
   - **Google OAuth 2.0 API Key** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Google Sheet** có cấu trúc chuẩn (xem chi tiết dưới đây).
2. **API Key Perplexity**:
   - Đăng ký tại [Perplexity API](https://www.perplexity.ai/api) và lấy **Bearer Token**.
3. **Slack API** (tùy chọn, để nhận cảnh báo lỗi):
   - **Slack App Token** (tạo tại [Slack API](https://api.slack.com/)).
   - **Channel ID** của nhóm Slack muốn nhận thông báo.
:::

---
## **📄 Cấu Trúc Google Sheets (Bắt Buộc)**
Workflow yêu cầu **2 tab** trong Google Sheets:
### **1. Tab "Main Data" (Dữ liệu chính)**
| **Cột**            | **Mô tả**                          | **Ví dụ**                     |
|---------------------|-------------------------------------|-------------------------------|
| **Name**            | Tên người cần nghiên cứu           | "Nguyễn Văn A"                |
| **Status**          | Trạng thái (Pending/Processing/Error) | "Pending"                     |
| **Current Company** | Công ty hiện tại                   | "TechCorp"                    |
| **Location**        | Địa chỉ/Địa phương                | "Hà Nội, Việt Nam"            |
| **Current Title**   | Chức vụ hiện tại                  | "CTO"                         |
| **Industry**        | Ngành nghề                          | "Tech, AI"                    |
| **Socials / Others**| Mạng xã hội/Thông tin khác        | "LinkedIn: linkedin.com/in/a"  |
| **Error Log**       | Ghi lỗi nếu AI không tìm thấy      | "Not found"                   |

### **2. Tab "Config" (Cấu hình câu hỏi)**
| **Cột**            | **Mô tả**                          | **Ví dụ**                     |
|---------------------|-------------------------------------|-------------------------------|
| **Field Key**       | Khóa cột trong Tab Main Data        | "CurrentCompany"              |
| **Question Template** | Câu hỏi gửi cho Perplexity AI      | "What is the current company of [NAME]?" |
| **Column**          | Tên cột trong Tab Main Data         | "Current Company"             |

**Lưu ý**:
- Sử dụng **`[NAME]`** làm placeholder (workflow sẽ thay thế bằng tên người thực tế).
- Mỗi dòng trong **Config Tab** tương ứng với một cột trong **Main Data**.

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13937](https://n8n.io/workflows/13937) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Không cần chỉnh sửa** cấu trúc node (nếu không muốn).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13937](https://n8n.io/workflows/13937).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.

---
### **2. Các Bước Cấu Hình Bắt Buộc 📌**
Sau khi import, các sếp **phải chỉnh** các node sau:

#### **🔹 Node "Get All Rows" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet ID**: Điền **ID của Google Sheet** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
- **Sheet Name**: Điền tên tab **Main Data** (ví dụ: `"Main Data"`).

#### **🔹 Node "Get Config Tab" (Google Sheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Sheet ID**: Cùng với node trên.
- **Sheet Name**: Điền tên tab **Config** (ví dụ: `"Config"`).

#### **🔹 Node "Perplexity — Research Call" (HTTP Request)**
- **URL**: `https://api.perplexity.ai/chat/completions`
- **Headers**:
  - `Authorization`: `Bearer YOUR_PERPLEXITY_API_KEY` (thay `YOUR_PERPLEXITY_API_KEY` bằng API Key thực tế).
  - `Content-Type`: `application/json`
- **Body (JSON)**:
  ```json
  {
    "model": "perplexity/perplexity-latest",
    "messages": [
      {"role": "system", "content": "You are a professional researcher. Answer concisely."},
      {"role": "user", "content": "{{ $node["Build Dynamic Prompt"].json["prompt"] }}"}
    ]
  }
  ```
  *(Node `Build Dynamic Prompt` sẽ tự động xây dựng câu hỏi từ Config Tab.)*

#### **🔹 Node "Slack — Missing Fields Alert" & "Slack — API Error Alert"**
- **Credentials**: Chọn `slack` (đã cấu hình trước).
- **Channel ID**: Điền **#channel-id** của Slack (tìm trong URL: `https://slack.com/archives/C123456789`).
- **Message Template**:
  ```json
  {
    "text": "⚠️ **Missing Fields Alert**\nName: {{ $node["Filter — Pending Only"].json["Name"] }}\nMissing: {{ $node["Parse Perplexity Response"].json["missingFields"] }}"
  }
  ```

#### **🔹 Node "Write Results to Sheet" & "Write Error to Sheet"**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Sheet ID**: Cùng với node `Get All Rows`.
- **Sheet Name**: `"Main Data"`.
- **Range**: `{{ $node["Loop Over Rows"].json["rowNumber"] }}:{{ $node["Loop Over Rows"].json["rowNumber"] }}` (để ghi vào dòng chính xác).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền tên vào cột **Name** trong Google Sheets.
   - Đặt **Status** thành **"Pending"**.
   - Chạy workflow (nhấn **Execute Workflow**).
   - Kiểm tra kết quả trong **Main Data Tab** và **Slack** (nếu có lỗi).
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** → **Active**.
   - **Lưu ý**: Workflow sẽ chạy tự động khi có dữ liệu mới trong **Status = Pending**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Câu Hỏi cho Perplexity**
- **Viết câu hỏi rõ ràng**: Ví dụ:
  - ❌ *"What is this person doing?"*
  - ✅ *"What is the current job title, company, and industry of [NAME]?"*
- **Sử dụng placeholder `[NAME]`** để tự động thay thế.

### **2. Gửi Báo Cáo Định Kỳ**
- **Kết hợp với Node `Set Interval`** (n8n Pro) để tự động chạy workflow hàng ngày/tuần.
- **Gửi báo cáo Slack/Email** với kết quả mới nhất.

### **3. Lưu Log Lịch Sử**
- Thêm **Node `Set`** để lưu thời gian cập nhật vào cột mới (ví dụ: `Last Updated`).
- **Node `Date/Time`** để lấy thời gian hiện tại.

### **4. Kết Nối Với CRM (CRM Integration)**
- **Node `HTTP Request`** để gửi kết quả vào **HubSpot**, **Salesforce**, hoặc **Notion**.
- Ví dụ:
  ```json
  {
    "url": "https://api.hubapi.com/crm/v3/objects/contacts",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer YOUR_HUBSPOT_API_KEY"
    },
    "body": {
      "properties": {
        "name": "{{ $json["Name"] }}",
        "company": "{{ $json["Current Company"] }}"
      }
    }
  }
  ```

---
## **📌 Kết Luận: Tự Động Hoá Nghiên Cứu Người Dùng Bây Giờ!**
Workflow này **giải phóng các sếp** khỏi công việc tra cứu thủ công, đồng thời **cập nhật thông tin chính xác** về nhân viên, đối thủ cạnh tranh hoặc khách hàng. Với **Perplexity AI**, dữ liệu được tổng hợp từ nhiều nguồn, và **Google Sheets** giúp theo dõi dễ dàng.

**Bước đầu tiên**: Cài đặt n8n trên **VPS riêng** để workflow chạy 24/7 mà không bị gián đoạn.

:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định, các sếp nên cài n8n trên **VPS Self-hosted**:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Hành động ngay**: Import workflow, cấu hình Google Sheets và **bắt đầu tự động hóa nghiên cứu người dùng** trong vòng 10 phút! 🚀

---
**🔗 [Tải Workflow Nguyên Bản](https://n8n.io/workflows/13937)** | **📌 [Câu Hỏi? Hỏi Tôi](https://t.me/your_n8n_support_channel)**