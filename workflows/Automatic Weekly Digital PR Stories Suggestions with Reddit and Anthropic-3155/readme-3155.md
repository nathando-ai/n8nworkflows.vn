---
title: "🚀 Tự Động Hóa Báo Cáo Gợi Ý Chuyên Mục PR Số Hàng Tuần Từ Reddit & AI Claude 3"
description: "Workflow tự động hóa tìm kiếm tin tức nóng trên Reddit, phân tích cảm xúc từ bình luận, tổng hợp thông tin từ nguồn tin chính và tạo gợi ý chiến lược PR số hàng tuần. Giúp các sếp tiết kiệm 10+ giờ/tháng và tăng hiệu quả PR 30%."
slug: "tieu-dong-hoa-bo-cao-gi-nguy-chuyen-muc-pr-so-hang-tuan"
tags: [n8n, automation, ai-marketing, reditt-automation, anthropic-claude, google-drive, mattermost]
keywords: [n8n workflow tự động hóa PR số, phân tích cảm xúc Reddit, AI Claude 3 cho marketing, tự động hóa báo cáo hàng tuần, công cụ PR số tự động]
---

# 🚀 **Tự Động Hóa Báo Cáo Gợi Ý Chuyên Mục PR Số Hàng Tuần Từ Reddit & AI Claude 3**

## **🔥 Nỗi Đau Của Các Sếp Trong PR Số Hàng Ngày**
Hàng tuần, các sếp phải:
- **Tìm kiếm thủ công** tin tức nóng trên Reddit, Facebook Groups hay diễn đàn chuyên ngành (tốn 3-5 giờ).
- **Phân tích cảm xúc** từ bình luận để đánh giá độ quan tâm thực sự của cộng đồng (khó khăn với volume lớn).
- **Tổng hợp thông tin** từ nhiều nguồn tin khác nhau và viết báo cáo để gửi cho ban lãnh đạo (rất dễ bị bỏ sót chi tiết quan trọng).
- **Tạo gợi ý chiến lược PR** dựa trên xu hướng hiện tại, nhưng thường chỉ dựa vào cảm nhận chủ quan.

**Kết quả?** Báo cáo PR số không được cập nhật kịp thời, gợi ý không chính xác, và các sếp phải mất nhiều thời gian hơn để điều chỉnh chiến lược.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% Không Code**
Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm đến báo cáo, sử dụng:
✅ **Reddit API** để lấy tin tức nóng và bình luận.
✅ **AI Claude 3 (Anthropic)** để phân tích cảm xúc, tổng hợp tin tức và tạo gợi ý chiến lược PR.
✅ **Google Drive** để lưu trữ báo cáo và chia sẻ với team.
✅ **Mattermost** để thông báo kết quả ngay khi có.

**Kết quả các sếp nhận được:**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc tìm kiếm và phân tích tin tức.
- **Báo cáo chính xác** với phân tích cảm xúc từ AI, không phụ thuộc vào cảm nhận chủ quan.
- **Gợi ý chiến lược PR** được tối ưu hóa dựa trên xu hướng thực tế của cộng đồng.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Chia sẻ tự động** báo cáo với team qua Mattermost và Google Drive.
:::

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Reddit** với API OAuth2 (để lấy dữ liệu từ Reddit).
2. **Tài khoản Anthropic** (để sử dụng AI Claude 3 phân tích và tạo nội dung).
3. **Tài khoản Google Drive** (để lưu trữ và chia sẻ báo cáo).
4. **Tài khoản Mattermost** (để thông báo kết quả).
5. **Danh sách chủ đề quan tâm** (mỗi chủ đề một dòng, ví dụ: "Tin tức công nghệ", "Startup Việt Nam").
6. **API Key của Jina** (nếu cần sử dụng trong quá trình xử lý dữ liệu).

