---
title: "🤖 Tự Động Hóa Trợ Lý Mua Sắm Cá Nhân Hóa với GPT-4, Zep Memory & Google Sheets - Không Cần Code!"
description: "Xây dựng một trợ lý mua sắm thông minh tự động tra cứu lịch sử đơn hàng, tồn kho và chính sách hoàn trả từ Google Sheets, kết hợp trí tuệ nhân tạo GPT-4 và bộ nhớ Zep để cung cấp gợi ý cá nhân hóa 24/7 cho khách hàng. Giảm thiểu thời gian phản hồi từ 5 phút xuống 0 giây!"
slug: "tro-ly-mua-sam-canh-nhan-hoa-gpt-4-zep-google-sheets"
tags: [n8n, automation, ai-agent, google-sheets, gpt-4, zep-memory, no-code]
keywords: [tự động hóa trợ lý mua sắm, gpt-4 n8n, zep memory, google sheets automation, ai agent no-code, chatbot cá nhân hóa]
---

# 🚀 **Trợ Lý Mua Sắm Cá Nhân Hóa Tự Động Hóa với GPT-4, Zep Memory & Google Sheets**

### **Giải pháp cho nỗi đau:**
Các sếp đang phải mất **thời gian quý báu** để tra cứu lịch sử đơn hàng, tồn kho và chính sách hoàn trả cho từng khách hàng mỗi khi họ có yêu cầu. Thậm chí, với số lượng khách hàng lớn, việc phản hồi cá nhân hóa trở nên **khó khăn và dễ sai sót**. Hãy tưởng tượng một **trợ lý ảo thông minh** có thể:
- **Tra cứu lịch sử đơn hàng** của khách hàng từ Google Sheets trong giây lát.
- **Kiểm tra tồn kho** thời gian thực để đề xuất sản phẩm phù hợp.
- **Hiểu và áp dụng chính sách hoàn trả** một cách chính xác.
- **Gợi ý sản phẩm cá nhân hóa** dựa trên lịch sử mua hàng qua trí tuệ nhân tạo **GPT-4** và bộ nhớ **Zep**.

**Workflow này tự động hóa toàn bộ quy trình đó – chỉ cần cài đặt một lần, nó sẽ hoạt động **24/7** mà không cần can thiệp của con người!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và không gián đoạn**, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ phản hồi nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian phản hồi** từ **5 phút xuống 0 giây** – khách hàng nhận được trợ giúp tức thì.
✅ **Cá nhân hóa hoàn toàn** – trợ lý hiểu lịch sử mua hàng và đề xuất sản phẩm phù hợp.
✅ **Chính xác 100%** – không sai sót trong tra cứu đơn hàng, tồn kho hoặc chính sách.
✅ **Hoạt động liên tục** – không cần nhân viên hỗ trợ 24/7, tiết kiệm chi phí nhân sự.
✅ **Dễ dàng mở rộng** – có thể kết nối với **Slack, Telegram, hoặc website** để khách hàng tương tác dễ dàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng **GPT-4.1-mini**) và **API Key**.
2. **Tài khoản Zep** (để lưu trữ bộ nhớ cá nhân hóa) và **API Key**.
3. **Google Sheets** với **3 bảng dữ liệu** (cấu trúc mẫu được cung cấp):
   - **Lịch sử đơn hàng** (`Get_Orders`).
   - **Tồn kho sản phẩm** (`Get_Inventory`).
   - **Chính sách hoàn trả** (`Get_ReturnPolicy`).
4. **Credentials OAuth2 cho Google Sheets** (để n8n có thể đọc dữ liệu).

---
:::note[LINK MẪU GOOGLE SHEETS]
Các sếp có thể tham khảo **bảng mẫu** để cấu trúc dữ liệu:
🔗 [Google Sheets Mẫu](https://docs.google.com/spreadsheets/d/17PsTWr5shCgA2RnHuj1xwqSRX7uBcb-psRYZA2jFOTo/edit?usp=sharing)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/7363) hoặc sử dụng file JSON đã cung cấp.
2. Mở **n8n Editor** và chọn **"Import Workflow"** (hoặc **"Create New Workflow"** và paste JSON).
3. **Kích hoạt workflow** bằng cách bấm **"Active"** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Cấu hình Credentials**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **OpenAI Chat Model** | Điền **API Key** từ tài khoản OpenAI vào `openAiApi`. Chọn mô hình: **`gpt-4.1-mini`**. |
| **Zep** | Điền **API Key** từ tài khoản Zep vào `zepApi`. |
| **Google Sheets** | Thêm **credentials OAuth2** vào `googleSheetsOAuth2Api` (cấu hình trong **n8n Credentials**). |

##### **B. Cấu hình Google Sheets**
- **Get_Orders**: Đặt **Sheet Name** là **"Đơn hàng"** (hoặc tên bảng chứa dữ liệu đơn hàng).
- **Get_Inventory**: Đặt **Sheet Name** là **"Tồn kho"** (hoặc tên bảng chứa dữ liệu sản phẩm).
- **Get_ReturnPolicy**: Đặt **Sheet Name** là **"Chính sách hoàn trả"** (hoặc tên bảng chứa quy định).

##### **C. Cấu hình AI Agent**
- **When chat message received**: Nếu muốn kết nối với **Slack/Telegram**, các sếp cần thêm **node Webhook** và cấu hình URL callback.
- **Zep Memory**: Đảm bảo **API Key** của Zep được điền chính xác để lưu trữ lịch sử chat.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một **dữ liệu mẫu** (ví dụ: "Hãy tra cứu đơn hàng của tôi").
2. Kiểm tra **log** để đảm bảo tất cả node hoạt động bình thường.
3. Bật **Active workflow** để nó bắt đầu hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Webhook** và cấu hình để nhận tin nhắn từ Slack/Telegram.
   - Khách hàng có thể tương tác với trợ lý qua **messenger** thay vì chat trực tiếp.

2. **Lưu log hoạt động**:
   - Thêm **node Set** hoặc **node Sticky Note** để ghi lại lịch sử tương tác.
   - Có thể **export log** vào Google Sheets để phân tích.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node Schedule** để gửi **báo cáo tổng hợp** về hoạt động của trợ lý mỗi ngày/tuần.

4. **Cải thiện trải nghiệm người dùng**:
   - Thêm **node Email** để gửi **gợi ý sản phẩm** tự động sau mỗi tương tác.
   - Sử dụng **node LLM** để **tự động trả lời** các câu hỏi thường gặp.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa **trợ lý mua sắm cá nhân hóa** một cách **không cần code**, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. **Chỉ cần cài đặt một lần**, nó sẽ hoạt động **mang lại lợi ích lâu dài** cho doanh nghiệp!

👉 **Bắt tay vào tự động hóa ngay hôm nay!** Nếu có bất kỳ câu hỏi, các sếp có thể để lại comment dưới đây. 🚀