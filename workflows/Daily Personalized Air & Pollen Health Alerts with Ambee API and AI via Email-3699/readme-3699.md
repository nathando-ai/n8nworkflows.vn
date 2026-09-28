---
title: "🌬️ **Cảnh báo Khí tượng & Bụi Phấn cá nhân hóa hàng ngày bằng API Ambee + AI qua Email (Miễn phí!)**"
description: "Tự động hóa nhận cảnh báo sức khỏe về chất lượng không khí và bụi phấn hàng ngày, được cá nhân hóa theo vị trí và tình trạng sức khỏe của bạn. Sử dụng API Ambee miễn phí + AI GPT-4.1 để gửi email cảnh báo tự động mỗi sáng, giúp bạn chủ động bảo vệ sức khỏe mỗi ngày."
slug: "cau-bao-khi-tieu-bui-phan-ai-ambee-email"
tags: [n8n, automation, no-code, ai-chatbot, ambee-api, email-automation, self-hosted]
keywords: [tự động hóa cảnh báo khí tượng, bụi phấn hàng ngày, api ambee miễn phí, n8n workflow ai, email cảnh báo sức khỏe, tự động hóa no-code]
---

# 🚀 **Cảnh báo Khí tượng & Bụi Phấn cá nhân hóa hàng ngày bằng AI qua Email**

### **💨 Bạn đã bao giờ phải lo lắng về chất lượng không khí hoặc bụi phấn gây dị ứng mỗi sáng?**
Hàng ngày, chất lượng không khí và lượng bụi phấn thay đổi liên tục, ảnh hưởng trực tiếp đến sức khỏe của bạn và gia đình. Thay vì phải tra cứu thông tin thủ công trên các trang web hoặc app, **workflow này sẽ tự động gửi email cảnh báo chi tiết, cá nhân hóa** về:
- **Chất lượng không khí** (không khí sạch, ô nhiễm nhẹ/mạnh, khuyến cáo đặc biệt).
- **Mức độ bụi phấn** (cao/rất cao, loại bụi phấn nào, khuyến cáo cho người bị dị ứng).
- **Gợi ý hành động** (ví dụ: "Hôm nay không khí ô nhiễm cao, nên tránh hoạt động ngoài trời vào buổi sáng").

