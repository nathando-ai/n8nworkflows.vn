---
title: "📈 Tự Động Hóa Báo Cáo Tin Tức Tài Chính Hàng Ngày Với AI Ollama - Email Tóm Tắt Chuyên Nghiệp"
description: "Workflow tự động hóa thu thập, xử lý và gửi email tóm tắt tin tức tài chính hàng ngày bằng AI Ollama, tiết kiệm thời gian cho các nhà phân tích và đội ngũ tài chính. Giúp các sếp cập nhật thông tin thị trường nhanh chóng, chính xác và cá nhân hóa."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-tai-chinh-hang-ngay-ollama"
tags: [n8n, automation, ai-summarization, financial-analysis, ollama, email-automation]
keywords: [tự động hóa tin tức tài chính, ollama n8n workflow, email báo cáo hàng ngày, ai tóm tắt tin tức, tự động hóa phân tích thị trường]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Tài Chính Hàng Ngày Với AI Ollama - Email Tóm Tắt Chuyên Nghiệp**

### **🔥 Nỗi Đau Của Các Sếp Trong Phân Tích Tài Chính**
Hàng ngày, các nhà phân tích tài chính và đội ngũ quản lý phải mất **giờ đồng hồ** để:
- **Thu thập** tin tức từ nhiều nguồn khác nhau (Bloomberg, Reuters, Forbes, VNDirect...).
- **Lọc** và **tóm tắt** những tin tức quan trọng nhất trong một thị trường biến động.
- **Gửi báo cáo** định kỳ cho đội ngũ hoặc khách hàng, thường phải làm thủ công qua email hoặc Excel.

Kết quả? **Thời gian bị lãng phí**, **thông tin không đầy đủ**, và **rủi ro bỏ lỡ cơ hội** vì không cập nhật kịp thời. **Workflow này giải quyết tất cả!**

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 3-5 giờ/ngày** cho việc thu thập và tóm tắt tin tức.
- **Tin tức được tóm tắt chính xác** bởi AI Ollama (mô hình Llama3.2-16k), phù hợp với ngữ cảnh tài chính.
- **Email tự động gửi hàng ngày** vào thời gian cố định, không phụ thuộc vào con người.
- **Cập nhật liên tục** 24/7, không bỏ lỡ bất kỳ tin tức quan trọng nào.
- **Dễ dàng mở rộng** cho nhiều nguồn tin, định dạng báo cáo khác nhau.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Ollama** (để sử dụng mô hình AI):
   - Cài đặt Ollama trên máy chủ hoặc VPS (hướng dẫn: [ollama.ai](https://ollama.ai/)).
   - Chạy lệnh `ollama pull llama3.2-16000` để tải mô hình.
   - **API Key Ollama**: Thêm vào n8n dưới **Credentials** với tên `ollamaApi`.

2. **Tài khoản Email SMTP** (để gửi email tự động):
   - Dịch vụ SMTP hỗ trợ (Gmail, SendGrid, Mailgun, hoặc SMTP của nhà cung cấp hosting).
   - **Thông tin SMTP**: Host, Port, Username, Password, và **Credentials** trong n8n với tên `smtp`.

3. **VPS hoặc máy chủ n8n** (để chạy 24/7):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**.
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5405](https://n8n.io/workflows/5405) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Node `Schedule Daily Trigger`**
- **Thời gian chạy**: Đặt theo giờ mong muốn (ví dụ: 8h sáng hàng ngày).
- **Time Zone**: Chọn theo múi giờ của doanh nghiệp (ví dụ: `Asia/Ho_Chi_Minh`).

##### **B. Cấu Hình Node `Fetch Financial News Webpage`**
- **URL nguồn tin**: Thay thế bằng URL của trang tin tức tài chính mong muốn (ví dụ: `https://www.reuters.com/finance`).
- **Headers**: Nếu trang yêu cầu, thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).

##### **C. Cấu Hình Node `LLM Chat Model` (ollamaApi)**
- **Model**: Đã mặc định là `llama3.2-16000:latest` (không cần thay đổi).
- **Prompt**: Workflow tự động sử dụng **prompt mặc định** để tóm tắt tin tức tài chính. Nếu muốn tùy chỉnh, chỉnh sửa ở node `AI Financial News Summarizer`:
  ```json
  "prompt": "Tóm tắt ngắn gọn (1-2 câu) tin tức tài chính sau đây cho nhà đầu tư chuyên nghiệp. Đảm bảo bao gồm:
  - Sự kiện chính
  - Ảnh hưởng đến thị trường
  - Dữ liệu số liệu quan trọng (nếu có)
  - Khuyến nghị ngắn gọn (nếu có)."
  ```

##### **D. Cấu Hình Node `Email Daily Financial Summary` (smtp)**
- **SMTP Credentials**: Điền thông tin từ tài khoản email SMTP của bạn.
- **Email recipients**: Thêm địa chỉ email của người nhận (ví dụ: `team@doanhnghiep.com`).
- **Subject**: Thay đổi tiêu đề email (ví dụ: `"Báo cáo Tin Tức Tài Chính Hàng Ngày - [Ngày Tháng]"`).
- **HTML Template**: Workflow tự động tạo email với **cấu trúc chuyên nghiệp**, bao gồm:
  - Tiêu đề tin tức.
  - Link trực tiếp đến nguồn.
  - Tóm tắt AI.

##### **E. Node `StickyNote` (Ghi chú)**
- Node này **không cần cấu hình**, chỉ dùng để ghi chú trong workflow.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng ngày.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Thêm nhiều nguồn tin**:
   - Sử dụng node `Set` để **ghép nhiều URL** vào một danh sách và chạy song song với `Fetch Financial News Webpage`.

2. **Lưu log và báo cáo**:
   - Thêm node `Google Sheets` hoặc `Notion` để **lưu lịch sử báo cáo** cho việc phân tích dài hạn.

3. **Gửi báo cáo đến Slack/Telegram**:
   - Thay thế node `emailSend` bằng `slackSend` hoặc `telegramSend` để thông báo tức thời.

4. **Tùy chỉnh mô hình AI**:
   - Thay đổi mô hình Ollama thành `mistral` hoặc `phi-3` nếu muốn kết quả khác nhau.

5. **Bộ lọc tin tức theo chủ đề**:
   - Sử dụng **regex** trong node `html` để **lọc chỉ tin tức liên quan** (ví dụ: chỉ tin về chứng khoán, crypto, hoặc ngân hàng).
:::

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **cung cấp thông tin tài chính chính xác và tóm tắt** bằng AI. **Không cần code, không cần chuyên gia IT** – chỉ cần **cấu hình theo hướng dẫn** và **bật chạy**.

**🚀 Hành động ngay!**
1. **Chuẩn bị tài khoản Ollama và SMTP** (nếu chưa có).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Bật Active** và **nhận báo cáo hàng ngày** vào email!

**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, hãy kiểm tra **log của node `LLM Chat Model`** để điều chỉnh prompt hoặc mô hình AI. **Hãy thử và chia sẻ kết quả với chúng tôi!** 🚀

---