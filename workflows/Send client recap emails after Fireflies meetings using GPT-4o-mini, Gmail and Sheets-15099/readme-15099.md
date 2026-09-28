---
title: "🤖 Tự Động Gửi Email Tóm Tắt Cuộc Họp Khách Hàng Sau Fireflies Với GPT-4o-mini, Gmail & Sheets – Giải Pháp Lead Nurturing AI 100% Không Code"
description: "Giải pháp tự động hóa hoàn toàn cho các account manager, consultant và chủ doanh nghiệp gửi email tóm tắt chuyên nghiệp sau mỗi cuộc họp Fireflies. Sử dụng GPT-4o-mini viết nội dung, Gmail gửi email cá nhân hóa và Google Sheets theo dõi tất cả hoạt động – tiết kiệm 5+ giờ/lần/người."
slug: "tu-dong-hoa-email-tom-tat-fireflies-gpt4o-mini"
tags: [n8n, automation, lead-nurturing, ai-summarization, fireflies, gmail, google-sheets, gpt-4o-mini]
keywords: [tự động hóa email sau cuộc họp, fireflies n8n workflow, gửi email tóm tắt khách hàng, gpt-4o-mini tự động hóa, lead nurturing không code, tự động hóa cuộc họp doanh nghiệp]
---

# 🚀 **Tự Động Gửi Email Tóm Tắt Cuộc Họp Khách Hàng Sau Fireflies – Giải Pháp AI 100% Không Code**

## **Nỗi Đau Của Các Sếp Và Giải Pháp Của Workflow Này**
Hàng ngày, các **account manager**, **consultant** và **chủ doanh nghiệp** phải:
- **Ghi chép lại nội dung cuộc họp** sau khi Fireflies hoàn thành phiên bản transcript.
- **Viết email tóm tắt** (250-300 từ) để gửi cho khách hàng – mất **30-60 phút/lần**.
- **Lo lắng về chất lượng nội dung** – liệu email có chuyên nghiệp, cá nhân hóa và không có dấu vết AI?
- **Không theo dõi được lịch sử** – không biết đã gửi cho khách hàng nào và nội dung gì.

**Workflow này giải quyết tất cả!**
Sau khi Fireflies hoàn thành ghi âm cuộc họp, hệ thống sẽ:
✅ **Tự động phát hiện email khách hàng** (từ danh sách tham dự, tiêu đề cuộc họp hoặc mặc định).
✅ **Sử dụng GPT-4o-mini viết email tóm tắt chuyên nghiệp** (250 từ, không dấu vết AI, không liên kết Fireflies).
✅ **Gửi email qua Gmail** với địa chỉ **Reply-To** là của bạn (để quản lý phản hồi dễ dàng).
✅ **Lưu lịch sử gửi vào Google Sheets** để theo dõi tất cả hoạt động.

