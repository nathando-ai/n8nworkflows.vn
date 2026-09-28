---
title: "🤖 Tự Động Hóa Telegram: Chuyển Output AI thành Tin Nhắn Đa Dạng & Tối Ưu Hóa Trải Nghiệm - Chia Đoạn Văn Bản & Gửi Link Tự Động"
description: "Workflow này tự động chuyển kết quả từ mô hình LLM (AI) thành tin nhắn Telegram phong phú, chia đoạn văn bản dài thành các chunk nhỏ, và gửi các loại link (ảnh, video, âm thanh) riêng biệt - tiết kiệm thời gian và cải thiện trải nghiệm người dùng 100% không cần code."
slug: "tieu-dong-hoa-telegram-chuyen-output-ai-thanh-tin-nhan-da-dang"
tags: [n8n, automation, telegram-bot, ai-chatbot, no-code, ai-workflow]
keywords: [n8n workflow telegram, tự động hóa tin nhắn telegram, chia đoạn văn bản dài, gửi link tự động, ai chatbot telegram, tối ưu trải nghiệm telegram]
---

# 🚀 **Tự Động Hóa Telegram: Chuyển Output AI thành Tin Nhắn Đa Dạng & Tối Ưu Hóa Trải Nghiệm**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp đã từng gặp phải tình huống này chưa?
- **Văn bản AI dài dòng** (ví dụ: kết quả từ ChatGPT, Bard, hoặc mô hình LLM riêng) quá dài, không thể gửi toàn bộ vào Telegram một lúc → người dùng phải đọc nhiều tin nhắn rời rạc.
- **Các link (ảnh, video, âm thanh)** trong kết quả AI bị gửi chung với văn bản → trải nghiệm người dùng bị gián đoạn, ảnh/video không thể xem trực tiếp.
- **Tốn thời gian** để thủ công chia đoạn văn bản và phân loại link → làm giảm hiệu quả của hệ thống tự động hóa.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Chia đoạn văn bản dài** thành các chunk nhỏ, gửi từng chunk một với định dạng đẹp.
✅ **Phân loại và gửi link riêng biệt** (ảnh, video, âm thanh) theo loại, không cần phải copy-paste thủ công.
✅ **Tối ưu trải nghiệm người dùng** bằng cách gửi nội dung đa dạng (text + media) một cách tự động và chuyên nghiệp.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với VPS, các sếp có thể:
- **Không phụ thuộc vào phiên bản miễn phí** của n8n.io (có giới hạn node và thời gian chạy).
- **Tăng tốc độ xử lý** và giảm thời gian chờ cho các tác vụ AI.
- **Bảo mật cao** khi không chia sẻ API key với bên thứ ba.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công chia đoạn văn bản hoặc phân loại link.
- **Trải nghiệm người dùng tốt hơn**: Tin nhắn được chia nhỏ, link được gửi riêng biệt → dễ đọc và tương tác.
- **Tự động hóa hoàn chỉnh**: Kết hợp với mô hình LLM (ChatGPT, Bard, hoặc mô hình riêng) để gửi kết quả một cách tự động.
- **Hỗ trợ nhiều loại nội dung**: Gửi văn bản, ảnh, video, âm thanh trong cùng một workflow.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không bị giới hạn phiên bản miễn phí.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo một bot Telegram mới từ [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân để nhận tin nhắn tự động.
2. **Credentials Telegram API**:
   - Trong n8n, tạo một **credentials** mới với loại `telegram` và điền **API Token** từ bước trên.
   - Tên credentials: `telegramApi` (phải trùng với tên trong workflow).
3. **(Tùy chọn) Mô Hình LLM**:
   - Nếu kết nối với mô hình AI (ChatGPT, Bard, hoặc mô hình riêng), các sếp cần:
     - API Key của mô hình đó (ví dụ: OpenAI API Key cho ChatGPT).
     - Workflow hoặc node khác để truyền dữ liệu vào workflow này (ví dụ: node `executeWorkflowTrigger`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/3961](https://n8n.io/workflows/3961) và import vào n8n Editor.
- **Copy/paste JSON** từ trang trên vào n8n Editor (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được thiết kế để xử lý **hai trường hợp chính**:
- **Gửi văn bản dài** (chia thành chunk).
- **Gửi link** (ảnh, video, âm thanh) riêng biệt.

##### **A. Cấu Hình Credentials Telegram**
- Trong workflow, tất cả các node `telegram` đều sử dụng credentials `telegramApi`.
- **Kiểm tra lại**:
  - Tên credentials phải **không có khoảng trắng** và trùng với `telegramApi`.
  - **Chat ID** của nhóm/chat cá nhân cần được điền vào các node `telegram` (nếu không tự động phát hiện).
    - **Lấy Chat ID**:
      - Gửi tin nhắn "Hello" từ bot Telegram cho nhóm/chat.
      - Mở liên kết: `https://api.telegram.org/bot<API_TOKEN>/getUpdates`
      - Tìm `chat.id` trong JSON trả về.

##### **B. Cấu Hình Node "When Executed by Another Workflow"**
- Node này là **điểm vào** của workflow (trigger).
- Nếu kết nối với mô hình LLM (ví dụ: ChatGPT), các sếp cần:
  - **Truyền dữ liệu vào node này** từ workflow khác.
  - **Dữ liệu đầu vào** phải có 2 trường:
    - `text`: Nội dung văn bản từ LLM (có thể dài).
    - `links`: Danh sách link (ảnh, video, âm thanh) trong văn bản (nếu có).

##### **C. Cấu Hình Node "Extract Links" (Code)**
- Node này sử dụng **JavaScript** để trích xuất link từ văn bản.
- **Lưu ý**:
  - Nếu văn bản không chứa link, node này sẽ trả về `null`.
  - Các sếp có thể **thay đổi mã** trong node này nếu cần hỗ trợ định dạng link khác.

##### **D. Cấu Hình Node "Split large text by chunks" (Code)**
- Node này chia văn bản dài thành các chunk nhỏ (mặc định là **1000 ký tự/chunk**).
- **Lưu ý**:
  - Các sếp có thể **thay đổi số lượng ký tự** trong mã JavaScript để phù hợp với giới hạn tin nhắn Telegram (4096 ký tự).
  - Ví dụ mã mặc định:
    ```javascript
    const chunkSize = 1000;
    const chunks = [];
    for (let i = 0; i < $input.all().text.length; i += chunkSize) {
      chunks.push($input.all().text.substr(i, chunkSize));
    }
    return chunks;
    ```

##### **E. Cấu Hình Node "Check Link Type" (Switch)**
- Node này phân loại link thành **3 loại**: ảnh, video, âm thanh.
- **Lưu ý**:
  - Các sếp có thể **thêm loại link mới** (ví dụ: file PDF) bằng cách chỉnh sửa node này.
  - Ví dụ, để kiểm tra loại link:
    - **Ảnh**: Kiểm tra `mimeType` chứa `image/`.
    - **Video**: Kiểm tra `mimeType` chứa `video/`.
    - **Âm thanh**: Kiểm tra `mimeType` chứa `audio/`.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một **dữ liệu mẫu** vào node `When Executed by Another Workflow` (ví dụ: văn bản dài + danh sách link).
  - Kiểm tra kết quả trên Telegram để đảm bảo:
    - Văn bản dài được chia thành chunk.
    - Link được gửi riêng biệt theo loại.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và kết nối với mô hình LLM (nếu có).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Mô Hình LLM**
   - Nếu các sếp đang sử dụng **ChatGPT, Bard, hoặc mô hình AI riêng**, có thể:
     - Tạo một workflow khác để gọi API LLM và truyền kết quả vào workflow này.
     - Ví dụ: Sử dụng node `http.request` để gọi API OpenAI và truyền `text` và `links` vào node `When Executed by Another Workflow`.

2. **Lưu Log & Theo Dõi**
   - Thêm node `stickyNote` để ghi lại kết quả của workflow (ví dụ: thời gian gửi, số chunk, số link).
   - Sử dụng node `set` hoặc `stickyNote` để lưu log vào cơ sở dữ liệu (ví dụ: Google Sheets, Airtable).

3. **Gửi Báo Cáo Định Kỳ**
   - Kết hợp với node `schedule` để gửi **báo cáo tổng hợp** (ví dụ: tin nhắn tổng kết hàng ngày từ LLM).
   - Ví dụ: Gửi một tin nhắn tổng kết "Tóm tắt kết quả AI của ngày hôm nay" vào buổi sáng.

4. **Tối Ưu Hóa Trải Nghiệm Người Dùng**
   - Thêm **button phản hồi** trong tin nhắn Telegram để người dùng có thể yêu cầu chia đoạn lại hoặc gửi lại link.
   - Sử dụng node `telegram` với `reply_markup` để thêm menu tương tác.

5. **Xử Lý Trùng Lặp Link**
   - Nếu văn bản có nhiều link trùng lặp, node `Extract Links` có thể bị lỗi.
   - **Giải pháp**: Thêm node `code` trước `Extract Links` để loại bỏ link trùng:
     ```javascript
     const uniqueLinks = [...new Map($input.all().text.split('\n').map(link => [link, link])).values()];
     return { links: uniqueLinks };
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc gửi kết quả từ mô hình AI (LLM) đến Telegram một cách **tối ưu, chuyên nghiệp và tự động hóa hoàn chỉnh**. Các sếp không cần viết một dòng code nào, chỉ cần:
1. **Import workflow** và cấu hình credentials Telegram.
2. **Kết nối với mô hình LLM** (nếu có).
3. **Bật workflow** và bắt đầu nhận tin nhắn tự động!

**Hành động ngay hôm nay**:
- **Self-host n8n** trên VPS để workflow chạy 24/7.
- **Test workflow** với dữ liệu mẫu và điều chỉnh nếu cần.
- **Áp dụng vào dự án** của các sếp để tiết kiệm thời gian và cải thiện trải nghiệm người dùng!

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại bình luận. Chúc các sếp thành công với tự động hóa Telegram! 🤖💬