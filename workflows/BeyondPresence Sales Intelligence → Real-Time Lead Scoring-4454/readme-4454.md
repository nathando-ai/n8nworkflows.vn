---
title: "🚀 **BeyondPresence Sales Intelligence: Tự Động Hóa Đánh Giá Lead Thực Tế Cho Doanh Nghiệp**"
description: "Workflow này tự động phân tích tin nhắn từ BeyondPresence, đánh giá điểm số lead theo các tín hiệu mua hàng, phát hiện đề cập đến đối thủ cạnh tranh và gửi cảnh báo thông minh đến Slack trong thời gian thực. Giúp các sếp tiết kiệm 10+ giờ/tuần theo dõi và đánh giá lead thủ công."
slug: "beyondpresence-sales-intelligence-real-time-lead-scoring"
tags: [n8n, automation, sales, ai, slack, beyondpresence]
keywords: [tự động hóa đánh giá lead, beyondpresence n8n, cảnh báo lead hot, scoring lead thực tế, tự động hóa sales intelligence]
---

# 🚀 **BeyondPresence Sales Intelligence: Đánh Giá Lead Thực Tế & Cảnh Báo Thông Minh**

## **🔍 Nỗi Đau Của Các Sếp: Tốn Thời Gian Theo Dõi Lead Thủ Công**
Hàng ngày, các sếp phải:
- **Lọc và đánh giá hàng trăm tin nhắn** từ BeyondPresence để tìm lead tiềm năng.
- **Đánh giá thủ công** xem ai là lead "hot" (có ý định mua) và ai chỉ "just looking".
- **Phát hiện đối thủ cạnh tranh** trong cuộc trò chuyện mà không có cảnh báo tự động.
- **Tập trung vào lead sai** vì thiếu công cụ phân tích tự động.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Đánh giá điểm số lead** dựa trên các tín hiệu mua hàng (buying signals).
✅ **Phát hiện đối thủ cạnh tranh** trong thời gian thực.
✅ **Gửi cảnh báo thông minh** đến Slack với thông tin chi tiết.
✅ **Tự động phân loại lead** thành "Hot Lead", "Qualified Lead" hoặc "Competitor Mention".

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** theo dõi lead thủ công.
- **Chỉ tập trung vào lead có tiềm năng cao** (score > 70).
- **Phát hiện đối thủ cạnh tranh ngay lập tức** trong cuộc trò chuyện.
- **Cảnh báo thông minh** với chi tiết cuộc gọi, điểm số và hành động tiếp theo.
- **Tự động lưu trữ và phân tích** lịch sử lead để cải thiện chiến lược bán hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản BeyondPresence** (để lấy webhook URL).
✔ **Tài khoản Slack** với quyền **OAuth2 API** (để gửi cảnh báo).
✔ **Các channel Slack** đã tạo sẵn:
   - `#hot-leads` (để cảnh báo lead hot).
   - `#competitors` (để cảnh báo đề cập đối thủ).
   - `#qualified-leads` (để lead đã được xác nhận).
   - `#call-summaries` (để tổng kết cuộc gọi).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4454) hoặc copy JSON từ canvas.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Webhook BeyondPresence**
- Node: **"BeyondPresence Real-Time Webhook"**
  - **Path:** `beyondpresence-sales-intelligence` (không đổi).
  - **HTTP Method:** `POST` (không đổi).
  - **Lưu ý:** Sau khi import, **copy URL webhook** từ node này và **cấu hình trong BeyondPresence** để gửi tin nhắn đến n8n.

##### **B. Cấu Hình Slack OAuth2**
- Node: **"Slack: Hot Lead Alert"**, **"Slack: Competitor Alert"**, **"Slack: Qualified Lead"**, **"Slack: Call Summary"**
  - **Bước 1:** Tạo **credentials Slack OAuth2** trong n8n:
    - Vào **Credentials** → **"New"** → Chọn **"Slack OAuth2 API"**.
    - Theo hướng dẫn OAuth2 để kết nối Slack.
    - **Chọn quyền:**
      - `channels:join` (tham gia channel).
      - `channels:history` (lịch sử tin nhắn).
      - `chat:write` (gửi tin nhắn).
  - **Bước 2:** Điền **channel name** cho mỗi node:
    - `Hot Lead Alert` → `#hot-leads`
    - `Competitor Alert` → `#competitors`
    - `Qualified Lead` → `#qualified-leads`
    - `Call Summary` → `#call-summaries`

