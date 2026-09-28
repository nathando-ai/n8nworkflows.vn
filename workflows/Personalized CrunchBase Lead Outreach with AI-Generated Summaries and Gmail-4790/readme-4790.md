---
title: "🚀 Tự Động Hóa Outreach Tiềm Năng Startup Với AI Tóm Tắt Tài Liệu & Email Gmail - Khai Thác Crunchbase Miễn Phí"
description: "Workflow tự động hóa lấy dữ liệu mới nhất từ Crunchbase, tóm tắt thông tin CEO/Founder bằng AI GPT-4o-mini, và gửi email outreach cá nhân hóa cho đội sales. Tiết kiệm 10+ giờ/tháng cho công việc nghiên cứu thị trường và outreach cold."
slug: "tieu-dong-hoa-outreach-startup-ai-gmail"
tags: [n8n, automation, sales, ai, crunchbase, gmail, no-code, outreach, startup]
keywords: [tự động hóa outreach startup, crunchbase api n8n, ai tự động hóa email outreach, gmail automation n8n, tìm kiếm tiềm năng startup, tóm tắt thông tin founder bằng ai]
---

# 🚀 **Tự Động Hóa Outreach Tiềm Năng Startup Với AI: Từ Crunchbase → Email Cá Nhân Hóa**

## **🔥 Nỗi Đau Của Các Sếp Trong Outreach Startup**
Bạn có bao giờ phải:
- **Tìm kiếm thủ công** trên Crunchbase hàng trăm startup mới mỗi tuần?
- **Copy-paste** thông tin CEO/Founder vào email mà lại **không chuyên nghiệp**?
- **Lặp lại** công việc này hàng ngày mà **không có kết quả rõ ràng**?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động lấy dữ liệu** từ Crunchbase (miễn phí)
✅ **Tóm tắt thông tin** của CEO/Founder bằng AI (GPT-4o-mini)
✅ **Gửi email outreach** cá nhân hóa cho đội sales

**Kết quả?** **Tiết kiệm 10+ giờ/tháng** và **tăng tỷ lệ phản hồi** lên gấp 3x!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công, AI tự tóm tắt thông tin chính xác.
- **Email outreach chuyên nghiệp**: Nội dung cá nhân hóa, tăng tỷ lệ mở email.
- **Dữ liệu mới nhất**: Lấy thông tin từ Crunchbase theo thời gian thực.
- **Hoạt động liên tục**: Chạy tự động mỗi khi có dữ liệu mới (hoặc manual trigger).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key Crunchbase** (miễn phí, đăng ký tại [Crunchbase Developer Portal](https://developer.crunchbase.com/))
2. **API Key OpenAI** (đăng ký tại [OpenAI Platform](https://platform.openai.com/))
3. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0 cho n8n)
4. **Tài khoản n8n** (self-hosted hoặc n8n.cloud)
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4790) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  ```bash
  # Nếu tự host, chạy lệnh:
  curl -X POST https://<your-n8n-url>/api/v1/workflows -H "Authorization: Bearer <your-api-key>" -H "Content-Type: application/json" --data-binary @workflow.json
  ```

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow chia thành **3 phần chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 PHẦN 1: Trigger + Lấy Dữ liệu Startup Mới**
- **Node Manual Trigger**: Dùng để **test workflow** hoặc chạy thủ công.
- **Node HTTP Request (Fetch: Updated Companies List)**:
  - **Tham số cần chỉnh**:
    - **URL**: Đảm bảo sử dụng API Crunchbase chính xác (ví dụ: `https://api.crunchbase.com/api/v4/companies?updated_since=2024-01-01`).
    - **Headers**: Thêm `Authorization: Bearer <crunchbase-api-key>`.
    - **Query Parameters**:
      - `page=1` (đổi thành `page=2` để lấy trang tiếp theo).
      - `updated_since=YYYY-MM-DD` (lọc startup mới nhất trong khoảng thời gian).

#### **🔹 PHẦN 2: Lấy Thông Tin CEO/Founder + Tóm Tắt**
- **Node HTTP Request (Fetch: Founder Profiles by UUID)**:
  - **Lấy UUID** của startup từ phần trước, sau đó gọi API Crunchbase để lấy thông tin người sáng lập.
  - **Ví dụ**:
    ```json
    "url": "https://api.crunchbase.com/api/v4/people?company_id=YOUR_COMPANY_UUID"
    ```
- **Node Set (Extract Key Profile Fields)**:
  - **Chọn trường cần lấy**: Full Name, Title, Biography, Education, Social Links, Associated Companies.
  - **Lưu ý**: Nếu startup có **nhiều co-founder**, chỉnh **array index** (ví dụ: `[0]` → `[1]` để lấy Founder thứ 2).

#### **🔹 PHẦN 3: AI Tóm Tắt + Gửi Email Outreach**
- **Node OpenAI Chat Model (GPT-4o-mini)**:
  - **Prompt mặc định**:
    > *"Tóm tắt thông tin của {Full Name} (CEO/Founder) ở startup {Company Name} thành một đoạn email outreach ngắn gọn, bao gồm: vị trí, kinh nghiệm, giáo dục, và liên kết LinkedIn. Đảm bảo chuyên nghiệp và cá nhân hóa."*
  - **Lưu ý**:
    - Đảm bảo **API Key OpenAI** được điền vào `openAiApi` trong n8n.
    - **Model**: Đặt là `gpt-4o-mini` (rẻ và hiệu quả).
- **Node Gmail (Send email for outreach)**:
  - **Tham số cần chỉnh**:
    - **Người nhận**: Đặt email của đội sales (ví dụ: `sales@company.com`).
    - **Tiêu đề email**: Thay đổi thành `"🚀 Tiềm năng mới: {Company Name} - CEO {Full Name}"`.
    - **Nội dung**: Sử dụng output từ AI (cấu trúc đã định sẵn).

---
### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Trigger** và kiểm tra:
    - Dữ liệu Crunchbase có đúng không?
    - AI có tóm tắt chính xác không?
    - Email có gửi được không?
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và chạy định kỳ (hoặc manual).

---

## **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Lưu log vào Google Sheets/Notion**:
  - Thêm node **Google Sheets** sau **Gmail** để ghi lại lịch sử outreach.
- **Gửi email đến Slack/Telegram**:
  - Thay thế node Gmail bằng **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả.
- **Lọc startup theo ngành**:
  - Thêm điều kiện trong **HTTP Request (Crunchbase)** để lấy startup trong ngành cụ thể (ví dụ: `industry=AI`).
- **Tự động hóa định kỳ**:
  - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày (ví dụ: `0 9 * * *` để chạy lúc 9h sáng).
:::

---

## **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc nghiên cứu tiềm năng startup và outreach cold. **Không cần code**, chỉ cần **cấu hình vài bước**, bạn đã có một **hệ thống tự động hóa hoàn chỉnh** từ Crunchbase → AI → Email.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Chỉnh sửa API keys** và email nhận.
3. **Test và bật chạy** để tiết kiệm thời gian!

**Nếu gặp vấn đề**, liên hệ với tác giả qua:
🔗 [LinkedIn Yaron Been](https://www.linkedin.com/in/yaronbeen/)
📺 [YouTube Channel](https://www.youtube.com/@YaronBeen/videos)

---
**💡 Lưu ý cuối cùng**: Nếu muốn **tăng hiệu quả**, kết hợp với **CRM như HubSpot** để tự động cập nhật lead vào hệ thống!