---
title: "🚀 Tự Động Nộp Sitemap URL Cho Google Indexing API & IndexNow - Giúp Website Rank Top Google Mới 10 Phút!"
description: "Workflow tự động hóa hoàn toàn không code để nộp tất cả URL từ sitemap.xml của bạn lên Google Indexing API và IndexNow của Bing, giúp trang web của các sếp được crawl và rank nhanh hơn trong vòng 24h. Giảm thời gian thủ công từ 8h xuống 0h!"
slug: "tu-dong-nop-sitemap-url-google-indexnow"
tags: [n8n, SEO, tự động hóa website, Google Indexing API, IndexNow, Oncrawl, sitemap, crawl optimization]
keywords: [n8n workflow SEO, tự động hóa nộp sitemap, IndexNow tự động, Google Indexing API tự động, Oncrawl API, tăng tốc crawl website, tự động hóa SEO]
---

# 🚀 **Tự Động Nộp Sitemap URL Cho Google & Bing - Giúp Website Rank Top Google Mới 10 Phút!**

## **💥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tải sitemap.xml** từ Oncrawl hoặc tự xây dựng từ trang web.
- **Chuyển đổi XML thành JSON** để nộp lên Google Indexing API.
- **Nộp từng URL một** lên Google Search Console và IndexNow của Bing (mỗi lần nộp tối đa 500 URL).
- **Chờ Google crawl** và cập nhật index, đôi khi mất **từ 1 ngày đến 1 tuần** mới thấy kết quả.

