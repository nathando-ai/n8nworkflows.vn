---
title: "🚀 Tự Động Hóa Trả Lời Tiềm Năng Thực Tế Trên Tất Cả Các Kênh Xã Hội Với AI Llama & Google Sheets"
description: "Workflow này tự động trả lời ngay lập tức cho tất cả các lead mới đến từ WhatsApp, Website, Instagram, Facebook và LinkedIn với AI Llama, đồng thời ghi chép toàn bộ tương tác vào Google Sheets. Giúp doanh nghiệp tăng tỷ lệ chuyển đổi và tiết kiệm thời gian cho đội SDR."
slug: "tieu-dong-hoa-tra-loi-tien-nang-thuc-te-voi-ai-llama"
tags: [n8n, automation, lead-nurturing, ai-chatbot, google-sheets, whatsapp, facebook, instagram, linkedin]
keywords: [n8n workflow tự động hóa lead, trả lời tiềm năng thực tế, AI Llama trong n8n, tự động hóa SDR, ghi chép lead vào Google Sheets]
---

# 🚀 **Tự Động Hóa Trả Lời Tiềm Năng Thực Tế Trên Tất Cả Kênh Xã Hội Với AI Llama & Google Sheets**

### **🔥 Bạn đã bao giờ phải mất nhiều giờ mỗi ngày để trả lời các lead mới từ nhiều kênh xã hội khác nhau?**
- **WhatsApp, Website, Instagram, Facebook, LinkedIn** đều gửi tin nhắn lead vào bất kỳ thời điểm nào, khiến đội SDR của bạn phải chạy đua để không bỏ lỡ bất kỳ cơ hội nào.
- **Trả lời chậm** có thể khiến lead chuyển sang đối thủ, trong khi **trả lời thủ công** lại tốn thời gian và dễ gây sai sót.
- **Không có hệ thống theo dõi** khiến bạn mất kiểm soát về số lượng lead, thời gian phản hồi và hiệu quả chuyển đổi.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động trả lời ngay lập tức** cho tất cả lead mới đến từ mọi kênh xã hội.
✅ **Sử dụng AI Llama** để tạo phản hồi tự nhiên, phù hợp với từng kênh và thời gian.
✅ **Ghi chép toàn bộ tương tác** vào Google Sheets để theo dõi và phân tích hiệu quả.
✅ **Chỉ hoạt động trong giờ làm việc** (theo giờ IST) để tránh phản hồi không cần thiết vào ban đêm hoặc cuối tuần.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải mất nhiều giờ để trả lời lead thủ công.
- **Tỷ lệ phản hồi cao**: Đảm bảo **không bỏ lỡ bất kỳ lead nào** nhờ tự động hóa.
- **Phản hồi tự nhiên**: AI Llama tạo ra những câu trả lời **phù hợp với từng kênh** (WhatsApp, Instagram, LinkedIn...) và thời gian.
- **Theo dõi toàn diện**: Tất cả lead và tương tác được **ghi chép vào Google Sheets**, giúp phân tích hiệu quả và tối ưu hóa chiến dịch.
- **Hoạt động liên tục**: Workflow hoạt động **24/7**, ngay cả khi đội SDR nghỉ ngơi.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản API của các kênh xã hội**:
   - WhatsApp Business API (hoặc API của nhà cung cấp như Twilio, MessageBird).
   - Facebook Messenger API (Meta Business Suite).
   - Instagram Business API (nếu kết nối với Facebook).
   - LinkedIn API (nếu cần).

✔ **Tài khoản Google Sheets**:
   - Một bảng Google Sheets để lưu trữ lead và lịch sử tương tác.
   - **Chia sẻ quyền truy cập** cho n8n để ghi dữ liệu.

✔ **API Key của AI Llama** (hoặc mô hình AI khác):
   - Nếu sử dụng **Llama AI**, cần kết nối với API của Meta hoặc mô hình AI tương tự (ví dụ: Mistral AI, Ollama).

✔ **Tài khoản Gmail** (nếu cần gửi email tự động).

