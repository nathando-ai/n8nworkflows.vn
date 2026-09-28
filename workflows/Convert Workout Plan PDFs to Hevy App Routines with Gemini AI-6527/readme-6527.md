---
title: "🧠 Chuyển Đổi Bảng Tập PDF Sang Routine Hevy Với AI Gemini - Tự Động Hóa Lịch Luyện Tập Miễn Code"
description: "Workflow tự động hóa chuyển đổi bảng tập PDF thành lịch tập Hevy thông minh bằng AI Gemini, tiết kiệm thời gian lên tới 90% cho các sếp fitness. Giúp bạn không còn phải nhập liệu thủ công, tránh sai sót và tối ưu hóa lịch tập theo chuẩn khoa học."
slug: "chuyen-doi-bang-tap-pdf-sang-routine-hevy-voi-gemini-ai"
tags: [n8n, automation, ai-summarization, fitness-tracking, gemini-ai, hevy-app]
keywords: [n8n workflow fitness, tự động hóa bảng tập PDF, gemini AI chuyển đổi lịch tập, hevy app automation, giải pháp tự động hóa thể dục thể thao]
---

# 🚀 Chuyển Đổi Bảng Tập PDF Sang Routine Hevy Với AI Gemini - Không Cần Code!

### 🔥 **Nỗi Đau Của Các Sếp Fitness**
Các sếp thường phải:
- **Nhập liệu thủ công** từ bảng tập PDF sang Hevy, mất **30-60 phút/lần**.
- **Sai sót cao** do nhập nhầm tên bài tập hoặc cấu trúc.
- **Không tối ưu hóa** vì không biết liệu bài tập đã phù hợp với mục tiêu của mình.
- **Phải tra cứu** tên bài tập trên Hevy để đảm bảo chính xác.

**Workflow này giải quyết tất cả!** Với AI Gemini, bạn chỉ cần **upload PDF**, hệ thống sẽ tự động:
✅ **Trích xuất văn bản** từ PDF.
✅ **So sánh và khớp** bài tập với danh sách Hevy.
✅ **Tạo lịch tập hoàn chỉnh** trên Hevy chỉ trong **vài giây**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn mất giờ nhập liệu thủ công.
- **Chính xác 100%**: AI khớp tên bài tập chính xác theo danh sách Hevy.
- **Tối ưu hóa lịch tập**: Bài tập được sắp xếp theo logic khoa học.
- **Hoạt động 24/7**: Workflow chạy tự động khi có file PDF mới.
- **Giảm sai sót**: Không còn lo lắng về tên bài tập sai hoặc thiếu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Hevy App** (để tạo lịch tập tự động).
2. **API Key của Hevy** (để kết nối với API Hevy).
   - **Lấy API Key**:
     - Đăng nhập Hevy → Cài đặt → **Developer API Key**.
     - Chia sẻ với n8n dưới dạng **HTTP Header Auth** (trong node `httpRequest`).
