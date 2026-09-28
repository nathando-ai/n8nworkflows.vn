---
title: "🤖 Tự Động Hóa Trợ Lý Chăm Sóc Khách Hàng AI với GPT-4o + SMS GoHighLevel (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp xây dựng một trợ lý AI hỗ trợ chăm sóc khách hàng 24/7 bằng GPT-4o, scrape website, và gửi phản hồi qua SMS GoHighLevel - tiết kiệm thời gian lên tới 80% cho bộ phận support."
slug: "tự-dộng-hoa-trợ-ly-chăm-sóc-khách-hàng-ai-ghl"
tags: [n8n, automation, ai-chatbot, gohighlevel, gpt-4o, scrape-website, support-automation]
keywords: [n8n workflow hỗ trợ khách hàng, tự động hóa SMS GoHighLevel, GPT-4o chatbot, scrape website tự động, trợ lý AI chăm sóc khách hàng]
---

# 🚀 **Tự Động Hóa Trợ Lý Chăm Sóc Khách Hàng AI với GPT-4o + SMS GoHighLevel**

## **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, bộ phận support của các sếp phải:
- **Trả lời hàng trăm tin nhắn SMS** từ khách hàng với các câu hỏi lặp đi lặp lại (ví dụ: "Giá sản phẩm bao nhiêu?", "Địa chỉ cửa hàng gần nhất?").
- **Tốn thời gian scrape website** để cập nhật thông tin mới (giá cả, sản phẩm mới, tin tức).
- **Không thể hỗ trợ 24/7** vì nhân sự có giờ làm việc giới hạn.
- **Phải tra cứu thủ công** thông tin trên nhiều kênh (website, email, SMS) để trả lời chính xác.