✔ **Webhook URLs của các kênh**:
   - Các URL để các kênh xã hội gửi lead đến n8n (sẽ được cấu hình trong workflow).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/12094](https://n8n.io/workflows/12094) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ file và dán vào **Import Workflow** trong n8n.

**Cách import:**
1. Mở **n8n Editor** và chọn **Import Workflow**.
2. Chọn **Upload JSON** hoặc **Paste JSON**.
3. Click **Import** để workflow xuất hiện trên canvas.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **A. Cấu hình Webhook cho các kênh xã hội**
Workflow này sử dụng **5 webhook** để nhận lead từ:
- WhatsApp (`/incoming-leads-whatsapp`)
- Website (`/incoming-leads-website`)
- Instagram (`/incoming-leads-instagram`)
- Facebook (`/incoming-leads-facebook`)
- LinkedIn (`/incoming-leads-linkdin`)

**Cách cấu hình:**
1. Mở mỗi **webhook node** và sao chép **URL** từ tab **Settings**.
2. **Kết nối URL này** với từng kênh xã hội tương ứng:
   - **WhatsApp**: Cấu hình trong **WhatsApp Business API** hoặc nhà cung cấp (Twilio, MessageBird).
   - **Facebook/Instagram**: Cấu hình trong **Meta Business Suite**.
   - **LinkedIn**: Cấu hình trong **LinkedIn API**.
   - **Website**: Cấu hình trong **server hoặc trang web** (sử dụng `fetch` hoặc `axios` để gửi POST đến URL webhook).

**Lưu ý:**
- Đảm bảo **cấu trúc payload** của lead phù hợp với workflow. Ví dụ:
  ```json
  {
    "name": "Tên Lead",
    "phone": "0123456789",
    "message": "Tôi quan tâm sản phẩm của bạn!",
    "source": "whatsapp"
  }
  ```

---

##### **B. Cấu hình Google Sheets**
Workflow sẽ **ghi chép tất cả lead** vào một bảng Google Sheets.
**Cách cấu hình:**
1. Tạo một **bảng mới** trong Google Sheets (ví dụ: `Lead_Management`).
2. Trong node **`google-sheet-name`**, chọn:
   - **Google Sheets Credential**: Tạo mới và kết nối với tài khoản Google.
   - **Sheet Name**: Nhập tên bảng (ví dụ: `Lead_Management`).
   - **Operation**: Đặt là `appendOrUpdate` để thêm hoặc cập nhật dữ liệu.

**Cấu trúc cột trong Google Sheets:**
| Name       | Phone      | Message          | Source      | AI Response       | Timestamp          | Status      |
|------------|------------|------------------|-------------|-------------------|--------------------|-------------|
| Tên Lead   | Số điện thoại | Nội dung tin nhắn | Kênh (FB, IG...) | Trả lời AI         | Thời gian ghi chép | Đã trả lời |

---

##### **C. Cấu hình AI Response (Llama AI)**
Workflow sử dụng **AI Llama** để tạo phản hồi tự nhiên.
**Cách cấu hình:**
1. Trong node **`Get Ai Response1`** (HTTP Request), cấu hình:
   - **URL**: Địa chỉ API của mô hình AI (ví dụ: `https://api.ollama.ai/api/chat`).
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer YOUR_API_KEY",
       "Content-Type": "application/json"
     }
     ```
   - **Body (Request Payload)**:
     ```json
     {
       "model": "llama3",
       "messages": [
         {"role": "system", "content": "Bạn là một trợ lý bán hàng chuyên nghiệp. Trả lời ngắn gọn và thân thiện."},
         {"role": "user", "content": "{{$json.message}}"} // Nội dung tin nhắn của lead
       ]
     }
     ```
   - **Response Format**: Chọn `JSON` và định dạng phản hồi như:
     ```json
     {
       "response": "Cảm ơn bạn về tin nhắn! Chúng tôi sẽ liên hệ lại trong 24h. Xin vui lòng để lại số điện thoại của bạn để chúng tôi có thể hỗ trợ tốt hơn."
     }
     ```

**Lưu ý:**
- Nếu không sử dụng **Llama AI**, có thể thay thế bằng **ChatGPT API**, **Mistral AI** hoặc mô hình AI khác.
- **Test API** trước để đảm bảo phản hồi đúng định dạng.

---

##### **D. Cấu hình giờ làm việc (IST)**
Workflow chỉ hoạt động trong **giờ làm việc** (theo giờ IST, ví dụ: 9h-18h, từ thứ 2 đến thứ 6).
**Cách cấu hình:**
1. Trong node **`Extract Day and Hours1`** (Code), kiểm tra logic:
   ```javascript
   // Kiểm tra ngày và giờ theo IST
   const now = new Date();
   const day = now.getDay(); // 0 (CN) đến 6 (T7)
   const hour = now.getHours();

   // Giờ làm việc: Thứ 2 đến thứ 6, 9h-18h
   const isWorkingDay = day >= 1 && day <= 5;
   const isWorkingHour = hour >= 9 && hour < 18;

   $json.isWorkingDay = isWorkingDay;
   $json.isWorkingHour = isWorkingHour;
   ```
2. Trong node **`Is Working Day and Working Hour?1`** (IF), điều kiện:
   - **If**: `$json.isWorkingDay && $json.isWorkingHour` (chỉ chạy khi trong giờ làm việc).

---

##### **E. Cấu hình gửi phản hồi đến kênh**
Workflow sử dụng **Switch nodes** để gửi phản hồi đến kênh tương ứng.
**Cách cấu hình:**
1. Trong node **`Switch2`** và **`Switch3`**, cấu hình điều kiện:
   - **Switch2**: Chọn kênh (`$json.source`).
   - **Switch3**: Chọn hành động (gửi tin nhắn hoặc email).
2. Trong các node **HTTP Request** (gửi tin nhắn):
   - **WhatsApp**: Sử dụng API của WhatsApp Business.
   - **Facebook/Instagram**: Sử dụng Graph API của Meta.
   - **LinkedIn**: Sử dụng API của LinkedIn.
3. Trong node **Gmail** (nếu cần gửi email):
   - Cấu hình tài khoản Gmail và nội dung email.

**Ví dụ cấu hình WhatsApp:**
```json
{
  "to": "{{$json.phone}}",
  "body": "{{$json.aiResponse}}"
}
```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một tin nhắn test từ **WhatsApp** hoặc **Facebook** để kiểm tra workflow.
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi chép không.
   - Kiểm tra **phản hồi AI** có hợp lý không.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node đều **đỏ (active)** và không có lỗi.
   - Click **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có lead mới.
   - Cấu hình trong node **HTTP Request** hoặc **Webhook**.

2. **Lưu log chi tiết**:
   - Thêm node **Sticky Note** để lưu thông tin debug (ví dụ: lỗi API, phản hồi AI).
   - Sử dụng **Google Sheets** để lưu log chi tiết hơn.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo hàng ngày về số lượng lead, tỷ lệ phản hồi, và hiệu quả chuyển đổi.
   - Cấu hình trong **Trigger** của n8n (ví dụ: chạy hàng ngày lúc 9h).

4. **Tối ưu hóa AI Response**:
   - Thêm **prompt nâng cao** cho AI để phản hồi phù hợp với từng ngành nghề (ví dụ: bất động sản, SaaS, eCommerce).
   - Ví dụ:
     ```json
     {
       "role": "system",
       "content": "Bạn là một trợ lý bán hàng chuyên nghiệp trong ngành SaaS. Trả lời ngắn gọn, chuyên nghiệp và đề xuất giải pháp phù hợp với nhu cầu của khách hàng."
     }
     ```

5. **Xử lý lead ưu tiên**:
   - Thêm logic để **ưu tiên lead từ kênh có giá trị cao** (ví dụ: LinkedIn > WhatsApp).
   - Sử dụng **Switch node** để điều hướng lead ưu tiên qua một workflow riêng.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa **trả lời lead thực tế** trên tất cả kênh xã hội, tiết kiệm thời gian cho đội SDR và tăng tỷ lệ chuyển đổi. Bằng cách kết hợp **AI Llama**, **Google Sheets** và **tự động hóa n8n**, các sếp có thể:
✔ **Không bỏ lỡ bất kỳ lead nào**.
✔ **Tự động trả lời nhanh chóng** với phản hồi tự nhiên.
✔ **Theo dõi toàn bộ tương tác** để phân tích hiệu quả.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và bắt đầu tự động hóa lead của bạn!

**Nếu có vấn đề, hãy liên hệ với tôi để hỗ trợ!** 🚀