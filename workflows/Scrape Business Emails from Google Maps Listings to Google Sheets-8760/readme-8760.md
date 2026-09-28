---
title: "🚀 Tự Động Hoàn Chỉnh: Scrape Email Doanh Nghiệp từ Google Maps sang Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp scrape email doanh nghiệp từ danh sách Google Maps, lưu trữ vào Google Sheets để outreach marketing hiệu quả. Tiết kiệm 10+ giờ/tháng và giảm thiểu sai sót thủ công."
slug: "scrape-email-google-maps-sang-google-sheets"
tags: [n8n, automation, no-code, content-creation, email-scraping, google-maps, google-sheets]
keywords: [tự động hóa scrape email, n8n workflow google maps, lấy email từ google maps, tự động hóa outreach marketing, scrape website không cần code]
---

# 🚀 **Scrape Email Doanh Nghiệp từ Google Maps sang Google Sheets (Không Cần Code)**

Bạn đã bao giờ phải tốn **10+ giờ** để thủ công tìm kiếm email của các doanh nghiệp trên Google Maps, sau đó nhập vào Google Sheets để chuẩn bị cho chiến dịch outreach? Hay phải lo lắng về **sai sót, trùng lặp, hoặc mất thời gian** khi làm thủ công? **Workflow này giải quyết tất cả!**