**Kết quả?** Trang web của các sếp **chậm rank**, mất thời gian quý giá để tối ưu SEO, và phải **lặp lại công việc này hàng tuần** để giữ vị trí trên Google.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tự động nộp tất cả URL** từ sitemap lên Google và Bing **mỗi khi có thay đổi mới** (không cần làm thủ công).
✅ **Giảm thời gian từ 8h xuống 0h** để nộp sitemap, giúp **crawl nhanh hơn 3-5 lần**.
✅ **Tối ưu hóa crawl** bằng cách chỉ nộp URL mới hoặc đã cập nhật trong **7 ngày gần nhất** (cấu hình được).
✅ **Kết hợp IndexNow (Bing) + Google Indexing API** để **crawl nhanh hơn trên cả hai công cụ**.
✅ **Lưu trữ log** để theo dõi trạng thái crawl của từng URL (nếu cần).

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                                                                 | **Liên Kết Đăng Ký**                                                                 |
|---------------------------|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Oncrawl**               | API Key (để lấy sitemap và dữ liệu crawl)                                              | [Đăng ký Oncrawl](https://www.oncrawl.com/)                                         |
| **Google Search Console** | Service Account (JSON Key) + Email Owner trong GSC                                  | [Tạo Service Account](https://console.cloud.google.com/iam-admin/serviceaccounts)     |
| **IndexNow (Bing)**       | API Key (để nộp URL lên Bing)                                                        | [Đăng ký IndexNow](https://www.bing.com/indexnow/getstarted)                         |
| **n8n Self-hosted**       | VPS (để chạy workflow 24/7)                                                          | 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N**) |

### **2. Cấu Hình Cần Điền**
Các biến quan trọng trong **node "Config"** (cần update theo yêu cầu):
```yaml
SITE_URL: "https://tênwebsite.com"  # Domain chính của bạn
SITEMAP_URL: "https://tênwebsite.com/sitemap.xml"  # Đường dẫn sitemap.xml
INDEXNOW_KEY: "abc123..."  # API Key từ Bing IndexNow
INDEXNOW_KEY_URL: "https://tênwebsite.com/<INDEXNOW_KEY>"  # Cấu trúc: domain + key
DAYS_BACK: 7  # Lấy URL mới/cập nhật trong 7 ngày gần nhất
BATCH_SIZE: 500  # Mỗi batch tối đa 500 URL (được IndexNow khuyến nghị)
USE_GOOGLE: true  # Bật/tắt nộp lên Google
USE_INDEXNOW: true  # Bật/tắt nộp lên Bing
```

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11837](https://n8n.io/workflows/11837) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên VPS của các sếp.
3. **Nhấn "Import"** và dán JSON vào.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ file tải xuống.
2. **Tạo workflow mới** trong n8n Editor.
3. **Nhấn "Import"** và dán JSON vào.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** vì kết hợp **Google Indexing API + IndexNow + Oncrawl**, nên các sếp **cần chú ý các node sau**:

#### **🔹 Node "Config" (Set)**
- **Cập nhật tất cả biến** như trong phần **Yêu cầu cần thiết** trên.
- **Không bỏ trống** `SITE_URL`, `SITEMAP_URL`, `INDEXNOW_KEY`, `INDEXNOW_KEY_URL`.

#### **🔹 Node "Gate: IndexNow" & "Gate: Google" (Code)**
- **Kiểm tra `USE_INDEXNOW` và `USE_GOOGLE`** trong Config.
- Nếu `USE_INDEXNOW=false`, workflow sẽ **bỏ qua phần nộp lên Bing**.

#### **🔹 Node "Build IndexNow payload" (Code)**
- **Không cần chỉnh sửa** (đã tối ưu sẵn cho IndexNow).
- Nếu muốn thay đổi định dạng payload, các sếp cần **hiểu JavaScript** và chỉnh sửa script.

#### **🔹 Node "Google Service Account API" (HTTP Request)**
- **Cấu hình Authentication**:
  - **Predefined credential type**: `Google Service Account API`.
  - **Credential Type**: `Google Service Account API`.
  - **Service Account Email**: Trích từ file JSON của Google.
  - **Private Key**: Dán từ file JSON.
  - **Scope**: `https://www.googleapis.com/auth/indexing`.
- **Kiểm tra quyền Owner** trong **Google Search Console** cho email service account.

#### **🔹 Node "Webhook" (Webhook)**
- **Cần thiết** để nhận thông báo từ Oncrawl khi crawl hoàn tất.
- **Cấu hình URL Webhook**:
  - Mở node **Webhook** → **HTTP Method**: `POST`.
  - **URL**: `https://<tên-VPS-của-bạn>/webhook` (đảm bảo VPS có domain và SSL).
- **Test Webhook**:
  - Gửi request POST từ Oncrawl (đã cấu hình trong **Oncrawl Dashboard**).

#### **🔹 Node "Filter: lastmod within DAYS_BACK" (Code)**
- **Lọc URL mới/cập nhật** trong `DAYS_BACK` ngày (mặc định 7 ngày).
- **Không cần chỉnh sửa** nếu muốn giữ mặc định.

#### **🔹 Node "Split In Batches (IndexNow ≤500)" (Split In Batches)**
- **Chia URL thành batch 500** (để IndexNow chấp nhận).
- **Không cần chỉnh sửa** nếu muốn giữ mặc định.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **log** để đảm bảo:
     - Oncrawl trả về sitemap XML.
     - Google Indexing API nhận được payload.
     - IndexNow (Bing) cũng nhận được URL.
2. **Bật Active**:
   - Sau khi test thành công, **đổi trạng thái workflow thành "Active"**.
   - **Cài đặt cron job** (nếu muốn chạy tự động hàng ngày):
     ```bash
     0 0 * * * curl -X POST http://<tên-VPS-của-bạn>/webhook/triggers/your-webhook-id
     ```

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Hợp với Slack/Telegram để Báo Lỗi**
- **Thêm node "Slack/Telegram"** sau node **Gate: Google** và **Gate: IndexNow**.
- **Cấu hình message**:
  ```json
  {
    "text": "🚨 Workflow Indexing Failed!\nURL: {{$node["Gate: Google"].json["url"]}}\nError: {{$node["Gate: Google"].json["error"]}}"
  }
  ```
- **Kết quả**: Các sếp **nhận thông báo ngay** khi có lỗi.

### **2. Lưu Log vào Google Sheets/Notion**
- **Thêm node "Google Sheets"** sau node **Check status**.
- **Cấu hình để lưu**:
  ```json
  {
    "url": "{{$json.url}}",
    "coverageState": "{{$json.coverageState}}",
    "lastCrawlTime": "{{$json.lastCrawlTime}}",
    "status": "{{$node["Gate: Google"].json["status"]}}"
  }
  ```
- **Kết quả**: Các sếp **theo dõi trạng thái crawl** của từng URL dễ dàng.

### **3. Chạy Workflow Hàng Ngày với Cron**
- **Cài đặt cron** trên VPS để chạy workflow mỗi ngày:
  ```bash
  0 8 * * * curl -X POST http://<tên-VPS-của-bạn>/webhook/triggers/your-webhook-id
  ```
- **Kết quả**: Workflow **tự động chạy** mỗi sáng 8h, nộp URL mới/cập nhật.

### **4. Tối Ưu Hóa cho Website Multi-Subdomain**
- **Cấu hình `SITEMAP_URL`** cho từng subdomain:
  ```yaml
  SITEMAP_URL_1: "https://sub1.tênwebsite.com/sitemap.xml"
  SITEMAP_URL_2: "https://sub2.tênwebsite.com/sitemap.xml"
  ```
- **Thêm node "Merge"** để kết hợp dữ liệu từ nhiều sitemap.

---
## **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề **nộp sitemap thủ công** cho Google và Bing, giúp:
✔ **Tiết kiệm 8h/tháng** cho các sếp.
✔ **Crawl nhanh hơn 3-5 lần** so với cách thủ công.
✔ **Tự động hóa SEO** một cách hoàn toàn không code.

**Hành động ngay hôm nay!**
1. **Cài đặt VPS** (n8n Self-hosted) với [TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N**).
2. **Import workflow** và **cấu hình API keys**.
3. **Bật Active** và **chạy test** để đảm bảo hoạt động.
4. **Kết hợp với Slack/Google Sheets** để theo dõi.

**🚀 Website của các sếp sẽ rank TOP Google trong vòng 24h!** 🚀

---
**🔗 Tài Liệu Tham Khảo:**
- [Google Indexing API Docs](https://developers.google.com/search/apis/indexing-api/v3)
- [IndexNow Bing Docs](https://www.bing.com/indexnow/getstarted)
- [Oncrawl API Docs](https://developer.oncrawl.com/)
- [Tutorial Google Indexing API](https://www.youtube.com/watch?v=HT56wExnN5k)