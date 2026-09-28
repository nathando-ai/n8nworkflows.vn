---
title: "🚀 Tự Động Hóa Tìm Kiếm & Trích Xuất Dữ Liệu B2B Từ Google Maps Sang Google Sheets (Không Cần Code)"
description: "Workflow này tự động hóa việc tìm kiếm, lọc và trích xuất thông tin doanh nghiệp (B2B leads) từ Google Maps, sau đó lưu vào Google Sheets với email tự động. Giúp các sếp tiết kiệm thời gian lên tới 20 giờ/tuần trong việc nghiên cứu thị trường và xây dựng danh sách khách hàng tiềm năng."
slug: "tieu-dung-b2b-tu-google-maps-sang-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, hasdata, no-code]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm B2B, trích xuất dữ liệu Google Maps, lưu dữ liệu vào Google Sheets, HasData API, tự động hóa bán hàng B2B]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Trích Xuất Dữ Liệu B2B Từ Google Maps Sang Google Sheets**

## **🔍 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường B2B**
Hàng ngày, các sếp và đội ngũ marketing phải mất **từ 10-20 giờ** để:
- Tìm kiếm doanh nghiệp tiềm năng trên Google Maps thủ công.
- Lọc thông tin như địa chỉ, website, email, số điện thoại.
- Lưu trữ dữ liệu vào Google Sheets hoặc Excel để phân tích.
- Xử lý trùng lặp và thiếu thông tin liên lạc.

Kết quả? **Thời gian quý giá bị lãng phí**, dữ liệu không đồng bộ, và khả năng chuyển đổi thấp do thiếu thông tin chi tiết.

