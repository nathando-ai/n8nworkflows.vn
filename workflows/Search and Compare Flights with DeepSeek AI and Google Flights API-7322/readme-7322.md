---
title: "🚀 Tự Động Hóa So Sánh Chuyến Bay Tối Ưu Với AI DeepSeek & API Google Flights – Không Cần Code!"
description: "Workflow này tự động tìm kiếm, so sánh và gợi ý chuyến bay tốt nhất từ Google Flights, sau đó phân tích chi tiết bằng AI DeepSeek. Giúp khách hàng tiết kiệm thời gian lên đến 90% so với cách thủ công, với kết quả chính xác và cá nhân hóa cao."
slug: "tieu-dong-hoa-so-sanh-chuyen-bay-deepseek-google-flights"
tags: [n8n, automation, no-code, ai-deepseek, google-flights-api, chatbot-travel, ai-multimodal]
keywords: [tự động hóa du lịch n8n, so sánh chuyến bay với AI, API Google Flights tự động, DeepSeek AI cho du lịch, workflow du lịch không code]
---

# 🚀 **Tự Động Hóa So Sánh Chuyến Bay Tối Ưu Với AI DeepSeek & API Google Flights**

### **Giải pháp cho khách sạn, tour du lịch, hoặc doanh nghiệp du lịch**
Hãy tưởng tượng một khách hàng gọi điện hoặc gửi tin nhắn yêu cầu tìm kiếm và so sánh nhiều tuyến bay từ Hà Nội đến New York, với ngân sách hạn chế và thời gian đi cụ thể. Bằng cách thủ công, bạn phải:
- **Tìm kiếm thủ công** trên Google Flights (thời gian: ~15-30 phút/tuyến).
- **So sánh giá, thời gian bay, và điểm dừng** trên nhiều trang web khác nhau.
- **Phân tích chi tiết** về thời tiết, an toàn hàng không, và các yếu tố khác để đưa ra lời khuyên chính xác.
- **Gửi kết quả** qua email, Slack, hoặc tin nhắn cá nhân hóa.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!** Bằng cách kết hợp **API Google Flights** (tìm kiếm chuyến bay) và **AI DeepSeek** (phân tích và gợi ý), bạn sẽ:
✅ **Tiết kiệm 90% thời gian** so với cách thủ công.
✅ **Tránh sai sót** do con người (ví dụ: bỏ qua tuyến bay rẻ hơn).
✅ **Cung cấp trải nghiệm cá nhân hóa** với khách hàng.
✅ **Hoạt động 24/7** mà không cần can thiệp của nhân viên.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 30 phút/tuyến bay xuống còn **vài giây**.
- **Chính xác 100%**: Không bỏ lỡ tuyến bay rẻ hơn hoặc thuận tiện hơn.
- **Cá nhân hóa cao**: AI DeepSeek phân tích và gợi ý dựa trên nhu cầu cụ thể của khách hàng (ví dụ: ưu tiên thời gian bay ngắn hơn, giá rẻ hơn, hoặc ít điểm dừng).
- **Hoạt động tự động**: Khách hàng có thể tương tác qua **Slack, WhatsApp, hoặc email** mà không cần hỗ trợ trực tiếp.
- **Dữ liệu cập nhật**: Kết quả luôn mới nhất từ Google Flights.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API SerpAPI** (để gọi API Google Flights):
   - Đăng ký tại [SerpAPI](https://serpapi.com/) và lấy **API Key**.
   - **Mã giảm giá**: Sử dụng mã `N8NFLIGHTS` để giảm 10% phí đầu tiên (nếu có).
2. **Tài khoản DeepSeek API**:
   - Đăng ký tại [DeepSeek](https://deepseek.com/) và lấy **API Key**.
   - **Lưu ý**: DeepSeek hiện hỗ trợ tiếng Trung và tiếng Anh; nếu khách hàng yêu cầu tiếng Việt, có thể kết hợp với **OpenAI GPT-4** (cần thêm node `lmChatOpenAI`).
3. **Credentials trong n8n**:
   - Tạo **credentials** cho SerpAPI và DeepSeek trong n8n (Settings > Credentials).
   - **Tên credentials**:
     - `serpApi`: Điền `apiKey` từ SerpAPI.
     - `deepSeekApi`: Điền `apiKey` từ DeepSeek.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **JSON**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/7322](https://n8n.io/workflows/7322) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đường dẫn: `https://[your-n8n-instance]/workflow/edit`).

:::note[LƯU Ý]
- Nếu import từ file JSON, **không cần chỉnh sửa** cấu trúc workflow.
- Nếu copy/paste, **đảm bảo không có ký tự đặc biệt bị mất** (ví dụ: `"` hoặc `\`).
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **5 node chính**, mỗi node đều cần cấu hình kỹ lưỡng:

##### **A. Node "Google_flights search in SerpApi" (Tìm kiếm chuyến bay)**
- **Yêu cầu**:
  - **Credentials**: Chọn `serpApi` (đã tạo trước).
  - **Key Parameters**:
    - `q`: Điền vào dạng `"from_city:Hanoi,to_city:New York,date:2024-12-15"` (thay đổi theo yêu cầu khách hàng).
    - `hl`: `vi` (nếu muốn kết quả tiếng Việt) hoặc `en` (tiếng Anh).
    - `api_key`: Điền từ credentials `serpApi`.
  - **Lưu ý**:
    - Nếu khách hàng nhập yêu cầu qua **Slack/email**, cần **dynamically build** query từ input (ví dụ: `{{$json["from_city"]}}`).
    - Thêm `max_results: 5` để lấy 5 tuyến bay tốt nhất.

##### **B. Node "DeepSeek Chat Model" (Phân tích bằng AI)**
- **Yêu cầu**:
  - **Credentials**: Chọn `deepSeekApi`.
  - **Prompt Template**:
    ```plaintext
    Bạn là một chuyên gia du lịch AI. Hãy phân tích và so sánh các tuyến bay sau từ Google Flights:
    {{$json["flights"]}}

    Yêu cầu:
    1. Lọc ra 3 tuyến bay tốt nhất dựa trên:
       - Giá thấp nhất.
       - Thời gian bay ngắn nhất.
       - Số điểm dừng ít nhất.
    2. Đánh giá thời tiết tại điểm đến vào ngày đi.
    3. Gợi ý điểm dừng nếu có (ví dụ: Tokyo, Seoul).
    4. Nếu có tuyến bay rẻ hơn 20% so với giá cao nhất, hãy nhấn mạnh.
    5. Trả lời bằng tiếng Việt và sử dụng ngôn ngữ chuyên nghiệp.
    ```
  - **Lưu ý**:
    - Nếu khách hàng yêu cầu **tiếng Anh**, thay `vi` thành `en` trong prompt.
    - **Optimize prompt** để AI trả lời ngắn gọn và rõ ràng.

##### **C. Node "AI Agent" (Tương tác tự động)**
- **Yêu cầu**:
  - **Memory Buffer**: Kết nối với node `Simple Memory` để lưu lịch sử tương tác (ví dụ: khách hàng đã tìm kiếm tuyến nào trước đó).
  - **Trigger**: Kết nối với node `Chat` để nhận input từ Slack/email/WhatsApp.

##### **D. Node "Simple Memory" (Lưu lịch sử)**
- **Yêu cầu**:
  - **Window Size**: Đặt `10` (lưu 10 lần tương tác gần nhất).
  - **Key**: Đặt `user_query` (để lưu nội dung yêu cầu của khách hàng).

##### **E. Node "Chat" (Nhận input từ khách hàng)**
- **Yêu cầu**:
  - **Trigger**: Chọn `webhook` (nếu khách hàng gửi yêu cầu qua URL) hoặc `slack`/`email` (nếu tích hợp với Slack/email).
  - **Example Input**:
    ```json
    {
      "from_city": "Hanoi",
      "to_city": "New York",
      "date": "2024-12-15",
      "preferences": "giá rẻ, ít điểm dừng"
    }
    ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **dữ liệu mẫu** vào node `Chat` (ví dụ: yêu cầu tìm chuyến bay từ Hà Nội đến New York ngày 15/12/2024).
   - Kiểm tra output từ node `DeepSeek Chat Model` có logic không?
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và chia sẻ **URL Webhook** (nếu dùng webhook) hoặc **link Slack/email** cho khách hàng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Tích hợp với Slack/Telegram**:
   - Thay node `Chat` bằng `slack` hoặc `telegram`, sau đó cấu hình **Slack App** hoặc **Bot Telegram**.
   - **Mẹo**: Sử dụng **Slack Blocks** để gửi kết quả dưới dạng card đẹp (ví dụ: hiển thị bảng so sánh chuyến bay).

2. **Lưu log và báo cáo**:
   - Thêm node `set` hoặc `file` để lưu kết quả vào **Google Sheets** hoặc **Firebase**.
   - **Example**: Tạo một sheet Google Sheets để theo dõi tất cả yêu cầu của khách hàng.

3. **Cá nhân hóa hơn với CRM**:
   - Kết nối với **HubSpot** hoặc **Zoho CRM** để lưu thông tin khách hàng và lịch sử tương tác.
   - **Mẹo**: Sử dụng node `crm` để cập nhật thông tin khách hàng sau mỗi tương tác.

4. **Phân tích thị trường**:
   - Thêm node `set` để tính toán **giá trung bình** của các tuyến bay trong tháng.
   - **Áp dụng**: Dùng để dự báo giá và đưa ra chiến lược khuyến mãi.

5. **Hỗ trợ nhiều ngôn ngữ**:
   - Nếu DeepSeek không hỗ trợ tiếng Việt, thay thế bằng **OpenAI GPT-4** (cần thêm node `lmChatOpenAI`).
   - **Prompt cho GPT-4**:
     ```plaintext
     Bạn là một chuyên gia du lịch AI. Hãy phân tích và so sánh các tuyến bay sau từ Google Flights với yêu cầu tiếng Việt:
     {{$json["flights"]}}
     ```

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp du lịch muốn tự động hóa quy trình tìm kiếm và so sánh chuyến bay, đồng thời cung cấp **trải nghiệm cá nhân hóa** cho khách hàng. Bằng cách kết hợp **API Google Flights** và **AI DeepSeek**, bạn không chỉ tiết kiệm thời gian mà còn **tăng cường hiệu suất và hài lòng khách hàng**.

**Bắt đầu ngay hôm nay!**
- **Import workflow** và cấu hình theo hướng dẫn.
- **Tích hợp với Slack/email** để khách hàng có thể tương tác 24/7.
- **Mở rộng** bằng cách thêm CRM hoặc báo cáo tự động.

👉 **Nếu cần hỗ trợ**, hãy liên hệ với **Fakhar Khan** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/fakhar-khan/) hoặc cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).

---
:::success[CHUYÊN MỤC N8N]
Nếu các sếp muốn **self-host n8n** để workflow hoạt động ổn định 24/7, hãy tham khảo:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)