**Workflow này giải quyết tất cả những vấn đề trên bằng:**
✅ **Trợ lý AI 24/7** sử dụng GPT-4o trả lời tin nhắn SMS tự động.
✅ **Scrape website tự động** để cập nhật thông tin mới nhất.
✅ **Gửi phản hồi SMS** qua GoHighLevel một cách nhanh chóng và cá nhân hóa.
✅ **Không cần viết một dòng code** – chỉ cần cấu hình và chạy!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** cho bộ phận support (không phải trả lời SMS lặp lại).
- **Hỗ trợ khách hàng 24/7** mà không cần nhân viên thêm.
- **Cập nhật thông tin website tự động** (giá cả, sản phẩm mới, tin tức).
- **Trả lời chính xác và cá nhân hóa** nhờ GPT-4o.
- **Kết nối GoHighLevel** để quản lý khách hàng một cách chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GoHighLevel** (để gửi/receive SMS và quản lý khách hàng).
2. **API Key OpenAI** (để sử dụng GPT-4o).
3. **BrightData API Key** (hoặc thay thế bằng HTTP Request nếu dùng n8n Cloud).
4. **Website cần scrape** (để lấy thông tin sản phẩm, giá cả, tin tức).
5. **Tài khoản Redis** (để lưu trữ bộ nhớ chat của AI – *khuyến cáo dùng Redis Cloud*).
6. **Tài khoản Pinecone/Supabase** (nếu muốn lưu vector database lâu dài – *không bắt buộc*).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4223](https://n8n.io/workflows/4223) (ấn nút "Export").
2. **Mở n8n Editor** trên máy chủ tự host của bạn.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/4223](https://n8n.io/workflows/4223).
2. **Mở n8n Editor** và nhấn **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để workflow xuất hiện.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 1. Cấu Hình GoHighLevel (GHL)**
- **Tạo OAuth2 Credential** trong n8n:
  - **Tên Credential:** `highLevelOAuth2Api`
  - **API Base URL:** `https://api.gohighlevel.com/v1/`
  - **Client ID & Secret:** Lấy từ [GoHighLevel Developer Portal](https://developers.gohighlevel.com/).
  - **Scope:** `read write`
- **Cấu hình Webhook GHL:**
  - Trong node **"Webhook from GHL - SMS Reply Trigger"**, copy **path** (`54259c33-52c0-4a19-97fe-3414a153f4d6`) và dán vào **Settings → Webhooks** của ứng dụng GHL.
  - **Hướng dẫn chi tiết:** [Loom Video](https://www.loom.com/share/f32384758de74a4dbb647e0b7962c4ea).

#### **🔹 2. Cấu Hình OpenAI (GPT-4o)**
- **Tạo Credential OpenAI:**
  - **Tên Credential:** `openAiApi`
  - **API Key:** Lấy từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys).
- **Kiểm tra model GPT-4o:**
  - Trong node **"OpenAI Chat Model"**, đảm bảo **model** được đặt là `gpt-4o`.

#### **🔹 3. Cấu Hình BrightData (hoặc thay thế bằng HTTP Request)**
- **Nếu dùng BrightData:**
  - **Tạo Credential BrightData:**
    - **Tên Credential:** `brightdataApi`
    - **API Key:** Lấy từ [BrightData Dashboard](https://brightdata.com/).
  - **Cấu hình trong node "BrightData" và "BrightData1"**.
- **Nếu dùng n8n Cloud (không BrightData):**
  - Thay thế node **BrightData** bằng **HTTP Request**.
  - **Cấu hình URL scrape** trong node **HTTP Request** (ví dụ: `https://website.com`).

#### **🔹 4. Cấu Hình Redis (Bộ Nhớ Chat AI)**
- **Tạo Credential Redis:**
  - **Tên Credential:** `redisChatMemory`
  - **Host:** `your-redis-host.ngrok.io` (nếu dùng Redis Cloud).
  - **Port:** `6379`
  - **Password:** (nếu có).
- **Lưu ý:** Nếu không muốn dùng Redis, có thể **xóa node "Redis Chat Memory"** và **cấu hình lại AI Agent** để lưu trữ trong bộ nhớ n8n (không khuyến cáo cho production).

#### **🔹 5. Cấu Hình Website URL**
- Trong node **"Set Website URL"** và **"Set Website URL1"**, điền **URL chính** của website bạn muốn scrape (ví dụ: `https://example.com`).

#### **🔹 6. Cấu Hình AI Agent**
- **Node "AI Agent"** sẽ tự động xử lý tin nhắn SMS từ GHL và trả lời bằng GPT-4o.
- **Không cần chỉnh sửa** trừ khi muốn **cập nhật prompt** trong node **"OpenAI Chat Model"**.

#### **🔹 7. Kiểm Tra Sitemap & Scrape Links**
- **Node "Get sitemap"** sẽ lấy danh sách tất cả trang của website.
- **Nếu sitemap không hoạt động**, chuyển sang **scrape links từ trang chủ** (node **"Get XML file"**).
- **Node "Merge"** sẽ kết hợp links từ sitemap và scrape để tránh trùng lặp.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu:**
   - Gửi một tin nhắn SMS từ GHL đến webhook của n8n.
   - Kiểm tra **node "Webhook from GHL"** có nhận được không.
   - AI Agent sẽ tự động trả lời qua SMS.
2. **Bật Active workflow:**
   - Nhấn **"Active"** trên canvas.
   - **Schedule Trigger** (nếu có) sẽ chạy định kỳ để cập nhật thông tin website.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Kết Nối Slack/Telegram để Log Lịch Sử**
- **Thêm node Slack/Telegram** sau node **"Send SMS via GHL"** để log tất cả tin nhắn.
- **Cấu hình Webhook Slack/Telegram** trong node tương ứng.

### **🔹 2. Gửi Báo Cáo Định Kỳ về Thống Kê SMS**
- **Thêm node "Schedule Trigger"** để chạy hàng ngày/tuần.
- **Tạo một workflow phụ** để tổng hợp thống kê SMS đã gửi/receive và gửi báo cáo qua email.

### **🔹 3. Cập Nhật Thông Tin Website Tự Động**
- **Sử dụng "Schedule Trigger"** để scrape website hàng ngày/tuần.
- **Lưu vector database** vào **Pinecone/Supabase** thay vì Redis để lưu lâu dài.

### **🔹 4. Tăng Cường AI Agent với Knowledge Base**
- **Thêm node "Document Default Data Loader"** để tải dữ liệu từ file PDF/Word.
- **Node "Embeddings OpenAI"** sẽ chuyển đổi text thành vector.
- **Node "Vector Store"** lưu trữ knowledge base cho AI Agent sử dụng.

### **🔹 5. Xử Lý Trùng Lặp SMS**
- **Thêm node "Remove Duplicates"** trước khi AI Agent xử lý.
- **Lọc tin nhắn cũ** bằng node **"Filter"** (ví dụ: chỉ trả lời SMS mới trong 1 giờ).

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa bộ phận support của các sếp bằng:
✔ **AI GPT-4o** trả lời SMS 24/7.
✔ **Scrape website tự động** cập nhật thông tin mới.
✔ **Kết nối GoHighLevel** để quản lý khách hàng chuyên nghiệp.

**🚀 Hành động ngay:**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình GoHighLevel, OpenAI và BrightData**.
3. **Test với một tin nhắn SMS**.
4. **Bật Active và bắt đầu tiết kiệm thời gian!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công với tự động hóa support AI!** 🚀