:::info[CHUẨN BỊ]
- **Reddit OAuth2 API**: Theo [hướng dẫn này](https://docs.n8n.io/integrations/builtin/credentials/reddit/).
- **Anthropic Account**: Theo [hướng dẫn này](https://docs.n8n.io/integrations/builtin/credentials/anthropic/).
- **Google Drive OAuth2**: Theo [hướng dẫn này](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/).
- **Mattermost Webhook**: Theo [hướng dẫn này](https://developers.mattermost.com/integrate/webhooks/incoming/).
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/3155) (hoặc copy toàn bộ JSON từ link trên).
2. Mở **n8n Editor** và nhấn **Import Workflow**.
3. Chọn file JSON và nhấn **Import**.

### **2. Các Bước Cấu Hình BẮT BUỘC**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

#### **🔹 Node "Set Data" (Đặt dữ liệu đầu vào)**
- **Tham số cần điền:**
  - **Topics**: Danh sách chủ đề quan tâm (mỗi chủ đề một dòng, ví dụ:
    ```
    Tin tức công nghệ
    Startup Việt Nam
    AI và tự động hóa
    ```
  - **Jina API Key** (nếu sử dụng): Nhập API Key từ [trang này](https://jina.ai/api-dashboard/key-manager).

#### **🔹 Node "Schedule Trigger" (Lịch trình chạy tự động)**
- **Cấu hình cron job**:
  - Mặc định: **0 6 * * 1** (chạy hàng tuần vào thứ Hai lúc 6h sáng).
  - Các sếp có thể điều chỉnh theo nhu cầu (ví dụ: **0 9 * * 2** để chạy thứ Ba lúc 9h sáng).

#### **🔹 Node "Reddit OAuth2 API" (Lấy dữ liệu từ Reddit)**
- **Tham số cần thiết:**
  - **Client ID & Secret**: Nhập từ tài khoản Reddit OAuth2 đã đăng ký.
  - **Scope**: Chọn `read` để lấy dữ liệu công khai.

#### **🔹 Node "Anthropic Chat Model" (Sử dụng AI Claude 3)**
- **Tham số cần thiết:**
  - **Model**: Đã mặc định là `claude-3-7-sonnet-20250219`.
  - **Credentials**: Chọn tài khoản Anthropic đã đăng ký.

#### **🔹 Node "Google Drive" (Lưu và chia sẻ báo cáo)**
- **Tham số cần thiết:**
  - **Folder ID**: Chọn thư mục Google Drive muốn lưu báo cáo.
  - **Permissions**: Chọn `anyone` hoặc `specific people` tùy theo yêu cầu.

#### **🔹 Node "Send files to Mattermost" (Thông báo kết quả)**
- **Tham số cần thiết:**
  - **Mattermost Instance URL**: Nhập URL của server Mattermost.
  - **Webhook ID & Channel**: Nhập từ webhook đã tạo.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả.
   - Đảm bảo tất cả node hoạt động bình thường.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch trình.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối ưu hóa chủ đề tìm kiếm**
- Các sếp có thể **thêm chủ đề mới** vào node "Set Data" để cập nhật xu hướng.
- Ví dụ: Thêm `Blockchain` hoặc `Metaverse` nếu muốn theo dõi xu hướng mới.

### **2. Lọc tin tức theo độ tin cậy**
- Sử dụng node **"Upvotes Requirement Filtering"** để chỉ lấy bài viết có **số upvote cao** (ví dụ: >100 upvotes).

### **3. Lưu log và theo dõi lịch sử**
- Thêm node **Google Sheets** hoặc **Notion** để lưu trữ lịch sử báo cáo.
- Ví dụ: Sử dụng node `n8n-nodes-base.googleSheets` để ghi dữ liệu vào bảng tính.

### **4. Gửi báo cáo qua Email**
- Thêm node **Gmail** hoặc **SendGrid** để gửi báo cáo tự động qua Email hàng tuần.

### **5. Tích hợp với Slack/Telegram**
- Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả ngay khi có.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tìm kiếm và phân tích tin tức thủ công, đồng thời **cung cấp báo cáo PR số chính xác và chiến lược hóa** dựa trên xu hướng thực tế của cộng đồng.

**Hành động ngay:**
1. **Chuẩn bị tài khoản và API Key** theo hướng dẫn trên.
2. **Import và cấu hình workflow**.
3. **Bật chạy tự động** và theo dõi kết quả hàng tuần!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với chiến lược PR số tự động hóa!** 🚀