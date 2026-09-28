---
title: "🛒 So sánh giá sản phẩm Amazon, Walmart & Google Shopping qua Telegram với AI - Tự động hóa thị trường 100% không code"
description: "Workflow tự động so sánh giá sản phẩm từ 3 thị trường lớn (Amazon, Walmart, Google Shopping) và gửi kết quả thông minh qua Telegram với AI GPT-4, giúp các sếp tiết kiệm thời gian tìm kiếm và mua hàng an toàn. Giúp lựa chọn sản phẩm chính xác với giá tốt nhất, bao gồm thông tin giá cả, độ tin cậy của nhà cung cấp và lý do chọn lựa."
slug: "so-sanh-gia-san-pham-amazon-walmart-google-shopping-telegram-ai"
tags: [n8n, automation, no-code, market-research, ai-chatbot, serpapi, openai, telegram-bot]
keywords: [n8n workflow so sánh giá, tự động hóa so sánh sản phẩm, AI GPT-4 so sánh giá, Telegram bot mua sắm, SerpApi n8n, tự động hóa thị trường điện tử]
---

# 🚀 **So sánh giá sản phẩm Amazon, Walmart & Google Shopping qua Telegram với AI - Giải pháp tự động hóa mua sắm thông minh**

### **Nỗi đau của các sếp khi mua sắm online**
Mua sắm online không chỉ tốn thời gian mà còn dễ bị lừa đảo, giá cả không rõ ràng hoặc thông tin sản phẩm không chính xác. Các sếp thường phải:
- **Tìm kiếm thủ công** trên nhiều trang web (Amazon, Walmart, Google Shopping) để so sánh giá.
- **Lo lắng về chất lượng** của sản phẩm và độ tin cậy của nhà cung cấp.
- **Mất thời gian** để lọc ra sản phẩm phù hợp nhất với ngân sách và nhu cầu.
- **Rủi ro mua hàng giả** hoặc sản phẩm không phù hợp với mô tả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động so sánh giá** trên 3 thị trường lớn (Amazon, Walmart, Google Shopping) chỉ với 1 tin nhắn Telegram.
✅ **Sử dụng AI GPT-4** để lọc ra sản phẩm **an toàn, giá tốt nhất** và lý do chọn lựa.
✅ **Gửi kết quả chi tiết** bao gồm: giá cả, nhà cung cấp, mức độ tin cậy, và liên kết mua hàng trực tiếp.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và không gián đoạn**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **90%** so với việc tìm kiếm thủ công.
- **Lựa chọn sản phẩm chính xác** với giá cả hợp lý và độ tin cậy cao.
- **Tránh mua hàng giả** nhờ AI đánh giá chất lượng và đánh giá của người dùng.
- **Mua hàng trực tiếp** từ liên kết được AI lọc sàng, không cần copy-paste.
- **Hoạt động tự động** 24/7, không phụ thuộc vào giờ làm việc.
- **Tối ưu ngân sách** với thông tin về **phạm vi giá** và **số lượng lựa chọn**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
   - Cài đặt bot vào nhóm hoặc chat cá nhân để nhận kết quả.

