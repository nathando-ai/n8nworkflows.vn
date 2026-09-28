---
title: "🚀 Tự Động Hóa Scrape Lead Từ Google Maps Với GPT-4, Gửi Notion & Giao Nhiệm Về Telegram - Giải Pháp Lead Gen AI Cho Doanh Nghiệp"
description: "Workflow tự động hóa scrape lead từ Google Maps, phân tích AI bằng GPT-4, tránh trùng lặp, lưu vào Notion và giao nhiệm vụ cho đội ngũ qua Telegram - tiết kiệm 80% thời gian cold outreach. Phù hợp cho doanh nghiệp B2B, dịch vụ địa phương và team bán hàng."
slug: "tieu-dong-hoa-scrape-lead-google-maps-gpt-4-notion-telegram"
tags: [n8n, automation, lead-generation, ai-chatbot, notion, telegram, google-maps-scraping, gpt-4, no-code]
keywords: [tự động hóa scrape lead google maps, workflow n8n lead gen, gpt-4 phân tích review, giao nhiệm vụ lead qua telegram, tự động hóa bán hàng b2b, notion crm automation]
---

# 🚀 **Scrape Lead Từ Google Maps → AI Phân Tích → Giao Nhiệm Về Telegram: Giải Pháp Lead Gen 100% Tự Động**

## **💥 Nỗi Đau Của Các Sếp Trong Cold Outreach**
Hàng ngày, đội ngũ bán hàng phải:
- **Tìm kiếm thủ công** leads từ Google Maps, Facebook, hoặc trang web đối thủ.
- **Lọc trùng lặp** giữa các nguồn dữ liệu (Excel, CRM, Notion).
- **Viết pitch cá nhân hóa** cho từng lead, mất thời gian và dễ sai sót.
- **Giao nhiệm vụ** cho team một cách rườm rà, không theo dõi được tiến độ thực tế.

**Kết quả?** Thời gian cold outreach tăng gấp 3-5 lần, tỷ lệ chuyển đổi thấp, và đội ngũ cảm thấy mệt mỏi.

---
### **🎯 Giải Pháp Của Workflow Này**
Workflow này **tự động hóa toàn bộ quy trình** từ scrape lead đến giao nhiệm vụ:
✅ **Scrape lead** từ Google Maps (hoặc Outscraper) với dữ liệu sạch, chuẩn hóa.
✅ **Tránh trùng lặp** bằng kiểm tra Notion trước khi xử lý.
✅ **AI GPT-4 phân tích** review của lead để tạo **pitch cá nhân hóa** (icebreaker).
✅ **Lưu lead vào Notion** với thông tin đầy đủ (địa chỉ, review, pitch AI).
✅ **Gửi lead qua Telegram** với **button "Take Lead"** để team giao nhiệm vụ nhanh chóng.
✅ **Cập nhật tự động** khi lead được giao cho thành viên nào.