**Kết quả?** **Tiết kiệm 5+ giờ/tháng**, **cải thiện trải nghiệm khách hàng** và **tăng hiệu quả lead nurturing** mà không cần viết code!

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải viết email tóm tắt sau mỗi cuộc họp.
- **Nội dung chuyên nghiệp**: Email được viết bởi GPT-4o-mini với **tôn trọng khách hàng** (không có dấu vết AI).
- **Cá nhân hóa hoàn toàn**: Hệ thống tự động phát hiện email khách hàng từ danh sách tham dự.
- **Quản lý dễ dàng**: Tất cả lịch sử gửi được lưu vào **Google Sheets** với chi tiết cuộc họp, nội dung email và trạng thái.
- **Hoạt động 24/7**: Không cần can thiệp thủ công – tự động chạy sau mỗi cuộc họp Fireflies.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Fireflies** (để lấy transcript và webhook).
2. **API Key Fireflies** (để fetch dữ liệu cuộc họp).
3. **Tài khoản Gmail** (để gửi email, phải là tài khoản chính của bạn).
4. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini).
5. **Google Sheets** (để lưu lịch sử gửi email).
6. **Địa chỉ email mặc định** (nếu không phát hiện được email khách hàng từ danh sách tham dự).
7. **Domain của công ty** (để hệ thống tự động phát hiện email khách hàng).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15099](https://n8n.io/workflows/15099) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (Menu → Import → Paste JSON).

:::note[LƯU Ý]
- **Không sử dụng phiên bản n8n Cloud** (nên cài **Self-hosted** trên VPS để tránh giới hạn API).
- **Không chia sẻ API Key** (đặc biệt là OpenAI và Gmail OAuth2).
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Webhook — Fireflies Transcript Done**
- **Không cần chỉnh gì** (n8n sẽ tự động tạo URL webhook).
- **Lưu ý**: Sau khi import, **copy URL webhook** từ node này và **dán vào Fireflies**:
  - Mở **Fireflies → Settings → Developer Settings → Webhooks**.
  - Thêm **New Webhook** với:
    - **URL**: `https://[your-n8n-url]/fireflies-recap-email` (đường dẫn từ node webhook).
    - **Event**: `transcript_done`.

#### **🔹 Node 2: Set — Config Values**
**BẮT BUỘC điền đầy đủ 7 trường sau**:
| Trường | Mô Tả | Ví Dụ |
|--------|--------|--------|
| **Fireflies API Key** | API Key từ Fireflies (trong **Settings → Developer Settings**). | `ff_abc123xyz...` |
| **Sender Name** | Tên người gửi (hiển thị trong email). | `John Doe` |
| **Sender Email** | Email của bạn (được hiển thị trong Reply-To). | `john@example.com` |
| **Company Name** | Tên công ty của bạn. | `Tech Solutions Inc.` |
| **Google Sheet ID** | ID của Google Sheet (tìm trong liên kết share: `https://docs.google.com/spreadsheets/d/[ID]...`). | `1A2b3C4d5E6f7G8h9I0j1K2l3M4n5O6p7Q8r9S0t1U2v3W4x5Y6z7` |
| **Default Client Email** | Email mặc định nếu không phát hiện được (ví dụ: `client@example.com`). | `client@example.com` |
| **Your Email Domain** | Domain email của bạn (ví dụ: `example.com`). | `example.com` |

#### **🔹 Node 3: HTTP — Fetch Transcript**
- **Không cần chỉnh gì** (n8n sẽ tự động lấy dữ liệu từ Fireflies bằng API Key đã đặt ở Node 2).

#### **🔹 Node 4: Code — Extract Data and Detect Client Email**
- **Không cần chỉnh** (hệ thống tự động phát hiện email khách hàng theo 3 chiến lược):
  1. **Phát hiện từ danh sách tham dự** (nếu email khác domain của bạn).
  2. **Phát hiện từ tiêu đề cuộc họp** (nếu có email trong tiêu đề).
  3. **Sử dụng email mặc định** (nếu không phát hiện được).

#### **🔹 Node 5: AI Agent — Write Recap Email**
- **Không cần chỉnh gì** (GPT-4o-mini sẽ tự động viết email với cấu trúc:
  - **Greeting** (chào đón khách hàng).
  - **Tóm tắt nội dung chính** (dưới dạng danh sách).
  - **Action items** (nhiệm vụ tiếp theo).
  - **Closing** (kết thúc chuyên nghiệp).

#### **🔹 Node 6: OpenAI — GPT-4o-mini Model**
- **BẮT BUỘC kết nối OpenAI**:
  1. Mở **Credentials** trong n8n.
  2. Thêm **OpenAI** với:
     - **API Key**: API Key từ tài khoản OpenAI.
     - **Model**: `gpt-4o-mini` (đã được cài đặt trong workflow).
  3. **Chọn credential này** trong Node 6.

#### **🔹 Node 7: Code — Prepare Email Fields**
- **Không cần chỉnh** (hệ thống tự động xây dựng **subject** và **nội dung email** từ output của GPT-4o-mini).

#### **🔹 Node 8: Gmail — Send Recap Email**
- **BẮT BUỘC kết nối Gmail OAuth2**:
  1. Mở **Credentials** trong n8n.
  2. Thêm **Gmail** với:
     - **Email**: `john@example.com` (phải là email đã đặt ở Node 2).
     - **Password**: Đăng nhập và cho phép quyền truy cập.
  3. **Chọn credential này** trong Node 8.

#### **🔹 Node 9: Google Sheets — Log Sent Recaps**
- **BẮT BUỘC kết nối Google Sheets OAuth2**:
  1. Mở **Credentials** trong n8n.
  2. Thêm **Google Sheets** với:
     - **Email**: Email Google của bạn.
     - **Password**: Đăng nhập và cho phép quyền truy cập.
  3. **Chọn credential này** trong Node 9.
  4. **Chỉnh Sheet ID** (nếu khác với Node 2).
  5. **Chỉnh tab** thành `Recap Email Log` (nếu khác).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với một cuộc họp mẫu:
   - Gọi API webhook với payload mẫu (có thể lấy từ Fireflies khi có cuộc họp).
   - Kiểm tra **output** của mỗi node để đảm bảo không có lỗi.
2. **Bật Active workflow**:
   - Click vào **Active** ở góc trên bên phải → **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Email Tóm Tắt**
- **Thêm template cá nhân hóa**:
  - Trong Node 5 (AI Agent), bạn có thể **cập nhật prompt** để thêm:
    - **Tên công ty khách hàng** (nếu có trong transcript).
    - **Link tài liệu tham khảo** (nếu có).
    - **Câu hỏi mở** (ví dụ: *"Bạn có ý kiến nào về [điểm này] không?"*).
  - **Ví dụ prompt nâng cao**:
    ```json
    "You are a professional meeting recap writer. Write a 250-word email summary for {clientName} at {clientCompany} based on the following meeting details:
    - Title: {meetingTitle}
    - Date: {meetingDate}
    - Key Points: {keyPoints}
    - Action Items: {actionItems}
    - Gist: {gist}
    The email should include:
    1. A warm greeting with the client's name.
    2. A brief thank-you for their time.
    3. A structured summary of key points (bullet points).
    4. Clear action items with deadlines (if any).
    5. A professional closing with next steps.
    6. No mention of AI or Fireflies.
    7. Reply-To should be {senderEmail}."
    ```

### **2. Theo Dõi & Báo Cáo Định Kỳ**
- **Tạo dashboard Google Data Studio** từ Google Sheets để:
  - **Báo cáo số lượng email đã gửi**.
  - **Phân tích phản hồi khách hàng** (nếu có).
  - **Theo dõi hiệu suất lead nurturing**.
- **Gửi báo cáo tự động** qua Slack/Telegram:
  - Sử dụng **node Slack/Telegram** kết nối với Google Sheets để gửi thông báo khi có email mới được gửi.

### **3. Xử Lý Lỗi & Log Debugging**
- **Thêm node StickyNote** để ghi chú lỗi:
  - Trong Node 6 (OpenAI), thêm **StickyNote** để lưu **error message** nếu GPT-4o-mini trả về lỗi.
  - Trong Node 8 (Gmail), thêm **StickyNote** để ghi **status** của email (gửi thành công/thất bại).
- **Sử dụng node Code để log lỗi**:
  ```javascript
  // Node 8 (Gmail) - Sau khi gửi email
  if ($json["status"] === "error") {
    $node.setError($json["errorMessage"]);
  }
  ```

### **4. Kết Hợp Với CRM (Salesforce, HubSpot)**
- **Sử dụng node Salesforce/HubSpot** để:
  - **Cập nhật trạng thái lead** sau khi gửi email.
  - **Ghi chú cuộc họp** vào CRM.
  - **Phân loại khách hàng** dựa trên phản hồi.

---
## 📌 **Kết Luận: Áp Dụng Ngay & Tăng Hiệu Quả Lead Nurturing!**

Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** và **quan hệ khách hàng** thay vì việc **ghi chép và gửi email thủ công**. Với **GPT-4o-mini viết nội dung chuyên nghiệp**, **Gmail gửi email cá nhân hóa** và **Google Sheets theo dõi lịch sử**, bạn đã có một **hệ thống tự động hóa lead nurturing hoàn chỉnh** mà **không cần viết một dòng code nào!**

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Cài đặt n8n trên VPS** (để tránh giới hạn API).
2. **Import workflow** và **cấu hình các node** theo hướng dẫn.
3. **Test với một cuộc họp mẫu** trước khi bật hoạt động 24/7.
4. **Theo dõi Google Sheets** để đảm bảo tất cả email được gửi và lưu trữ đúng.
5. **Tối ưu hóa prompt** để email trở nên **cá nhân hóa hơn**.
:::

**🚀 Đừng bỏ lỡ cơ hội tự động hóa quy trình này – bắt đầu ngay từ hôm nay!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã