---
title: "🚀 Tự Động Tạo Ticket Linear Từ Notion Với AI (No-Code)"
description: "Workflow n8n giúp chuyển đổi nội dung Notion thành ticket Linear chuyên nghiệp, tự động rút gọn tiêu đề bằng OpenAI và cập nhật liên kết ngược về Notion."
slug: "tu-dong-tao-ticket-linear-tu-notion"
tags: [n8n, automation, no-code, linear, notion, openai]
keywords: [n8n workflow, tự động hóa ticket, notion to linear, openai integration, quản lý dự án]
---

# 🚀 Tự Động Tạo Ticket Linear Từ Notion Với AI (No-Code)

Các sếp đang quản lý dự án có bao giờ gặp tình trạng này không? Team Product hay Design viết rất chi tiết các yêu cầu, bug report, hoặc feature request trong Notion. Nhưng khi chuyển sang Linear (công cụ quản lý task phổ biến của các team Engineering hiện đại), các sếp lại phải mất thời gian copy-paste, chỉnh sửa định dạng, và đặc biệt là phải nghĩ ra một tiêu đề ngắn gọn, súc tích cho từng ticket.

Quy trình thủ công này không chỉ tốn thời gian mà còn dễ gây sai sót về dữ liệu. Workflow **"Create Linear tickets from Notion content"** này chính là giải pháp hoàn hảo. Nó tự động quét các khối nội dung (blocks) trong Notion, sử dụng **OpenAI** để phân tích và rút gọn tiêu đề ticket một cách thông minh, tạo ticket trong Linear, và cuối cùng là thêm liên kết ngược về Notion để team biết ticket đã được tạo. Tất cả diễn ra trong vài giây, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đáng kể:** Loại bỏ hoàn toàn bước copy-paste và chỉnh sửa thủ công giữa Notion và Linear.
- **Tiêu đề Ticket chuyên nghiệp nhờ AI:** OpenAI tự động đọc nội dung dài dòng và tạo ra tiêu đề ngắn gọn, dễ hiểu, chuẩn SEO nội bộ.
- **Đảm bảo tính nhất quán:** Mọi ticket đều được tạo theo đúng cấu trúc, gán đúng team và người phụ trách (nếu có).
- **Truy xuất nguồn gốc dễ dàng:** Liên kết Linear được tự động chèn ngược vào Notion, giúp team Product/Design biết chính xác ticket nào đã được tạo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
2. **Tài khoản Notion:**
   - Tạo một Integration trong Notion.
   - Chia sẻ trang Notion chứa các issue cần chuyển sang Linear với Integration này.
   - Trang Notion cần được định dạng theo cấu trúc mẫu (có các block `to_do` hoặc văn bản mô tả).
3. **Tài khoản Linear:**
   - Tạo API Key trong Linear Settings.
   - Xác định tên Team trong Linear (ví dụ: "Engineering", "Product").
