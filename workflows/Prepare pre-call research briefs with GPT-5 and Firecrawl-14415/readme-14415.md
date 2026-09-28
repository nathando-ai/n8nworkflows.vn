---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Nghiên Cứu Trước Cuộc Gọi với GPT-5 và Web Scraping (Không Cần Code)"
description: "Workflow tự động hóa nghiên cứu trước cuộc gọi với GPT-5 và Firecrawl, giúp các sếp tiết kiệm 10+ giờ/tháng chuẩn bị báo cáo chi tiết, cá nhân hóa cho từng khách hàng. Kết quả: Cuộc gọi chuyên nghiệp, thông tin cập nhật và hiệu quả cao."
slug: "tieu-dong-hoan-thanh-bao-cao-nghien-cuu-truoc-cuoc-goi-gpt-5"
tags: [n8n, automation, market-research, ai-summarization, google-drive, slack-integration]
keywords: [n8n workflow nghiên cứu trước cuộc gọi, tự động hóa báo cáo GPT-5, web scraping cho doanh nghiệp, tự động hóa cuộc gọi bán hàng, n8n + Firecrawl]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Nghiên Cứu Trước Cuộc Gọi với GPT-5 và Web Scraping**

### **Giải pháp cho vấn đề:**
Các sếp thường mất **30-60 phút/tuần** để chuẩn bị báo cáo nghiên cứu trước cuộc gọi với khách hàng. Thông tin thường **lặp lại, không cập nhật** và thiếu **cá nhân hóa**. Kết quả là cuộc gọi trở nên **chán ngấy, thiếu chuyên nghiệp** và mất thời gian.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Tự động lấy lịch Google Calendar** để xác định cuộc gọi sắp diễn ra.
✅ **Scrape thông tin mới nhất** về khách hàng từ web (Firecrawl).
✅ **Sử dụng GPT-5** để tổng hợp báo cáo ngắn gọn, chuyên nghiệp.
✅ **Lưu báo cáo vào Google Drive** và **gửi thông báo Slack** để toàn bộ team biết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** chuẩn bị báo cáo thủ công.
- **Báo cáo luôn cập nhật** với thông tin mới nhất từ web.
- **Cá nhân hóa hoàn toàn** cho từng khách hàng.
- **Cuộc gọi chuyên nghiệp hơn** với thông tin chi tiết, mở câu hỏi thông minh.
- **Hoạt động tự động 24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (để lấy lịch cuộc gọi).
✔ **Tài khoản Google Drive** và **folder "CLIENTS"** (để lưu báo cáo).
✔ **Tài khoản Slack** và **channel #ops** (để thông báo).
✔ **API Key OpenAI** (để sử dụng GPT-5).
✔ **API Key Firecrawl** (để scrape thông tin khách hàng).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14415](https://n8n.io/workflows/14415) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14415) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Schedule Trigger (Định giờ chạy)**
- Node **"Daily 4PM Trigger"** sẽ chạy **mỗi ngày lúc 16:00**.
- **Lưu ý:** Nếu muốn chạy vào giờ khác, chỉnh **`cron`** trong node này thành:
  ```json
  "cron": "0 10 * * *"  // Ví dụ: 10:00 sáng
  ```

##### **B. Cấu hình Google Calendar (Lấy lịch cuộc gọi)**
- Node **"Fetch Calendar Events"** cần **credentials `googleCalendarOAuth2Api`**.
- **Lưu ý:**
  - Chọn **folder Calendar** chứa lịch cuộc gọi.
  - **Lọc theo keyword** (`discovery`, `call`, `meeting`, `NCA`) để xác định cuộc gọi cần brief.
  - **Bỏ qua** các cuộc gọi đã brief trước.

##### **C. Cấu hình Agent + GPT-5 (Tạo báo cáo)**
- Node **"Research Brief Generator"** sử dụng **Agent + GPT-5 Mini (`cx/gpt-5.5`)**.
- **Lưu ý:**
  - **Prompt mặc định** đã được tối ưu, nhưng các sếp có thể **cập nhật** trong node **"GPT-5 Mini Model"** để phù hợp với phong cách của team.
  - **Output Parser** sẽ chuyển kết quả thành **schema chuẩn** (background, opening questions, etc.).

##### **D. Cấu hình Firecrawl (Scrape thông tin khách hàng)**
- Node **"Scrape Web Pages"** sử dụng **Firecrawl API**.
- **Lưu ý:**
  - **Resource `MapSearch`** sẽ tìm kiếm **website chính thức** của khách hàng.
  - **Tham số `query`** có thể chỉnh sửa để tìm kiếm **tên công ty + ngành nghề**.

##### **E. Cấu hình Google Drive (Lưu báo cáo)**
- Node **"Save Brief to Drive"** sẽ tạo **folder mới** nếu chưa có (`"CLIENTS"`).
- **Lưu ý:**
  - **Folder "CLIENTS"** phải được **chọn trong credentials `googleDriveOAuth2Api`**.
  - **Tên file** sẽ tự động tạo theo **format: `ClientName_Brief_YYYYMMDD.txt`**.

##### **F. Cấu hình Slack (Thông báo)**
- Node **"Notify Ops Channel"** sẽ gửi **tóm tắt báo cáo + link Drive** vào **#ops**.
- **Lưu ý:**
  - **Channel Slack** phải được **chọn trong credentials `slackApi`**.
  - **Thông báo mẫu** có thể chỉnh sửa trong node này.

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy **manual test** với một cuộc gọi mẫu để kiểm tra kết quả.
- **Bật Active:** Sau khi kiểm tra, **bật workflow** để chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Zoom/Teams:** Sử dụng **n8n-nodes-zoom** để tự động **tạo ghi chú cuộc gọi** từ báo cáo.
2. **Lưu log vào Google Sheets:** Thêm node **Google Sheets** để **theo dõi lịch sử brief**.
3. **Gửi báo cáo qua Email:** Sử dụng **n8n-nodes-email** để tự động **gửi báo cáo cho khách hàng**.
4. **Cập nhật Firecrawl API Key:** Nếu Firecrawl có **gói premium**, có thể **tăng số lượng scrape** để lấy thông tin chi tiết hơn.
5. **Tối ưu GPT-5:** Nếu muốn **báo cáo dài hơn**, thay đổi **model** trong node `"GPT-5 Mini Model"` thành `gpt-4` (nếu có budget).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **cuộc gọi thực tế** thay vì chuẩn bị báo cáo. **Tự động hóa 100% không cần code**, kết hợp **AI + Web Scraping + Google Drive + Slack** để tạo **báo cáo chuyên nghiệp, cá nhân hóa và cập nhật**.

**🚀 Hãy import ngay và thử nghiệm!** Nếu có vấn đề, **comment bên dưới** hoặc liên hệ admin để hỗ trợ.

---
**#TựĐộngHóa #N8N #AI #MarketResearch #DoanhNhânHiệuQuả**