**Kết quả?** Tiết kiệm **80% thời gian** cold outreach, tăng **tỷ lệ chuyển đổi 30%** nhờ pitch cá nhân hóa, và **theo dõi tiến độ** toàn bộ team trên Telegram.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong cold outreach (không cần scrape thủ công).
- **Tăng tỷ lệ chuyển đổi 30%** nhờ pitch cá nhân hóa từ GPT-4.
- **Tránh trùng lặp lead** với kiểm tra Notion tự động.
- **Giao nhiệm vụ nhanh chóng** qua Telegram với button "Take Lead".
- **Theo dõi tiến độ team** trên một nền tảng duy nhất (Notion + Telegram).
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (đã tạo 2 database: **"Active Deals"** và **"Agents"**).
2. **API Key Outscraper** (miễn phí, dùng để scrape Google Maps).
3. **Bot Telegram** (tạo trên [@BotFather](https://t.me/BotFather)) và **Chat ID** của nhóm bán hàng.
4. **API Key OpenAI** (để sử dụng GPT-4 phân tích review).
5. **Tài khoản n8n** (self-hosted hoặc n8n.cloud).

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12632](https://n8n.io/workflows/12632).
- **Import vào n8n Editor**:
  - Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON → **"Import Workflow"**.
  - **Hoặc** copy toàn bộ JSON vào **"Import Workflow"** từ menu.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **21 node**, các bước quan trọng cần cấu hình:

##### **📌 Node 1: Manual Trigger**
- **Không cần chỉnh**, dùng để kích hoạt workflow thủ công khi cần.

##### **📌 Node 2: CONFIGURATION (Set)**
- **Điền API Key Outscraper** vào biến `OUTSCRAPER_API_KEY`.
- **Điền URL Google Maps** (ví dụ: `https://www.google.com/maps/search/cafe+da+lat+da+nang`).
- **Điền Chat ID Telegram** (lấy từ [@userinfobot](https://t.me/userinfobot)).

##### **📌 Node 3: Fetch Google Maps Data (HTTP Request)**
- **Không cần chỉnh**, tự động gọi API Outscraper với dữ liệu từ `CONFIGURATION`.

##### **📌 Node 4: Clean & Normalize (Code)**
- **Không cần chỉnh**, tự động sạch dữ liệu (điện thoại, địa chỉ, review).

##### **📌 Node 5: Search Duplicate (Notion)**
- **Chọn database Notion**: **"Active Deals"** (đã tạo trước).
- **Cấu hình query**:
  ```json
  {
    "filter": {
      "property": "Name",
      "relation": "contains",
      "value": "{{ $node["1. Fetch Google Maps Data"].json["name"] }}"
    }
  }
  ```

##### **📌 Node 8: AI Icebreaker (OpenAI)**
- **Điền API Key OpenAI** vào biến `OPENAI_API_KEY`.
- **Prompt mẫu** (có thể chỉnh sửa):
  ```json
  "You are a sales expert. Analyze the following Google Maps review and create a 3-sentence icebreaker pitch for a local business owner:
  Review: '{{ $node["🔎 Search Duplicate"].json["reviews"][0] }}'
  Business: '{{ $node["🔎 Search Duplicate"].json["name"] }}'"
  ```

##### **📌 Node 11: Create New Lead (Notion)**
- **Chọn database**: **"Active Deals"**.
- **Cấu hình fields**:
  - `Name`: `{{ $node["🔎 Search Duplicate"].json["name"] }}`
  - `Phone`: `{{ $node["2. Clean & Normalize"].json["phone"] }}`
  - `Address`: `{{ $node["2. Clean & Normalize"].json["address"] }}`
  - `AI Icebreaker`: `{{ $node["🤖 AI Icebreaker"].json["response"] }}`

##### **📌 Node 12: Prepare Message (Code)**
- **Không cần chỉnh**, tự động tạo card HTML cho Telegram.

##### **📌 Node 13: Notify Team (Telegram)**
- **Chọn Chat ID** từ `CONFIGURATION`.
- **Message template**:
  ```html
  <b>📢 New Lead Alert!</b>
  <b>Business:</b> {{ $node["🔎 Search Duplicate"].json["name"] }}
  <b>Location:</b> {{ $node["2. Clean & Normalize"].json["address"] }}
  <b>AI Pitch:</b> {{ $node["🤖 AI Icebreaker"].json["response"] }}
  <button>⚡ Take Lead</button>
  ```

##### **📌 Node 14-19: Handle Button Clicks (Assignment)**
- **Node 14: Find Agent (Notion)**
  - Chọn database: **"Agents"**.
  - Query để lấy Telegram ID của thành viên:
    ```json
    {
      "filter": {
        "property": "TelegramID",
        "relation": "equals",
        "value": "{{ $node["Telegram Callback"].json["data"]["message"]["chat"]["id"] }}"
      }
    }
    ```
- **Node 16: Assign Lead (Notion)**
  - **Update field "Assigned To"** trong **"Active Deals"** với ID từ `Node 14`.
- **Node 18: Update Chat (Telegram)**
  - Cập nhật tin nhắn với thông tin:
    ```html
    <b>✅ Lead Assigned to:</b> {{ $node["🕵️‍♂️ Find Agent"].json["name"] }}
    ```

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với 1-2 lead mẫu:
   - Nhấn **"Run Workflow"** → Chọn **"Manual Trigger"** → Nhấn **"Run"**.
   - Kiểm tra Notion và Telegram có nhận được lead không.
2. **Bật Active workflow**:
   - Nhấn **"Active"** trên tab workflow.

---

### **✍️ Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack**:
   - Thay vì Telegram, có thể gửi lead qua Slack với button "Claim" bằng node `slack`.
2. **Lưu log hoạt động**:
   - Thêm node `set` sau **"Create New Lead"** để lưu log vào database Notion.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `schedule` để gửi báo cáo lead mới vào cuối ngày qua Telegram.
4. **Tối ưu scrape**:
   - Nếu Outscraper không đủ, có thể dùng **Puppeteer** (node `code`) để scrape Google Maps thủ công.
5. **Cập nhật AI prompt**:
   - Chỉnh sửa prompt GPT-4 để phù hợp với ngành nghề (ví dụ: spa, nhà hàng, dịch vụ pháp lý).

---
### **📌 Kết luận**
Workflow này **giải phóng đội ngũ bán hàng** khỏi công việc lặp lại, giúp họ tập trung vào **giao tiếp và đóng giao dịch**. Với **AI phân tích review + giao nhiệm vụ tự động**, tỷ lệ chuyển đổi tăng mạnh, trong khi thời gian cold outreach giảm đáng kể.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 lead** để đảm bảo hoạt động.
3. **Bật Active** và theo dõi kết quả!

**Nếu gặp vấn đề**, để lại comment bên dưới hoặc liên hệ [LogicCraft Automation](https://logiccraft.vn) để hỗ trợ tối ưu hóa workflow!

---
**🔥 Bạn có thể mở rộng workflow này thêm:**
- **Kết hợp với CRM** (HubSpot, Zoho) thay vì Notion.
- **Thêm phân tích sentiment** từ review bằng GPT-4.
- **Tích hợp với Zoom/Calendly** để tự động đặt lịch gọi.