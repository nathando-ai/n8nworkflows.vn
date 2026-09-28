---
title: "🤖 Tự Động Chất Lượng Lead Inbound với AI Gọi Điện Vapi + Log Kết Quả lên Google Sheets (N8N)"
description: "Giải pháp tự động hóa 100% không code giúp các doanh nghiệp nhanh chóng lọc và đánh giá chất lượng lead mới qua cuộc gọi AI tự động, đồng thời ghi chép kết quả chi tiết vào Google Sheets. Tiết kiệm thời gian, tăng hiệu quả bán hàng và tối ưu quy trình chăm sóc khách hàng."
slug: "tieu-dong-chat-luong-lead-voi-ai-goi-dien-vapi"
tags: [n8n, automation, lead-generation, ai-chatbot, google-sheets, vapi, no-code]
keywords: [n8n workflow tự động hóa lead, AI gọi điện tự động, chất lượng lead inbound, log kết quả vào Google Sheets, Vapi AI, tự động hóa bán hàng]
---

# 🚀 **Tự Động Chất Lượng Lead Inbound với AI Gọi Điện Vapi + Log Kết Quả lên Google Sheets**

## **Nỗi Đau Của Các Sếp: Tốn Thời Gian Và Tài Nguyên Cho Lead Không Chất Lượng**
Hàng ngày, các đội bán hàng và marketing phải dành nhiều giờ để gọi điện, gửi email hoặc chat với lead mới để xác minh thông tin, đánh giá sự hứng thú và khả năng mua hàng. Quá trình này không chỉ tốn thời gian mà còn dễ gây mất niềm tin với khách hàng nếu không được xử lý chuyên nghiệp. **Workflow này giải quyết vấn đề này bằng cách:**
- **Gọi điện tự động** qua AI để chất lượng lead ngay lập tức (không cần nhân viên gọi điện).
- **Lọc bỏ lead không hợp lệ** (số điện thoại sai, không trả lời) tự động.
- **Ghi chép kết quả chi tiết** vào Google Sheets với thông tin AI extra như: sự hứng thú dịch vụ, động cơ mua hàng, mức độ khẩn cấp, kinh nghiệm trước đây, ngân sách và ý định mua.
- **Tối ưu quy trình** bằng cách loại bỏ công việc thủ công, giảm thiểu sai sót và tăng hiệu quả chăm sóc khách hàng.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gọi điện thủ công, tự động hóa 100% quy trình chất lượng lead.
- **Chính xác cao**: AI gọi điện 24/7, không mệt mỏi và không bỏ lỡ thông tin quan trọng.
- **Dữ liệu chi tiết**: Ghi chép tất cả kết quả vào Google Sheets với các thông tin AI extra, giúp phân tích và quyết định marketing chính xác hơn.
- **Tối ưu nguồn lực**: Loại bỏ lead không hợp lệ ngay từ đầu, tập trung vào khách hàng có tiềm năng cao.
- **Hoạt động liên tục**: Workflow chạy tự động, không cần can thiệp người dùng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Vapi**:
   - Đăng ký và cấu hình một **Voice Assistant** trên [Vapi](https://www.vapi.ai/) với các trường extra output sau:
     - `Service Interest` (Sự hứng thú dịch vụ)
     - `Motivation` (Động cơ mua hàng)
     - `Urgency` (Mức độ khẩn cấp)
     - `Past Experience` (Kinh nghiệm trước đây)
     - `Budget` (Ngân sách)
     - `Intent` (Ý định mua)
   - Lấy **Assistant ID** và **Phone Number ID** từ trang quản lý Vapi.
   - Lấy **API Key** của Vapi để kết nối với n8n (Bearer Token).

2. **Google Sheets**:
   - Tạo một bảng Google Sheets với các cột sau (đảm bảo tên cột chính xác):
     ```
     Date, Name, Phone, Email, Company, Role, Request, Company Size, Service Interest, Motivation, Urgency, Past Experience, Budget, Intent?, Status
     ```
   - Cung cấp quyền chia sẻ cho n8n (URL bảng + token API của Google Sheets).

3. **Tài khoản n8n**:
   - N8N Cloud (miễn phí cho dự án nhỏ) hoặc **Self-hosted** (khuyến nghị cho sản xuất 24/7).
   - Cài đặt **credentials** cho:
     - Vapi (Bearer Token).
     - Google Sheets (Service Account hoặc OAuth 2.0).

4. **Form nhận lead**:
   - Một trang web hoặc công cụ (như Typeform, Google Form, hoặc trang HTML đơn giản) để thu thập thông tin lead (tên, số điện thoại, email, công ty, vai trò, yêu cầu).
   - **Lưu ý**: Sử dụng node `formTrigger` trong n8n để bắt đầu workflow khi có submission mới.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13948](https://n8n.io/workflows/13948) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** (trang chủ của workflow) và chọn **Import Workflow** (từ menu hàng đầu).
- Chọn file JSON đã tải hoặc dán toàn bộ JSON vào ô nhập liệu và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **13 node**, nhưng các bước quan trọng nhất cần chú ý như sau:

##### **A. Cấu Hình Node `On form submission` (formTrigger)**
- **Mục đích**: Bắt đầu workflow khi lead submit thông tin qua form.
- **Lưu ý**:
  - Đảm bảo form của bạn gửi dữ liệu dưới dạng **JSON** hoặc **x-www-form-urlencoded**.
  - Thêm **URL Webhook** của node này vào form (thông tin này sẽ hiển thị khi bạn click vào node `On form submission` trong n8n Editor).
  - Ví dụ: Nếu form của bạn là trên Typeform, bạn sẽ cần tạo một **Webhook Integration** và gán URL Webhook từ n8n vào đó.

##### **B. Cấu Hình Node `Standardize Data` (Code)**
- **Mục đích**: Chuyển đổi số điện thoại thành định dạng 10 chữ số (US format).
- **Lưu ý**:
  - Node này sử dụng **JavaScript** để chuẩn hóa dữ liệu. Nếu số điện thoại của lead không hợp lệ, nó sẽ được chuyển đến node `Log Incorrect Phone`.
  - **Không cần chỉnh sửa** nếu bạn sử dụng định dạng US. Nếu số điện thoại quốc tế, cần chỉnh sửa mã nguồn trong node này.

##### **C. Cấu Hình Node `Call Lead` (httpRequest)**
- **Mục đích**: Gọi điện AI qua Vapi để chất lượng lead.
- **Lưu ý**:
  - **Thay đổi JSON body** trong node này để phù hợp với cấu hình của bạn:
    ```json
    {
      "method": "POST",
      "url": "https://api.vapi.ai/v1/calls",
      "headers": {
        "Authorization": "Bearer YOUR_VAPI_API_KEY",
        "Content-Type": "application/json"
      },
      "body": {
        "to": "{{$node["Standardize Data"].json["phone"]}}",
        "from": "YOUR_VAPI_PHONE_NUMBER_ID",
        "assistantId": "YOUR_VAPI_ASSISTANT_ID",
        "structuredOutputs": [
          {
            "uuid": "YOUR_SERVICE_INTEREST_UUID",
            "name": "Service Interest"
          },
          {
            "uuid": "YOUR_MOTIVATION_UUID",
            "name": "Motivation"
          },
          // Thêm các UUID khác tương ứng với các trường extra output của bạn
        ]
      }
    }
    ```
  - **Thay thế**:
    - `YOUR_VAPI_API_KEY` bằng API Key của bạn.
    - `YOUR_VAPI_PHONE_NUMBER_ID` bằng ID số điện thoại từ Vapi.
    - `YOUR_VAPI_ASSISTANT_ID` bằng ID của Voice Assistant.
    - `YOUR_SERVICE_INTEREST_UUID`, `YOUR_MOTIVATION_UUID`, ... bằng UUID của các trường extra output trong Vapi.

##### **D. Cấu Hình Node `Log Complete` (googleSheets)**
- **Mục đích**: Ghi kết quả cuộc gọi vào Google Sheets.
- **Lưu ý**:
  - **Thay đổi JSON body** để trích xuất dữ liệu từ Vapi và ghi vào bảng:
    ```json
    {
      "operation": "append",
      "sheetName": "Sheet1",
      "values": [
        {
          "Date": "{{$node["Get Call Details"].json["date"]}}",
          "Name": "{{$node["On form submission"].json["name"]}}",
          "Phone": "{{$node["On form submission"].json["phone"]}}",
          "Email": "{{$node["On form submission"].json["email"]}}",
          "Company": "{{$node["On form submission"].json["company"]}}",
          "Role": "{{$node["On form submission"].json["role"]}}",
          "Request": "{{$node["On form submission"].json["request"]}}",
          "Service Interest": "{{$node["Get Call Details"].json["structuredOutputs"]["Service Interest"]}}",
          "Motivation": "{{$node["Get Call Details"].json["structuredOutputs"]["Motivation"]}}",
          "Urgency": "{{$node["Get Call Details"].json["structuredOutputs"]["Urgency"]}}",
          "Past Experience": "{{$node["Get Call Details"].json["structuredOutputs"]["Past Experience"]}}",
          "Budget": "{{$node["Get Call Details"].json["structuredOutputs"]["Budget"]}}",
          "Intent?": "{{$node["Get Call Details"].json["structuredOutputs"]["Intent"]}}",
          "Status": "Completed"
        }
      ]
    }
    ```
  - **Thay thế**:
    - `Sheet1` bằng tên sheet của bạn.
    - Các trường `structuredOutputs` phải khớp với UUID trong Vapi (đã cấu hình ở bước C).

##### **E. Cấu Hình Credentials**
- **Vapi**:
  - Trong node `Call Lead` và `Get Call Details`, chọn **Credentials** là `Vapi` (đã cấu hình trước).
- **Google Sheets**:
  - Trong các node `Log Incorrect Phone`, `Log Voicemail`, và `Log Complete`, chọn **Credentials** là `Google Sheets` (đã cấu hình trước).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và gửi một lead mẫu qua form để kiểm tra.
  - Kiểm tra Google Sheets xem kết quả có được ghi đúng không.
- **Active Workflow**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi Email/Báo Cáo Tự Động**:
   - Thêm node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` để gửi thông báo khi lead có **intent cao** (ví dụ: `Intent? = "Yes"`).
   - Ví dụ: Gửi email cho đội bán hàng khi lead có `Urgency = "High"` và `Budget = "High"`.

2. **Lưu Log Chi Tiết**:
   - Thêm node `n8n-nodes-base.fileSystem` hoặc `n8n-nodes-base.ftp` để lưu file log của mỗi cuộc gọi (như audio hoặc transcript) vào VPS hoặc cloud storage.

3. **Tích Hợp CRM**:
   - Kết nối với **HubSpot**, **Salesforce**, hoặc **Zoho CRM** để tự động cập nhật lead đã chất lượng vào hệ thống CRM.

4. **Cấu Hình Thời Gian Chờ**:
   - Điều chỉnh thời gian chờ trong node `Wait` (60s mặc định) để phù hợp với thời gian cuộc gọi trung bình của bạn.

5. **Lọc Lead Theo Động Cơ**:
   - Sử dụng node `n8n-nodes-base.if` để phân loại lead theo `Motivation` (ví dụ: chỉ gửi lead có `Motivation = "Cost Savings"` đến đội bán hàng chuyên dụng).

6. **Tích Hợp Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả cuộc gọi ngay lập tức vào kênh team.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa quy trình chất lượng lead một cách hiệu quả, không cần code. Bằng cách kết hợp **AI gọi điện Vapi** và **Google Sheets**, bạn không chỉ tiết kiệm thời gian mà còn nhận được **dữ liệu chi tiết** để ra quyết định marketing chính xác hơn.

**Hành động ngay hôm nay**:
1. **Chuẩn bị tài khoản Vapi và Google Sheets** theo hướng dẫn trên.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test run** với lead mẫu và **active workflow** để bắt đầu tự động hóa!

---
:::note[CHÚ Ý]
- **Self-hosted n8n** được khuyến nghị để workflow chạy 24/7 mà không bị giới hạn.
- **Đăng ký VPS TinoHost** với mã giảm giá **VPSN8N** để tiết kiệm chi phí:
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%)
- Nếu gặp vấn đề, tham khảo [hỗ trợ n8n](https://docs.n8n.io/) hoặc cộng đồng [n8n Community](https://community.n8n.io/).
:::

---
**Bắt đầu tự động hóa ngay hôm nay và để AI làm việc thay bạn!** 🚀