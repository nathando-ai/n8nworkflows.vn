---
title: "🤖 PayInsighter: Bot Telegram Tự Động Hóa Analytics Razorpay Với AI Gemini - Không Cần Code"
description: "Tự động hóa hoàn toàn việc phân tích dữ liệu thanh toán, đơn hàng và hoàn tiền từ Razorpay qua Telegram với AI Gemini, tiết kiệm thời gian lên đến 80% cho bộ phận tài chính và kinh doanh."
slug: "payinsighter-bot-telegram-razorpay-gemini"
tags: [n8n, automation, ai-chatbot, razorpay, google-gemini, telegram-bot]
keywords: [tự động hóa razorpay, bot telegram phân tích thanh toán, gemini ai cho doanh nghiệp, workflow n8n razorpay, tự động hóa bộ phận tài chính]
---

# 🚀 **PayInsighter: Bot Telegram Tự Động Hóa Analytics Razorpay Với AI Gemini**

### **Giải pháp AI cho bộ phận tài chính: Từ "Tìm kiếm dữ liệu" sang "Hiểu dữ liệu" chỉ trong vài giây**

Hiện nay, các sếp và bộ phận tài chính thường phải mất **từ 30 phút đến 2 giờ** mỗi ngày để:
- Lọc và tổng hợp dữ liệu thanh toán từ Razorpay.
- Tính toán tổng doanh thu theo ngày/tuần/tháng.
- Theo dõi tình trạng hoàn tiền và đơn hàng.
- Trả lời các câu hỏi liên quan đến dữ liệu từ đồng nghiệp.

**PayInsighter** là một **bot Telegram thông minh** kết hợp **Razorpay API + Google Gemini AI** để:
✅ **Trả lời tất cả các câu hỏi về thanh toán, đơn hàng và hoàn tiền chỉ trong vài giây** (không cần code).
✅ **Tự động phân tích dữ liệu** và cung cấp báo cáo cá nhân hóa.
✅ **Hoạt động 24/7**, không cần can thiệp của con người.
✅ **Tiết kiệm thời gian lên đến 80%** cho việc phân tích dữ liệu thủ công.

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần phải lọc dữ liệu từ Razorpay Dashboard hoặc Excel.
- **Chính xác 100%**: AI phân tích dữ liệu theo yêu cầu chính xác, không sai sót như con người.
- **Cá nhân hóa**: Trả lời từng câu hỏi riêng biệt (ví dụ: "Cho tôi báo cáo doanh thu tuần này" vs. "Hãy cho tôi biết tất cả đơn hàng hoàn tiền trong tháng 11").
- **Hoạt động liên tục**: Bot hoạt động 24/7, trả lời ngay lập tức dù bạn đang ngủ.
- **Tích hợp hoàn hảo**: Kết nối trực tiếp với Razorpay và Telegram, không cần API key phức tạp.
:::

---

## 🔧 **Yêu cầu cần thiết**

:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Razorpay**:
   - API Key và API Secret từ [Razorpay Dashboard](https://dashboard.razorpay.com/).
   - Quyền truy cập vào API của Razorpay (đảm bảo không bị giới hạn).

2. **Tài khoản Telegram**:
   - Một **bot Telegram** riêng (không phải tài khoản cá nhân).
   - **Token API** của bot (tạo từ [@BotFather](https://t.me/BotFather)).
   - **Chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).

3. **Google Cloud AI API**:
   - **API Key** từ [Google Cloud Console](https://console.cloud.google.com/).
   - **Model Gemini 2.5 Flash** (hoặc phiên bản khác) được kích hoạt.

4. **n8n Self-hosted**:
   - Workflow này **không chạy được trên n8n Cloud** (do sử dụng nhiều AI Agent và Razorpay API).
   - **Khuyến nghị**: Cài đặt trên **VPS** để ổn định 24/7.
     👉 [Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N** - 39% off)](https://tino.vn/vps-n8n?affid=388)
     👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10815](https://n8n.io/workflows/10815).
- **Import vào n8n Editor**:
  - Nhấn **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON và dán vào **Create Workflow** → **Paste JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Telegram Trigger**
- **Node**: `Telegram Trigger`
- **Cấu hình**:
  - **Token**: Điền **Token API** của bot Telegram.
  - **Chat ID**: Điền **Chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Update Type**: Chọn **message** (để bot phản hồi tất cả tin nhắn).

#### **B. Cấu hình Razorpay API**
- **Nodes liên quan**: `Fetch all orders`, `Fetch all payments`, `Fetch all refunds`
- **Cấu hình chung**:
  - **API Key**: Điền **API Key** từ Razorpay Dashboard.
  - **API Secret**: Điền **API Secret** từ Razorpay Dashboard.
  - **Environment**: Chọn **Live** (nếu dùng môi trường thực) hoặc **Test** (nếu dùng môi trường thử nghiệm).

#### **C. Cấu hình Google Gemini AI**
- **Nodes liên quan**: `Google Gemini Chat Model1`, `Google Gemini Chat Model`, `Intent Classifier`, `AI Agents`
- **Cấu hình chung**:
  - **API Key**: Điền **API Key** từ Google Cloud Console.
  - **Model**: Chọn **gemini-2.5-flash** (hoặc phiên bản khác nếu muốn).
  - **Temperature**: Giữ mặc định **0.7** (đảm bảo trả lời logic và không quá ngẫu nhiên).

#### **D. Cấu hình AI Agents**
- **Nodes**: `Orders`, `Refunds`, `Payments Processor`, `Intent Classifier`, `General Chat Processing Agent`
- **Lưu ý**:
  - **Prompt Template**: Các AI Agent đã được cấu hình sẵn với **prompt tự động** để phân tích dữ liệu.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi cách AI trả lời (ví dụ: thay đổi giọng điệu của bot).

#### **E. Cấu hình Routing Logic (IF Nodes)**
- **Nodes**: `Payment Branch`, `Order Branch`, `Refund Branch`, `General Chat Branch1`
- **Lưu ý**:
  - Các **IF Node** sẽ tự động phân loại yêu cầu của người dùng (thanh toán, đơn hàng, hoàn tiền, hoặc chat tổng quát).
  - **Không cần chỉnh sửa** trừ khi muốn thêm/loại bỏ một loại yêu cầu nào đó.

#### **F. Cấu hình Merge & Telegram Response**
- **Node**: `Merge Responses` → `Send a text message`
- **Lưu ý**:
  - **Merge Node** sẽ kết hợp tất cả các phản hồi từ các branch (nếu người dùng hỏi nhiều yêu cầu cùng lúc).
  - **Telegram Node** sẽ gửi phản hồi về chat của người dùng.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn đến bot Telegram (ví dụ: *"Cho tôi báo cáo doanh thu tuần này"*).
   - Kiểm tra phản hồi có logic không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Không cần restart** (n8n sẽ tự động kích hoạt).

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa AI Agent**
- **Thay đổi model Gemini**:
  - Nếu muốn phản hồi **chi tiết hơn**, thay đổi model thành **gemini-1.5-pro**.
  - Nếu muốn **tiết kiệm chi phí**, giữ nguyên **gemini-2.5-flash**.

- **Cải thiện prompt**:
  - Nếu AI trả lời không chính xác, chỉnh sửa **prompt template** trong các AI Agent (ví dụ: `Orders`, `Payments Processor`).

### **2. Lưu log và báo cáo định kỳ**
- **Thêm Node `Set`** sau `Merge Responses` để lưu phản hồi vào **Google Sheets** hoặc **Database**.
- **Kết hợp với `Schedule Node`** để gửi báo cáo tự động hàng tuần.

### **3. Kết nối với Slack/Email**
- Thay vì chỉ trả lời Telegram, bạn có thể **gửi báo cáo tự động** đến Slack hoặc Email:
  - Thêm **Node `Slack`** hoặc **Node `Email`** sau `Merge Responses`.
  - Cấu hình **webhook Slack** hoặc **SMTP Email**.

### **4. Xử lý lỗi Razorpay API**
- **Thêm Node `Set`** trước `Fetch all orders/payments/refunds` để kiểm tra lỗi:
  ```json
  {
    "jsonpath": "$",
    "operation": "set",
    "property": "error",
    "value": "null"
  }
  ```
- **Thêm Node `If`** để xử lý lỗi:
  - Nếu `error` không null → Gửi tin nhắn **"Lỗi API Razorpay, vui lòng thử lại sau"** về Telegram.

---

## 📌 **Kết luận**

**PayInsighter** là **công cụ tự động hóa AI hoàn hảo** cho bộ phận tài chính, giúp:
✔ **Tiết kiệm thời gian** lên đến 80% trong việc phân tích dữ liệu.
✔ **Trả lời tất cả câu hỏi về Razorpay** chỉ trong vài giây.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để ổn định 24/7).
2. **Import workflow** và cấu hình API.
3. **Test với bot Telegram** và trải nghiệm sự thay đổi!

**🚀 [Tải workflow ngay](https://n8n.io/workflows/10815) và tự động hóa bộ phận tài chính của bạn!**

---