---
title: "🚀 Tự Động Hóa Giải Quyet Ticket Trên Zammad Siêu Nhanh Với SerpAPI - Không Cần Code!"
description: "Workflow này tự động tra cứu thông tin từ 15 nguồn khác nhau (Google, Bing, Baidu, eBay...) để hỗ trợ các sếp giải quyết ticket hỗ trợ khách hàng nhanh chóng, chính xác và tiết kiệm thời gian lên đến 80%. Đặc biệt phù hợp cho đội ngũ support, kỹ thuật và doanh nghiệp cần tối ưu hóa hiệu suất."
slug: "tieu-dong-hoa-giai-quyet-ticket-zammad-serpapi"
tags: [n8n, automation, support, serpapi, zammad, no-code, ai]
keywords: [n8n workflow zammad, tự động hóa giải quyết ticket, serpapi n8n, tra cứu thông tin nhanh, hỗ trợ khách hàng tự động]
---

# 🚀 **Tự Động Hóa Giải Quyet Ticket Trên Zammad Siêu Nhanh Với SerpAPI**

## **📌 Nỗi Đau Của Các Sếp Trong Việc Giải Quyet Ticket**
Các sếp đã từng gặp phải tình huống này chưa?
- **Tốn thời gian quá lâu** để tra cứu thông tin từ nhiều nguồn khác nhau (Google, Bing, eBay, Baidu...) để hỗ trợ khách hàng.
- **Không thể tra cứu đồng thời** trên nhiều nền tảng, dẫn đến trải nghiệm khách hàng chậm chạp.
- **Rủi ro sai sót** khi copy-paste thông tin từ nhiều trang web khác nhau, gây mất tin cậy.
- **Không thể tự động hóa** quy trình hỗ trợ, buộc phải làm thủ công mỗi khi có ticket mới.

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách **tự động tra cứu thông tin từ 15 nguồn khác nhau** (Google, Bing, Baidu, eBay, Google Flights, Google Maps, Google News...) chỉ trong **vài giây**, giúp các sếp **giải quyết ticket nhanh hơn 80%** mà không cần viết một dòng code nào!

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** khi giải quyết ticket hỗ trợ khách hàng.
✅ **Tra cứu thông tin chính xác** từ nhiều nguồn đồng thời (Google, Bing, Baidu, eBay, Google Flights, Google Maps, Google News...).
✅ **Không cần code** – chỉ cần cấu hình và chạy workflow.
✅ **Hỗ trợ khách hàng 24/7** – workflow hoạt động tự động khi có ticket mới.
✅ **Giảm sai sót** khi copy-paste thông tin từ nhiều trang web khác nhau.
✅ **Tích hợp hoàn hảo với Zammad** – tự động cập nhật kết quả tra cứu vào ticket.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Zammad** (để lấy API Key hoặc Webhook URL).
2. **API Key của SerpAPI** (miễn phí 100 request/ngày, trả phí từ 20$/tháng).
   - 👉 [Đăng ký SerpAPI miễn phí](https://serpapi.com/) (sử dụng mã giới thiệu **N8N20** để giảm 20% phí đầu tiên).
3. **n8n Self-hosted** (để workflow chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
4. **Nếu muốn lưu log hoặc gửi báo cáo**, cần thêm tài khoản **Google Sheets** hoặc **Slack/Telegram**.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**.

#### **Cách import từ file JSON:**
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/5058).
2. Trong **n8n Editor**, nhấn **Import** → Chọn file JSON → Nhấn **Import**.

#### **Cách copy/paste JSON:**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán JSON từ file → Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

Workflow này sử dụng **SerpAPI** để tra cứu thông tin từ nhiều nguồn khác nhau. Các bước cấu hình quan trọng nhất:

#### **🔹 Cấu Hình Node `SerpApi Official Tool MCP Server` (Trigger)**
- **Type:** `mcpTrigger`
- **Configuration:**
  - **Name:** Đặt tên cho trigger (ví dụ: `Zammad Ticket Trigger`).
  - **Credentials:** Chọn **SerpAPI** (đã cấu hình trước).
  - **Webhook URL:** Nhập **Webhook URL của Zammad** (cần lấy từ Zammad Admin → Settings → Webhooks).
  - **Payload Format:** Chọn `JSON`.

#### **🔹 Cấu Hình Node `Search Google` (và các node tra cứu khác)**
Mỗi node tra cứu (ví dụ: `Search Google`, `Search Bing`, `Search Baidu`) cần cấu hình:
- **Credentials:** Chọn **SerpAPI** (đã cấu hình trước).
- **API Key:** Điền **API Key của SerpAPI**.
- **Query:** Sử dụng **`{{ $json["query"] }}`** (để lấy từ payload của Zammad ticket).
- **Engine:** Chọn **Google**, **Bing**, **Baidu**, **eBay**,... tùy theo node.
- **Additional Parameters (nếu cần):**
  - **q:** `{{ $json["query"] }}` (để tra cứu từ khóa từ ticket).
  - **hl:** `vi-VN` (để tra cứu bằng tiếng Việt).
  - **gl:** `vn` (để tra cứu ở Việt Nam).

#### **🔹 Cấu Hình Node `Sticky Note` (Lưu ý quan trọng)**
- **Dùng để ghi chú** các thông tin cần lưu ý khi cấu hình.
- Ví dụ: *"Chỉ tra cứu từ khóa trong ticket, không thêm từ khóa khác"*.

#### **🔹 Kết Nối Với Zammad**
- Sau khi tra cứu xong, kết nối với **Zammad API** để cập nhật kết quả vào ticket.
- Sử dụng node **HTTP Request** với:
  - **Method:** `POST`
  - **URL:** `https://[your-zammad-domain]/api/v1/tickets/[ticket-id]/update`
  - **Headers:**
    - `Authorization: Bearer [API_KEY_ZAMMAD]`
    - `Content-Type: application/json`
  - **Body:**
    ```json
    {
      "ticket": {
        "description": "{{ $json["result"] }}"
      }
    }
    ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một ticket mẫu:
   - Tạo ticket mẫu trên Zammad.
   - Chạy workflow và kiểm tra kết quả tra cứu.
2. **Bật Active workflow**:
   - Trong **n8n Editor**, nhấn **Active** để workflow chạy tự động khi có ticket mới.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp Slack/Telegram để Báo Lỗi**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi workflow gặp lỗi.
- Ví dụ:
  - Nếu tra cứu thất bại, gửi tin nhắn: *"Lỗi tra cứu từ khóa: {{ $json["query"] }}"*.

### **🔹 Lưu Log Tra Cứu Vào Google Sheets**
- Sử dụng node **Google Sheets** để lưu lịch sử tra cứu.
- Cấu hình:
  - **Spreadsheet ID:** ID của file Google Sheets.
  - **Sheet Name:** Tên sheet (ví dụ: `Log_Tra_Cứu`).
  - **Row:** `{{ $node["Set"].json["row"] + 1 }}` (để thêm dữ liệu vào dòng mới).

### **🔹 Gửi Báo Cáo Định Kỳ**
- Sử dụng node **n8n-nodes-base.schedule** để chạy workflow định kỳ (ví dụ: hàng ngày) và gửi báo cáo tổng hợp.
- Ví dụ:
  - Tra cứu tất cả ticket chưa giải quyết trong ngày.
  - Gửi báo cáo qua **Email** hoặc **Slack**.

### **🔹 Cải Tiến Query Tra Cứu**
- Nếu muốn tra cứu từ khóa cụ thể hơn, có thể sử dụng **node `Set`** để xử lý payload trước khi gửi đến SerpAPI.
- Ví dụ:
  - Loại bỏ từ khóa không cần thiết (ví dụ: "hỗ trợ", "giải quyết").

---

## **📌 Kết Luận**
Workflow này **giải quyết triệt để vấn đề tra cứu thông tin từ nhiều nguồn khác nhau** khi giải quyết ticket trên Zammad, giúp các sếp **tiết kiệm thời gian, tăng hiệu suất và giảm sai sót**.

**Hãy áp dụng ngay workflow này và tự động hóa quy trình hỗ trợ khách hàng của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/5058)
👉 [Đăng ký SerpAPI miễn phí](https://serpapi.com/) (mã giới thiệu **N8N20**).

---
**Chia sẻ ý kiến của các sếp về workflow này ở phần comment dưới đây!** 🚀