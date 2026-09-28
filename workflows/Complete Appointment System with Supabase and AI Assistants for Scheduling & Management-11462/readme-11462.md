---
title: "🤖 Hệ Thống Đặt Lịch & Trợ Lý AI Tự Động Hóa Cho Phỏng Vấn & Đăng Ký Lớp - Supabase + Ollama"
description: "Workflow tự động hóa hoàn chỉnh cho việc quản lý lịch hẹn phỏng vấn, đăng ký lớp học và hỗ trợ AI thông minh bằng Supabase và mô hình Ollama. Giúp tiết kiệm 80% thời gian quản lý và giảm thiểu lỗi nhân sự."
slug: "he-thong-dat-lich-ai-trong-dong-voi-supabase"
tags: [n8n, automation, no-code, supabase, ollama, ai-chatbot, scheduling, support-chatbot]
keywords: [tự động hóa đặt lịch phỏng vấn, workflow n8n supabase, trợ lý AI quản lý lịch, tự động hóa đăng ký lớp học, ollama n8n, tự động hóa phỏng vấn]
---

# 🚀 **Hệ Thống Đặt Lịch & Trợ Lý AI Tự Động Hóa Cho Phỏng Vấn & Đăng Ký Lớp**

Hãy tưởng tượng một hệ thống tự động hóa hoàn chỉnh giúp **giải phóng bạn khỏi việc quản lý lịch phỏng vấn, đăng ký lớp học và hỗ trợ khách hàng 24/7** mà không cần viết một dòng code nào! Workflow này kết hợp **Supabase** (database cloud tiên tiến) với **AI Ollama** (mô hình Qwen3:14b) để xử lý tất cả các yêu cầu đặt lịch, thay đổi lịch, hủy lịch và tra cứu thông tin một cách **tự động, chính xác và cá nhân hóa**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. N8n chạy trên VPS sẽ đảm bảo **tốc độ cao, bảo mật tuyệt đối** và không phụ thuộc vào phiên bản miễn phí có giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian quản lý lịch**: Không cần phải thủ công gõ vào Excel hoặc CRM.
- **Trợ lý AI thông minh**: Ollama xử lý yêu cầu đặt lịch, thay đổi lịch và hủy lịch **như con người**, với khả năng hiểu ngữ cảnh và đề xuất lịch hợp lý.
- **Quản lý tự động hóa hoàn chỉnh**: Tự động **gán phỏng vấn viên**, **cập nhật lịch**, **xóa lịch cũ** và **trả về kết quả JSON chuẩn**.
- **Hỗ trợ đa chức năng**: Từ **đặt lịch phỏng vấn** đến **tra cứu danh sách lớp học**, **thông tin đăng ký** – tất cả đều được tự động hóa.
- **Bảo mật & linh hoạt**: Kết nối với **Supabase** (database cloud) để quản lý dữ liệu một cách an toàn và dễ dàng mở rộng.
- **Gửi thông báo tự động**: Email thông báo đặt lịch, thay đổi lịch và hủy lịch **không cần can thiệp thủ công**.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Supabase**:
   - **Supabase Project ID** và **Supabase API Key** (để kết nối với database).
   - **Table cấu trúc sẵn sàng**:
     - `interviewers` (bảng quản lý phỏng vấn viên, với trường như `id`, `name`, `availability`).
     - `enrollers` (bảng quản lý người đăng ký, với trường như `id`, `name`, `email`, `interview_slot`).
     - `classes` (nếu có yêu cầu tra cứu danh sách lớp học).

2. **Mô hình AI Ollama**:
   - **Cài đặt Ollama** trên máy chủ VPS (n8n sẽ kết nối để gọi API mô hình **Qwen3:14b**).
   - **Không cần GPU**: Mô hình Ollama chạy hiệu quả trên CPU, phù hợp với VPS 2GB+ RAM.

3. **API Key Ollama**:
   - **Không cần API Key** (Ollama chạy offline trên máy chủ), nhưng cần **cài đặt mô hình Qwen3:14b** trước.

