---
title: "🚀 Tự Động Hóa Xử Lý & Theo Dõi Đơn Hàng Từ Email Với Gemini-GPT & Notion (Không Cần Code)"
description: "Workflow tự động phân loại, trích xuất thông tin đơn hàng từ email, đồng bộ hóa dữ liệu lên Notion và gửi thông báo tự động - tiết kiệm 8+ giờ/lần cho bộ phận logistics và bán hàng."
slug: "tieu-ly-don-hang-tu-email-voi-gemini-gpt-notion"
tags: [n8n, automation, no-code, email-processing, notion-integration, ai-gemini, logistics-automation]
keywords: [tự động hóa đơn hàng email, gemini gpt trích xuất dữ liệu, đồng bộ hóa notion từ email, n8n workflow logistics, tự động hóa bán hàng không code]
---

# 🚀 **Tự Động Hóa Xử Lý Đơn Hàng Từ Email Với Gemini-GPT & Notion (Không Cần Code)**

### **📌 Nỗi Đau Của Các Sếp Trong Logistics & Bán Hàng**
Hàng ngày, bộ phận logistics và bán hàng phải mất **tối thiểu 8-10 giờ** để:
- **Quét và phân loại** hàng trăm email đơn hàng từ khách hàng.
- **Trích xuất thủ công** thông tin đơn hàng (mã đơn, sản phẩm, trạng thái giao hàng, địa chỉ).
- **Nhập liệu vào Notion/Excel** để theo dõi, gây ra sai sót và mất thời gian.
- **Gửi thông báo thủ công** khi trạng thái đơn hàng thay đổi (đã ship, đã giao, lỗi giao hàng).

**Kết quả?** Dữ liệu không đồng bộ, phản hồi chậm, và khách hàng không hài lòng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 8+ giờ/tuần** cho bộ phận logistics và bán hàng.
✅ **Trích xuất dữ liệu chính xác 100%** từ email (mã đơn, sản phẩm, trạng thái, địa chỉ).
✅ **Dữ liệu tự động đồng bộ** lên Notion với định dạng chuẩn (không sai sót nhập liệu).
✅ **Nhận thông báo tự động** khi đơn hàng có sự thay đổi (ship, giao hàng, lỗi).
✅ **Theo dõi toàn bộ đơn hàng** từ một bảng Notion duy nhất, không cần mở email.
✅ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng và dữ liệu chính xác.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản & API Key:**
- **Gmail** (để lấy email và gửi thông báo tự động).
- **Notion** (để đồng bộ hóa dữ liệu đơn hàng).
- **Google Gemini API** (để phân tích và trích xuất dữ liệu từ email).
- **OpenAI API** (không bắt buộc, nhưng có thể sử dụng làm backup nếu Gemini gặp lỗi).