3. **Tài khoản OpenRouter.ai** (để sử dụng mô hình Gemini AI).
   - **Lấy API Key**:
     - Đăng ký tại [OpenRouter.ai](https://openrouter.ai/) → Tạo API Key.
     - Thêm vào n8n dưới dạng **OpenRouter API Credentials**.
4. **File PDF** (bảng tập cần chuyển đổi).
   - Upload qua **Form Trigger** (node đầu tiên).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6527](https://n8n.io/workflows/6527) hoặc copy JSON từ trang này.
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Node "On form submission" (Trigger)**
- **Cấu hình**:
  - Chọn **"File"** trong **Form Trigger**.
  - **File Type**: Chỉ chọn **PDF** (để tránh file khác).
  - **Lưu ý**: Nếu muốn tự động chạy, có thể thay bằng **Webhook** (node `httpRequest`) và gọi API từ bên ngoài.

##### **B. Node "google/gemini-2.5-flash" (AI Gemini)**
- **Cấu hình**:
  - **Model**: Đã mặc định là `google/gemini-2.5-flash`.
  - **Prompt** (đã sẵn trong workflow):
    ```plaintext
    You are an expert fitness coach. Extract all exercises from the following workout plan PDF text.
    Return a structured JSON with:
    - "exercises": [{"name": "string", "sets": number, "reps": number, "rest": number}]
    ```
  - **Structured Output Parser** (node kế tiếp):
    - **Schema** (đã định sẵn):
      ```json
      {
        "exercises": [
          {
            "name": "string",
            "sets": "number",
            "reps": "number",
            "rest": "number"
          }
        ]
      }
      ```
    - **Lưu ý**: Nếu kết quả AI không chính xác, **cập nhật prompt** để rõ ràng hơn về định dạng output.

##### **C. Node "Create Hevy Routine" (API Hevy)**
- **Cấu hình**:
  - **Method**: `POST` (để tạo routine mới).
  - **URL**: `https://api.hevyapp.com/v1/routines` (mặc định).
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY_HEVY}` (điền từ tài khoản Hevy).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "name": "Auto-Generated Routine from PDF",
      "exercises": [
        {
          "name": "$json.exercises[0].name",
          "sets": $json.exercises[0].sets,
          "reps": $json.exercises[0].reps,
          "rest": $json.exercises[0].rest
        }
      ]
    }
    ```
  - **Lưu ý**:
    - Đảm bảo **danh sách bài tập** trong JSON trùng khớp với danh sách Hevy.
    - Nếu API Hevy yêu cầu thêm trường (ví dụ `program_id`), thêm vào body.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Upload **1 file PDF mẫu** (ví dụ: bảng tập bắp cơ).
  - Kiểm tra **Structured Output Parser** để xem AI trích xuất dữ liệu như thế nào.
  - Nếu sai, **cập nhật prompt** hoặc **schema**.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **đặt lên VPS** để chạy 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node `Create Hevy Routine` để thông báo khi tạo lịch tập thành công.
   - Ví dụ:
     ```json
     {
       "text": "🚀 Lịch tập tự động đã được tạo trên Hevy: $json.name"
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả lịch tập đã tạo.
   - Cấu hình:
     - **Sheet Name**: `Workout_Logs`.
     - **Columns**: `Date`, `Routine Name`, `Exercises`, `Status`.

3. **Tự Động Chuyển Đổi Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để tự động scan folder chứa PDF mới (ví dụ: `C:\Workouts\`).
   - Cấu hình:
     - **Schedule**: `0 0 * * *` (lúc 00:00 hàng ngày).
     - **File Path**: `C:/Workouts/*.pdf`.

4. **Cải Thiện Prompt AI**:
   - Nếu AI không khớp được tên bài tập, **cập nhật prompt** như sau:
     ```plaintext
     You are an expert in Hevy exercise names. For each exercise in the text, match it to the closest name in Hevy's database.
     If an exercise is not found, suggest the closest alternative.
     Return JSON with "matched_exercises" and "unmatched_exercises".
     ```

5. **Xử Lý File Lớn**:
   - Nếu PDF quá lớn, **tách thành nhiều trang** trước khi gửi đến AI.
   - Sử dụng node **Split PDF** (n8n-nodes-base.extractFromFile) với `operation: "splitByPages"`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp fitness khỏi công việc nhập liệu nhàm chán, đồng thời **tăng độ chính xác** và **tối ưu hóa lịch tập**. Với **AI Gemini**, bạn không chỉ có một công cụ tự động hóa, mà còn có một **hệ thống tư vấn thể dục thông minh**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để chạy 24/7).
2. **Import workflow** và cấu hình API Hevy + OpenRouter.
3. **Test với 1 file PDF** và bắt đầu tự động hóa!

:::success[💡 LƯU Ý CUỐI CÙNG]
- Nếu gặp lỗi **API Hevy**, kiểm tra lại **API Key** và **URL API**.
- Nếu AI **không khớp được bài tập**, **cập nhật prompt** để rõ ràng hơn.
- **Backup workflow** trước khi bật Active trên VPS.
:::

**Chúc các sếp tự động hóa thành công!** 💪🚀