**Với workflow này, bạn sẽ:**
✅ **Tiết kiệm thời gian** – Không cần tra cứu thủ công mỗi sáng.
✅ **Cảnh báo chính xác** – Dữ liệu thời gian thực từ API Ambee (miễn phí).
✅ **Cá nhân hóa** – AI phân tích và gợi ý dựa trên tuổi tác và tình trạng sức khỏe của bạn.
✅ **Hoạt động 24/7** – Email tự động gửi vào thời gian bạn đặt (ví dụ: 7h sáng).

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Sức khỏe được bảo vệ** – Nhận cảnh báo kịp thời về không khí ô nhiễm hoặc bụi phấn cao.
- **Tiết kiệm thời gian** – Không cần mở nhiều tab hoặc app để kiểm tra dữ liệu.
- **Gợi ý hành động cụ thể** – AI phân tích và đề xuất cách ứng phó phù hợp (ví dụ: "Người bị hen suyễn nên đeo khẩu trang").
- **Dữ liệu cá nhân hóa** – Cảnh báo được tối ưu dựa trên tuổi tác và tình trạng sức khỏe của bạn.
- **Miễn phí** – Sử dụng API Ambee miễn phí và API OpenAI (có giới hạn miễn phí).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Ambee API** (miễn phí):
   - Đăng ký tại [https://www.getambee.com](https://www.getambee.com) **sử dụng email công ty/đại học** (không dùng Gmail/Outlook cá nhân).
   - Sau khi đăng ký, copy **API Key** từ dashboard và lưu lại.

2. **Tài khoản Gmail** (để gửi email cảnh báo):
   - Cần **OAuth 2.0** để n8n có thể gửi email tự động.
   - Hướng dẫn cấu hình OAuth 2.0 cho Gmail: [Tại đây](https://developers.google.com/gmail/api/quickstart/nodejs).

3. **Tài khoản OpenAI** (để sử dụng AI GPT-4.1):
   - Đăng ký tại [https://platform.openai.com/](https://platform.openai.com/) và tạo **API Key**.
   - Lưu ý: API Key này sẽ được sử dụng trong node `OpenAI Chat Model`.

4. **Thông tin cá nhân hóa**:
   - **Vị trí** (toạ độ latitude & longitude) của bạn (ví dụ: Hà Nội: lat=21.0355, lng=105.8542).
   - **Thông tin sức khỏe** (tuổi, tình trạng dị ứng, bệnh lý liên quan như hen suyễn, dị ứng bụi phấn).

5. **n8n Self-hosted** (không dùng n8n Cloud):
   - Workflow này **không hoạt động trên n8n Cloud** do sử dụng API OpenAI và Gmail OAuth 2.0.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [đây](https://n8n.io/workflows/3699) (ấn "Export").
- **Cách 1: Import từ file JSON**
  - Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Cách 2: Copy/Paste JSON**
  - Mở n8n Editor → Nhấn **"Import"** → Chọn **"Paste JSON"** → Dán toàn bộ nội dung JSON từ file.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node**, các sếp cần cấu hình kỹ các node sau:

##### **A. Cấu hình API Ambee (2 node `httpRequest`)**
- **Node "Get Air data"**:
  - **Method**: `GET`
  - **URL**: `https://api.ambeemodel.com/v2/air-pollution?lat={lat}&lng={lng}&index=true`
  - **Headers**:
    ```
    x-api-key: YOUR_AMBEE_API_KEY_HERE
    Accept: application/json
    ```
  - **Thay thế `{lat}` và `{lng}`** bằng toạ độ của bạn (ví dụ: lat=21.0355, lng=105.8542).

- **Node "Get Pollen data"**:
  - **Method**: `GET`
  - **URL**: `https://api.ambeemodel.com/v2/pollen?lat={lat}&lng={lng}&index=true`
  - **Headers**:
    ```
    x-api-key: YOUR_AMBEE_API_KEY_HERE
    Accept: application/json
    ```
  - **Thay thế `{lat}` và `{lng}`** giống như trên.

##### **B. Cấu hình AI Agent (3 node)**
- **Node "Set Your Location Coordinates" (type: `set`)**:
  - Thêm **toạ độ** (lat & lng) vào `json` để truyền cho node sau.
  - Ví dụ:
    ```json
    {
      "lat": "21.0355",
      "lng": "105.8542"
    }
    ```

- **Node "Set User Profile" (type: `set`)**:
  - Thêm **thông tin cá nhân hóa** như:
    ```json
    {
      "age": 30,
      "health_sensitivities": ["asthma", "allergy_to_pollen"],
      "preferences": "avoid outdoor activities on high pollen days"
    }
    ```
  - **Lưu ý**: Thông tin này sẽ được AI sử dụng để tạo cảnh báo phù hợp.

- **Node "OpenAI Chat Model"**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
  - **Model**: Chọn `gpt-4.1` (hoặc `gpt-4` nếu không có).
  - **Prompt mẫu** (cần chỉnh sửa để phù hợp):
    ```
    You are an air and pollen health assistant. Based on the following data:
    - Air quality index: {air_quality}
    - Pollen concentration: {pollen_concentration}
    - User profile: {user_profile}
    Provide a personalized health alert with actionable advice.
    ```

##### **C. Cấu hình Gmail (node `gmailTool`)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình OAuth 2.0).
- **Thiết lập email**:
  - **Subject**: `🌬️ Cảnh báo Khí tượng & Bụi Phấn Hôm nay - {Date}`
  - **Body**: Sử dụng nội dung từ node `AI Agent` (đã được AI xử lý).
  - **Người nhận**: Điền email của bạn.

##### **D. Cấu hình Schedule Trigger (node `scheduleTrigger`)**
- **Chọn lịch trình**: Ví dụ: `0 7 * * *` (gửi email lúc 7h sáng hàng ngày).
- **Lưu ý**: Nếu muốn gửi vào giờ khác, chỉnh sửa theo định dạng `cron`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra logic):
   - Nhấn **"Run Workflow"** và chọn **test data** (nếu có).
   - Kiểm tra email đã được gửi chưa.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[**TẠO TRẢI NGHIỆM HƠN**]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì chỉ gửi email, bạn có thể **gửi thông báo trên Slack/Telegram** bằng node `webhook` hoặc `slackTool`.
   - Ví dụ: Gửi tin nhắn cảnh báo vào nhóm Slack của công ty.

2. **Lưu log dữ liệu**:
   - Sử dụng node `stickyNote` hoặc `set` để lưu dữ liệu cảnh báo vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử.

3. **Cảnh báo cho nhiều vị trí**:
   - Sử dụng **loop** (node `set` + `foreach`) để gửi cảnh báo cho **nhiều địa điểm** (ví dụ: nhà, công ty, du lịch).

4. **Tối ưu API OpenAI**:
   - Nếu sử dụng API OpenAI miễn phí, **hạn chế số lượng request** để tránh bị giới hạn.
   - Sử dụng **cache** cho kết quả AI nếu không thay đổi dữ liệu.

5. **Thêm cảnh báo SMS**:
   - Kết hợp với **Twilio API** để gửi SMS cảnh báo khi không khí ô nhiễm cao.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp và gia đình **chủ động bảo vệ sức khỏe** mỗi ngày, với **cảnh báo cá nhân hóa** về chất lượng không khí và bụi phấn. Bằng cách tự động hóa quá trình này, bạn sẽ:
✔ **Tiết kiệm thời gian** không cần tra cứu thủ công.
✔ **Nhận thông tin chính xác** từ API Ambee (miễn phí).
✔ **Được AI tư vấn hành động** phù hợp với tình trạng sức khỏe của mình.

**Hãy import workflow này ngay hôm nay và bảo vệ sức khỏe của gia đình mình!** 🌿💨

---
**🔗 [Tải workflow JSON tại đây](https://n8n.io/workflows/3699)**
**📌 Cần hỗ trợ cấu hình? Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và chat với chúng tôi!**