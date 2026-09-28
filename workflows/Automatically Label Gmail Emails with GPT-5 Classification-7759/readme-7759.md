---
title: "🤖 **Tự Động Nhãn Gmail với GPT-5: Sắp Xếp Inbox Chỉ Với 1 Clic!**"
description: "Workflow tự động hóa nhãn Gmail bằng AI GPT-5 giúp các sếp, đội ngũ Marketing/Sales và doanh nghiệp nhỏ tự động phân loại email thành 4 danh mục chính: **Đặc biệt, Quảng cáo, Tài chính/Hóa đơn, Hỗ trợ Khách hàng** – tiết kiệm thời gian và tăng hiệu quả quản lý thông tin 100%."
slug: "tu-dong-nhan-gmail-voi-gpt-5"
tags: [n8n, automation, gmail, ai, gpt-5, no-code, sales-marketing]
keywords: [tự động hóa gmail, nhãn email bằng ai, gpt-5 n8n, sắp xếp inbox gmail, workflow n8n marketing]
---

# 🚀 **Tự Động Nhãn Gmail với GPT-5: Giải Pháp AI Cho Inbox Rất Nhiều Email**

### **Nỗi Đau Của Các Sếp & Đội Ngũ Marketing/Sales**
Hàng ngày, các sếp và đội ngũ Marketing/Sales phải mất **giờ đồng hồ** để sắp xếp email trong Gmail:
- **Nhiều email quảng cáo** lẫn lộn với email quan trọng.
- **Email hỗ trợ khách hàng** bị "chìm" trong đống tin nhắn.
- **Hóa đơn và tài chính** không được theo dõi kịp thời, gây rủi ro.
- **Email đặc biệt** (urgent) bị bỏ qua vì không được nhãn rõ ràng.

**Kết quả?** Thời gian làm việc bị "chôn vùi" trong công việc thủ công, giảm hiệu quả và tăng stress.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 5-10 giờ/tuần** không phải sắp xếp email thủ công.
✅ **Tự động phân loại email** thành **4 danh mục chính** với độ chính xác cao (dựa trên GPT-5).
✅ **Tìm kiếm và quản lý email dễ dàng** nhờ nhãn tự động (High Priority, Promotion, Finance/Billing, Customer Support).
✅ **Không bỏ lỡ email quan trọng** nhờ nhãn "Đặc biệt" được AI nhận diện.
✅ **Cá nhân hóa quy trình** cho từng đội ngũ (Marketing, Sales, Tài chính, Hỗ trợ Khách Hàng).

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản Gmail** với **OAuth2** được kích hoạt (để n8n có quyền truy cập).
📌 **API Key OpenAI** (để sử dụng GPT-5).
📌 **4 nhãn Gmail** đã tạo trước:
   - **High Priority** (Đặc biệt)
   - **Promotion** (Quảng cáo)
   - **Finance/Billing** (Tài chính/Hóa đơn)
   - **Customer Support** (Hỗ trợ Khách Hàng)

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **24/7** mà không gián đoạn, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7759](https://n8n.io/workflows/7759) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần cấu hình như sau:

#### **🔹 Node 1: Gmail Trigger (GmailTrigger)**
- **Chọn credentials**: `gmailOAuth2` (đã tạo trước).
- **Cấu hình**:
  - **Polling interval**: 1 phút (có thể điều chỉnh theo email volume).
  - **Filter**: Có thể thêm điều kiện lọc (ví dụ: chỉ lấy email từ domain cụ thể).

#### **🔹 Node 2: Text Classifier (TextClassifier)**
- **Mô tả các danh mục** cần chính xác:
  - **High Priority**: Email từ CEO, khách hàng VIP, yêu cầu khẩn cấp.
  - **Promotion**: Email marketing, ưu đãi, sự kiện.
  - **Finance/Billing**: Hóa đơn, thanh toán, tài chính.
  - **Customer Support**: Yêu cầu hỗ trợ, phản hồi khách hàng.
- **Không cần chỉnh sửa** nếu sử dụng mặc định của GPT-5.

#### **🔹 Node 3: OpenAI Chat Model (lmChatOpenAi)**
- **Chọn credentials**: `openAiApi` (API Key OpenAI).
- **Model**: **GPT-5** (có thể thay thế bằng GPT-4 nếu không có API).
- **Prompt**: Workflow đã tự động cấu hình, **không cần chỉnh sửa**.

#### **🔹 Node 4-7: Gmail (Add Labels)**
- **Tên node**: High Priority, Promotion, Finance/Billing, Customer Support.
- **Chọn credentials**: `gmailOAuth2`.
- **Cấu hình**:
  - **Operation**: `addLabels`.
  - **Label ID**: **Bắt buộc phải thay đổi** thành **Label ID thực tế** của các sếp.
    - **Cách lấy Label ID**:
      1. Mở Gmail → Nhấn **Gmail Settings (⚙️) → See all settings**.
      2. Chọn **Labels** → Nhấn **Label ID** (hiển thị dưới dạng số).
      3. Thay thế giá trị trong node bằng Label ID này.

---
### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**: Chạy thử với **1 email mẫu** để kiểm tra phân loại.
- **Active Workflow**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Thêm Nhãn "Star" cho Email Đặc Biệt**
- **Cách làm**:
  - Thêm **1 node Gmail mới** với **operation: markAsStarred**.
  - Kết nối node này sau **High Priority** để email đặc biệt được đánh dấu sao.

### **2. Gửi Email Đặc Biệt đến Slack/Telegram**
- **Cách làm**:
  - Thêm **node Slack/Telegram** sau node **High Priority**.
  - Cấu hình gửi thông báo khi có email đặc biệt.

### **3. Lưu Log Email vào Google Sheets**
- **Cách làm**:
  - Thêm **node Google Sheets** sau node **Text Classifier**.
  - Cấu hình ghi dữ liệu: **Người gửi, Chủ đề, Danh mục, Thời gian**.

### **4. Tự Động Trả Lời Email Hỗ Trợ**
- **Cách làm**:
  - Thêm **node Gmail (Send Email)** sau node **Customer Support**.
  - Cấu hình trả lời tự động với template: *"Chúng tôi đã nhận được yêu cầu của bạn và sẽ xử lý trong 24h."*

### **5. Thay Đổi Model AI (Nếu Không Có GPT-5)**
- **Cách làm**:
  - Trong node **OpenAI Chat Model**, thay **model: gpt-5** thành:
    - `gpt-4` (độ chính xác cao, giá rẻ hơn).
    - `gpt-3.5-turbo` (rẻ nhất, nhưng độ chính xác thấp hơn).

---
## **📌 Kết Luận**
Workflow **Tự Động Nhãn Gmail với GPT-5** là **giải pháp hoàn hảo** để các sếp và đội ngũ Marketing/Sales **tự động hóa quản lý email**, tiết kiệm thời gian và tăng hiệu quả làm việc.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình **Gmail OAuth2 + OpenAI API**.
3. **Chỉnh Label ID** và **test run** với email mẫu.
4. **Active workflow** và **nhận inbox được sắp xếp tự động!**

👉 **Bắt đầu tự động hóa ngay hôm nay!** 🚀

---
**💡 Lưu ý cuối cùng**:
- **Không bao giờ hardcode API Key** trong workflow (sử dụng **n8n Credentials**).
- **Test với email không quan trọng** trước khi áp dụng cho email thực tế.
- **Monitor OpenAI API usage** để tránh vượt quá giới hạn.