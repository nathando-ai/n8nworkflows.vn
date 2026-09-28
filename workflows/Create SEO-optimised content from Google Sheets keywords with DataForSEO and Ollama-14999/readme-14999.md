---
title: "🚀 Tự Động Hóa Viết Nội Dung SEO Tối Ưu Hóa Từ Từ Khóa Google Sheets Với AI Ollama & DataForSEO"
description: "Workflow này tự động tạo nội dung SEO tối ưu từ hàng trăm từ khóa trong Google Sheets, tích hợp SERP data và AI Ollama để đảm bảo chất lượng cao, tiết kiệm thời gian và tuân thủ Google Helpful Content Policy. Phù hợp cho chiến lược pSEO, viết blog hoặc nội dung sản phẩm."
slug: "tieu-dong-hoa-viet-noi-dung-seo-tu-tu-khoa-google-sheets"
tags: [n8n, automation, no-code, ai-rag, seo, content-creation, ollama, google-sheets]
keywords: [n8n workflow seo, tự động hóa viết bài blog, ai viết nội dung seo, ollama n8n, dataforseo api, content creation seo]
---

# 🚀 **Tự Động Hóa Viết Nội Dung SEO Tối Ưu Hóa Từ Từ Khóa (Không Cần Code)**

### **Giải pháp cho các sếp muốn viết nội dung SEO chất lượng cao, nhanh chóng và không tốn chi phí API**
Bạn có một chiến lược SEO *programmatic* với hàng nghìn từ khóa? Hay đang gặp khó khăn trong việc tạo nội dung *helpful* mà vẫn tuân thủ chính sách của Google? Với workflow này, các sếp có thể **tự động hóa toàn bộ quy trình viết nội dung SEO** từ việc phân tích SERP đến tạo bài viết hoàn chỉnh, chỉ với một nhấp chuột!

Workflow này kết hợp **Google Sheets** (để quản lý từ khóa), **DataForSEO API** (để lấy dữ liệu SERP), và **AI Ollama** (để viết nội dung) để:
✅ **Tạo nội dung SEO tối ưu** từ hàng trăm từ khóa trong một sheet.
✅ **Tích hợp SERP data** (top results, AI overviews, PAA, related searches) để nội dung phù hợp với yêu cầu thực tế.
✅ **Chạy trên máy chủ riêng** (self-hosted) với Ollama, tiết kiệm chi phí API.
✅ **Cập nhật tự động** vào Google Sheets, không cần can thiệp thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Viết nội dung SEO cho hàng trăm từ khóa chỉ trong vài phút.
- **Nội dung chất lượng cao**: AI Ollama đảm bảo tính độc đáo, SEO-friendly và tuân thủ Google Helpful Content Policy.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động 24/7.
- **Tiết kiệm chi phí**: Sử dụng Ollama (máy chủ riêng) thay vì API đắt tiền.
- **Cập nhật liên tục**: Dữ liệu SERP được lấy mới mỗi lần chạy workflow.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** với sheet có **2 cột**:
   - **Keyword** (danh sách từ khóa cần viết nội dung).
   - **Output** (để lưu kết quả nội dung).

