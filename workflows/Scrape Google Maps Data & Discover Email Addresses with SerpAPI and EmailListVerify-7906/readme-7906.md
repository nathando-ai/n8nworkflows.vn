---
title: "🚀 Tự Động Hoà Scrape Dữ Liệu Google Maps & Tìm Email Liên Lạc với SerpAPI & EmailListVerify (N8N)"
description: "Workflow tự động hóa scrape dữ liệu doanh nghiệp từ Google Maps, trích xuất email liên lạc thông qua SerpAPI và EmailListVerify - tiết kiệm thời gian lên đến 90% so với thủ công."
slug: "tieu-dong-hoa-scrape-google-maps-tim-email"
tags: [n8n, automation, lead-generation, serpapi, email-list-verify, google-maps-scraping]
keywords: [n8n workflow scrape google maps, tự động hóa tìm email doanh nghiệp, lead generation tự động, serpapi api, email list verify]
---

# 🚀 **Tự Động Hoà Scrape Dữ Liệu Google Maps & Tìm Email Liên Lạc (N8N)**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 90% thời gian** so với việc scrape thủ công từ Google Maps.
- **Lấy toàn bộ thông tin doanh nghiệp** (địa chỉ, điện thoại, website, rating, đánh giá) từ Google Maps **một cách chính xác và tự động**.
- **Tự động tìm kiếm email liên lạc** cho các doanh nghiệp có website thông qua API EmailListVerify.
- **Lưu trữ dữ liệu vào Google Sheets** để theo dõi và phân tích dễ dàng.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Scrape hàng trăm doanh nghiệp chỉ trong vài phút thay vì nhiều giờ.
✅ **Dữ liệu chính xác**: Trích xuất thông tin từ Google Maps một cách tự động, giảm sai sót.
✅ **Tìm kiếm email tự động**: Nếu doanh nghiệp có website, workflow sẽ tự động tìm kiếm email liên lạc.
✅ **Lưu trữ dữ liệu**: Tất cả thông tin được ghi vào Google Sheets, dễ dàng theo dõi và phân tích.
✅ **Hoạt động 24/7**: Cấu hình chạy định kỳ (tùy chọn hàng tuần) để cập nhật dữ liệu liên tục.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu scrape).
2. **API Key SerpAPI** (đăng ký miễn phí tại [serpapi.com](https://serpapi.com/)).
3. **API Key EmailListVerify** (đăng ký miễn phí tại [EmailListVerify.com](https://emailverify.io/)).
4. **Tài khoản n8n** (self-hosted hoặc dùng phiên bản cloud).
5. **File mẫu Google Sheets** (tải từ [đây](https://docs.google.com/spreadsheets/d/1d5m3tmmqM1TPL0fnrrbhaPdoXVs4EIrniDI-nv01UKg/edit?gid=0)).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [workflow gốc](https://n8n.io/workflows/7906) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7906) và paste vào n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **17 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình API Keys**
- **SerpAPI**:
  - Vào node **"SERPAPI - Scrape Google Maps URL"** → Thêm `serpApi` vào credentials.
  - Điền **API Key** từ SerpAPI vào `apiKey` trong `httpRequest` settings.

- **EmailListVerify**:
  - Vào node **"Use EmailListVerify API to find generic emails"** → Thêm `httpHeaderAuth` vào credentials.
  - Điền **API Key** từ EmailListVerify vào `Authorization` header.

#### **B. Cấu hình Google Sheets**
- **Node "Google Sheets - Get searches to scrap"**:
  - Chọn **credentials** là `googleSheetsOAuth2Api`.
  - Điền **Sheet Name** là `Searches` (tương ứng với file mẫu đã tải).

- **Node "Add rows in Google Sheets"**:
  - Chọn **credentials** là `googleSheetsOAuth2Api`.
  - Điền **Sheet Name** là `Scraped Data` (để lưu kết quả scrape).

#### **C. Cấu hình Schedule Trigger (Tùy chọn)**
- Node **"Run workflow once a week"** cho phép chạy tự động hàng tuần.
- Các sếp có thể điều chỉnh **frequency** (ví dụ: hàng ngày, hàng tháng) theo nhu cầu.

#### **D. Cấu hình Manual Trigger**
- Node **"When clicking 'Execute Workflow'"** cho phép chạy thủ công khi cần.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Điền **Google Maps URL** vào Google Sheets (Sheet `Searches`).
   - Chạy **Manual Trigger** để test.
   - Kiểm tra kết quả trong **Sheet `Scraped Data`**.

2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐT NHẤT]
- **Kết hợp với Slack/Telegram**: Gửi thông báo khi workflow hoàn thành bằng node **Slack** hoặc **Telegram Bot**.
- **Lưu log hoạt động**: Sử dụng node **HTTP Request** để gửi log đến một file CSV hoặc database.
- **Tự động gửi báo cáo**: Kết hợp với **Google Calendar** để gửi báo cáo hàng tuần.
- **Lọc dữ liệu**: Sử dụng node **Filter** để chỉ lấy doanh nghiệp có website hoặc rating cao.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc scrape dữ liệu Google Maps và tìm kiếm email liên lạc **không cần viết code**. Với chỉ vài bước cấu hình, các sếp có thể **tiết kiệm thời gian, tăng hiệu suất và nâng cao chất lượng dữ liệu**.

**Hãy áp dụng ngay và bắt đầu tự động hóa lead generation của mình!** 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi, hãy kiểm tra lại **API Key** và **credentials** của Google Sheets.
- Để workflow chạy ổn định 24/7, các sếp nên **self-host n8n** trên VPS.
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::