**Workflow này giải quyết tất cả vấn đề đó bằng cách:**
✅ **Tự động hóa 100% quá trình tìm kiếm** trên Google Maps.
✅ **Trích xuất thông tin chi tiết** (website, email, số điện thoại) từ trang web của doanh nghiệp.
✅ **Lọc bỏ trùng lặp** và **cập nhật liên tục** vào Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 15-20 giờ/tuần** cho việc nghiên cứu thị trường.
- **Dữ liệu chính xác và đồng bộ**, không bị thiếu hoặc sai sót.
- **Tự động cập nhật** khi có thay đổi mới trên Google Maps.
- **Dễ dàng phân tích** với Google Sheets (sắp xếp, lọc, export).
- **Không cần kỹ năng code** – chỉ cần cấu hình API và Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets và API).
2. **API Key của HasData** (dùng để trích xuất dữ liệu từ Google Maps và website).
   - 👉 [Đăng ký API HasData miễn phí](https://hasdata.com/) (có giới hạn miễn phí).
3. **Google Sheet mẫu** (để lưu cấu hình và kết quả).
4. **VPS (nếu muốn chạy 24/7)** – Để workflow hoạt động liên tục.
   :::info[**Gợi ý hạ tầng cho n8n**]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải workflow từ link gốc**: [Scrape B2B Leads from Google Maps](https://n8n.io/workflows/15653).
- **Import vào n8n**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON từ link trên.
  3. Chọn **Create New Workflow** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: "Start Lead Generation" (Manual Trigger)**
- **Cách hoạt động**: Workflow được kích hoạt thủ công.
- **Lưu ý**: Đảm bảo **Manual Trigger** được bật (**Active**).

#### **🔹 Node 2 & 3: "Create Leads Sheet" & "Read Configurations" (Google Sheets)**
- **Yêu cầu**:
  - Các sếp phải **cấu hình OAuth 2.0** cho Google Sheets trong **Credentials**.
  - **Google Sheet mẫu** phải có **2 sheet**:
    1. **"Config"** (để lưu cấu hình tìm kiếm).
    2. **"Leads"** (để lưu kết quả).
  - **Cấu trúc Config Sheet**:
    | Key          | Value (Dùng để tìm kiếm) |
    |--------------|--------------------------|
    | `location`   | "Hà Nội" hoặc "TP.HCM"   |
    | `keyword`    | "Công ty marketing"      |
    | `max_results`| 50                       |

#### **🔹 Node 4: "Initialize Search Tasks" (Code)**
- **Lưu ý**: Node này **không cần chỉnh sửa** (n8n tự động xây dựng query từ Config Sheet).

#### **🔹 Node 5 & 11: "Search in Google Maps" & "Find Emails Via Google" (HasData)**
- **Yêu cầu**:
  - **API Key HasData** phải được thêm vào **Credentials** (tên: `hasDataApi`).
  - **Resource**:
    - Node 5: `google_maps` (tìm kiếm doanh nghiệp).
    - Node 11: `google_search` (tìm kiếm email từ website).
  - **Lưu ý**:
    - HasData có **giới hạn miễn phí** (khoảng 1000 request/tháng).
    - Nếu vượt quá, cần **upgrade plan**.

#### **🔹 Node 6: "Split Local Results" (SplitOut)**
- **Cách hoạt động**: Chia dữ liệu thành các batch nhỏ để xử lý hiệu quả.

#### **🔹 Node 7: "Deduplicate Local Results" (RemoveDuplicates)**
- **Lưu ý**: Node này **xóa trùng lặp** dựa trên **ID doanh nghiệp** (Google Maps ID).

#### **🔹 Node 8 & 9: "Check Website Availability" & "Scrape Website Data" (If + HasData)**
- **Yêu cầu**:
  - Nếu doanh nghiệp có **website**, workflow sẽ **trích xuất email** từ trang chủ.
  - Nếu không có website, sẽ **bỏ qua** và lưu thông tin cơ bản.

#### **🔹 Node 10 & 12: "Check for Emails" & "Extract Emails" (If + Code)**
- **Lưu ý**:
  - Node **Extract Emails** sử dụng **regex** để tìm email từ trang web.
  - Nếu không tìm thấy email, sẽ lưu **null** trong cột `email`.

#### **🔹 Node 13 & 15: "Format Lead With Contact" & "Format Lead Without Contact" (Set)**
- **Cách hoạt động**:
  - Nếu có email → Lưu vào **Leads With Contact**.
  - Nếu không có email → Lưu vào **Leads Without Contact**.

#### **🔹 Node 14 & 16: "Merge Leads for Google Search" & "Combine All Leads" (Merge)**
- **Lưu ý**: Node này **ghép dữ liệu** từ các nguồn khác nhau trước khi lưu vào Google Sheets.

#### **🔹 Node 17: "Append to Leads Sheet" (Google Sheets)**
- **Yêu cầu**:
  - Chọn **sheet "Leads"** để **append** (thêm mới) dữ liệu.
  - **Cấu trúc dữ liệu tự động**:
    | Name          | Website       | Email          | Phone          | Google Maps ID |
    |---------------|---------------|----------------|----------------|----------------|
    | Công ty ABC   | abc.com       | abc@abc.com    | 0123456789     | ID_123         |

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả trong **Google Sheet**.
2. **Bật Active**:
   - Đảm bảo tất cả **Credentials** (Google Sheets + HasData) được cấu hình đúng.
   - Nhấn **Active** để workflow chạy tự động khi kích hoạt thủ công.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Kích Hoạt Hàng Ngày**
- Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày/lần tuần**.
- **Cách cấu hình**:
  ```json
  {
    "type": "n8n-nodes-base.cron",
    "name": "Daily Lead Update",
    "options": {
      "cronExpression": "0 0 * * *" // Chạy lúc 00:00 hàng ngày
    }
  }
  ```

### **2. Gửi Báo Cáo Định Kỳ Về Slack/Email**
- Thêm **Node Slack** hoặc **Node Email** để báo cáo kết quả:
  ```json
  {
    "name": "Notify Result",
    "type": "n8n-nodes-base.slack",
    "credentials": {
      "slackApiToken": "YOUR_SLACK_TOKEN"
    },
    "options": {
      "message": "🚀 Đã cập nhật {{ $node["Append to Leads Sheet"].json["$.length"] }} leads mới vào Google Sheets!"
    }
  }
  ```

### **3. Lưu Log Dữ Liệu**
- Thêm **Node Log** để theo dõi lỗi và tiến trình:
  ```json
  {
    "name": "Log Results",
    "type": "n8n-nodes-base.log"
  }
  ```

### **4. Tăng Cường Dữ Liệu Bằng API Khác**
- Nếu cần **số điện thoại**, có thể kết hợp với **API Truecaller** hoặc **API số điện thoại Việt Nam**.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì việc **nhập liệu thủ công**. Với **n8n + HasData**, các sếp có thể:
✔ **Tìm kiếm và trích xuất dữ liệu B2B một cách tự động**.
✔ **Lưu trữ và phân tích** trên Google Sheets.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Đăng ký API HasData** (miễn phí).
2. **Cài đặt n8n trên VPS** (nếu muốn chạy liên tục).
3. **Import workflow** và **cấu hình Google Sheets**.
4. **Kích hoạt và theo dõi kết quả!**

👉 **[Tải workflow ngay](https://n8n.io/workflows/15653)** và bắt đầu tự động hóa nghiên cứu thị trường của bạn! 🚀