4. **Dữ liệu mẫu để test**:
   - JSON yêu cầu đặt lịch (ví dụ: `{"action": "set_appointment", "name": "Nguyễn Văn A", "email": "a@example.com", "preferred_date": "2024-12-25"}`).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11462](https://n8n.io/workflows/11462) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và có **40 nodes**, nhưng chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình Webhook (Node đầu tiên)**
- **Node**: `Webhook` (HTTP Method: **POST**)
- **Path**: `46161ac6-9838-4b3d-ad4a-c8d62362a656` (không thay đổi).
- **Lưu ý**:
  - Các sếp cần **bật Webhook** và **lưu URL** để gửi yêu cầu từ bên ngoài (ví dụ: từ ứng dụng web hoặc API khác).
  - **Test Webhook** bằng công cụ như **Postman** với payload mẫu:
    ```json
    {
      "action": "set_appointment",
      "name": "Nguyễn Văn A",
      "email": "a@example.com",
      "preferred_date": "2024-12-25"
    }
    ```

#### **B. Cấu hình Supabase (Tất cả nodes có `supabaseApi`)**
- **Node**: `Load Interviewers Table`, `Create Interview Record`, `Update Enroller Record`, v.v.
- **Bước 1**: Tạo **credentials Supabase** trong n8n:
  - **Tên credentials**: `supabaseApi`
  - **URL**: `https://[PROJECT_REF].supabase.co`
  - **Key**: `your-supabase-anon-key` (tìm trong **Project Settings → API**).
- **Bước 2**: Kiểm tra **table cấu trúc**:
  - `interviewers` phải có trường `id`, `name`, `availability`.
  - `enrollers` phải có trường `id`, `name`, `email`, `interview_slot`.

#### **C. Cấu hình AI Ollama (Tất cả nodes `lmChatOllama`)**
- **Node**: `Ollama Chat Model`, `Assign Interviewer & Schedule`, `AI Rescheduling Agent`, v.v.
- **Bước 1**: **Cài đặt Ollama** trên VPS:
  ```bash
  curl -fsSL https://ollama.com/install.sh | sh
  ollama pull qwen3:14b
  ```
- **Bước 2**: **Không cần API Key** (Ollama chạy offline).
- **Lưu ý**:
  - AI sẽ **xử lý logic phức tạp** như:
    - **Gán phỏng vấn viên** dựa trên sẵn có.
    - **Đề xuất lịch thay thế** khi lịch bị trùng.
    - **Xác nhận hủy lịch** và giải phóng slot.
  - **Test AI** bằng cách gửi yêu cầu:
    ```json
    {
      "action": "reschedule",
      "old_slot": "2024-12-25 10:00",
      "new_preferred_date": "2024-12-26"
    }
    ```

#### **D. Cấu hình Email (Nodes `if` và `noOp`)**
- **Node**: `Appointment Email`, `Reschedule Email`, `Cancel Email`.
- **Lưu ý**:
  - Workflow **kiểm tra email** trước khi gửi thông báo.
  - Nếu **email không tồn tại** trong yêu cầu, nó sẽ **bỏ qua** (nodes `Skip If No Email`).
  - **Cấu hình SMTP** (nếu muốn gửi email thực tế):
    - Thêm node **`n8n-nodes-base.email`** và cấu hình tài khoản Gmail/Outlook.
    - **Không bắt buộc**: Workflow có thể trả về **JSON thông báo** thay vì gửi email.

#### **E. Cấu hình Agent AI (Nodes `agent`)**
- **Node**: `Assign Interviewer & Schedule`, `AI Rescheduling Agent`, `AI Cancellation Agent`.
- **Lưu ý**:
  - **Agent AI** sẽ tự động:
    - **Tải danh sách phỏng vấn viên** (`Load Interviewers Table`).
    - **Xóa lịch cũ** (`Delete Interviewer Record`).
    - **Tạo lịch mới** (`Create Interview Record`).
    - **Trả về kết quả** dưới dạng JSON.
  - **Test Agent** bằng cách gửi yêu cầu:
    ```json
    {
      "action": "set_appointment",
      "name": "Trần Thị B",
      "email": "b@example.com",
      "preferred_date": "2024-12-25"
    }
    ```

---

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi yêu cầu mẫu qua Webhook và kiểm tra **JSON response**.
  - **Dữ liệu mẫu**:
    ```json
    // Đặt lịch mới
    {
      "action": "set_appointment",
      "name": "Lê Văn C",
      "email": "c@example.com",
      "preferred_date": "2024-12-25"
    }

    // Thay đổi lịch
    {
      "action": "reschedule",
      "old_slot": "2024-12-25 10:00",
      "new_preferred_date": "2024-12-26"
    }

    // Hủy lịch
    {
      "action": "cancel",
      "interview_slot": "2024-12-25 10:00"
    }

    // Tra cứu danh sách lớp
    {
      "action": "get_list"
    }

    // Tra cứu thông tin đăng ký
    {
      "action": "get_user_info",
      "email": "a@example.com"
    }
    ```
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **lưu lại**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết nối với Slack/Telegram để thông báo**
- Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** sau các node `Respond Appointment Booking` để **thông báo tức thời** khi có yêu cầu mới.

### **2. Lưu log hoạt động**
- Thêm **node `n8n-nodes-base.file`** để **ghi log** tất cả yêu cầu vào file CSV/JSON trên VPS. Ví dụ:
  ```json
  {
    "timestamp": "2024-10-01T12:00:00Z",
    "action": "set_appointment",
    "user": "Nguyễn Văn A",
    "status": "success",
    "interviewer_assigned": "Phỏng vấn viên 1"
  }
  ```

### **3. Tự động gửi báo cáo hàng tuần**
- Sử dụng **node `n8n-nodes-base.cron`** để chạy **tối ngày thứ 7** và gửi **báo cáo thống kê** (số lượng lịch đặt, hủy, thành công) qua email hoặc Slack.

### **4. Cập nhật AI với mô hình mới**
- Nếu muốn **mô hình AI thông minh hơn**, các sếp có thể:
  - **Thay thế Qwen3:14b** bằng mô hình khác (ví dụ: `llama3`).
  - **Tùy chỉnh prompt** trong nodes `lmChatOllama` để AI trả lời **phù hợp với ngữ cảnh doanh nghiệp**.

### **5. Bảo mật dữ liệu**
- **Không lưu email thực tế** trong log (nếu không cần thiết).
- **Sử dụng Supabase Row Level Security (RLS)** để bảo vệ dữ liệu người dùng.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** cho việc tự động hóa **đặt lịch phỏng vấn, đăng ký lớp học và hỗ trợ AI** mà không cần viết code. Với **Supabase** làm nền tảng dữ liệu và **Ollama** làm não bộ AI, hệ thống sẽ:
✅ **Giải phóng thời gian** của các sếp khỏi việc quản lý lịch thủ công.
✅ **Giảm thiểu lỗi** nhờ AI xử lý logic phức tạp.
✅ **Cung cấp trải nghiệm cá nhân hóa** cho khách hàng.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình Supabase + Ollama.
3. **Test với dữ liệu mẫu** và bật hoạt động.
4. **Mở rộng** bằng cách kết nối Slack, Telegram hoặc báo cáo tự động.

**🚀 Chúc các sếp thành công với hệ thống tự động hóa thông minh nhất!**