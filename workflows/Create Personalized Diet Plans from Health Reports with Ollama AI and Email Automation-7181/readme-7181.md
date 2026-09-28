---
title: "🍽️ Tự Động Hoá Lập Kế Hoạch Ăn Uống Cá Nhân Hóa Từ Báo Cáo Y Tế Với Ollama AI & Email (N8N)"
description: "Workflow tự động hóa 100% không code giúp các bác sĩ, dược sĩ và chuyên gia sức khỏe tạo kế hoạch ăn uống cá nhân hóa từ dữ liệu y tế trong email, tiết kiệm thời gian lên đến 80% so với phương pháp thủ công."
slug: "tieu-dong-hoa-ke-hoach-an-uong-tu-bao-cao-y-te"
tags: [n8n, automation, ollama, ai, email-automation, y-te-su-khoe]
keywords: [n8n workflow y tế, tự động hóa kế hoạch ăn uống, ollama ai, email automation, dược sĩ tự động hóa, báo cáo y tế]
---

# 🚀 **Tự Động Hoá Lập Kế Hoạch Ăn Uống Cá Nhân Hóa Từ Báo Cáo Y Tế Với Ollama AI**

### **Giải pháp cho ai?**
Các sếp làm trong lĩnh vực **y tế, dinh dưỡng, hoặc chăm sóc sức khỏe** đang phải mất **giờ đồng hồ** để phân tích báo cáo y tế (chỉ số cholesterol, glucose, huyết áp...) và viết kế hoạch ăn uống cá nhân hóa cho từng bệnh nhân? **Workflow này sẽ tự động hóa toàn bộ quy trình** chỉ trong vài giây, với độ chính xác cao nhờ AI Ollama!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Tự động xử lý **ngàn báo cáo y tế** trong vài giây thay vì làm thủ công.
✅ **Chính xác cao**: AI Ollama phân tích dữ liệu y tế và đề xuất **kế hoạch ăn uống cá nhân hóa** với độ tin cậy cao.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
✅ **Tích hợp email**: Nhận báo cáo y tế từ email → Xử lý → Gửi kế hoạch ăn uống ngay về email bệnh nhân.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản email IMAP** (để nhận báo cáo y tế):
   - Thông tin IMAP (Server, Port, Username, Password).
   - **Lưu ý**: Cần **cho phép truy cập IMAP** trong cài đặt email (Gmail, Outlook, Yahoo...).
2. **API Key Ollama** (để kết nối với mô hình AI):
   - Cài đặt Ollama trên máy chủ hoặc máy local (hướng dẫn: [ollama.ai](https://ollama.ai/)).
   - **Mô hình AI khuyến nghị**: `llama3` hoặc `mistral`.
3. **Tài khoản SMTP** (để gửi email kết quả):
   - Thông tin SMTP (Server, Port, Username, Password).
   - **Lưu ý**: Nếu dùng Gmail, cần **bật "Less Secure Apps"** hoặc tạo **App Password**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7181](https://n8n.io/workflows/7181) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Create New Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Node "Receive Health Report Email" (emailReadImap)**
- **Chọn credentials**: `imap` (đã tạo trước khi import).
- **Cấu hình**:
  - **Host**: `imap.gmail.com` (hoặc `imap.yourdomain.com`).
  - **Port**: `993` (SSL).
  - **Username**: Email nhận báo cáo y tế.
  - **Password**: App Password (nếu dùng Gmail).
  - **Folder**: `INBOX` (hoặc folder chứa báo cáo y tế).
  - **Search Query**: `FROM "bacsi@yte.com"` (để chỉ lấy email từ bác sĩ).

##### **B. Node "Process Report with AI Nutrition Engine" (chainLlm)**
- **Không cần cấu hình** (n8n sẽ tự động truyền dữ liệu từ node trước sang node sau).

##### **C. Node "AI Nutrition Model" (lmOllama)**
- **Chọn credentials**: `ollamaApi` (đã tạo trước khi import).
- **Cấu hình Prompt**:
  ```plaintext
  Tôi là một chuyên gia dinh dưỡng. Hãy phân tích dữ liệu y tế sau và đề xuất một kế hoạch ăn uống cá nhân hóa trong 7 ngày:
  - Chỉ số cholesterol: {{$json["cholesterol"]}}
  - Chỉ số glucose: {{$json["glucose"]}}
  - Huyết áp: {{$json["blood_pressure"]}}
  - Chỉ số BMI: {{$json["bmi"]}}
  Kết quả phải bao gồm:
  1. Lịch ăn uống chi tiết (bữa sáng, trưa, tối).
  2. Danh sách thực phẩm khuyến nghị và tránh.
  3. Gợi ý bài tập phù hợp.
  ```
  - **Lưu ý**: Thay thế `{{$json["key"]}}` bằng các trường dữ liệu thực tế trong email (ví dụ: `{{$json["emailBody"]}}`).

##### **D. Node "Wait Before Sending Plan" (wait)**
- **Thời gian chờ**: `30000` (30 giây) → **Cần điều chỉnh** nếu cần thời gian xử lý dài hơn.

##### **E. Node "Send Personalized Diet Plan" (emailSend)**
- **Chọn credentials**: `smtp` (đã tạo trước khi import).
- **Cấu hình**:
  - **From**: Email gửi kết quả (ví dụ: `dinhduong@yte.com`).
  - **To**: `{{$json["email"]}}` (địa chỉ email bệnh nhân).
  - **Subject**: `Kế hoạch ăn uống cá nhân hóa cho bạn`.
  - **HTML Content**: Sử dụng template HTML để hiển thị kế hoạch ăn uống đẹp mắt.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email mẫu chứa **báo cáo y tế** (ví dụ: `Chỉ số cholesterol: 220 mg/dL, Glucose: 150 mg/dL`).
   - Chạy workflow và kiểm tra kết quả.
2. **Bật Active** sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả ngay khi workflow hoàn tất.
2. **Lưu log vào Google Sheets**:
   - Thêm node `n8n-nodes-base.googleSheets` để ghi lại lịch sử các kế hoạch ăn uống.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để tự động gửi kế hoạch ăn uống hàng tuần.
4. **Cải thiện Prompt AI**:
   - Thêm yêu cầu cụ thể hơn cho AI (ví dụ: "Không đề xuất thực phẩm chứa đường").

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong lĩnh vực y tế, giúp họ tập trung vào **chăm sóc bệnh nhân** thay vì làm thủ công. **Hãy tự động hóa ngay hôm nay** và đưa **AI vào việc làm** của mình!

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/7181) và **self-host n8n** trên VPS để chạy 24/7!

---
**Chia sẻ & phản hồi**: Nếu các sếp có bất kỳ câu hỏi hoặc đề xuất cải tiến, hãy comment bên dưới hoặc liên hệ với **Oneclick AI Squad** qua [website](https://oneclickai.squad/).