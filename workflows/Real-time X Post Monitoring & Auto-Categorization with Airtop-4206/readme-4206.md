---
title: "🚀 Tự Động Hóa Theo Dõi & Phân Loại Bài Đăng X (Twitter) Thời Thực với Airtop - Không Cần Code"
description: "Workflow này tự động theo dõi, trích xuất và phân loại bài đăng X (Twitter) liên quan đến các chủ đề quan tâm của doanh nghiệp, tiết kiệm thời gian lên tới 80% cho công việc phân tích thị trường, phát hiện lead hay theo dõi đối thủ cạnh tranh."
slug: "tu-dong-hoa-theo-doi-phan-loai-bai-dang-x-airtop"
tags: [n8n, automation, marketing, airtop, no-code, x-twitter-automation]
keywords: [n8n workflow x twitter, tự động hóa bài đăng twitter, phân loại bài đăng xã hội, airtop n8n, theo dõi thị trường thời thực]
---

# 🚀 **Tự Động Hóa Theo Dõi & Phân Loại Bài Đăng X (Twitter) Thời Thực với Airtop**

### **🔍 Nỗi Đau Của Các Sếp**
Các sếp thường phải **tốn thời gian hàng giờ** để:
- Theo dõi xu hướng trên X (Twitter) liên quan đến ngành nghề.
- Lọc ra những bài đăng chất lượng từ hàng trăm kết quả tìm kiếm.
- Phân loại bài đăng theo chủ đề (thought leadership, lead discovery, competitive analysis).
- Cập nhật thông tin cho đội ngũ marketing hoặc team phân tích.

