---
title: "🚀 Tự Động Hóa Gửi Trả Lời Liên Hệ LinkedIn Tự Động Cho Người Xem Profile - N8n + SourceGeek"
description: "Tiết kiệm 100% thời gian theo dõi và gửi trả lời chuyên nghiệp cho những người xem profile LinkedIn của bạn. Workflow này tự động phân tích, gửi yêu cầu kết nối hoặc tin nhắn cá nhân hóa dựa trên tình trạng kết nối hiện tại."
slug: "tu-dong-hoa-gui-tra-loi-linkedin-sourcegeek"
tags: [n8n, automation, lead-nurturing, linkedin-automation, sourcegeek]
keywords: [n8n workflow linkedin, tự động hóa liên hệ linkedin, sourcegeek n8n, gửi tin nhắn tự động linkedin, lead nurturing]
---

# 🚀 **Tự Động Hóa Gửi Trả Lời LinkedIn Cho Người Xem Profile - Cách Tiết Kiệm 100% Thời Gian Theo Dõi**

## **💡 Nỗi Đau Của Các Sếp: Theo Dõi & Trả Lời Từng Người Xem Profile LinkedIn**
Bạn đã bao giờ cảm thấy **mệt mỏi** khi phải theo dõi danh sách người xem profile LinkedIn của mình, sau đó phải **gửi từng tin nhắn cá nhân hóa** cho họ? Thời gian này có thể được sử dụng để **nurture leads**, **xây dựng mối quan hệ** hoặc **tăng doanh số** thay vì bị "chôn vùi" trong công việc thủ công?