📌 **Cấu hình trước:**
- **Notion Database:** Tạo một bảng dữ liệu đơn hàng với các cột:
  - `Order Number` (mã đơn)
  - `Customer Name` (tên khách hàng)
  - `Order Status` (trạng thái đơn hàng: Ordered, Shipped, Delivered, Cancelled)
  - `Items` (danh sách sản phẩm)
  - `Delivery Address` (địa chỉ giao hàng)
  - `Tracking Number` (mã theo dõi)
  - `Created At` (thời gian tạo)
  - `Updated At` (thời gian cập nhật)

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9689](https://n8n.io/workflows/9689).
- **Import vào n8n Editor** bằng cách:
  - Nhấp vào **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Gmail Trigger (Gmail Trigger)**
- **Chọn credentials:** `gmailOAuth2` (đã cấu hình trước khi import).
- **Cấu hình:**
  - **Label:** Chọn `inbox` (hoặc tạo một label riêng cho email đơn hàng).
  - **Subject:** Có thể lọc theo từ khóa như `Order Confirmation`, `Shipment Update`, `Delivery Status`.

##### **🔹 Node 2: Email Classification and Extraction Agent (Agent)**
- **Mô tả:** Node này phân loại email và trích xuất dữ liệu dựa trên **Gemini-GPT** và **OpenAI**.
- **Lưu ý:**
  - **Credentials:** Chọn `googlePalmApi` (API Key của Google Gemini).
  - **Key Parameters:**
    - `model`: Đảm bảo chọn `gemini-1.0-pro` (hoặc phiên bản mới nhất).
    - **Prompt:** Node này đã được tối ưu hóa sẵn, **không cần chỉnh sửa** trừ khi cần thay đổi logic phân loại.

##### **🔹 Node 3: Structured Output Parser (Structured Output Parser)**
- **Mô tả:** Chuyển dữ liệu trích xuất từ text thành **JSON chuẩn**.
- **Lưu ý:**
  - **Schema:** Đảm bảo cấu trúc JSON phù hợp với Notion Database (ví dụ: `orderNumber`, `items`, `status`).

##### **🔹 Node 4: Notion Database Sync Agent (Agent)**
- **Mô tả:** Tự động **tạo hoặc cập nhật** đơn hàng trong Notion.
- **Lưu ý:**
  - **Credentials:** Chọn `notionApi` (API Key của Notion).
  - **Logic:**
    - **Search Database:** Tìm kiếm đơn hàng bằng `orderNumber`.
    - **Create/Update:** Nếu đơn hàng tồn tại, cập nhật; nếu không, tạo mới.
    - **Status Change:** Chỉ cập nhật trạng thái (`Shipped`, `Delivered`) nếu thay đổi.

##### **🔹 Node 5: Email Router (If)**
- **Mô tả:** **Lọc email** dựa trên kết quả phân loại (`isOrderEmail`).
  - **TRUE:** Email liên quan đến đơn hàng → tiếp tục xử lý.
  - **FALSE:** Email không liên quan → **bỏ qua** (node `No action taken`).

##### **🔹 Node 6: Send a Message (Gmail)**
- **Mô tả:** Gửi **thông báo tự động** về trạng thái đơn hàng.
- **Lưu ý:**
  - **Credentials:** Chọn `gmailOAuth2`.
  - **Nội dung email:** Có thể tùy chỉnh để thông báo cho khách hàng hoặc bộ phận logistics.

##### **🔹 Node 7: Search a page in Notion (Notion Tool)**
- **Mô tả:** Trước khi cập nhật, node này **kiểm tra đơn hàng đã tồn tại** trong Notion.
- **Lưu ý:**
  - **Query:** Sử dụng `orderNumber` để tìm kiếm.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn một email mẫu (ví dụ: email xác nhận đơn hàng) và **run test**.
- **Kiểm tra:**
  - Dữ liệu có được trích xuất chính xác không?
  - Notion có cập nhật đơn hàng không?
  - Email thông báo có được gửi không?
- **Bật Active:** Sau khi test thành công, **bật workflow** để hoạt động 24/7.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thay vì gửi email, **gửi thông báo vào Slack/Telegram** bằng node `webhook` hoặc `slack`.
   - **Cách làm:**
     - Thêm node `webhook` sau `Send a message`.
     - Cấu hình URL webhook từ Slack/Telegram.

2. **Lưu Log Lịch Sử:**
   - Thêm node `stickyNote` để **ghi lại lịch sử** của mỗi đơn hàng (ví dụ: ai cập nhật, thời gian, lý do).
   - **Cách làm:**
     - Sau node `Update a database page in Notion`, thêm node `stickyNote` với nội dung:
       ```json
       {
         "action": "updated_order",
         "orderNumber": "{{$node["Update a database page in Notion"].json.orderNumber}}",
         "updatedBy": "automation",
         "timestamp": "{{$node["Update a database page in Notion"].json.updatedAt}}"
       }
       ```

3. **Báo Cáo Định Kỳ:**
   - Tạo một **báo cáo hàng ngày/tuần** về đơn hàng mới, đã ship, đã giao.
   - **Cách làm:**
     - Sử dụng node `notionTool` với `queryDatabase` để lấy dữ liệu.
     - Gửi báo cáo qua email hoặc Slack.

4. **Sử Dụng OpenAI Làm Backup:**
   - Nếu Gemini gặp lỗi, **chuyển sang OpenAI** bằng node `OpenAI Chat Model`.
   - **Cách làm:**
     - Thêm node `if` sau `Google Gemini Chat Model`.
     - Nếu Gemini trả về lỗi, chuyển sang OpenAI với `gpt-4.1-mini`.

---
### **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề xử lý đơn hàng từ email một cách tự động, không cần code. Các sếp sẽ:
✔ **Tiết kiệm thời gian** cho bộ phận logistics và bán hàng.
✔ **Đảm bảo dữ liệu chính xác** với AI Gemini-GPT.
✔ **Theo dõi đơn hàng một cách dễ dàng** trên Notion.
✔ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng.

**🚀 Hành động ngay!**
- **Import workflow** và cấu hình theo hướng dẫn.
- **Test với email mẫu** trước khi bật hoạt động 24/7.
- **Tối ưu hóa** bằng cách kết hợp Slack, Telegram hoặc báo cáo tự động.

**💡 Lưu ý cuối cùng:**
Nếu gặp khó khăn trong quá trình cấu hình, **hãy liên hệ với cộng đồng n8n** hoặc **đăng ký VPS Self-hosted** để workflow chạy ổn định 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔥 Bắt đầu tự động hóa ngay hôm nay!**