**Workflow này giải quyết tất cả bằng cách tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động trích xuất và phân loại **10 bài đăng chất lượng** mỗi lần chạy (không cần scan thủ công).
- **Chính xác cao**: Sử dụng AI phân loại bài đăng theo **danh sách chủ đề** do các sếp định nghĩa.
- **Hoạt động liên tục**: Theo dõi thời thực, không phụ thuộc vào giờ làm việc.
- **Dữ liệu sẵn sàng sử dụng**: Kết quả trả về dưới dạng **JSON structured**, dễ dàng tích hợp vào các workflow tiếp theo (Slack, email, CRM...).
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtop**:
   - [Đăng ký Airtop](https://airtop.ai/) và tạo **1 profile X (Twitter) đã đăng nhập**.
   - Cài đặt **API Key Airtop** trong n8n (Settings → Credentials → Add Airtop API).
2. **URL tìm kiếm X**:
   - Ví dụ: `https://x.com/search?q=AI+agents&f=live` (tìm kiếm live tweets về AI agents).
3. **Danh sách chủ đề phân loại**:
   - Các sếp định nghĩa các **chủ đề quan tâm** (ví dụ: "Web automation use cases", "Thought leadership", "Competitor updates").
   - Dữ liệu này sẽ được sử dụng trong **prompt AI** để phân loại bài đăng.
4. **Workflow cha (Parent Workflow)**:
   - Workflow này **không chạy độc lập**, mà được kích hoạt bởi một workflow khác (ví dụ: định kỳ hoặc sau khi nhận input từ API).
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4206](https://n8n.io/workflows/4206) và import vào n8n Editor.
- **Hoặc copy/paste** JSON vào tab **Import** của n8n.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **8 node** chính, nhưng các sếp cần chú ý đặc biệt đến:

##### **🔹 Node "Inputs" (n8n-nodes-base.set)**
- **Định nghĩa input cần thiết** cho workflow:
  ```json
  {
    "airtop_profile": "your_airtop_profile_id",  // ID profile Airtop đã đăng nhập X
    "x_url": "https://x.com/search?q=AI+agents&f=live",  // URL tìm kiếm X
    "relevant_categories": "Web automation use cases|Thought leadership|Competitor updates"  // Danh sách chủ đề phân loại
  }
  ```
- **Lưu ý**:
  - Thay thế `your_airtop_profile_id` bằng **ID profile Airtop** của các sếp.
  - Sử dụng **kiểu pipe (`|`)** để phân cách các chủ đề trong `relevant_categories`.

##### **🔹 Node "Extract posts" (n8n-nodes-base.airtop)**
- **Prompt AI** đã được cấu hình sẵn để:
  - Trích xuất **10 bài đăng không phải quảng cáo** (non-sponsored).
  - Lọc bài đăng có **URL chứa `/status/`** (tránh bài đăng khác như tweet embed).
  - Phân loại bài đăng theo **danh sách chủ đề** trong `relevant_categories`.
  - Trả về **JSON structured** với các trường:
    ```json
    {
      "writer": "Tên tác giả",
      "time": "Thời gian đăng",
      "text": "Nội dung bài đăng",
      "url": "Link bài đăng",
      "category": "Chủ đề phân loại (hoặc [NA] nếu không phù hợp)"
    }
    ```
- **Không cần chỉnh sửa prompt** nếu các sếp muốn sử dụng logic mặc định.

##### **🔹 Node "Filter out [NA] posts" (n8n-nodes-base.filter)**
- **Lọc bỏ bài đăng không phân loại được** (`category: [NA]`).
- **Cấu hình**:
  - Chọn **field**: `category`
  - **Operator**: `does not equal`
  - **Value**: `[NA]`

##### **🔹 Node "Parse JSON output" (n8n-nodes-base.code)**
- **Node này không cần chỉnh sửa** vì đã được cấu hình để **trả về JSON sạch** từ kết quả trích xuất.

##### **🔹 Các Node Airtop khác (Session, Window, End session)**
- **Không cần chỉnh sửa** vì đã được cấu hình để:
  1. **Khởi tạo session** (Session).
  2. **Mở cửa sổ browser** và tải URL tìm kiếm (Window).
  3. **Kết thúc session** sau khi hoàn thành (End session).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và nhập **input mẫu** như ví dụ trên.
   - Kiểm tra kết quả JSON trả về có đúng không.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động khi được kích hoạt.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**:
   - Sử dụng **node Slack/Telegram** để gửi kết quả phân loại vào kênh chat.
   - Ví dụ: Khi có bài đăng mới thuộc chủ đề "Thought leadership", tự động thông báo cho team.

2. **Lưu Log Dữ Liệu**:
   - Sử dụng **node Google Sheets** hoặc **node Database** để lưu lịch sử bài đăng đã phân loại.
   - Cấu hình **triggers** để lưu dữ liệu định kỳ (ví dụ: hàng ngày).

3. **Tự Động Trả Lời Bài Đăng**:
   - Kết hợp với **node X API** để tự động **retweet** hoặc **reply** với bài đăng phù hợp.
   - Ví dụ: Nếu bài đăng thuộc chủ đề "Lead discovery", tự động gửi tin nhắn cá nhân hóa.

4. **Cập Nhật Danh Sách Chủ Đề**:
   - Sử dụng **node UI** (n8n UI) để cho phép **cập nhật danh sách chủ đề** mà không cần chỉnh sửa code.

5. **Báo Cáo Định Kỳ**:
   - Sử dụng **node Email** hoặc **node Notion** để gửi **báo cáo tuần/month** về xu hướng bài đăng.

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tiết kiệm thời gian** trong việc theo dõi X (Twitter).
✅ **Tự động phân loại** bài đăng theo chủ đề quan tâm.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
- **Import workflow** và cấu hình theo hướng dẫn.
- **Kết hợp với các workflow khác** để tối ưu hóa quy trình marketing.
- **Đăng ký VPS** để chạy workflow ổn định (liên kết dưới đây).

👉 [Mua VPS TinoHost với mã giảm giá **VPSN8N**](https://tino.vn/vps-n8n?affid=388) để tự động hóa mọi thứ!

---