**Giải pháp?** Workflow này sẽ **tự động hóa toàn bộ quy trình**:
✅ **Lấy danh sách 10 người gần đây xem profile**
✅ **Kiểm tra tình trạng kết nối** (1st degree hay 2nd degree)
✅ **Gửi yêu cầu kết nối** (nếu là 2nd degree) **hoặc tin nhắn cá nhân hóa** (nếu là 1st degree)
✅ **Tất cả chỉ với một cú nhấp chuột!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** theo dõi và gửi tin nhắn thủ công.
- **Tăng cơ hội kết nối** với những người tiềm năng (candidate, client, partner).
- **Cá nhân hóa tương tác** với tin nhắn tự động dựa trên tình trạng kết nối.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Tăng hiệu quả lead nurturing** với chiến lược tự động hóa chuyên nghiệp.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
✔ **Tài khoản LinkedIn** (để SourceGeek kết nối và gửi yêu cầu).
✔ **Tài khoản SourceGeek** ([Đăng ký miễn phí](https://sourcegeek.com/)) và **API Key** của SourceGeek.
✔ **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
✔ **Thời gian 15 phút** để cấu hình workflow.
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15075](https://n8n.io/workflows/15075) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. **Nhấn "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên và **copy toàn bộ nội dung**.
2. **Trên n8n Editor**, nhấn **"Import"** → **"Paste JSON"** và dán.
3. **Xác nhận** để workflow được tạo.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần chỉnh gì**, chỉ cần nhấn **"Execute workflow"** khi muốn chạy.

#### **🔹 Node 2 & 3: Import & Check Connection Status (SourceGeek)**
- **Credentials**: Đảm bảo đã cấu hình **"sourcegeekCredentialsApi"** trong **n8n Credentials**.
  - **Cách cấu hình**:
    1. **Truy cập n8n Credentials** → **"Add new"** → Chọn **"SourceGeek"**.
    2. **Nhập API Key** từ SourceGeek (tìm trong **Settings → API Keys**).
    3. **Lưu** và chọn credential này trong node **Import users** và **Check connection status**.

#### **🔹 Node 4: Code (JavaScript) - Lọc người mới xem**
- **Mã mặc định** đã lọc **10 người gần đây nhất**, nhưng các sếp có thể **sửa số lượng** nếu muốn.
- **Cách chỉnh**:
  ```javascript
  // Thay đổi `10` thành số lượng mong muốn (ví dụ: 20)
  const viewers = $input.all();
  return viewers.slice(0, 10); // Lấy 10 người đầu tiên
  ```

#### **🔹 Node 5: Switch (Phân loại 1st vs 2nd Degree)**
- **Không cần chỉnh**, node này tự động phân loại dựa trên kết quả từ **Check Connection Status**.

#### **🔹 Node 6: Split in Batches (Loop qua từng người)**
- **Không cần chỉnh**, node này sẽ **lặp qua từng người** trong danh sách.

#### **🔹 Node 7 & 8: Send Connection Request / Send Message**
- **Credentials**: Đảm bảo sử dụng **sourcegeekCredentialsApi** (như node 2 & 3).
- **Cá nhân hóa tin nhắn**:
  - Trong node **Send Message**, các sếp có thể **sửa nội dung mặc định** để phù hợp với chiến lược marketing.
  - Ví dụ:
    ```json
    {
      "message": "Xin chào {{$node["Check connection status"].json["$.name"]}}, tôi thấy bạn đã xem profile của tôi. Tôi là [Tên bạn], chuyên gia về [ngành nghề]. Có thể trao đổi về [chủ đề] không? Trân trọng!"
    }
    ```

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute workflow"** → Chọn **"Test"** để kiểm tra.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **đổi trạng thái từ "Inactive" sang "Active"**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để báo cáo**
- **Thêm node Slack/Telegram** sau **"Send Message"** để **báo cáo kết quả** cho team.
- **Ví dụ**:
  ```json
  {
    "message": "🚀 **Tin nhắn tự động gửi thành công!**\n- Người nhận: {{$node["Send message"].json["$.name"]}}\n- Trạng thái kết nối: {{$node["Check connection status"].json["$.connectionStatus"]}}"
  }
  ```

### **🔹 Lưu log vào Google Sheets/Notion**
- **Thêm node Google Sheets** sau **"Send Connection Request"** để **lưu danh sách người đã gửi yêu cầu kết nối**.
- **Cách cấu hình**:
  1. **Tạo sheet mới** trên Google Sheets.
  2. **Cấu hình node Google Sheets** với **credentials** và **sheet name**.
  3. **Chọn "Append row"** để thêm dữ liệu mới mỗi lần chạy.

### **🔹 Gửi báo cáo định kỳ (Hàng tuần/tháng)**
- **Sử dụng node n8n-nodes-base.schedule** để **chạy workflow tự động** vào thời gian cố định.
- **Cách cấu hình**:
  1. **Thêm node "Schedule"** trước **"Manual Trigger"**.
  2. **Chọn thời gian** (ví dụ: **7h sáng thứ 2 hàng tuần**).
  3. **Bật "Active"** để workflow chạy tự động.

### **🔹 Cá nhân hóa tin nhắn theo ngành nghề**
- **Sử dụng node Code** để **lấy thông tin ngành nghề** từ LinkedIn và **sửa tin nhắn tương ứng**.
- **Ví dụ**:
  ```javascript
  const industry = $input.all()[0].industry;
  let message = "Xin chào, tôi thấy bạn làm trong ngành {{industry}}.";

  if (industry === "Tech") {
    message += " Tôi có giải pháp giúp doanh nghiệp của bạn tăng hiệu suất DevOps!";
  } else if (industry === "Marketing") {
    message += " Tôi chuyên hỗ trợ chiến lược digital marketing!";
  }

  return { message: message };
  ```

---
## **📌 Kết Luận: Bắt Đầu Tự Động Hóa Ngay!**

Workflow này không chỉ **giúp tiết kiệm thời gian** mà còn **tăng cơ hội kết nối** với những người tiềm năng trên LinkedIn. **Đừng để những cơ hội trôi qua vì bạn phải theo dõi thủ công!**

### **🔥 Bước đầu tiên:**
1. **Cài n8n Self-hosted** trên VPS (để an toàn và ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình SourceGeek API Key**.
3. **Chạy test** và **bật Active** để tự động hóa ngay!

**Hãy bắt đầu từ hôm nay và xem kết quả như thế nào!** 🚀

---
**💬 Có thắc mắc? Hãy để lại comment bên dưới!**