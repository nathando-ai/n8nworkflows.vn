---
title: "🎨 Tự Động Viết Nội Dung 5 Tôn Ngữ Khác Nhau Với GPT-4o-mini, Google Drive & Slack – Không Cần Code!"
description: "Workflow tự động hóa viết lại nội dung với 5 phong cách khác nhau (chuyên nghiệp, thân thiện, marketing, học thuật, và giải trí) bằng GPT-4o-mini, tự động lưu vào Google Drive và thông báo trên Slack. Giúp các sếp tiết kiệm thời gian viết nội dung đa dạng lên đến 80%!"
slug: "tieu-dong-viet-noi-dung-5-ton-voi-gpt-4o-mini"
tags: [n8n, automation, content-creation, ai-gpt-4, google-drive, slack, no-code]
keywords: [tự động hóa viết nội dung, gpt-4o-mini n8n, viết bài đa phong cách, tự động hóa content marketing, lưu file google drive, thông báo slack]
---

# 🚀 **Tự Động Viết Nội Dung 5 Tôn Ngữ Khác Nhau Với AI – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Viết Nội Dung**
Các sếp thường phải mất **giờ đồng hồ** để viết một bài blog, bài marketing, hoặc nội dung social media với **nhiều phong cách khác nhau**:
- **Chuyên nghiệp** cho báo cáo nội bộ.
- **Thân thiện** cho email khách hàng.
- **Marketing** để thu hút người dùng.
- **Học thuật** cho tài liệu nghiên cứu.
- **Giải trí** cho nội dung trên mạng xã hội.

Với **n8n + GPT-4o-mini**, các sếp **không cần viết một dòng nào** – chỉ cần **nhập nội dung gốc**, workflow sẽ tự động **tạo ra 5 phiên bản khác nhau** và **lưu vào Google Drive** cùng **thông báo kết quả trên Slack**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Viết 5 phiên bản nội dung trong **vài giây** thay vì **giờ đồng hồ**.
✅ **Đa dạng phong cách**: Tùy chỉnh nội dung cho **khách hàng, nội bộ, marketing, học thuật, giải trí**.
✅ **Tự động lưu trữ**: Tất cả phiên bản được **lưu vào Google Drive** với tên file rõ ràng.
✅ **Thông báo Slack**: Kết quả được **gửi tự động** đến kênh Slack để theo dõi.
✅ **Không cần code**: Sử dụng **n8n Self-hosted** để chạy 24/7 mà **không tốn chi phí API cao**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys).
   - **Mã giảm giá** (nếu có) để tiết kiệm chi phí API.
