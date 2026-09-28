---
title: "🚀 **Tự Động Hóa Đánh Giá & Cảnh Báo Top Deal BizQuest Với AI Claude, Google Sheets & Slack**"
description: "Workflow tự động hóa hàng ngày để scrap, đánh giá độ phù hợp và cảnh báo top 100 deal BizQuest cho doanh nghiệp, tiết kiệm thời gian nghiên cứu thị trường lên đến 80%. Kết hợp AI Claude Haiku/Sonnet, Google Sheets và Slack để tối ưu hóa quy trình mua bán doanh nghiệp."
slug: "tieu-dong-hoa-danh-gia-deal-bizquest-ai-claude-slack"
tags: [n8n, automation, ai-summarization, market-research, business-deals]
keywords: [n8n workflow tự động hóa, đánh giá deal BizQuest, AI Claude Haiku, Slack alert, Google Sheets tự động]
---

# 🚀 **Tự Động Hóa Đánh Giá Deal BizQuest: Từ Scrap → AI → Slack Cảnh Báo Top Deal**

### **Nỗi Đau Của Các Sếp**
Mua bán doanh nghiệp (M&A) là một trong những quyết định lớn nhất của doanh nghiệp, nhưng quá trình **tìm kiếm, đánh giá và lựa chọn deal phù hợp** lại tốn thời gian và dễ bị bỏ lỡ cơ hội. Các sếp thường phải:
- **Tốn hàng giờ** để scrap và phân tích hàng trăm deal trên BizQuest.
- **Không có tiêu chí khách quan** để đánh giá độ phù hợp của deal với chiến lược kinh doanh.
- **Bỏ lỡ top deal** vì không được cảnh báo kịp thời.
- **Tốn chi phí** cho việc thuê chuyên gia phân tích hoặc sử dụng công cụ đắt đỏ.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động scrap** tất cả deal mới trên BizQuest hàng ngày (5h sáng).
✅ **Đánh giá độ phù hợp** (Fit Score 1-5) bằng AI Claude Haiku (mô hình chuyên gia).
✅ **Lọc top 100 deal** có SDE (Seller’s Discretionary Earnings) cao nhất.
✅ **Tự động viết tin nhắn cá nhân hóa** cho broker bằng Claude Sonnet.
✅ **Cảnh báo ngay trên Slack** với deal có Fit Score ≥ 4 (độ tin cậy cao).
✅ **Lưu toàn bộ log** vào Google Sheets để theo dõi và review sau này.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian** nghiên cứu thị trường so với làm thủ công.
- **Đánh giá deal khách quan** với Fit Score từ AI (không phụ thuộc vào cảm nhận cá nhân).
- **Nhận top 100 deal hàng ngày** được sàng lọc theo tiêu chí cá nhân hóa (buy box).
- **Tin nhắn cá nhân hóa** sẵn sàng copy-paste gửi broker, tăng tỷ lệ thành công giao dịch.
- **Cảnh báo kịp thời** trên Slack để không bỏ lỡ cơ hội.
- **Lưu trữ toàn bộ dữ liệu** trên Google Sheets, dễ dàng theo dõi và báo cáo.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrap BizQuest):
   - [Tạo tài khoản miễn phí Apify](https://apify.com/) và lấy **API Token**.
   - **Task URL**: [BizQuest Scraper của Memo23](https://apify.com/memo23/bizquest-scraper) (cần thay đổi trong node "Scrape BizQuest").

2. **Tài khoản Google Sheets**:
   - **Bảng tính chuẩn bị sẵn** với 16 cột (xem cấu trúc dưới đây).
   - **OAuth2 API Key** cho Google Sheets (cài đặt trong n8n Credentials).

3. **Tài khoản Slack**:
   - **OAuth2 API Key** cho Slack (để gửi cảnh báo).
   - **DM/Channel** để nhận thông báo deal.

4. **API Key Anthropic** (để sử dụng AI Claude):
   - [Đăng ký miễn phí tại Anthropic](https://www.anthropic.com/) và lấy **API Key**.

5. **VPS cho n8n Self-hosted** (khuyến nghị):
   - Workflow chạy 24/7, nên cài trên máy chủ riêng để ổn định.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 📊 **Cấu Trúc Google Sheets Chuẩn**
| **Tiêu Đề**               | **Mô Tả**                          |
|----------------------------|-------------------------------------|
| Title                      | Tên doanh nghiệp                    |
| Source                     | Nguồn (BizQuest)                   |
| Keyword                    | Từ khóa liên quan                   |
| Location                   | Địa chỉ doanh nghiệp               |
| Asking Price               | Giá bán yêu cầu (USD)               |
| Revenue                    | Doanh thu hàng năm (USD)            |
| SDE                        | Seller’s Discretionary Earnings     |
| SDE Estimated              | (True nếu SDE chưa rõ)              |
| Listed Date                | Ngày đăng deal                     |
| Link                       | Link BizQuest                       |
| First Seen                 | Ngày đầu tiên phát hiện deal       |
| Stage                      | Giai đoạn (Draft/Active/Closed)     |
| Fit Rationale               | Lý do đánh giá Fit Score (AI viết)  |
| Fit Score                  | Điểm phù hợp (1-5)                 |
| Fit Confidence             | Độ tin cậy (0-1)                   |
| Broker Message             | Tin nhắn cá nhân hóa (AI viết)      |

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ JSON**
:::info[**BƯỚC 1: Tải Workflow JSON**]
- Tải file JSON từ [n8n.io/workflows/16056](https://n8n.io/workflows/16056).
- Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
:::

### **2. Cấu Hình Cần Thiết (BẮT BUỘC)**
:::warning[**LƯU Ý: CẦN CHỈNH CÁC NODE NÀY**]
Dưới đây là danh sách các node **phải chỉnh** để workflow hoạt động đúng:

#### **A. "Scrape BizQuest" (HTTP Request)**
- **Thay đổi URL Apify**:
  - Mở node này → Tab **Request** → Thay `https://api.apify.com/v2/act/memo23/bizquest-scraper/run` thành URL của **Apify Task** bạn đã tạo.
  - Thêm **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APIFY_API_TOKEN"
    }
    ```
  - **Query Parameters**:
    ```json
    {
      "input": {
        "buyBox": "{{$node["Define Buy Box"].json()}}"
      }
    }
    ```

#### **B. "Define Buy Box" (Set)**
- **Chỉnh 5 trường sau** theo tiêu chí của bạn:
  - `buyBox`: Mô tả chi tiết về loại deal bạn muốn (ví dụ: *"Doanh nghiệp F&B có SDE > 500K, revenue > 1M, địa chỉ TP.HCM"*).
  - `keyword`: Từ khóa tìm kiếm (ví dụ: *"restaurant", "café"*).
  - `cashFlowMin`: Doanh thu tối thiểu (USD).
  - `priceMax`: Giá bán tối đa (USD).
  - `listingAgeDays`: Thời gian deal được đăng tối đa (ngày).

#### **C. "Look Up Link in Sheets" (Google Sheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api`.
- **Thiết lập**:
  - **Sheet Name**: Tên bảng tính chứa deal đã đánh giá.
  - **Range**: `Sheet1!A:P` (các cột từ A đến P).
  - **Operation**: `read`.

#### **D. "Anthropic Chat Model" (Claude Haiku & Sonnet)**
- **Thiết lập Credentials**: `anthropicApi`.
- **Model**:
  - **Claude Haiku 4.5** (đánh giá Fit Score).
  - **Claude Sonnet 4.6** (viết tin nhắn broker).
- **Prompt Template**:
  - Node này đã sẵn sàng, nhưng các sếp có thể **tùy chỉnh prompt** trong tab **Parameters** nếu cần.

#### **E. "Send Deal Alert to Slack" (Slack)**
- **Chọn Credentials**: `slackOAuth2Api`.
- **Thiết lập**:
  - **Channel/DM**: Chọn kênh hoặc tin nhắn riêng để nhận cảnh báo.
  - **Blocks**: Workflow đã tự động xây dựng blocks Slack, nhưng các sếp có thể chỉnh sửa trong node **Build Slack Blocks** (Code).

#### **F. "Append Green Score to Sheet" & "Append Low Score to Sheet" (Google Sheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api`.
- **Range**: `Sheet1!A:P` (để ghi dữ liệu mới).
- **Operation**: `append`.

---
### **3. Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra các node quan trọng (đặc biệt là **Claude Haiku** và **Slack Alert**).
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN THÊM**]
1. **Kết hợp với Notion/ClickUp**:
   - Thay vì Google Sheets, các sếp có thể **lưu log vào Notion** hoặc **ClickUp** bằng node `notion` hoặc `clickup`.
   - Cài đặt thêm **node `webhook`** để nhận cảnh báo qua email.

2. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **node `scheduleTrigger`** để chạy workflow vào cuối tuần.
   - Gửi **báo cáo tổng hợp** qua Slack/Email với top 5 deal có Fit Score cao nhất.

3. **Tối ưu Fit Score**:
   - Nếu AI Claude đánh giá không chính xác, các sếp có thể **tùy chỉnh prompt** trong node `lmChatAnthropic` để rõ ràng hơn về tiêu chí đánh giá.

4. **Lọc deal theo vùng miền**:
   - Thêm **node `code`** sau "Scrape BizQuest" để lọc deal theo tỉnh/thành phố cụ thể.

5. **Dùng AI khác (GPT-4, Llama)**:
   - Thay thế Claude bằng **GPT-4** (OpenAI) hoặc **Llama** (Mistral) bằng cách thay đổi node `lmChatAnthropic`.

---
## 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Ngay!**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong việc phân tích deal.
✔ **Nhận top deal hàng ngày** với tiêu chí cá nhân hóa.
✔ **Tự động viết tin nhắn** để liên hệ broker.
✔ **Cảnh báo kịp thời** trên Slack.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (khuyến nghị).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận **top deal hàng ngày**!

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/16056)
- [BizQuest Scraper Apify](https://apify.com/memo23/bizquest-scraper)
- [Hướng dẫn cài n8n Self-hosted](https://docs.n8n.io/hosting/installation/)
- [Tạo API Key Anthropic](https://www.anthropic.com/docs/api/quickstart)