Với **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình** từ việc scrape danh sách doanh nghiệp trên Google Maps, trích xuất email từ website của họ, đến lưu trữ vào Google Sheets – **một cách nhanh chóng, chính xác và không cần viết một dòng code nào!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần thủ công tìm kiếm email trên Google Maps.
- **Dữ liệu chính xác 100%**: Không trùng lặp, không sai sót như khi làm thủ công.
- **Cá nhân hóa outreach**: Sẵn sàng email danh sách doanh nghiệp mục tiêu cho chiến dịch marketing.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi cần (ví dụ: hàng tháng).
- **Không giới hạn quy mô**: Thích ứng với bất kỳ danh sách doanh nghiệp nào trên Google Maps.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** trống để lưu trữ kết quả (các sếp có thể tạo một sheet mới với các cột: `Website`, `Email`, `Business Name`).
   - **API Key OAuth2** của Google Sheets (cài đặt trong [n8n Credentials](https://n8n.io/docs/credentials/google-sheets/)).
2. **Khả năng truy cập Internet**: Workflow scrape trực tiếp từ Google Maps và website doanh nghiệp.
3. **Thời gian test**: Để điều chỉnh các tham số như **batch size** và **delay** để tránh bị chặn IP.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/8760) (hoặc sao chép JSON từ link trên).
- Trong **n8n Dashboard**, chọn **"Import"** > **"From JSON"** và dán nội dung JSON vào.
- **Hoặc** copy/paste JSON vào **n8n Editor** (nếu muốn chỉnh sửa trực tiếp).

---
### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **15 node** và được chia thành **4 bước chính**. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **🗺️ Bước 1: Scrape Google Maps**
- **Node**: `Scrape Google Maps` (HTTP Request)
  - **Tham số cần chỉnh**:
    - **URL**: Thay đổi từ `https://www.google.com/maps/search/Calgary+dentists` thành **danh sách doanh nghiệp mục tiêu** của các sếp (ví dụ: `https://www.google.com/maps/search/TP.HCM+café`).
    - **Headers**: Đảm bảo có `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).
    - **Method**: `GET`.

#### **🔗 Bước 2: Xử lý URL Website**
- **Node `Extract URLs` (Code)**:
  - **Lưu ý**: Node này sử dụng **regex** để trích xuất URL từ HTML. Các sếp **không cần chỉnh sửa mã** (n8n tự động chạy).
- **Node `Filter Google URLs` (Filter)**:
  - **Tham số**:
    - **Condition**: Lọc bỏ các URL chứa `google.com`, `gstatic.com`, `maps.googleapis.com`.
- **Node `Remove Duplicates`**:
  - **Lưu ý**: Deduplicate URL để tránh scrape trùng lặp.
- **Node `Limit`**:
  - **Tham số**: Đặt số lượng **batch** phù hợp (ví dụ: `10` để test, sau đó tăng lên `50-100` cho sản xuất).

#### **🔄 Bước 3: Scrape Website & Trích Xuất Email**
- **Node `Loop Over Items` (Split In Batches)**:
  - **Lưu ý**: Quá trình này **chạy từng website một** để tránh bị chặn IP.
- **Node `Wait1` và `Wait` (Wait)**:
  - **Tham số**: Thiết lập **delay** giữa các request (ví dụ: `5000ms` = 5 giây) để tránh bị chặn.
- **Node `Scrape Site` (HTTP Request)**:
  - **Lưu ý**: Node này tải HTML của website. Các sếp **không cần chỉnh sửa**, nhưng có thể thêm **headers** như `Accept-Language: en-US` để đảm bảo trích xuất email chính xác.
- **Node `Extract Emails` (Code)**:
  - **Lưu ý**: Node này sử dụng **regex** để tìm email trong HTML. **Không cần chỉnh sửa**, nhưng các sếp có thể kiểm tra log để đảm bảo trích xuất đúng.
- **Node `Filter Out Empties` (Filter)**:
  - **Tham số**: Lọc bỏ các website **không có email** (trống).
- **Node `Remove Duplicates (2)`**:
  - **Lưu ý**: Deduplicate email cuối cùng để tránh trùng lặp.

#### **📧 Bước 4: Lưu Email vào Google Sheets**
- **Node `Add to Sheet` (Google Sheets)**:
  - **Tham số cần chỉnh**:
    - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
    - **Operation**: `append` (thêm dữ liệu mới vào sheet).
    - **Sheet Name**: Đặt tên sheet (ví dụ: `Business Emails`).
    - **Range**: `Sheet1!A1` (đảm bảo sheet có cột `Website`, `Email`, `Business Name`).
  - **Lưu ý**: Nếu sheet chưa có cột, các sếp cần **tạo trước** hoặc chỉnh sửa `Range` để phù hợp.

---
### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **"Test"** trên node `When clicking ‘Test workflow’` (Manual Trigger).
   - Kiểm tra **log** để đảm bảo workflow chạy đúng:
     - Có scrape được URL từ Google Maps?
     - Email được trích xuất chính xác?
     - Dữ liệu được append vào Google Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN & MỞ RỘNG]
1. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tháng (ví dụ: `0 0 1 * *` = chạy vào ngày 1 hàng tháng).
2. **Gửi báo cáo qua Email/Slack**:
   - Thêm node **Email** hoặc **Slack** sau `Add to Sheet` để thông báo khi workflow hoàn thành.
   - Ví dụ: `n8n-nodes-base.email` với nội dung: *"Workflow scrape email thành công! Có [số lượng email] mới được thêm vào sheet."*
3. **Lọc doanh nghiệp theo ngành nghề**:
   - Thêm node **Filter** sau `Scrape Google Maps` để chỉ lấy doanh nghiệp có từ khóa cụ thể (ví dụ: `dentist`, `café`, `lawyer`).
4. **Lưu log scrape**:
   - Thêm node **HTTP Request** để gửi log scrape vào một **Google Drive** hoặc **Notion Database** để theo dõi lịch sử.
5. **Kết hợp với AI (LLM)**:
   - Sử dụng node **n8n-nodes-base.llm** (nếu có API OpenAI) để **tự động phân loại** doanh nghiệp theo ngành nghề từ tên website.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công mệt mỏi, đồng thời **cung cấp dữ liệu outreach chính xác** để tăng hiệu quả marketing. **Không cần code, không giới hạn quy mô** – chỉ cần **cài đặt và chạy**!

👉 **Bắt đầu ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test và bật Active** để tự động scrape email mỗi khi cần!

**Chúc các sếp thành công với chiến dịch outreach mới!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::