---
title: "🔍 Tự Động Lấy Trả Lời Bình Luận Xiaohongshu (Little Red Book) Với JustOneAPI - Không Cần Code"
description: "Workflow tự động hóa lấy tất cả bình luận và trả lời từ Xiaohongshu (Little Red Book) bằng API JustOneAPI, giúp các sếp nghiên cứu thị trường, phân tích xu hướng và theo dõi phản hồi khách hàng một cách nhanh chóng và chính xác. Giảm thời gian thủ công từ 2-3 tiếng xuống chỉ vài giây!"
slug: "tu-dong-lay-tra-loi-binh-luan-xiaohongshu-justoneapi"
tags: [n8n, automation, market-research, api-integration, xiaohongshu, justoneapi]
keywords: [tự động hóa lấy bình luận little red book, api xiaohongshu, nghiên cứu thị trường xã hội, tự động hóa no-code, n8n workflow]
---

# 🚀 **Tự Động Lấy Trả Lời Bình Luận Xiaohongshu (Little Red Book) Với JustOneAPI - Không Cần Code**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường Xã Hội**
Hiện nay, các doanh nghiệp và marketer phải mất **2-3 tiếng** để thủ công:
- Tìm kiếm và sao chép bình luận từ Xiaohongshu (Little Red Book).
- Lọc và phân tích trả lời của người dùng.
- Lưu trữ dữ liệu để theo dõi xu hướng.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Tự động hóa 100%** lấy bình luận và trả lời từ Xiaohongshu.
✅ **Chỉ cần kích hoạt 1 lần** để có dữ liệu sạch, có cấu trúc.
✅ **Kết hợp với JustOneAPI** (API chính thức của Xiaohongshu) để đảm bảo tính chính xác cao.
✅ **Hoạt động 24/7** khi tự động hóa trên VPS riêng (self-hosted).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị giới hạn bởi n8n.cloud, các sếp nên **cài đặt n8n trên VPS riêng** (self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **2-3 tiếng thủ công** xuống **chỉ vài giây** với 1 lần kích hoạt.
- **Dữ liệu chính xác**: Lấy trực tiếp từ API JustOneAPI (không phụ thuộc vào scraping).
- **Cấu trúc hóa dữ liệu**: Trả lời được **sắp xếp thành danh sách**, dễ dàng phân tích với Excel, Google Sheets hoặc AI.
- **Hoạt động liên tục**: Khi tự động hóa trên VPS, workflow có thể **lấy dữ liệu định kỳ** (ví dụ: hàng ngày).
- **Tích hợp với các công cụ khác**: Dữ liệu có thể được gửi đến **Slack, Telegram, Email** hoặc **lưu vào Google Drive**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản JustOneAPI**:
   - [Đăng ký API Key JustOneAPI](https://www.justoneapi.com/) (miễn phí hoặc trả phí tùy theo nhu cầu).
   - **Endpoint API**: `https://api.justoneapi.com/xiaohongshu/v1/comments/{post_id}/replies` (cần thay `{post_id}` bằng ID bài viết của bạn).
✔ **ID bài viết Xiaohongshu (Post ID)**:
   - Lấy từ URL của bài viết trên Xiaohongshu (ví dụ: `https://www.xiaohongshu.com/post/123456789` → `123456789`).
✔ **Tài khoản n8n** (cả trên cloud hoặc self-hosted).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/15811](https://n8n.io/workflows/15811) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **6 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **Node 1: Start Workflow Manually (Bắt Đầu Tự Động)**
- **Không cần chỉnh sửa gì**, chỉ cần kích hoạt thủ công khi cần.

##### **Node 2: Set API and Reply Parameters (Cấu Hình API & Tham Số)**
- **Thêm API Key JustOneAPI**:
  - Mở node này → Tab **"Credentials"** → Chọn **"Add New Credentials"** → Nhập **API Key** từ JustOneAPI.
  - Lưu ý: **Không chia sẻ API Key** với ai!
- **Thêm tham số API**:
  - Trong tab **"Parameters"**, thêm các trường sau:
    ```json
    {
      "post_id": "123456789",  // Thay bằng ID bài viết của bạn
      "limit": 100,            // Số lượng trả lời lấy (mặc định 100)
      "offset": 0              // Bắt đầu từ trả lời thứ 0
    }
    ```

##### **Node 3: Fetch Xiaohongshu Replies via API (Lấy Trả Lời Bằng HTTP Request)**
- **Cấu hình URL API**:
  - Trong tab **"HTTP Request"**, nhập URL:
    ```
    https://api.justoneapi.com/xiaohongshu/v1/comments/{post_id}/replies
    ```
  - Thay `{post_id}` bằng ID bài viết của bạn (ví dụ: `123456789`).
- **Method**: Đặt là **GET**.
- **Headers**:
  - Thêm `Authorization: Bearer {API_KEY}` (API Key từ node trước).
  - Thêm `Content-Type: application/json`.
- **Body**: Để trống (sử dụng tham số từ node 2).

##### **Node 4 & 5: Parse Reply Data (Xử Lý Dữ Liệu Thô)**
- **Node 4 (Output Raw Reply Data)**: **Không cần chỉnh sửa**, chỉ lưu trữ dữ liệu thô từ API.
- **Node 5 (Parse Reply Data into List - Xử Lý Dữ Liệu Bằng Code)**:
  - Mở tab **"Code"** và **chỉnh sửa script** để **tách dữ liệu thành danh sách**:
    ```javascript
    // Dữ liệu thô từ API (dạng JSON)
    const rawData = $input.all();

    // Tách danh sách trả lời
    const replies = rawData[0].data?.replies || [];

    // Trả về danh sách trả lời có cấu trúc
    return {
      json: {
        replies: replies.map(reply => ({
          user_id: reply.user_id,
          user_name: reply.user_name,
          content: reply.content,
          time: reply.time,
          like_count: reply.like_count
        }))
      }
    };
    ```
  - **Lưu ý**: Nếu API trả về cấu trúc khác, các sếp cần **đọc kỹ JSON** và **cập nhật script** tương ứng.

##### **Node 6: Output Final Reply List (Xuất Dữ Liệu Cuối Cùng)**
- **Không cần chỉnh sửa**, chỉ **hiển thị kết quả** dưới dạng danh sách trả lời đã xử lý.

#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**:
  - Kích hoạt node **"Start Workflow Manually"**.
  - Kiểm tra **Output** của node cuối (`Output Final Reply List`).
  - Nếu dữ liệu sai, **quay lại chỉnh sửa Node 5 (Code)**.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lấy Dữ Liệu Định Kỳ**:
   - Sử dụng **n8n Trigger (Schedule)** để chạy workflow **hàng ngày/tuần**.
   - Ví dụ: Lấy tất cả trả lời mới của bài viết hàng ngày để theo dõi xu hướng.

2. **Gửi Dữ Liệu Đến Slack/Telegram**:
   - Thêm **node Slack/Telegram Webhook** sau node cuối để **báo cáo tự động** khi có dữ liệu mới.

3. **Lưu Dữ Liệu Vào Google Sheets/Excel**:
   - Sử dụng **node Google Sheets** để **ghi dữ liệu vào bảng tự động**.
   - Cấu hình **Sheet Name** và **Range** phù hợp.

4. **Phân Tích Dữ Liệu Với AI**:
   - Sử dụng **node LLM (AI)** để **tóm tắt cảm xúc** trong bình luận (ví dụ: "Bài viết này có nhiều phản hồi tích cực về sản phẩm X").
   - Ví dụ:
     ```json
     {
       "prompt": "Analyze the following Xiaohongshu replies and summarize the sentiment: {{$json['replies']}}",
       "model": "gpt-3.5-turbo"
     }
     ```

5. **Lưu Log Lịch Sử**:
   - Thêm **node Database (MongoDB/PostgreSQL)** để **lưu trữ lịch sử** các lần lấy dữ liệu.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **cung cấp dữ liệu chính xác** từ Xiaohongshu, và **tích hợp dễ dàng** với các công cụ khác (Slack, Google Sheets, AI).

**Hành động ngay hôm nay:**
1. **Đăng ký JustOneAPI** và lấy **API Key**.
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Kích hoạt** và **theo dõi kết quả**!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với **n8n Community** để được hỗ trợ kỹ thuật!

---
**#TựĐộngHóa #NghiênCứuThịTrường #Xiaohongshu #JustOneAPI #n8n**