2. **Tài khoản Google Drive**:
   - **API Key** và **Client ID** từ [Google Cloud Console](https://console.cloud.google.com/).
   - **Folder** để lưu các phiên bản nội dung.
3. **Tài khoản Slack**:
   - **Token Slack** (để gửi thông báo).
   - **Kênh Slack** để nhận kết quả.
4. **n8n Self-hosted**:
   - Cài đặt n8n trên **VPS** để chạy 24/7 (không phụ thuộc vào phiên bản miễn phí).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải xuống file JSON** từ [n8n.io/workflows/14989](https://n8n.io/workflows/14989) và **import vào n8n Editor**.
- **Copy/Paste JSON** từ link trên vào **n8n Editor** (tab **Import/Export**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **các node chính sau** (cần cấu hình kỹ):

##### **A. Node `Form Trigger` (Bắt đầu workflow)**
- **Không cần cấu hình gì**, chỉ dùng để **kích hoạt workflow** khi cần.

##### **B. Node `Sticky Note` (Ghi chú nội dung gốc)**
- **Điền nội dung gốc** vào ô `Content` (ví dụ: *"Tại sao n8n là công cụ tự động hóa tốt nhất cho doanh nghiệp?"*).
- **Chọn 5 tone** (phong cách) cần chuyển đổi:
  - **Chuyên nghiệp** (Business)
  - **Thân thiện** (Friendly)
  - **Marketing** (Marketing)
  - **Học thuật** (Academic)
  - **Giải trí** (Entertainment)

##### **C. Node `LangChain LMChatOpenAi` (Gọi API GPT-4o-mini)**
- **Cấu hình API Key**:
  - Vào **Credentials** → **Add** → **OpenAI**.
  - Điền **API Key** từ OpenAI.
- **Prompt Template**:
  ```json
  "You are a professional content writer. Rewrite the following text in {tone} tone. Keep the original meaning but adjust the style to match the requested tone. Original text: {content}"
  ```
  - Thay `{tone}` và `{content}` bằng các giá trị từ **Sticky Note**.
- **Model**: Chọn **gpt-4o-mini** (rẻ và hiệu quả).

##### **D. Node `LangChain Agent` (Quản lý quá trình viết)**
- **Không cần chỉnh sửa**, node này tự động **gọi API GPT-4o-mini** với các **prompt khác nhau**.

##### **E. Node `Google Drive` (Lưu file)**
- **Cấu hình Google Drive**:
  - Vào **Credentials** → **Add** → **Google Drive**.
  - Điền **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
  - Chọn **Folder** muốn lưu file.
- **Cấu hình Node**:
  - **File Name**: `{tone}_rewrite_{date}.txt` (ví dụ: `business_rewrite_2024-05-20.txt`).
  - **File Content**: Nội dung từ **LangChain Agent**.

##### **F. Node `Slack` (Gửi thông báo)**
- **Cấu hình Slack**:
  - Vào **Credentials** → **Add** → **Slack**.
  - Điền **Token Slack** (tạo từ [API Slack](https://api.slack.com/apps)).
  - Chọn **Kênh Slack** muốn nhận thông báo.
- **Message Template**:
  ```json
  "Tone: {tone}\n\nContent:\n{content}"
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và kiểm tra **Google Drive** và **Slack** để xem kết quả.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động khi cần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
1. **Tự động hóa viết nội dung định kỳ**:
   - Sử dụng **n8n Webhook** để **kích hoạt workflow** từ **Google Form** hoặc **email**.
   - Ví dụ: Khách hàng gửi **email yêu cầu viết bài**, workflow tự động **xử lý và gửi kết quả**.

2. **Lưu log và theo dõi chi phí API**:
   - Sử dụng **n8n Node `Set`** để **lưu chi phí API** vào **Google Sheets**.
   - Cài đặt **ngưỡng cảnh báo** khi chi phí vượt quá ngân sách.

3. **Kết hợp với Notion/Coda**:
   - Thay vì **Google Drive**, lưu nội dung vào **Notion** hoặc **Coda** để **quản lý dễ dàng hơn**.

4. **Tạo bộ sưu tập tone chuẩn**:
   - Tạo **Sticky Note** riêng để lưu **các tone mặc định** (ví dụ: tone marketing của brand).
   - Sử dụng **n8n Node `Code`** để **tự động chọn tone** từ danh sách.

5. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Node `Schedule`** để **gửi báo cáo tổng hợp** về **tất cả phiên bản nội dung** vào **Slack/Email** hàng tuần.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **viết nội dung thủ công**. Với **GPT-4o-mini**, **Google Drive**, và **Slack**, các sếp có thể:
✔ **Viết 5 phiên bản nội dung trong vài giây**.
✔ **Lưu trữ an toàn** và **theo dõi dễ dàng**.
✔ **Tự động hóa hoàn toàn** mà **không cần code**.

**Hãy thử ngay!** Nếu có bất kỳ câu hỏi, các sếp có thể **comment bên dưới** hoặc liên hệ với **Incrementors** qua [n8n.io](https://n8n.io).

---
**🚀 Bắt đầu tự động hóa nội dung của mình ngay hôm nay!**