---
title: "🚀 Tự Động Hóa Email Tóm Tắt Thông Tin Hàng Ngày Từ Dữ Liệu Web Cấu Trúc Với Firecrawl + OpenAI"
description: "Workflow này tự động trích xuất và tóm tắt nội dung từ bất kỳ trang web nào (không cần API) hàng ngày, sau đó gửi kết quả qua email với AI. Giúp các sếp tiết kiệm thời gian theo dõi thị trường, cạnh tranh và thông tin quan trọng mà không cần viết một dòng code."
slug: "tieu-dong-hoa-email-tom-tat-thong-tin-hang-ngay"
tags: [n8n, automation, marketing, web-scraping, ai-summarization, gmail-automation]
keywords: [n8n workflow web scraping, tự động hóa email hàng ngày, firecrawl n8n, openai tóm tắt nội dung, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Thông Tin Hàng Ngày Từ Web Với Firecrawl + OpenAI**

### **🔍 Nỗi Đau Của Các Sếp**
Bạn có phải là một **giám đốc marketing**, **người phân tích thị trường**, **founder startup** hay **người nghiên cứu cạnh tranh** phải mất **giờ đồng hồ** mỗi ngày để:
- **Tìm kiếm và đọc** thông tin từ nhiều trang web khác nhau?
- **Lọc và tóm tắt** những điểm quan trọng trong nội dung dài?
- **Ghi chép và gửi báo cáo** cho đồng nghiệp hoặc bản thân?

Với **tự động hóa hoàn toàn**, bạn có thể **ngủ yên** mỗi đêm, biết rằng **n8n** sẽ tự động:
✅ **Trích xuất** dữ liệu từ bất kỳ trang web nào (không cần API).
✅ **Tóm tắt** nội dung bằng **OpenAI** với prompt tùy chỉnh.
✅ **Gửi email** kết quả vào hộp thư của bạn **mỗi ngày**.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 5-10 giờ/tuần** theo dõi thị trường, cạnh tranh và tin tức.
- **Nội dung được tóm tắt chính xác** bởi AI, không bỏ sót chi tiết quan trọng.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa** với prompt AI tùy chỉnh theo nhu cầu của bạn.
- **Không cần viết code** – chỉ cần cấu hình và chạy.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Firecrawl** (để trích xuất dữ liệu web):
   - [Đăng ký miễn phí Firecrawl](https://www.firecrawl.io/) (có phiên bản free với giới hạn request).
   - **Lấy API Key** từ dashboard và lưu vào **Credentials** của n8n.

2. **Tài khoản Gmail** (để nhận email kết quả):
   - **Enable Gmail API** và tạo **OAuth 2.0 Credentials** (hướng dẫn [tại đây](https://developers.google.com/gmail/api/quickstart/python)).
   - **Lưu OAuth Client ID/Secret** vào **Credentials** của n8n.

3. **Tài khoản OpenAI** (để tóm tắt nội dung):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - **Lưu API Key** vào **Credentials** của n8n.

4. **URL trang web** bạn muốn trích xuất (ví dụ: `https://example.com/news`).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4654](https://n8n.io/workflows/4654) (chọn **Download JSON**).
2. **Mở n8n Editor** trên máy chủ của bạn.
3. Nhấn **Import Workflow** và chọn file JSON vừa tải.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/4654](https://n8n.io/workflows/4654).
2. Trong **n8n Editor**, nhấn **Import Workflow** → **Paste JSON**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node** chính, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

#### **🔹 Node 1: Schedule Trigger (Động cơ kích hoạt hàng ngày)**
- **Cấu hình:**
  - **Frequency:** `Daily` (lựa chọn **8:00 AM** hoặc thời gian phù hợp).
  - **Time Zone:** Chọn múi giờ của bạn (ví dụ: `Asia/Ho Chi Minh`).
- **Lưu ý:** Nếu muốn chạy **ngày nào cũng khác**, có thể sử dụng **Cron Expression** như `0 8 * * *`.

#### **🔹 Node 2: POST Request (Gửi yêu cầu đến Firecrawl)**
- **Tham số cần điền:**
  - **Method:** `POST`
  - **URL:** `https://api.firecrawl.io/v1/extract`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_FIRECRAWL_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "url": "https://example.com/news",  // Thay đổi URL này
      "selectors": ["*"]  // Chọn tất cả các phần tử (có thể tùy chỉnh)
    }
    ```
- **Lưu ý:**
  - **Thay đổi `YOUR_FIRECRAWL_API_KEY`** bằng API Key của bạn.
  - **Thay đổi URL** thành trang web bạn muốn trích xuất.
  - **Thời gian chờ (Wait 60s)** sau node này để Firecrawl hoàn thành trích xuất.

#### **🔹 Node 3: OpenAI (Tóm tắt nội dung bằng AI)**
- **Tham số cần điền:**
  - **Model:** `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).
  - **Prompt (tùy chỉnh):**
    ```plaintext
    Tóm tắt nội dung dưới đây thành 3 điểm chính:
    1. Tin tức mới nhất về [ngành/nội dung].
    2. Thông tin quan trọng nhất cần lưu ý.
    3. Kết luận và ý kiến cá nhân của bạn.

    Nội dung:
    {{ $json["data"]["html"] }}
    ```
  - **Lưu ý:**
    - **Thay đổi prompt** để phù hợp với nhu cầu của bạn (ví dụ: tóm tắt cho **marketing**, **kinh doanh**, **cạnh tranh**).
    - **Kiểm tra `$json["data"]["html"]`** trong **Sticky Note** để đảm bảo dữ liệu trích xuất đúng.

#### **🔹 Node 4: Gmail (Gửi email kết quả)**
- **Tham số cần điền:**
  - **Credentials:** Chọn **Gmail OAuth 2.0** đã cấu hình trước.
  - **To:** Email của bạn (hoặc nhóm email).
  - **Subject:** `Daily Insight - {{ $json["data"]["url"] }}`
  - **Body (HTML):**
    ```html
    <h2>Tóm tắt thông tin hàng ngày</h2>
    <p><strong>Trang web:</strong> {{ $json["data"]["url"] }}</p>
    <p><strong>Nội dung:</strong></p>
    {{ $json["data"]["summary"] }}  <!-- Dữ liệu từ OpenAI -->
    ```
- **Lưu ý:**
  - **Kiểm tra email** sau khi chạy test để đảm bảo nội dung hiển thị đúng.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run (Chạy thử):**
   - Nhấn **Run Workflow** và kiểm tra:
     - Firecrawl có trích xuất dữ liệu không?
     - OpenAI có tóm tắt đúng không?
     - Email có gửi đến đúng không?

2. **Bật Active:**
   - Sau khi kiểm tra thành công, **bật switch Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hiệu Quả**]
1. **Tùy chỉnh prompt OpenAI:**
   - Nếu bạn theo dõi **thị trường chứng khoán**, có thể viết prompt:
     ```plaintext
     Tóm tắt tin tức về [công ty] trong 3 điểm:
     1. Thay đổi giá cổ phiếu và lý do.
     2. Tin tức mới nhất về sản phẩm/dịch vụ.
     3. Dự báo xu hướng trong 3 tháng tới.
     ```

2. **Gửi email định kỳ cho nhiều người:**
   - Sử dụng **Gmail Merge** để gửi cùng một email cho nhiều người:
     ```json
     "to": ["email1@example.com", "email2@example.com"]
     ```

3. **Lưu log vào Google Sheets:**
   - Thêm **Google Sheets Node** sau OpenAI để ghi lại lịch sử tóm tắt:
     ```json
     {
       "sheetName": "Daily Insights",
       "data": {
         "URL": "{{ $json["data"]["url"] }}",
         "Summary": "{{ $json["data"]["summary"] }}",
         "Date": "{{ $json["date"] }}"
       }
     }
     ```

4. **Kết hợp với Slack/Telegram:**
   - Thay vì email, có thể gửi kết quả qua **Slack Webhook** hoặc **Telegram Bot** để thông báo tức thời.

5. **Chạy nhiều URL cùng lúc:**
   - Sử dụng **Loop Node** để trích xuất từ **nhiều trang web khác nhau** trong một workflow.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho những ai muốn:
✔ **Tự động hóa theo dõi thị trường** mà không cần viết code.
✔ **Nhận email tóm tắt thông tin** hàng ngày vào hộp thư.
✔ **Tiết kiệm thời gian** để tập trung vào quyết định chiến lược.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có) với [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy thử** và **bật tự động hóa** để bắt đầu cuộc sống **không cần lo lắng** về việc theo dõi thông tin!

---
**🔗 Xem video hướng dẫn chi tiết:** [Automate With Marc - YouTube](https://www.youtube.com/@Automatewithmarc)
**💡 Cần hỗ trợ?** Hãy để lại comment bên dưới hoặc liên hệ với tôi! 🚀