4. **Tài khoản OpenAI:**
   - API Key để sử dụng cho việc rút gọn tiêu đề (Shorten title).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/2138` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy một workflow với 19 nodes được kết nối logic rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình lại các node sau để khớp với dữ liệu của mình:

**A. Cấu hình Trigger & Input**
- **Node: `n8n Form Trigger`**
  - Đây là node khởi động workflow.
  - **Lưu ý:** Trong phần cấu hình Form, các sếp cần điền vào trường "Linear Team Names" (hoặc tương tự) danh sách tên các team trong Linear của mình (ví dụ: `Engineering, Product, Design`). Điều này giúp form hiển thị đúng các lựa chọn cho người dùng.

**B. Cấu hình Notion**
- **Node: `Get issues`** và **`Get issue contents`**
  - Chọn credentials **Notion API** đã tạo ở bước chuẩn bị.
  - **Page ID:** Điền ID của trang Notion chứa các issue cần chuyển. Các sếp có thể lấy ID từ URL của trang Notion (phần sau cùng của link).
  - **Resource:** Đảm bảo chọn đúng `block` và operation `getAll`.

**C. Cấu hình Linear**
- **Node: `Fetch Linear team details`**
  - Chọn credentials **Linear API** (thường là `httpHeaderAuth` với API Key).
  - Node này dùng GraphQL để lấy thông tin chi tiết của team (ID, v.v.) dựa trên tên team nhập từ Form.
- **Node: `Create linear issue`**
  - Chọn credentials **Linear API**.
  - Đảm bảo các trường `Team ID`, `Title`, `Description` được ánh xạ đúng từ các node trước đó.

**D. Cấu hình OpenAI (AI)**
- **Node: `Shorten title`**
  - Chọn credentials **OpenAI API**.
  - **Model:** Chọn model phù hợp (ví dụ: `gpt-4o-mini` hoặc `gpt-3.5-turbo` để tiết kiệm chi phí).
  - **Prompt:** Mặc định workflow đã có prompt tốt, nhưng các sếp có thể chỉnh sửa để yêu cầu AI rút gọn tiêu đề theo phong cách riêng của công ty (ví dụ: "Dùng tiếng Anh, dưới 50 ký tự, bắt đầu bằng động từ").

**E. Logic & Xử lý dữ liệu**
- **Node: `Unimported, unchecked to_do blocks only`**
  - Node `Filter` này đảm bảo chỉ xử lý các khối nội dung chưa được import và chưa được đánh dấu hoàn thành. Các sếp không cần chỉnh gì nhiều, nhưng hãy đảm bảo dữ liệu đầu vào từ Notion có cấu trúc đúng.
- **Node: `Set assignee and title`**
  - Node `Code` này xử lý logic gán người phụ trách (assignee) và chuẩn bị tiêu đề. Nếu các sếp muốn gán assignee cố định, có thể chỉnh sửa code trong node này.
- **Node: `Add link to Notion block`**
  - Dùng `httpRequest` để gọi API Notion, chèn link Linear vừa tạo vào trang Notion gốc. Đảm bảo credentials Notion API có quyền ghi (write) vào trang.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Test Workflow** (hoặc Execute Workflow).
   - Một form sẽ hiện ra. Các sếp nhập tên Team Linear và các thông tin cần thiết.
   - Quan sát các node chạy lần lượt: Lấy dữ liệu Notion -> AI rút gọn tiêu đề -> Tạo ticket Linear -> Cập nhật link về Notion.
2. **Kiểm tra kết quả:**
   - Mở Linear, xem ticket mới có đúng không.
   - Mở Notion, xem link Linear đã được chèn vào chưa.
3. **Bật Active:**
   - Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng chạy khi có yêu cầu từ Form.

### ✍️ Mẹo & gợi ý nâng cao

- **Tự động hóa hoàn toàn với Webhook:** Thay vì dùng `Form Trigger`, các sếp có thể thay bằng `Webhook Trigger` hoặc `Schedule Trigger` (chạy định kỳ mỗi giờ) để tự động quét Notion và tạo ticket mà không cần ai bấm nút.
- **Gửi thông báo qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau node `Create linear issue` để gửi thông báo "Ticket mới đã được tạo" vào kênh chat của team.
- **Phân loại ưu tiên (Priority):** Sử dụng thêm một node OpenAI để phân tích nội dung và gán mức độ ưu tiên (Low, Medium, High, Urgent) cho ticket Linear dựa trên từ khóa trong mô tả.
- **Log lỗi:** Thêm node `Error Trigger` để ghi log các lỗi xảy ra (ví dụ: Notion API lỗi, Linear API lỗi) vào một bảng Google Sheets hoặc gửi email cảnh báo cho admin.

### 📌 Kết luận

Workflow **"Create Linear tickets from Notion content"** là một ví dụ tuyệt vời về cách kết hợp sức mạnh của **Notion** (quản lý tri thức), **Linear** (quản lý công việc), và **OpenAI** (xử lý ngôn ngữ tự nhiên) thông qua n8n. Thay vì mất hàng giờ mỗi tuần để chuyển đổi dữ liệu thủ công, các sếp chỉ cần vài cú click chuột. Hãy import workflow này, cấu hình credentials, và trải nghiệm sự khác biệt ngay hôm nay!