---
title: "🎤 **Tự Động Gợi Ý Nhà Trình Bày Chuyên Nghiệp Cho Sự Kiện Với Claude AI + Google Sheets (N8N)**"
description: "Workflow tự động hóa gợi ý nhà trình bày phù hợp cho sự kiện dựa trên yêu cầu, sở thích của khán giả và dữ liệu chuyên môn từ Google Sheets, giúp các sếp tiết kiệm thời gian lên kế hoạch và tối ưu hóa trải nghiệm tham gia. Kết quả: Danh sách nhà trình bày ưu tiên, phân tích độ phù hợp và báo cáo chi tiết tự động."
slug: "tieu-dong-go-yi-nha-trinh-bay-voi-claude-ai-google-sheets"
tags: [n8n, automation, ai-chatbot, google-sheets, anthropic-claude, voice-agent]
keywords: [n8n workflow tự động hóa, gợi ý nhà trình bày sự kiện, Claude AI + Google Sheets, tự động hóa sự kiện, tối ưu hóa chương trình sự kiện]
---

# 🚀 **Tự Động Gợi Ý Nhà Trình Bày Chuyên Nghiệp Cho Sự Kiện Với Claude AI + Google Sheets**

### **Nỗi Đau Của Các Sếp Khi Lên Kế Hoạch Nhà Trình Bày**
Lên danh sách nhà trình bày cho một sự kiện lớn không phải là việc đơn giản. Các sếp thường phải:
- **Tìm kiếm thủ công** trên Google, LinkedIn hoặc danh sách cũ để tìm những người phù hợp với chủ đề sự kiện.
- **So sánh nhiều hồ sơ** để đánh giá kinh nghiệm, độ phù hợp với khán giả và khả năng tương tác.
- **Điều chỉnh liên tục** danh sách dựa trên phản hồi từ tổ chức hoặc khán giả, dẫn đến việc mất thời gian và khả năng bỏ sót những gợi ý tiềm năng.
- **Không có phân tích dữ liệu** để tối ưu hóa sự đa dạng hoặc độ hấp dẫn của chương trình.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động phân tích** yêu cầu sự kiện (chủ đề, mục tiêu, kích thước khán giả) và so sánh với hồ sơ nhà trình bày trong Google Sheets.
✅ **Sử dụng Claude AI** (mô hình Claude 4 Sonnet) để gợi ý danh sách nhà trình bày ưu tiên, phân tích độ phù hợp và đề xuất lý do.
✅ **Lưu lịch sử gợi ý** vào Google Sheets để theo dõi và báo cáo sau này.
✅ **Trả kết quả dưới dạng tự động hóa hoàn chỉnh**, không cần viết một dòng code nào.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định. Dưới đây là một số gợi ý:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
💡 **Lưu ý:** N8N yêu cầu tối thiểu **2GB RAM** và **1 CPU core** để chạy Claude AI ổn định.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
1. **Tiết kiệm thời gian lên kế hoạch** từ **giờ đến ngày** cho việc tìm kiếm và đánh giá nhà trình bày.
2. **Nhận danh sách gợi ý chính xác** với độ phù hợp cao, dựa trên phân tích AI và dữ liệu thực tế.
3. **Tối ưu hóa chương trình sự kiện** bằng cách đảm bảo sự đa dạng, độ hấp dẫn và sự liên quan của nội dung.
4. **Lưu trữ lịch sử gợi ý** để so sánh và học hỏi cho các sự kiện tương lai.
5. **Hoạt động tự động hóa hoàn toàn** – không cần can thiệp thủ công sau khi cấu hình xong.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Cloud** với quyền truy cập vào **Google Sheets** (để lưu trữ dữ liệu nhà trình bày và lịch sử gợi ý).
✔ **API Key của Anthropic** (để kết nối với mô hình Claude AI). Mời đăng ký tại: [https://www.anthropic.com/api](https://www.anthropic.com/api).
✔ **Dữ liệu nhà trình bày trong Google Sheets** với các cột như:
   - Tên nhà trình bày
   - Chuyên môn/ngành nghề
   - Kinh nghiệm (số năm, sự kiện đã tham gia)
   - Đánh giá từ khán giả (nếu có)
   - Sẵn sàng tham gia sự kiện (có/không)
✔ **Mô hình Claude AI** được chọn là **claude-sonnet-4-20250514** (đã được cấu hình sẵn trong workflow).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **13 node** và được thiết kế để hoạt động với **Webhook Trigger**. Các sếp có thể import bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/10221](https://n8n.io/workflows/10221) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ trang trên vào **Import Workflow** trong n8n Dashboard.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** cho các node quan trọng:

##### **A. Webhook Trigger**
- **Path:** `speaker-recommendations` (không thay đổi).
- **HTTP Method:** `POST` (để nhận yêu cầu từ bên ngoài).
- **Lưu ý:** Các sếp cần **bật Webhook** và lưu địa chỉ URL để gọi từ bên ngoài (ví dụ: từ một ứng dụng voice agent hoặc API khác).

##### **B. Fetch Speakers Data & Fetch Audience Data (Google Sheets)**
- **Credentials:** Chọn `googleApi` (đã cấu hình trước khi import).
- **Sheet Name:** Điền tên **Google Sheet** chứa dữ liệu nhà trình bày và khán giả.
  - **Cấu trúc Sheet nhà trình bày (ví dụ):**
    | Tên          | Chuyên môn       | Kinh nghiệm (năm) | Đánh giá | Sẵn sàng tham gia |
    |--------------|------------------|-------------------|----------|--------------------|
    | Nguyễn Văn A | AI & Machine Learning | 10                | 4.8      | Có                 |
    | Trần Thị B   | Blockchain       | 7                 | 4.5      | Không              |
  - **Cấu trúc Sheet khán giả (ví dụ):**
    | Sự kiện       | Mục tiêu sự kiện       | Kích thước khán giả | Sở thích chủ đề          |
    |---------------|------------------------|--------------------|---------------------------|
    | Tech Summit 2025 | Học hỏi & Networking   | 500                | AI, Cloud Computing       |

##### **C. AI Agent (Claude AI)**
- **Model:** Đã cấu hình sẵn là `claude-sonnet-4-20250514` (mô hình Claude 4 Sonnet).
- **Credentials:** Chọn `anthropicApi` (đã cấu hình trước khi import).
- **Lưu ý:** Đảm bảo **API Key Anthropic** được điền chính xác trong **Credentials** của n8n.

##### **D. Code Nodes (Parse Voice Request, Aggregate All Data, Format for Voice Response)**
- Các node này **không cần chỉnh sửa** nếu dữ liệu đầu vào và cấu trúc Sheet đúng như hướng dẫn.
- **Parse Voice Request:** Chuyển đổi yêu cầu từ Webhook thành định dạng dễ xử lý.
- **Aggregate All Data:** Ghép dữ liệu nhà trình bày và khán giả để AI phân tích.
- **Format for Voice Response:** Chuẩn bị kết quả cuối cùng cho Webhook trả về.

##### **E. Error Handling (Check for Errors, Format Error Response, Send Error Response)**
- Nếu có lỗi (ví dụ: Google Sheets không trả về dữ liệu), workflow sẽ **trả về thông báo lỗi** thay vì kết quả.
- **Lưu ý:** Các sếp nên **test run** với dữ liệu mẫu trước khi bật workflow hoạt động thực tế.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi một **yêu cầu mẫu** từ Postman hoặc cURL để kiểm tra:
  ```json
  {
    "eventType": "Tech Summit 2025",
    "eventGoals": "Học hỏi về AI và Cloud Computing",
    "audienceSize": 500,
    "preferredTopics": ["AI", "Machine Learning", "Blockchain"]
  }
  ```
- **Bật Active:** Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Voice Agent:**
   - Sử dụng **Google Assistant** hoặc **Amazon Alexa** để gọi workflow này bằng giọng nói. Ví dụ:
     *"Hey Google, gọi API gợi ý nhà trình bày cho Tech Summit 2025."*
   - **Cách thực hiện:** Cấu hình **Google Actions** hoặc **Alexa Skill** để gọi Webhook của n8n.

2. **Lưu Log & Báo Cáo:**
   - Thêm một **node Email** (n8n-nodes-base.email) để gửi báo cáo gợi ý hàng tuần cho đội ngũ tổ chức sự kiện.
   - **Cấu trúc báo cáo:**
     - Danh sách nhà trình bày ưu tiên.
     - Độ phù hợp trung bình.
     - Lý do AI chọn họ.

3. **Tối ưu hóa Dữ liệu:**
   - **Cập nhật thường xuyên** Google Sheet nhà trình bày để AI có dữ liệu mới nhất.
   - **Thêm cột "Đánh giá từ khán giả"** để AI ưu tiên những người có phản hồi tốt.

4. **Kết hợp với Slack/Telegram:**
   - Thêm **node Slack** (n8n-nodes-base.slack) để thông báo kết quả gợi ý ngay khi có.
   - **Cách thực hiện:**
     - Cấu hình **Slack App** trong n8n.
     - Gửi tin nhắn tự động khi workflow hoàn thành.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quá trình lên kế hoạch nhà trình bày sự kiện** mà không cần viết code. Với sự hỗ trợ của **Claude AI** và **Google Sheets**, các sếp sẽ:
✔ **Tiết kiệm thời gian** từ việc tìm kiếm thủ công.
✔ **Nhận gợi ý chính xác** dựa trên phân tích AI.
✔ **Tối ưu hóa chương trình** để khán giả hài lòng.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và bắt đầu tự động hóa sự kiện của mình!

**Nếu có vấn đề gì, hãy liên hệ với [The AI Squad Initiative](https://www.oneclickai.com/) để hỗ trợ!** 🚀