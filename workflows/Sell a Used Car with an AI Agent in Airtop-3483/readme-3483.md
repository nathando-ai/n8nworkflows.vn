---
title: "🚀 Tự Động Hóa Bán Xe Cũ Với AI Agent Trên Airtop - Không Cần Code!"
description: "Workflow này tự động tương tác với trang web bán xe cũ, lấy thông tin chi tiết, tính giá và nhận báo giá mua lại từ AI Agent Airtop - tiết kiệm thời gian lên đến 80% cho các sếp kinh doanh xe cũ."
slug: "tieu-dong-hoa-ban-xe-cu-voi-ai-agent-airtop"
tags: [n8n, automation, ai-agent, airtop, no-code, bán xe cũ]
keywords: [n8n workflow bán xe cũ, tự động hóa bán xe cũ, AI Agent Airtop, tính giá xe cũ, báo giá mua lại xe]
---

# 🚀 **Tự Động Hóa Bán Xe Cũ Với AI Agent Airtop - Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Kinh Doanh Xe Cũ**
Bán xe cũ thủ công là một quá trình **mệt mỏi, tốn thời gian và dễ sai sót**:
- **Lặp đi lặp lại**: Phải nhập liệu chi tiết xe (VIN, năm sản xuất, trạng thái,...) vào nhiều trang web để lấy báo giá.
- **Rủi ro sai sót**: Thông tin nhập sai dẫn đến báo giá không chính xác hoặc mất cơ hội bán với giá cao nhất.
- **Thời gian chờ**: Phải chờ đợi phản hồi từ nhiều bên mua lại, làm chậm quá trình quyết định.
- **Không tối ưu giá**: Không biết được giá trị thực sự của xe trên thị trường, dẫn đến bán với giá thấp hơn giá thị trường.

**Workflow này giải quyết tất cả!** Sử dụng **AI Agent Airtop** kết hợp với **n8n**, bạn có thể:
✅ **Tự động lấy thông tin xe** từ trang web (VIN, năm sản xuất, km, trạng thái,...).
✅ **Tính giá xe chính xác** dựa trên dữ liệu thị trường.
✅ **Nhận báo giá mua lại** từ nhiều bên một cách tự động.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không gián đoạn, các sếp nên **self-host n8n** trên một **VPS ổn định**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI Agent)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, AI tự động lấy và phân tích thông tin xe.
- **Giá bán tối ưu**: AI Agent **so sánh giá thị trường** và đưa ra báo giá mua lại **cực kỳ chính xác**.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
- **Không sai sót**: AI **không mệt mỏi** và **không bị lỗi nhập liệu** như con người.
- **Tăng doanh thu**: Bán xe với **giá cao nhất** nhờ phân tích thị trường tự động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Airtop AI** (để sử dụng AI Agent):
   - [Đăng ký tài khoản Airtop](https://www.airtop.ai/) (miễn phí hoặc trả phí tùy thuộc vào nhu cầu).
   - **API Key Airtop** (tạo trong **Credentials** của n8n).
✔ **Thông tin xe cần bán**:
   - **VIN (Số khung xe)** hoặc **bản sao giấy tờ xe** (nếu AI Agent cần tương tác trực tiếp).
   - **Link trang web** (nếu muốn AI Agent lấy thông tin từ trang bán xe cụ thể).
✔ **n8n Self-hosted** (không thể chạy trên n8n Cloud do yêu cầu AI Agent).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/3483](https://n8n.io/workflows/3483) và **import vào n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste vào n8n Editor** (tab "Import").

:::note[Lưu ý khi import]
- **Không chỉnh sửa cấu trúc** của workflow trừ khi biết rõ logic.
- **Đảm bảo n8n phiên bản ≥ 1.0** (do sử dụng nodes Airtop mới).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **không hoàn toàn tự động** vì cần **cài đặt và cấu hình** một số node quan trọng:

##### **A. Cấu Hình Credentials Airtop**
- **Tạo credential Airtop**:
  1. Trong **n8n Editor**, vào **Credentials** (cánh cửa sổ bên trái).
  2. Nhấn **"Add"** → Chọn **"Airtop"**.
  3. Điền:
     - **Name**: `airtopApi` (phải trùng với keyParameters trong nodes).
     - **API Key**: Copy từ **Airtop Dashboard** (trong tài khoản của bạn).
     - **Base URL**: `https://api.airtop.ai` (mặc định).

##### **B. Cấu Hình Node "Create session"**
- **Resource**: `https://www.example.com` (thay bằng **trang web bạn muốn AI tương tác**, ví dụ: `https://www.vinfast.com`).
- **Browser**: Chọn **Chrome** (Airtop hỗ trợ Chrome best).

##### **C. Cấu Hình Node "Think next action" (Prompt AI)**
- **Prompt** đã được cấu hình sẵn để:
  - **Tính giá xe** dựa trên thông tin VIN.
  - **Nhận báo giá mua lại** từ AI Agent.
- **Không cần chỉnh sửa** trừ khi muốn **tùy biến logic** (ví dụ: thêm điều kiện khác).

##### **D. Node "Click VIN button"**
- **Selector**: Điền **CSS Selector** của nút **nhập VIN** trên trang web (ví dụ: `#vin-input`).
  - **Lấy CSS Selector**:
    1. Mở **DevTools** (F12) trên trang web.
    2. Chọn nút cần click → **Copy Selector** (trong tab Elements).

##### **E. Node "Load website"**
- **URL**: Điền **trang web chính** của xe (ví dụ: `https://www.vinfast.com/xe-may/vinfast-maverick`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test Workflow"** và điền **VIN của xe** vào node **"Parse response"** (nếu cần).
   - Kiểm tra **log** để đảm bảo AI Agent tương tác đúng.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi có yêu cầu.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để **báo cáo kết quả** (báo giá, giá thị trường) ngay khi AI Agent hoàn thành.
   - **Cách làm**:
     - Sau node **"Offer received"**, thêm node **Slack** với message:
       ```json
       {"text": "🚗 Xe {{$node["Variables"].json["vin"]}} đã nhận báo giá: {{$node["Offer received"].json["price"]}}"}
       ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Airtable** để **lưu tất cả lịch sử báo giá** của xe.
   - **Cách làm**:
     - Sau node **"Offer received"**, thêm node **Google Sheets** với:
       - **Sheet Name**: `Báo giá xe cũ`
       - **Row**: `{{$json}}` (để lưu toàn bộ dữ liệu).

3. **Tự Động Bán Xe Khi Có Báo Giá Tốt**:
   - Sử dụng **node "Switch"** để **so sánh báo giá** với giá mục tiêu.
   - Nếu báo giá cao hơn **ngưỡng** (ví dụ: 80% giá thị trường), tự động **gửi yêu cầu bán** qua email hoặc Slack.

4. **Tích Hợp với CRM (HubSpot, Zoho)**:
   - Sau khi nhận báo giá, **cập nhật thông tin xe** vào CRM để **theo dõi tiến độ bán**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhập liệu, tính giá và chờ đợi báo giá** khi bán xe cũ. Với **AI Agent Airtop**, bạn không chỉ **tiết kiệm thời gian** mà còn **bán xe với giá cao nhất** nhờ phân tích thị trường tự động.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Airtop API** và **CSS Selector**.
3. **Test và bật Active** để bắt đầu tự động hóa bán xe!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ **Airtop Support** để được hỗ trợ!

---
**#TựĐộngHóaBánXe #AIAgent #n8nWorkflows #BánXeCũKhôngCầnCode**