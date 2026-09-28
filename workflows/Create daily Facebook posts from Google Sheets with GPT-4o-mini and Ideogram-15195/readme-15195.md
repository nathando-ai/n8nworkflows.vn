---
title: "🚀 Tự Động Hóa Bài Đăng Facebook Hàng Ngày Từ Google Sheets Với GPT-4o-mini & Ideogram – Giúp Các Sếp Tiết Kiệm 500+ Phút/Năm"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các SEO agency và quản lý mạng xã hội tự động tạo và đăng bài Facebook hàng ngày từ Google Sheets, với nội dung AI viết và hình ảnh chuyên nghiệp từ Ideogram. Giúp tiết kiệm thời gian, tăng hiệu quả và cá nhân hóa nội dung."
slug: "tieu-dong-hoa-bai-dang-facebook-tu-google-sheets"
tags: [n8n, automation, social-media, ai-content-generation, ideogram, facebook-graph-api, gpt-4o-mini, google-sheets]
keywords: [tự động hóa facebook, n8n workflow facebook, tạo bài viết facebook bằng ai, ideogram api, gpt-4o-mini tự động hóa, đăng bài facebook tự động]
---

# 🚀 **Tự Động Hóa Bài Đăng Facebook Hàng Ngày Từ Google Sheets Với GPT-4o-mini & Ideogram**

### **Giải pháp hoàn toàn tự động hóa cho các sếp SEO và quản lý mạng xã hội**
Hết sức phiền phức phải viết bài Facebook hàng ngày? Hay phải mất nhiều giờ để tạo hình ảnh chuyên nghiệp và đăng tải? **Workflow này sẽ giải quyết tất cả!** Hàng ngày lúc 6h sáng, hệ thống sẽ tự động:
- Đọc **từ khóa** và nội dung đã lên kế hoạch từ Google Sheets.
- **Viết bài** với tiêu đề hấp dẫn và nội dung ngắn gọn (50 từ/đoạn) bằng GPT-4o-mini.
- **Tạo hình ảnh chuyên nghiệp** 1280x704 pixel với Ideogram (mô phỏng thực tế).
- **Đăng bài** lên Facebook Page với hình ảnh + caption tự động.
- **Ghi log** URL bài đăng và thông tin vào Google Sheets để theo dõi.

**Kết quả?** Các sếp chỉ cần **đăng ký workflow 1 lần**, sau đó **quên đi việc viết bài Facebook** hàng ngày!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh gián đoạn do server công cộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 500+ phút/năm** (tương đương 8 ngày làm việc) không phải viết bài thủ công.
✅ **Nội dung chuyên nghiệp** với tiêu đề hấp dẫn và hình ảnh đẹp mắt tự động tạo.
✅ **Tăng tương tác** nhờ bài viết được cá nhân hóa theo từ khóa hàng ngày.
✅ **Hoạt động liên tục** (không cần can thiệp người dùng) với lịch trình tự động.
✅ **Theo dõi dễ dàng** với log URL bài đăng trong Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để đọc/writing dữ liệu).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini).
3. **API Key Ideogram** (để tạo hình ảnh).
4. **Access Token Facebook Page** (để đăng bài).
5. **Google Sheet mẫu** với các cột sau:
   - `Work Day` (Thứ trong tuần: Mon, Tue, ...)
   - `Keyword` (Từ khóa chính)
   - `Landing Page` (Link liên kết)
   - `Title` (Tiêu đề dự kiến, có thể bỏ trống)
   - `Content` (Nội dung dự kiến, có thể bỏ trống)
   - `Critical Instructions` (Hướng dẫn đặc biệt)
   - `Domain ID` (ID miền để log)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15195](https://n8n.io/workflows/15195) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15195) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **Node 2: Google Sheets — Read Today Keywords**
- **Chọn credential:** `googleSheetsOAuth2Api` (đã cài đặt trước).
- **Điền tham số:**
  - `Sheet ID`: ID của Google Sheet (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - `Tab Name`: Tên tab chứa dữ liệu (ví dụ: `Bài viết hàng ngày`).
  - **Lọc dữ liệu:** `Work Day` = `{{ $node["Schedule — Daily 6AM"].json()["day"] }}` (được tự động lấy ngày trong tuần).

##### **Node 5: OpenAI — GPT-4o-mini Model**
- **Chọn credential:** `openAiApi` (đã cài đặt API Key).
- **Không cần chỉnh sửa** (model đã được cài đặt là `gpt-4o-mini`).

##### **Node 7: HTTP — Generate Image Ideogram**
- **Thay thế API Key:**
  ```json
  "headers": {
    "Authorization": "Bearer REPLACE_WITH_IDEOGRAM_API_KEY"
  }
  ```
- **Cấu hình:**
  - `url`: `https://api.ideogram.ai/v1/images`
  - `body`: JSON mẫu (được tự động tạo từ AI).

##### **Node 9: HTTP — Post to Facebook**
- **Thay thế Access Token:**
  ```json
  "headers": {
    "Authorization": "Bearer REPLACE_WITH_FB_PAGE_ACCESS_TOKEN"
  }
  ```
- **Cấu hình:**
  - `url`: `https://graph.facebook.com/v23/[PAGE_ID]/feed` (thay `[PAGE_ID]` bằng ID Page của bạn).
  - **Lưu ý:** Đảm bảo Access Token có quyền `publish_pages`.

##### **Node 10: Google Sheets — Log Posted URL**
- **Chọn credential:** `googleSheetsOAuth2Api`.
- **Điền tham số:**
  - `Sheet ID`: ID của sheet log (có thể cùng sheet với node 2).
  - `Tab Name`: Tên tab log (ví dụ: `Log bài đăng`).
  - **Cột cần append:** `Timestamp`, `Domain ID`, `Link Type`, `Live URL`.

##### **Node 11: Wait — 1 Minute Rate Limit**
- **Không cần chỉnh sửa** (đã cấu hình 60 giây giữa các bài đăng để tránh bị chặn).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **1 row** trong Google Sheets và chạy **Test Tab**.
   - Kiểm tra:
     - AI có viết bài không?
     - Ideogram có tạo hình ảnh không?
     - Facebook có đăng bài thành công không?
     - Log có ghi URL không?
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hình ảnh Ideogram:**
   - Thử các **style khác nhau** trong prompt (ví dụ: "Phong cách minimalist", "Phong cách động vật").
   - Sử dụng **TURBO mode** để tiết kiệm chi phí.

2. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram** để thông báo khi bài đăng thành công/thất bại.

3. **Lưu log chi tiết:**
   - Thêm cột `Status` trong sheet log để ghi `Success/Failure` và `Error Message` (nếu có).

4. **Tăng tương tác với CTA:**
   - Thêm **link call-to-action** vào nội dung bài viết (ví dụ: "Xem chi tiết tại [link]").

5. **Sử dụng nhiều từ khóa cùng lúc:**
   - Nếu có nhiều từ khóa, **tăng số lượng batch** trong `SplitInBatches` (node 3).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp SEO và quản lý mạng xã hội, đồng thời **tăng hiệu quả** với nội dung tự động hóa và hình ảnh chuyên nghiệp. **Chỉ cần setup 1 lần**, sau đó **quên đi việc viết bài Facebook** hàng ngày!

**Bắt đầu ngay:**
1. Import workflow.
2. Cấu hình API Keys và Google Sheets.
3. **Bật Active** và xem workflow hoạt động như thế nào!

🚀 **Hãy tự động hóa ngay hôm nay và tập trung vào những việc quan trọng hơn!**