2. **API Key SerpApi**:
   - Đăng ký tài khoản [SerpApi](https://serpapi.com/) và lấy **API Key** (miễn phí có giới hạn).
   - Thêm API Key vào **3 node HTTP Request** (Amazon, Walmart, Google Shopping).

3. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Chọn mô hình **GPT-4** (hoặc **gpt-5-mini** nếu có) trong node **Price Analysis Model**.

4. **Tham số tùy chỉnh (nếu cần)**:
   - Điều chỉnh **vị trí/địa phương** trong các node HTTP Request để phù hợp với thị trường mục tiêu.
   - Thêm **từ khóa hoặc quy tắc lọc** trong code nodes (nếu cần).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/14330](https://n8n.io/workflows/14330) (nếu có link download).
  2. Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON.
  3. Chọn **Create New Workflow** và nhấn **Import**.

- **Cách 2: Copy/Paste JSON**
  1. Copy toàn bộ mã JSON từ [n8n.io/workflows/14330](https://n8n.io/workflows/14330) (nếu có).
  2. Trong **n8n Editor**, chọn **Create New Workflow** → **Import Workflow** → **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Cấu hình Telegram Trigger**
- Node: **"Telegram Product Request" (telegramTrigger)**
  - **Credentials**: Chọn bot Telegram đã tạo và thêm **API Token**.
  - **Tham số**:
    - **Chat ID**: Thêm ID của chat cá nhân hoặc nhóm (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
    - **Command**: Đặt là `/so_sanh` (hoặc tùy chỉnh theo ý muốn).
    - **Text**: Cấu hình để nhận **tên sản phẩm** từ người dùng.

##### **B. Cấu hình SerpApi (3 node HTTP Request)**
- Node: **"Search Amazon via SerpApi"**, **"Search Walmart via SerpApi"**, **"Search Google Shopping via SerpApi"**
  - **Credentials**: Thêm **API Key SerpApi** vào **Headers** của mỗi node.
  - **URL**: Đã cấu hình sẵn, không cần thay đổi.
  - **Query Parameters**:
    - Thêm **`q={{ $node["Telegram Product Request"].json["text"] }}`** (để lấy tên sản phẩm từ Telegram).
    - Điều chỉnh **`location`** (ví dụ: `location=Vietnam` hoặc `location=USA` tùy thị trường).

##### **C. Cấu hình AI Agent (GPT-4)**
- Node: **"AI: Choose Best Offer" (agent)** và **"Price Analysis Model" (lmChatOpenAi)**
  - **Credentials**: Thêm **API Key OpenAI**.
  - **Model**: Chọn **`gpt-5-mini`** (hoặc **`gpt-4`** nếu có).
  - **Prompt**: Đã cấu hình sẵn để AI đánh giá:
    - Giá cả, độ tin cậy của nhà cung cấp.
    - Đánh giá của người dùng (nếu có).
    - Phù hợp với mô tả sản phẩm.
    - Lọc bỏ sản phẩm **giá quá rẻ** hoặc **không phù hợp**.

##### **D. Cấu hình Code Nodes (Parse Response)**
- Node: **"Parse Amazon Response"**, **"Parse Walmart Response"**, **"Parse Google Shopping Response"**
  - **Mã JavaScript**: Đã chuẩn bị sẵn để **tách dữ liệu** từ response của SerpApi.
  - **Lưu ý**: Không cần chỉnh sửa nếu không hiểu code, nhưng có thể mở ra để hiểu cách xử lý dữ liệu.

##### **E. Cấu hình Telegram Output**
- Node: **"Send Telegram Recommendation" (telegram)**
  - **Credentials**: Chọn bot Telegram cùng với **API Token**.
  - **Tham số**:
    - **Chat ID**: Cùng với node Telegram Trigger.
    - **Message**: Đã cấu hình sẵn để gửi **kết quả AI** bao gồm:
      - **Giá tốt nhất**.
      - **Nhà cung cấp**.
      - **Phạm vi giá**.
      - **Số lượng lựa chọn**.
      - **Mức độ tin cậy**.
      - **Lý do chọn lựa**.
      - **Liên kết mua hàng**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn `/so_sanh [tên sản phẩm]` (ví dụ: `/so_sanh iPhone 15`) đến bot Telegram.
   - Kiểm tra kết quả trong **n8n Editor** để đảm bảo workflow chạy đúng.

2. **Bật Active Workflow**:
   - Chọn workflow trong danh sách và bật **Active** để hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa AI với Prompt Custom**:
   - Thêm **yêu cầu cụ thể** vào Prompt của node **Price Analysis Model** để AI đánh giá thêm:
     - **Độ phù hợp với nhu cầu** (ví dụ: "sản phẩm phải có pin 5000mAh").
     - **Kiểm tra xem có phiên bản mới** hơn không.

2. **Lưu log kết quả**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử so sánh giá.
   - Cấu hình node **Merge** để gửi dữ liệu vào bảng tính.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi **báo cáo tuần/month** về sản phẩm đã so sánh.
   - Ví dụ: "Trong tuần này, sản phẩm X có giá giảm 10% so với tuần trước".

4. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để thông báo kết quả cho team.
   - Ví dụ: Khi có sản phẩm phù hợp, gửi tin nhắn Slack hoặc email cảnh báo.

5. **Lọc sản phẩm theo ngân sách**:
   - Thêm **điều kiện trong code node** để chỉ so sánh sản phẩm trong **ngưỡng giá** nhất định.
   - Ví dụ: Chỉ lấy sản phẩm dưới **3 triệu đồng**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa so sánh giá sản phẩm** trên 3 thị trường lớn nhất thế giới (Amazon, Walmart, Google Shopping) chỉ với **một tin nhắn Telegram**. Với sự hỗ trợ của **AI GPT-4**, các sếp không chỉ tiết kiệm thời gian mà còn **mua hàng an toàn, chính xác và với giá tốt nhất**.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình API Keys.
3. **Test với sản phẩm đầu tiên** và trải nghiệm sự tiện lợi của tự động hóa!

**Cần hỗ trợ?** Đăng ký [hỗ trợ kỹ thuật n8n](https://n8n.io/community) hoặc liên hệ với cộng đồng [n8n Việt Nam](https://facebook.com/groups/n8nvietnam) để được giải đáp nhanh chóng! 🚀