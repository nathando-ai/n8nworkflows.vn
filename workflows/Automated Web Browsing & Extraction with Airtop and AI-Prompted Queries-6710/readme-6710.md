---
title: "🤖 Tự Động Trực Tuyến: Trích Xuất Dữ Liệu Web & Trải Nghiệm AI-Powered Với Airtop & n8n (Không Cần Code)"
description: "Workflow này tự động hóa việc duyệt web, trích xuất dữ liệu từ trang web phức tạp, và sử dụng AI để tối ưu hóa các query. Giúp các sếp tiết kiệm hàng giờ công việc thủ công hàng ngày, đồng thời đảm bảo độ chính xác cao và mở rộng khả năng tự động hóa cho các dự án lớn."
slug: "tự-dộng-trực-tuyến-airtop-ai-n8n"
tags: [n8n, automation, no-code, airtop, ai-chatbot, web-scraping, tự động hóa web]
keywords: [n8n workflow web scraping, tự động hóa duyệt web, airtop n8n, trích xuất dữ liệu tự động, ai-powered automation, công cụ tự động hóa không code]
---

# 🚀 **Tự Động Trực Tuyến: Trích Xuất Dữ Liệu Web & Trải Nghiệm AI-Powered Với Airtop & n8n**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 10-20 giờ/ngày** trích xuất dữ liệu từ các trang web phức tạp (ví dụ: danh sách sản phẩm, thông tin liên hệ, giá cả động).
- **Không cần viết code** nhưng vẫn tự động hóa các tác vụ phức tạp như **điền form, duyệt trang, chụp màn hình, và trích xuất dữ liệu** một cách chính xác.
- **Tối ưu hóa với AI** bằng cách sử dụng các **prompt thông minh** để tự động hóa các query phức tạp.
- **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào máy tính cá nhân.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và liên tục**, các sếp nên **self-host n8n** trên VPS riêng. Với VPS, các sếp có thể:
✅ **Chạy 24/7** mà không lo ngắt kết nối.
✅ **Tùy chỉnh tài nguyên** (CPU, RAM) theo nhu cầu.
✅ **Bảo mật cao** (không phụ thuộc vào cloud miễn phí có giới hạn).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất **30-60 phút** để trích xuất dữ liệu thủ công, workflow này hoàn thành trong **vài giây**.
- **Độ chính xác cao**: Tránh sai sót khi copy-paste hoặc bỏ sót dữ liệu.
- **Tự động hóa phức tạp**: Khả năng **điền form, duyệt trang, chụp màn hình** và **trích xuất dữ liệu** từ các trang web động (SPA, JavaScript-heavy).
- **Kết hợp AI**: Sử dụng **prompt thông minh** để tự động hóa các query phức tạp (ví dụ: tìm kiếm sản phẩm theo tiêu chí cụ thể).
- **Hoạt động liên tục**: Chạy trên VPS, không phụ thuộc vào máy tính cá nhân.
- **Mở rộng dễ dàng**: Thêm các tác vụ mới như **gửi báo cáo Slack/Email** hoặc **lưu log** cho quản lý.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtop**:
   - Đăng ký tại [Airtop](https://airtop.ai/) (dịch vụ tự động hóa web).
   - **API Key** của Airtop (để kết nối với n8n).
   - **Credentials** trong n8n: `airtopApi` (cấu hình trong **Credentials Manager** của n8n).

2. **n8n Self-hosted** (không dùng phiên bản cloud miễn phí):
   - Cài đặt n8n trên VPS (hướng dẫn tại [n8n.io](https://n8n.io/)).
   - Cài đặt **n8n-nodes-base.airtopTool** và **@n8n/n8n-nodes-langchain** (nếu chưa có).

3. **Dữ liệu đầu vào (nếu cần)**:
   - **URL trang web** cần trích xuất.
   - **Prompt AI** (nếu sử dụng `Query page` hoặc `Query page with pagination`).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/6710](https://n8n.io/workflows/6710) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/6710](https://n8n.io/workflows/6710).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã.
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **Airtop** để tương tác với trang web, vì vậy các sếp cần **cấu hình chính xác các node sau**:

#### **A. Cấu hình Credentials Airtop**
1. Trong **Credentials Manager** của n8n:
   - Nhấn **Add new credential** → Chọn **Airtop**.
   - Điền:
     - **Name**: `airtopApi` (giữ nguyên hoặc đổi tên tùy ý).
     - **API Key**: Copy từ tài khoản Airtop.
   - Nhấn **Add**.

#### **B. Cấu hình Node MCP Trigger (đầu workflow)**
- Node này **khởi động workflow** khi có yêu cầu từ Airtop.
- **Không cần chỉnh sửa** (n8n sẽ tự động xử lý).

#### **C. Cấu hình Node "Query page" và "Query page with pagination"**
- Các node này sử dụng **prompt AI** để trích xuất dữ liệu.
- **Cách chỉnh:**
  1. Nhấn vào node `Query page` → Tab **Parameters**.
  2. Tìm phần `Prompt` (được đánh dấu `n8n-auto-generated-fromAI-override`).
  3. **Điền prompt** theo yêu cầu trích xuất (ví dụ:
     ```json
     "Prompt": "Trích xuất tất cả thông tin sản phẩm: tên, giá, mô tả, và đánh giá từ trang này."
     ```
  4. Lặp lại cho node `Query page with pagination` (nếu cần trích xuất nhiều trang).

#### **D. Cấu hình Node "Load a page"**
- Điền **URL trang web** cần duyệt vào `url` (ví dụ: `https://example.com/products`).
- **Lưu ý**:
  - Nếu trang yêu cầu **login**, các sếp cần sử dụng node `Fill form` để tự động điền thông tin.
  - **Không cần API Key** nếu trang không yêu cầu xác thực.

#### **E. Cấu hình Node "Fill form" (nếu cần)**
- Nếu trang web có **form đăng nhập**, các sếp cần:
  1. Nhấn vào node `Fill form` → Tab **Parameters**.
  2. Điền:
     - `fields`: Danh sách các trường cần điền (ví dụ:
       ```json
       {
         "email": "your-email@example.com",
         "password": "your-password"
       }
       ```
  3. **Kết nối với node `Load a page`** trước khi submit.

#### **F. Cấu hình Node "Wait for download"**
- Nếu workflow cần **tải xuống file** (ví dụ: PDF, Excel), các sếp cần:
  1. Đảm bảo node `Query page` hoặc `Click an element` đã **trích xuất dữ liệu** trước.
  2. Node này sẽ **chờ file tải xuống hoàn tất** trước khi tiếp tục.

#### **G. Cấu hình Node "Take screenshot" (nếu cần)**
- Nếu muốn **chụp màn hình** trang web:
  1. Nhấn vào node `Take screenshot` → Tab **Parameters**.
  2. Điền:
     - `windowId`: ID của cửa sổ đang duyệt (thường tự động lấy từ node `Load a page`).
  3. **Lưu ý**: Node này sẽ tạo **link screenshot** trong output.

---

### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhấn **Execute Workflow** (button chạy ở góc trên phải).
   - Kiểm tra **output** của mỗi node (đặc biệt là `Query page` và `Wait for download`).
   - **Sửa lỗi** nếu có (ví dụ: prompt không chính xác, URL sai).

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** (button ở góc trên phải).
   - Workflow sẽ **chạy tự động** khi có yêu cầu từ Airtop.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết hợp với Slack/Telegram để báo cáo kết quả**
- Thêm node **Slack** hoặc **Telegram Bot** vào cuối workflow để:
  - Gửi **kết quả trích xuất** dưới dạng tin nhắn.
  - **Báo lỗi** nếu workflow thất bại.
- **Cách làm**:
  1. Thêm node **Slack** (hoặc **Telegram Bot**) sau node `Wait for download`.
  2. Cấu hình **webhook URL** từ Slack/Telegram.
  3. Chọn **Message** để gửi nội dung trích xuất.

### **2. Lưu log vào Google Sheets/Notion**
- Thêm node **Google Sheets** hoặc **Notion** để:
  - **Lưu lịch sử trích xuất** cho quản lý.
  - **Tạo báo cáo định kỳ** (hàng ngày/tuần).
- **Cách làm**:
  1. Thêm node **Google Sheets** sau node `Query page`.
  2. Cấu hình **Sheet Name** và **Range** (ví dụ: `A1`).
  3. Chọn **Append Row** để thêm dữ liệu mới.

### **3. Tự động hóa nhiều trang web cùng lúc**
- Sử dụng **node `Set`** để lưu **danh sách URL** và **loop** qua từng trang:
  ```json
  {
    "url": ["https://example.com/page1", "https://example.com/page2"]
  }
  ```
- Kết nối với node `Load a page` để duyệt từng trang.

### **4. Sử dụng AI để tối ưu prompt**
- Nếu không chắc prompt nào hiệu quả, các sếp có thể:
  - **Test nhiều prompt** và chọn kết quả tốt nhất.
  - Sử dụng **LangChain** (nếu đã cài node `@n8n/n8n-nodes-langchain`) để **tối ưu hóa query**.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa trích xuất dữ liệu web** mà không cần viết code.
✔ **Tiết kiệm thời gian** và giảm sai sót trong công việc thủ công.
✔ **Kết hợp AI** để tối ưu hóa các query phức tạp.
✔ **Chạy 24/7** trên VPS riêng, không phụ thuộc vào máy tính cá nhân.

**Hành động ngay hôm nay!**
1. **Đăng ký VPS** (nếu chưa có) và cài đặt n8n.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test run** và bật **Active** để tự động hóa công việc!

👉 **[Tải workflow ngay từ n8n.io](https://n8n.io/workflows/6710)** và bắt đầu tự động hóa! 🚀

---
**Chia sẻ và đặt câu hỏi:**
- Có vấn đề khi cấu hình? Đăng câu hỏi tại [n8n Community](https://community.n8n.io/).
- Muốn workflow tùy chỉnh? Liên hệ với **KORE Soluções** (tác giả workflow) tại [website](https://koresolucoes.com.br/).