##### **C. Cấu Hình Đánh Giá Lead (Scoring Logic)**
- Node: **"Score Sales Opportunity" (type: code)**
  - **Mở node này** và chỉnh sửa logic điểm số theo nhu cầu:
    ```javascript
    // Dữ liệu mặc định (có thể chỉnh sửa)
    const buyingSignals = {
      "interested": 20,
      "tell me more": 20,
      "budget": 15,
      "pricing": 15,
      "timeline": 15,
      "demo": 25,
      "trial": 25,
      "decision maker": 30,
      "purchase": 30,
      "buy": 30
    };

    const negativeSignals = {
      "too expensive": -20,
      "not interested": -30,
      "just looking": -15,
      "maybe later": -10
    };

    // Kiểm tra tin nhắn và tính điểm
    let score = 0;
    const message = $input.all()[0].json.message.toLowerCase();

    for (const [signal, points] of Object.entries(buyingSignals)) {
      if (message.includes(signal)) score += points;
    }

    for (const [signal, points] of Object.entries(negativeSignals)) {
      if (message.includes(signal)) score += points;
    }

    // Gửi kết quả về node tiếp theo
    $node.setOutput("data", {
      score: score,
      message: $input.all()[0].json.message,
      callId: $input.all()[0].json.callId
    });
    ```
  - **Lưu ý:** Nếu muốn **phát hiện đối thủ cạnh tranh**, thêm logic kiểm tra tên đối thủ trong tin nhắn:
    ```javascript
    const competitors = ["Vietcombank", "Techcombank", "ACB", "ViettinBank"];
    const isCompetitorMentioned = competitors.some(comp => message.includes(comp));
    $node.setOutput("data", { ...data, isCompetitorMentioned });
    ```

##### **D. Cấu Hình Tổng Kết Cuộc Gọi**
- Node: **"Process Call Summary" (type: code)**
  - Mở node này và chỉnh sửa để **tóm tắt cuộc gọi** (ví dụ: thời gian, lead, điểm số, hành động tiếp theo).
  - Ví dụ:
    ```javascript
    const summary = {
      callId: $input.all()[0].json.callId,
      leadName: $input.all()[0].json.leadName,
      score: $input.all()[0].json.score,
      message: $input.all()[0].json.message,
      timestamp: new Date().toISOString(),
      action: $input.all()[0].json.score > 70 ? "Follow up immediately" : "Monitor"
    };
    $node.setOutput("data", summary);
    ```

#### **3. Kích Hoạt ⚡️**
- **Test run** với tin nhắn mẫu:
  - Gửi tin nhắn từ BeyondPresence (ví dụ: *"Tôi quan tâm đến gói premium, khi nào có demo?"*).
  - Kiểm tra Slack có nhận được cảnh báo **"Hot Lead"** không.
- **Bật Active workflow** khi đã kiểm tra hoàn chỉnh.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Sheets/Notion**
   - Thêm node **Google Sheets** hoặc **Notion** để **lưu lịch sử lead** và **báo cáo định kỳ**.
   - Ví dụ: Sau mỗi cảnh báo, lưu dữ liệu vào sheet với cột: `Call ID`, `Lead Name`, `Score`, `Timestamp`.

2. **Tự động gửi email cảnh báo**
   - Thêm node **Email (SMTP)** hoặc **Gmail** để gửi cảnh báo cho team khi có lead hot.

3. **Phân tích dữ liệu theo thời gian**
   - Sử dụng node **Code** để tính **trung bình điểm số lead** theo tháng và gửi báo cáo định kỳ.

4. **Cảnh báo qua Telegram**
   - Thêm node **Telegram Bot** để nhận cảnh báo trên điện thoại.

5. **Tự động gán task cho team**
   - Kết hợp với **Jira** hoặc **Trello** để tự động tạo task cho lead hot.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tăng Doanh Thu!**
Workflow **BeyondPresence Sales Intelligence** là **công cụ tự động hóa hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** theo dõi lead thủ công.
✔ **Phát hiện lead hot** ngay khi họ có ý định mua.
✔ **Phát hiện đối thủ cạnh tranh** trong thời gian thực.
✔ **Tự động cảnh báo** qua Slack/Telegram/Email.

**Hành động ngay:**
1. **Import workflow** vào n8n.
2. **Cấu hình Slack và BeyondPresence** theo hướng dẫn.
3. **Test với tin nhắn mẫu** và bật workflow.
4. **Theo dõi kết quả** và tối ưu hóa logic scoring!

**🚀 CÓ THỂ LÀM ĐƠN GIẢN HƠN VẬY!** Hãy bắt đầu tự động hóa sales intelligence của mình ngay hôm nay! 💪