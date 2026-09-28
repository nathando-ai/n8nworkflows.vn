---
title: "🍳 **Tự Động Hóa Sáng Tạo Công Thức Ăn Uống Từ Email & Form Với Ollama & Llama 3.2 (Không Cần Code!)**"
description: "Workflow tự động hóa nhận yêu cầu công thức ăn uống từ email hoặc form, sử dụng AI Llama 3.2 trên Ollama để tạo ra công thức chi tiết và gửi kết quả về email người dùng. Giúp tiết kiệm thời gian, tăng trải nghiệm cá nhân hóa cho khách hàng."
slug: "tu-dong-hoa-tao-cong-thuc-an-uong-ollama-llama3-2"
tags: [n8n, automation, no-code, ollama, llm, gmail, form-trigger]
keywords: [n8n workflow tự động hóa, tạo công thức ăn uống bằng AI, Ollama Llama 3.2, tự động hóa email, form trigger n8n]
---

# 🚀 **Tự Động Hóa Sáng Tạo Công Thức Ăn Uống Từ Email & Form Với Ollama & Llama 3.2**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp & Nhà Hàng**
Bạn có bao giờ phải mất nhiều thời gian để trả lời hàng loạt yêu cầu về công thức ăn uống từ khách hàng qua email hoặc form? Hay phải lo lắng về tính chính xác và sự cá nhân hóa của mỗi công thức? **Workflow này sẽ tự động hóa toàn bộ quy trình đó chỉ trong vài giây!**

Dựa trên **AI Llama 3.2** (mô hình ngôn ngữ lớn tiên tiến nhất hiện nay) và nền tảng **Ollama**, workflow này sẽ:
✅ **Nhận yêu cầu** từ email hoặc form (Google Form, Typeform,...) một cách tự động.
✅ **Sáng tạo công thức ăn uống chi tiết** (nguyên liệu, cách chế biến, thời gian nấu,...) chỉ trong vài giây.
✅ **Định dạng & gửi kết quả** về email người dùng với định dạng chuyên nghiệp.

Không cần viết một dòng code nào cả! **Chỉ cần cài đặt và chạy**, workflow sẽ hoạt động 24/7 như một "bác sĩ ẩm thực" ảo.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS riêng. Điều này đảm bảo tính riêng tư và hiệu suất cao nhất.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh để chạy Ollama + Llama 3.2)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải trả lời hàng trăm yêu cầu công thức ăn uống thủ công.
- **Chính xác & sáng tạo**: AI Llama 3.2 tạo ra công thức **cá nhân hóa**, phù hợp với nhu cầu cụ thể của khách hàng.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp của con người.
- **Tăng trải nghiệm khách hàng**: Người dùng nhận được **công thức chi tiết, định dạng đẹp** ngay lập tức.
- **Dễ dàng mở rộng**: Có thể kết nối với Slack, Telegram, hoặc lưu log để phân tích yêu cầu thường gặp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google OAuth 2.0** (để kết nối với Gmail và nhận/sending email).
2. **API Key Ollama** (để sử dụng mô hình Llama 3.2).
3. **Google Form hoặc Form khác** (nếu muốn nhận yêu cầu từ form).
4. **n8n Self-hosted** (để chạy workflow ổn định).

:::note[Lưu ý quan trọng]
- **Ollama phải được cài đặt và chạy trên cùng máy chủ VPS** với n8n (hoặc trên một máy chủ khác nhưng kết nối mạng ổn định).
- **Mô hình Llama 3.2** phải được tải xuống trước bằng Ollama:
  ```bash
  ollama pull llama3.2-16000:latest
  ```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/5871) (hoặc copy toàn bộ JSON từ link trên).
2. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.
3. Workflow sẽ xuất hiện trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **Node 1 & 2: Nhận Yêu Cầu (Gmail & Form Trigger)**
- **Recipe Request - Gmail (gmailTrigger)**
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước).
  - **Lọc email**: Chỉ lấy email có chủ đề chứa từ khóa như *"công thức"*, *"recipe"*, *"nấu ăn"*,...
  - **Test**: Gửi một email mẫu đến địa chỉ email đã kết nối để kiểm tra.

- **Recipe Request - Web Form (formTrigger)**
  - Nếu sử dụng **Google Form**, cần cấu hình:
    - **URL Form**: Địa chỉ của form (ví dụ: `https://forms.google.com/...`).
    - **Fields**: Chọn các trường cần lấy (ví dụ: `name`, `email`, `recipe_request`).
  - **Test**: Điền form và gửi để đảm bảo dữ liệu được nhận đúng.

