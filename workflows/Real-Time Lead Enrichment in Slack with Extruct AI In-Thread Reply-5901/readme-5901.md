---
title: "🚀 Tự Động Hoàn Chỉnh Lead Tốc Độ Thực Tế Trên Slack Với Extruct AI (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp phát hiện và enrich thông tin công ty từ tin nhắn Slack chỉ trong vài giây, tiết kiệm thời gian nghiên cứu lên tới 80%. Kết quả: nhận được profile công ty chi tiết (website, LinkedIn, số nhân viên, ngành nghề, tin tức mới nhất) ngay trong thread Slack."
slug: "tự-dộng-hoàn-chỉnh-lead-trên-slack-voi-extruct-ai"
tags: [n8n, automation, lead-generation, ai-summarization, slack-integration, no-code]
keywords: [tự động hóa lead generation, enrich lead trên slack, extruct ai n8n, tự động hóa nghiên cứu thị trường, tự động hóa bán hàng, tự động hóa CRM]
---

# 🚀 **Tự Động Hoàn Chỉnh Lead Tốc Độ Thực Tế Trên Slack Với Extruct AI**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải mất **30 phút đến 1 giờ** để tìm hiểu thông tin chi tiết về một công ty từ email lead? Hay phải **copy-paste** tên miền vào Google, LinkedIn, Crunchbase rồi chờ đợi kết quả không chính xác? Với **Real-Time Lead Enrichment**, các sếp sẽ:
- **Tiết kiệm thời gian** lên tới **80%** khi không cần nghiên cứu thủ công.
- **Nhận thông tin chính xác** từ nguồn dữ liệu live (không phải database tĩnh).
- **Tương tác ngay trong Slack** với profile công ty đầy đủ (website, LinkedIn, số nhân viên, ngành nghề, tin tức mới nhất, và liên lạc).
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm thời gian**: Từ 30 phút/thông tin lead xuống còn **vài giây**.
✅ **Dữ liệu chính xác**: Thay vì copy-paste, Extruct AI **scrape và enrich** thông tin từ nguồn live (website, LinkedIn, tin tức mới nhất).
✅ **Tương tác trong Slack**: Nhận **thẻ công ty structured** ngay trong thread, không cần chuyển sang tab khác.
✅ **Hoạt động tự động**: Bot hoạt động **24/7**, không cần can thiệp của con người.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản Extruct AI**
- **Đăng ký miễn phí** tại [Extruct AI](https://www.extruct.ai/) (có **1.000 credit trial**).
- **Tạo một bảng (Table)** từ template:
  - Mở [bảng mẫu](https://app.extruct.ai/tables/shared/wZ6FxspNc5ctrB55).
  - **Copy Table ID** từ URL (ví dụ: `wZ6FxspNc5ctrB55`).
  - **Dùng Table ID này** trong node **"Set Extruct Table ID"** của n8n.

### **2. Tài Khoản Slack & App Bot**
- **Tạo một app Slack mới**:
  - Đăng nhập [Slack API](https://api.slack.com/apps) → **Create New App** → **From scratch**.
  - **Tên app**: Ví dụ `n8n Lead Enricher`.
  - **OAuth & Permissions**:
    - **Bot Token Scopes** thêm:
      - `channels:read`
      - `channels:history`
      - `chat:write`
  - **Lưu Bot User OAuth Token** (`xoxb-...`) để dùng sau.
  - **Enable Events**:
    - Trong **Event Subscriptions**, bật **Enable Events**.
    - **Request URL**: Dán **URL Webhook Production** từ node **"New Message Catcher"** của n8n.
    - **Subscribe to Bot Events**: Chọn `message.channels`.
    - **Reinstall to Workspace** để cập nhật scope mới.

### **3. API Key Extruct (Bearer Token)**
- Sau khi đăng ký Extruct, **copy API Key** từ **Settings → API Keys**.
- Sử dụng API Key này trong **tất cả node HTTP Request** của n8n (chọn **Generic Credential (Bearer Auth)**).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5901](https://n8n.io/workflows/5901) (hoặc copy JSON từ trang này).
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON.
- **Hoặc** tải file JSON từ [đây](https://github.com/n8n-io/workflows/raw/main/workflows/5901.json) (nếu link trên không hoạt động).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Slack**
- **Tất cả node Slack** (trừ **"New Message Catcher"**) cần:
  - **Credentials**: Chọn **Slack OAuth2 API** → Điền **Bot User OAuth Token** (`xoxb-...`).
  - **Channel**: Chọn **channel Slack** muốn theo dõi (ví dụ: `#leads`).
- **Node "New Message Catcher"**:
  - **Credentials**: Chọn **Slack OAuth2 API** → Điền **Bot User OAuth Token**.
  - **Event**: Chọn `message.channels`.

#### **B. Cấu Hình Extruct API**
- **Tất cả node HTTP Request** (trừ **"New Message Catcher"**) cần:
  - **Credentials**: Chọn **Generic Credential (Bearer Auth)** → Điền **Extruct API Key**.
  - **URL Base**: `https://api.extruct.ai/v1`.
- **Node "Set Extruct Table ID"**:
  - **Value**: Điền **Table ID** từ Extruct (ví dụ: `wZ6FxspNc5ctrB55`).

#### **C. Node "Extract Company Name Input" (Code)**
- **Mã mặc định** đã xử lý việc **trích xuất tên miền từ tin nhắn Slack**.
- **Không cần chỉnh sửa** trừ khi cần **lọc thêm điều kiện** (ví dụ: chỉ lấy domain có `.com`).
  ```javascript
  // Mã mặc định (không cần thay đổi)
  return {
    json: {
      domain: $input.all().message.text.match(/https?:\/\/(?:www\.)?([^\s/]+)/i)?.[1] ||
              $input.all().message.text.match(/@([^\s]+)/i)?.[1] ||
              $input.all().message.text.match(/([^\s]+(?:\.com|\.net|\.org))/i)?.[0]
    }
  };
  ```

#### **D. Node "Format Slack Company Card" (Code)**
- **Mã mặc định** tạo **thẻ Slack structured** từ dữ liệu enrich.
- **Không cần chỉnh sửa** trừ khi muốn **thay đổi layout** (ví dụ: thêm/loại bỏ trường dữ liệu).
  ```javascript
  // Mã mặc định (không cần thay đổi)
  const companyData = $input.all();
  return {
    json: {
      blocks: [
        {
          type: "section",
          text: {
            type: "mrkdwn",
            text: `*${companyData[0].$.company.name}*`
          }
        },
        {
          type: "section",
          fields: [
            {
              type: "mrkdwn",
              text: `Website: ${companyData[0].$.company.website || "N/A"}`
            },
            {
              type: "mrkdwn",
              text: `LinkedIn: ${companyData[0].$.company.linkedin || "N/A"}`
            }
          ]
        },
        {
          type: "section",
          fields: [
            {
              type: "mrkdwn",
              text: `Số nhân viên: ${companyData[0].$.company.employees || "N/A"}`
            },
            {
              type: "mrkdwn",
              text: `Ngành nghề: ${companyData[0].$.company.industry || "N/A"}`
            }
          ]
        },
        {
          type: "section",
          text: {
            type: "mrkdwn",
            text: `*Tin tức mới nhất:*\n${companyData[0].$.company.news || "Không có tin tức mới."}`
          }
        }
      ]
    }
  };
  ```

### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một tin nhắn Slack chứa **tên miền hoặc tên công ty** (ví dụ: `https://extruct.ai` hoặc `@Extruct`).
  - Bot sẽ tự động **trích xuất domain**, **gửi yêu cầu enrich** và **trả lời với thẻ công ty**.
- **Bật Active**:
  - Nhấn **Toggle Active** ở góc trên phải của n8n Editor.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Lọc Lead Theo Đặc Trưng**
- **Thêm node "if"** trước **"Start Company Enrichment"** để **lọc domain** theo quy tắc:
  - Ví dụ: Chỉ enrich domain có `.com` hoặc `.io`.
  ```javascript
  // Ví dụ mã lọc domain
  if ($input.all().domain.includes('.com') || $input.all().domain.includes('.io')) {
    return { json: { domain: $input.all().domain } };
  } else {
    return { json: { error: "Domain không hợp lệ" } };
  }
  ```

### **2. Lưu Log Hoạt Động**
- **Thêm node "Set"** sau **"Get Company Data"** để lưu **ID enrichment** vào biến:
  ```json
  {
    "json": {
      "extructRunId": $input.all().$.run_id
    }
  }
  ```
- **Kết hợp với node "Slack"** để báo cáo lỗi:
  ```json
  {
    "json": {
      "text": `❌ Lỗi enrich: ${$input.all().error || "Không rõ"}`,
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*Lỗi:* ${$input.all().error || "Không có lỗi"}`}
          }
        }
      ]
    }
  }
  ```

### **3. Gửi Báo Cáo Định Kỳ**
- **Thêm node "Schedule"** (n8n Premium) để **gửi báo cáo hàng tuần** về lead enrich thành công.
- **Kết hợp với node "Google Sheets"** để lưu dữ liệu vào bảng tính.

### **4. Kết Nối Với CRM**
- **Thêm node "Make"** (n8n Premium) để **push dữ liệu enrich vào HubSpot, Salesforce, hoặc CRM khác**.
- **Ví dụ**:
  - Sau khi lấy dữ liệu từ Extruct, **tạo record mới** trong CRM với thông tin công ty.

---
## **📌 Kết Luận**
Với **Real-Time Lead Enrichment**, các sếp không chỉ **tiết kiệm thời gian** mà còn **nhận dữ liệu chính xác và chi tiết** ngay trong Slack. **Không cần code**, không cần scrape thủ công – chỉ cần **cài đặt một lần** và **bật bot hoạt động 24/7**.

### **🔥 Bắt Đầu Ngay Hôm Nay!**
1. **Đăng ký Extruct AI** và lấy **Table ID**.
2. **Tạo app Slack** và lấy **Bot Token**.
3. **Import workflow** và cấu hình theo hướng dẫn.
4. **Test với một lead** và xem bot làm việc như thế nào!

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp tự động hóa thành công!** 🚀
Nếu có vấn đề, hãy để lại **comment** dưới bài viết hoặc liên hệ **Extruct AI** qua [support@extruct.ai](mailto:support@extruct.ai).