✔ **Tài khoản DataForSEO** (đăng ký với email công ty để nhận **5 USD credit miễn phí**).
   - [Trang đăng ký DataForSEO](https://dataforseo.com/blog/a-kickstart-guide-to-using-dataforseo-apis)
   - **API Key** của DataForSEO (để cấu hình trong node HTTP Request).

✔ **Ollama cài đặt trên máy chủ VPS** (self-hosted) với mô hình `llama3.2:latest`.
   - [Hướng dẫn cài Ollama](https://docs.ollama.com/quickstart)
   - **Yêu cầu hệ thống**: M1/M2 Chip + 16GB RAM (đủ để chạy hiệu quả).

✔ **MongoDB Atlas** (miễn phí) để lưu trữ bộ nhớ chat của AI.
   - [Hướng dẫn kết nối MongoDB với n8n](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.mongodb/)
   - **Connection String** của MongoDB (để cấu hình trong node `MongoDB Chat Memory`).

✔ **Google Sheets OAuth 2.0 Credentials** (để n8n có quyền truy cập sheet).
   - [Hướng dẫn tạo OAuth 2.0](https://developers.google.com/sheets/api/quickstart/python)
---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **Workflow Editor**.
2. Nhấp vào **Import Workflow** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/14999)).
3. **Kích hoạt workflow** sau khi import xong.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần cấu hình gì**, chỉ cần nhấn **Execute Workflow** để chạy.

#### **🔹 Node 2: MongoDB Chat Memory**
- **Credentials**: Chọn `mongoDb` (đã cấu hình trước trong n8n).
- **Lưu ý**:
  - Nếu chưa có, tạo **MongoDB Atlas** miễn phí và lấy **Connection String**.
  - Cấu hình trong **n8n Settings > Credentials > Add MongoDB**.

#### **🔹 Node 3: Ollama Chat Model**
- **Model**: Đặt là `llama3.2:latest` (đã cài trên Ollama).
- **Lưu ý**:
  - Ollama phải chạy trên **VPS riêng** (self-hosted) để workflow hoạt động 24/7.
  - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**
  - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**

#### **🔹 Node 4: Fetch Rows from Google Sheets**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình OAuth 2.0).
- **Sheet Name**: Đặt tên sheet của các sếp.
- **Range**: Đặt là `Sheet1!A:B` (cột Keyword và Output).
- **Lưu ý**:
  - Sheet phải có **2 cột**: `Keyword` và `Output`.
  - Nếu `Output` trống, workflow sẽ tự động bỏ qua (do node Filter sau).

#### **🔹 Node 5: Filter rows that are already populated**
- **Condition**: `$.Output === null` (lọc chỉ các hàng chưa có nội dung).
- **Lưu ý**:
  - Nếu `Output` không trống, hàng đó sẽ bị bỏ qua (tránh viết lại).

#### **🔹 Node 6: Fetch SERP Results + AI Mode Answers (HTTP Request)**
- **URL**: `https://api.dataforseo.com/v1/search`
- **Headers**:
  - `Authorization`: `Bearer <API_KEY>` (thay `<API_KEY>` bằng API Key của DataForSEO).
  - `Content-Type`: `application/json`
- **Body (JSON)**:
  ```json
  {
    "keyword": "{{$node["Loop Over Items"].json["$.Keyword"]}}",
    "country": "US",
    "language": "en",
    "limit": 10,
    "mode": "ai"
  }
  ```
- **Lưu ý**:
  - **DataForSEO miễn phí 5 USD credit** cho tài khoản doanh nghiệp.
  - Nếu API trả về **status code != 200**, workflow sẽ **báo lỗi vào Google Sheets** (do node `Error Handling`).

#### **🔹 Node 7: Compile SERP Data into one Output for Prompt (Code)**
- **Code**:
  ```javascript
  return {
    keyword: $input.all()[0].json.keyword,
    serp_data: $input.all()[0].json.data,
    prompt: `Write a SEO-optimized blog post for the keyword "${$input.all()[0].json.keyword}" using the following SERP data:
    - Top 10 search results: ${JSON.stringify($input.all()[0].json.data.results)}
    - AI Overviews: ${JSON.stringify($input.all()[0].json.data.ai_overview)}
    - People Also Ask: ${JSON.stringify($input.all()[0].json.data.people_also_ask)}
    - Related Searches: ${JSON.stringify($input.all()[0].json.data.related_searches)}
    Ensure the content is unique, engaging, and follows Google's Helpful Content guidelines.`
  };
  ```
- **Lưu ý**:
  - Node này **tạo prompt** cho AI Ollama dựa trên dữ liệu SERP.

#### **🔹 Node 8: Compose SEO-optimised Content (Agent)**
- **Model**: Chọn `Ollama Chat Model` (đã cấu hình trước).
- **Prompt**: Sử dụng **prompt** từ node `Compile SERP Data`.
- **Lưu ý**:
  - AI Ollama sẽ **viết nội dung SEO** dựa trên SERP data.
  - **Tối ưu hóa**: Các sếp có thể chỉnh sửa **prompt** để phù hợp với ngành nghề.

#### **🔹 Node 9: Clean output (Code)**
- **Code**:
  ```javascript
  return {
    html: $input.all()[0].json.output.html,
    keyword: $input.all()[0].json.keyword
  };
  ```
- **Lưu ý**:
  - Node này **làm sạch output** và chuyển sang định dạng HTML.

#### **🔹 Node 10: Update Row with HTML Output (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Operation**: `update`.
- **Range**: `Sheet1!B2` (đặt theo cột `Output` của sheet).
- **Value**: `{{$node["Clean output"].json["$.html"]}}`.
- **Lưu ý**:
  - **Không quên kiểm tra cột `Keyword`** để đảm bảo cập nhật đúng hàng.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**: Chạy workflow với **1-2 từ khóa mẫu** để kiểm tra kết quả.
2. **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
- **Gửi kết quả vào Slack/Telegram**: Sử dụng node `webhook` để thông báo khi workflow hoàn thành.
- **Lưu log hoạt động**: Sử dụng node `stickyNote` để ghi lại lỗi hoặc thành công.
- **Chạy định kỳ**: Sử dụng **n8n Cron Trigger** để tự động chạy workflow hàng ngày/tuần.
- **Tối ưu Ollama**: Nếu có nhiều từ khóa, các sếp có thể **tăng RAM** hoặc sử dụng mô hình nhỏ hơn như `llama3:8b`.
- **Tích hợp Google Analytics**: Theo dõi hiệu suất của nội dung vừa viết.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa viết nội dung SEO** mà không cần code. Với **Ollama (self-hosted)**, **DataForSEO (miễn phí 5 USD)**, và **Google Sheets**, các sếp có thể:
✔ **Tiết kiệm thời gian** viết nội dung cho hàng trăm từ khóa.
✔ **Đảm bảo chất lượng SEO** với dữ liệu SERP thực tế.
✔ **Hoạt động 24/7** trên VPS riêng.

**🚀 Hãy thử ngay và tự động hóa nội dung SEO của mình!**
Nếu có vấn đề, các sếp có thể **comment dưới bài viết** hoặc liên hệ qua [n8n Community](https://community.n8n.io/).

---
:::note[CHÚ Ý CUỐI CUNG]
- **Không sử dụng API Key DataForSEO công khai** (có thể bị chặn).
- **Ollama phải chạy liên tục** trên VPS để workflow hoạt động.
- **Google Sheets phải có quyền truy cập** cho n8n.
:::