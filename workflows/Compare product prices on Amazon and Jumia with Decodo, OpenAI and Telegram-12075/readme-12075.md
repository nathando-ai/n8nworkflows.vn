---
title: "🛒💰 **So Sánh Giá Sản Phẩm Amazon & Jumia Tự Động Với AI - Không Cần Code!**"
description: "Workflow tự động hóa so sánh giá sản phẩm trên Amazon và Jumia, sử dụng AI (GPT-4o) và Telegram để gửi kết quả nhanh chóng. Giúp các sếp tiết kiệm thời gian tìm kiếm giá tốt nhất, tránh mua hàng giá cao hoặc hàng giả."
slug: "so-sanh-gia-amazon-jumia-ai-telegram"
tags: [n8n, automation, market-research, ai-chatbot, decodo, openai, telegram-bot]
keywords: [n8n workflow so sánh giá, tự động hóa tìm giá tốt nhất, AI so sánh Amazon Jumia, Telegram bot giá sản phẩm, n8n self-hosted]
---

# 🚀 **So Sánh Giá Sản Phẩm Amazon & Jumia Tự Động Với AI - Không Cần Code!**

### **🔍 Nỗi Đau Của Các Sếp Khi Tìm Giá Sản Phẩm**
Mỗi khi muốn mua một sản phẩm, các sếp phải:
✅ **Tìm kiếm thủ công** trên Amazon, Jumia, Shopee, Lazada...
✅ **So sánh giá** giữa nhiều trang web khác nhau
✅ **Lo lắng về hàng giả** hoặc thông tin không chính xác
✅ **Tốn thời gian** khi phải copy-paste, so sánh giá một cách thủ công

**Workflow này giải quyết tất cả!** Chỉ cần **gửi tên sản phẩm qua Telegram**, AI sẽ tự động:
✔ **Tìm kiếm** sản phẩm trên Google (Amazon, Jumia, Shopee...)
✔ **Scrape** giá và thông tin chi tiết từ trang web
✔ **So sánh** giá giữa các trang
✔ **Gửi kết quả** với **giá tốt nhất** và **liên kết mua hàng** về Telegram

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** (không cần tìm kiếm thủ công)
- **Giá chính xác** (AI scrape và so sánh tự động)
- **Tránh hàng giả** (kiểm tra thông tin sản phẩm)
- **Cá nhân hóa** (gửi kết quả qua Telegram, Slack, Email...)
- **Hoạt động 24/7** (không cần can thiệp người dùng)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Telegram** (để nhận kết quả)
✅ **API Key Telegram Bot** (tạo bot trên [@BotFather](https://t.me/BotFather))
✅ **API Key OpenAI** (để sử dụng GPT-4o)
✅ **Tài khoản Decodo** (để scrape Amazon, Jumia)
✅ **VPS Self-hosted n8n** (để workflow chạy 24/7)
:::

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/12075](https://n8n.io/workflows/12075) (chọn **Export JSON**).
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Xác nhận import** và workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ [n8n.io/workflows/12075](https://n8n.io/workflows/12075).
2. **Mở n8n Editor** và nhấp vào **"Import"** → **"Paste JSON"**.
3. **Dán JSON** và nhấp **"Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **20 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ:

#### **🔹 Node 1: Telegram Trigger (Bắt đầu workflow)**
- **Cấu hình:**
  - **Webhook URL:** `https://<tên-vps-của-bạn>/webhook`
  - **Token Telegram:** API Key của bot Telegram (tạo trên [@BotFather](https://t.me/BotFather))
  - **Chat ID:** ID của chat Telegram muốn nhận kết quả (tìm bằng cách gửi `/getid` cho bot)

#### **🔹 Node 2: Decodo (Google Search & Scrape)**
- **Cấu hình:**
  - **API Key Decodo:** Đăng ký tại [Decodo](https://decodo.com/) và lấy API Key.
  - **Operation:** Đảm bảo chọn `google_search` và `amazon`/`jumia` đúng.

#### **🔹 Node 3: AI Extraction Agent (GPT-4o)**
- **Cấu hình:**
  - **API Key OpenAI:** Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy API Key.
  - **Model:** Chọn `gpt-4o-mini` (được cấu hình sẵn trong workflow).

#### **🔹 Node 4: Telegram (Gửi kết quả)**
- **Cấu hình:**
  - **Token Telegram:** Cùng API Key như ở Node 1.
  - **Chat ID:** Cùng Chat ID như ở Node 1.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn **"Giá iPhone 15"** vào Telegram bot.
   - Kiểm tra workflow có chạy không và kết quả có xuất hiện trên Telegram không.
2. **Bật Active workflow** (nhấp vào nút **Active** ở góc trên bên phải).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **🔹 Thêm Hỗ Trợ Cho Các Trang Web Khác**
- **Mở rộng "Build Queries" node** để thêm **Shopee, Lazada, Tiki** vào danh sách scrape.
- **Cách làm:**
  - Mở node **"Build Queries"** (Code node thứ 2).
  - Thêm các **query mới** vào mảng `queries`:
    ```javascript
    const queries = [
      "site:amazon.com \"iPhone 15\"",
      "site:jumia.com.vn \"iPhone 15\"",
      "site:shopee.vn \"iPhone 15\"",
      "site:lazada.vn \"iPhone 15\""
    ];
    ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node "Set"** sau **"Merge Results"** để lưu kết quả vào **Google Sheets** hoặc **Notion**.
- **Cách làm:**
  - Thêm node **Google Sheets** (nếu cần).
  - Cấu hình **Sheet Name** và **Credentials**.

### **🔹 Kết Hợp Với Slack/Email**
- **Thay thế Telegram bằng Slack/Email** trong node **"Send Reply"**.
- **Cách làm:**
  - Thay đổi node **Telegram** thành **Slack** hoặc **Email**.
  - Cấu hình **Webhook Slack** hoặc **SMTP Email**.

### **🔹 Tối Ưu Hóa AI Extraction**
- **Cải thiện prompt** trong node **"GPT Model"** để AI hiểu rõ hơn về sản phẩm.
- **Ví dụ:**
  ```json
  {
    "role": "user",
    "content": "Tóm tắt giá và đặc điểm của sản phẩm này từ HTML scraped. Nếu có nhiều phiên bản, hãy so sánh và chọn phiên bản tốt nhất."
  }
  ```

---

## 📌 **Kết Luận**
Workflow này **giúp các sếp tiết kiệm thời gian, tránh mua hàng giá cao hoặc hàng giả** bằng cách tự động so sánh giá trên **Amazon, Jumia, Shopee, Lazada** và gửi kết quả qua **Telegram**.

**🚀 Hãy áp dụng ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Telegram, OpenAI và Decodo**.
3. **Test với sản phẩm đầu tiên** và **tận hưởng kết quả tự động hóa!**

**💡 Mẹo cuối:** Nếu muốn **mở rộng thêm**, hãy thử **thêm node "Set"** để lưu kết quả vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử giá!

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/12075) | 🛠️ [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**