##### **Node 3 & 4: Sáng Tạo Công Thức (Ollama & Llama 3.2)**
- **Ollama Recipe Generator (agent)**
  - Node này sẽ **truyền dữ liệu** từ Gmail/Form đến **Llama 3.2**.
  - **Không cần cấu hình thêm**, chỉ cần đảm bảo **credentials `ollamaApi`** đã được thiết lập.

- **Llama 3.2 - Chef Model (lmChatOllama)**
  - **Credentials**: Chọn `ollamaApi` (đã cấu hình trước).
  - **Model**: Đảm bảo đã chọn `llama3.2-16000:latest`.
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    Tôi là một đầu bếp AI. Hãy tạo một công thức ăn uống chi tiết cho yêu cầu sau:
    - Yêu cầu: {json["query"]}
    - Đảm bảo bao gồm:
      1. Danh sách nguyên liệu chi tiết (đơn vị, số lượng).
      2. Cách chế biến bước bằng bước (với thời gian ước tính).
      3. Gợi ý ăn kèm và lưu ý đặc biệt (nếu có).
    - Trả về kết quả dưới dạng JSON với structure:
    {
      "title": "Tên công thức",
      "ingredients": ["nguyên liệu 1", "nguyên liệu 2"],
      "steps": ["bước 1", "bước 2"],
      "notes": "Ghi chú đặc biệt"
    }
    ```
  - **Test**: Gửi một yêu cầu mẫu (ví dụ: *"Tạo công thức bánh mì nướng đơn giản"*) để kiểm tra kết quả.

##### **Node 5: Định Dạng Kết Quả (Code)**
- Node này **chuyển đổi JSON từ Llama 3.2 thành định dạng email đẹp**.
- **Mã mẫu** (có thể chỉnh sửa trong node `Format Recipe Output`):
  ```javascript
  // Input: JSON từ Llama 3.2
  // Output: HTML email đẹp

  const recipe = $input.all();
  const htmlTemplate = `
    <h2>${recipe.title}</h2>
    <h3>Nguyên liệu:</h3>
    <ul>
      ${recipe.ingredients.map(ing => `<li>${ing}</li>`).join('')}
    </ul>
    <h3>Cách làm:</h3>
    <ol>
      ${recipe.steps.map(step => `<li>${step}</li>`).join('')}
    </ol>
    ${recipe.notes ? `<p><strong>Ghi chú:</strong> ${recipe.notes}</p>` : ''}
  `;

  return { html: htmlTemplate };
  `
  - **Test**: Chạy node này với dữ liệu mẫu để đảm bảo định dạng đúng.

##### **Node 6: Gửi Email Trở Lại (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình).
- **Địa chỉ nhận**: Sử dụng trường `email` từ Gmail/Form.
- **Tiêu đề email**: *"Công thức ăn uống cho bạn: {recipe.title}"*.
- **Nội dung**: Sử dụng kết quả từ node `Format Recipe Output`.
- **Test**: Gửi email mẫu để kiểm tra định dạng và nội dung.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy workflow với dữ liệu mẫu để đảm bảo tất cả node hoạt động.
2. **Bật Active**: Sau khi kiểm tra xong, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả cho team hoặc khách hàng.

2. **Lưu Log & Phân Tích Yêu Cầu**
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu tất cả yêu cầu và kết quả, giúp phân tích xu hướng yêu cầu thường gặp.

3. **Tùy Chỉnh Prompt AI**
   - Nếu muốn công thức phù hợp với **đặc điểm địa phương**, chỉnh sửa prompt trong node `Llama 3.2` để AI thêm thông tin về nguyên liệu địa phương.

4. **Tạo Form Cá Nhân Hóa**
   - Thêm các trường trong form như *"loại thực phẩm"* (chay, thịt,...) hoặc *"thời gian nấu"* để AI tạo công thức phù hợp.

5. **Tự Động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng **n8n Scheduler** để gửi email tổng hợp tất cả công thức đã tạo trong tuần cho khách hàng.

---

### 📌 **Kết Luận**
Workflow này không chỉ **giải phóng thời gian** cho các sếp khỏi công việc lặp lại mà còn **tăng trải nghiệm khách hàng** với công thức ăn uống **cá nhân hóa và chuyên nghiệp**. **Chỉ cần cài đặt và chạy**, workflow sẽ tự động hóa toàn bộ quy trình từ nhận yêu cầu đến gửi kết quả.

**Hãy áp dụng ngay và trở thành "bác sĩ ẩm thực" ảo cho doanh nghiệp của mình!** 🍴✨

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/5871)**
**📌 [Hướng dẫn cài đặt Ollama](https://ollama.com/)**