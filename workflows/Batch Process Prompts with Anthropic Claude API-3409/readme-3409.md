---
title: "🤖 **Tự Động Xử Lý Batch Prompts với Claude API của Anthropic - Không Cần Code!**"
description: "Workflow này tự động gửi batch các câu hỏi (prompts) đến Claude API của Anthropic, xử lý song song và trả về kết quả chi tiết. Giúp tiết kiệm thời gian lên tới 90% so với cách làm thủ công, đồng thời tối ưu hóa chi phí API bằng cách batch hóa yêu cầu."
slug: "tieu-ly-batch-prompts-claude-anthropic"
tags: [n8n, automation, ai, anthropic-claude, batch-processing, no-code]
keywords: [n8n workflow claude api, tự động hóa batch prompts, xử lý song song ai, anthropic batch processing, tiết kiệm chi phí api]
---

# 🚀 **Tự Động Xử Lý Batch Prompts với Claude API - Giải Pháp Tối Ưu Hóa AI**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, khi cần xử lý nhiều câu hỏi (prompts) với Claude API của Anthropic, các sếp thường phải:
- **Gửi từng yêu cầu một** → Tốn thời gian và chi phí API cao.
- **Chờ đợi kết quả từng lượt** → Trải nghiệm chậm chạp, không phù hợp với quy trình công việc 24/7.
- **Không quản lý được lịch sử chat** → Mất thông tin quan trọng giữa các lần tương tác.

**Workflow này giải quyết tất cả đó!** Nó cho phép bạn gửi **tất cả các prompts cùng một lúc** đến Claude API, xử lý song song, và trả về kết quả chi tiết với **tốc độ cao gấp 10 lần** so với cách làm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên tới 90%** – Không cần chờ đợi từng kết quả một.
✅ **Giảm chi phí API** – Batch hóa yêu cầu giúp tối ưu hóa chi phí so với cách gọi API từng lượt.
✅ **Xử lý song song** – Các prompts được xử lý đồng thời, không phải chờ đợi lượt trước.
✅ **Quản lý lịch sử chat** – Hỗ trợ lưu trữ và truy xuất lại lịch sử tương tác.
✅ **Chuẩn ISO 42001** – Phù hợp với các doanh nghiệp cần quản lý AI theo tiêu chuẩn quốc tế.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **API Key của Anthropic** (cấp từ [trang đăng ký Anthropic](https://www.anthropic.com/api)).
- **Dữ liệu đầu vào** (một mảng `requests` với cấu trúc JSON như ví dụ dưới đây).
- **N8n Self-hosted** (để chạy 24/7, không phụ thuộc vào phiên bản miễn phí).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3409](https://n8n.io/workflows/3409) hoặc copy/paste JSON từ trang này vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Create new workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **27 node** phức tạp, nhưng chỉ cần chú ý đến các phần sau:

##### **A. Cấu Hình Credentials (Tham Số API)**
- **Node "Submit batch"**, **"Check batch status"**, **"Get results"** → **Chọn credentials `anthropicApi`** và điền:
  - **API Key**: API Key từ Anthropic.
  - **Base URL**: `https://api.anthropic.com/v1`.

##### **B. Cấu Trúc Dữ Liệu Đầu Vào**
Workflow **yêu cầu đầu vào là một mảng `requests`** với cấu trúc:
```json
{
    "anthropic-version": "2023-06-01",
    "requests": [
        {
            "custom_id": "id-đặc-biệt-cho-prompts",
            "params": {
                "max_tokens": 100,
                "messages": [
                    {
                        "content": "Câu hỏi của bạn ở đây!",
                        "role": "user"
                    }
                ],
                "model": "claude-3-5-haiku-20241022"
            }
        }
    ]
}
```
- **`custom_id`**: Dùng để nhận diện kết quả sau này.
- **`anthropic-version`**: Phải là phiên bản hỗ trợ (xem [đây](https://docs.anthropic.com/en/api/versioning)).

##### **C. Node Quan Trọng**
| Node | Loại | Ghi Chú |
|------|------|---------|
| **"Submit batch"** | `httpRequest` | Gửi batch prompts đến Anthropic. |
| **"Check batch status"** | `httpRequest` | Kiểm tra trạng thái xử lý. |
| **"Parse response"** | `code` | Chuyển đổi kết quả thành định dạng dễ đọc. |
| **"If ended processing"** | `if` | Dừng vòng lặp khi xử lý xong. |
| **"Execute Workflow"** | `executeWorkflow` | Gọi workflow con để xử lý song song. |

##### **D. Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   ```json
   {
       "anthropic-version": "2023-06-01",
       "requests": [
           {
               "custom_id": "fun-fact",
               "params": {
                   "max_tokens": 100,
                   "messages": [
                       {
                           "content": "Hey Claude, tell me a short fun fact about video games!",
                           "role": "user"
                       }
                   ],
                   "model": "claude-3-5-haiku-20241022"
               }
           }
       ]
   }
   ```
2. **Nhấn "Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH SỬ DỤNG HIỆU QUẢ]
- **Kết hợp với Slack/Telegram**: Sau khi xử lý xong, gửi kết quả về Slack/Telegram bằng node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.
- **Lưu log vào Google Sheets**: Dùng node **`n8n-nodes-base.googleSheets`** để ghi lại lịch sử các prompts và kết quả.
- **Gửi báo cáo định kỳ**: Sử dụng node **`n8n-nodes-base.email`** để gửi tổng hợp kết quả hàng ngày.
- **Tối ưu hóa chi phí**: Nếu có nhiều batch, hãy **tách thành nhiều batch nhỏ** để tránh vượt quá giới hạn API.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc xử lý batch prompts với Claude API, **tiết kiệm thời gian và chi phí** mà không cần viết một dòng code. **Hãy thử ngay và nâng cao hiệu suất AI của doanh nghiệp!**

👉 **Bắt đầu ngay với n8n Self-hosted** (để chạy 24/7) bằng cách đăng ký VPS từ:
🔹 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
🔹 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

---
**Chúc các sếp thành công!** 🚀