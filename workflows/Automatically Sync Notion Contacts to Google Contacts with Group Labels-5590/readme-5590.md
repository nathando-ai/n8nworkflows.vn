---
title: "🔄 Tự Động Hóa Đồng Bộ Liên Lạc Notion → Google Contacts Với Nhóm Nhãn (CRM) - Không Cần Code"
description: "Workflow này tự động đồng bộ tất cả liên lạc từ Notion sang Google Contacts, phân loại theo nhóm nhãn từ Notion, và cập nhật trạng thái đã đồng bộ. Giúp các sếp tiết kiệm thời gian quản lý CRM, đồng thời đảm bảo dữ liệu liên lạc luôn chính xác và cập nhật liên tục."
slug: "tieu-dong-bo-notion-google-contacts-nhom-nhan"
tags: [n8n, automation, crm, notion, google-contacts, no-code]
keywords: [tự động hóa CRM, đồng bộ Notion Google Contacts, quản lý liên lạc tự động, workflow n8n, đồng bộ nhãn nhóm]
---

# 🚀 **Tự Động Hóa Đồng Bộ Liên Lạc Notion → Google Contacts Với Nhóm Nhãn (CRM)**

### **Giải Phóng Tay Các Sếp Từ Công Việc Nhập Dữ Liên Lạc Tay Chân!**
Hãy tưởng tượng: **Mỗi khi có liên lạc mới hoặc cập nhật trong Notion, hệ thống tự động chuyển dữ liệu sang Google Contacts**, phân loại theo nhóm nhãn (như "Khách Hàng", "Đối Tác", "Nhân Viên"), và **cập nhật trạng thái đã đồng bộ** trong Notion. Không cần viết code, không cần nhập dữ liệu thủ công – chỉ cần **cài đặt 1 lần và workflow hoạt động 24/7**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính liên tục và bảo mật dữ liệu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu liên lạc thủ công từ Notion sang Google Contacts.
- **Dữ liệu đồng bộ tự động**: Mỗi khi có liên lạc mới hoặc cập nhật trong Notion, hệ thống tự động đồng bộ sang Google Contacts.
- **Phân loại tự động theo nhóm nhãn**: Liên lạc được phân loại vào nhóm tương ứng (ví dụ: "Khách Hàng", "Đối Tác") dựa trên nhãn trong Notion.
- **Trạng thái cập nhật tự động**: Notion sẽ tự động đánh dấu liên lạc đã đồng bộ, tránh trùng lặp.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Notion** với một **bảng dữ liệu liên lạc** (database) có các trường sau:
   - **Tên (Name)**
   - **Số điện thoại (Phone)**
   - **Nhãn (Labels)** (ví dụ: "Khách Hàng", "Đối Tác")
   - **Trạng thái đã đồng bộ (Added to Contacts)** (checkbox)
2. **Tài khoản Google Contacts** với quyền **OAuth2** để n8n có thể truy cập và đồng bộ.
3. **n8n self-hosted** (không thể chạy trên n8n.cloud vì sử dụng **community nodes**).
4. **API Key Notion** (nếu không muốn sử dụng OAuth2, mặc dù OAuth2 được khuyến cáo).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/5590) (n8n.io).
- **Import vào n8n Editor**:
  - Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Import Workflow"**.
  - Hoặc **copy/paste** JSON từ [đây](https://n8n.io/workflows/5590) (ấn **"Export"** trên trang workflow).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Cấu Hình Notion Trigger**
- **Node**: *Trigger on New Notion Contact* và *Trigger on Updated Notion Contact*
  - **Database ID**: Tìm trong URL của bảng Notion (ví dụ: `https://www.notion.so/workspace/0427eb01ed3b4947873382c566f23785` → **0427eb01ed3b4947873382c566f23785**).
  - **Properties to Watch**: Chọn các trường cần theo dõi (ví dụ: `Name`, `Phone`, `Labels`).

##### **B. Cấu Hình Google Contacts**
- **Node**: *Add Contact to Google Contacts*
  - **Credentials**: Chọn **Google Contacts OAuth2** đã cấu hình trước (n8n → Credentials → Thêm Google Contacts).
  - **Mapping Fields**:
    - `name` → `Full Name`
    - `phone` → `Phone Number`
    - `labels` → **Phân loại nhóm nhãn** (xem phần sau).

##### **C. Xử Lý Nhãn (Labels) và Nhóm Google Contacts**
- **Node**: *Find Match Labels* (Code Node)
  - **Mã JavaScript** sẽ **chuyển đổi nhãn Notion thành nhóm Google Contacts**.
  - Ví dụ: Nếu Notion có nhãn `"Khách Hàng"`, hệ thống sẽ tạo nhóm tương ứng trong Google Contacts.
  - **Lưu ý**: Các sếp cần **chỉnh sửa mã** trong Code Node để phù hợp với nhãn của mình:
    ```javascript
    // Ví dụ mã trong Code Node (cần chỉnh sửa theo nhãn của các sếp)
    const labelGroups = {
      "Khách Hàng": "Customers",
      "Đối Tác": "Partners",
      "Nhân Viên": "Employees"
    };
    return labelGroups[label] || label; // Nếu nhãn không có trong danh sách, giữ nguyên
    ```

##### **D. Kiểm Tra Trùng Lặp và Đồng Bộ**
- **Node**: *Check if Contact Already Synced* (If Node)
  - Kiểm tra trường **"Added to Contacts"** trong Notion. Nếu đã đồng bộ, workflow **bỏ qua** liên lạc đó.
- **Node**: *Mark Contact as Synced in Notion*
  - Sau khi đồng bộ thành công, **cập nhật trạng thái** trong Notion để tránh trùng lặp.

##### **E. Tạo Nhóm Google Contacts Nếu Không Tồn Tại**
- **Node**: *Fetch Google Contact Groups* và *Create New Google Contact Group*
  - Hệ thống sẽ **kiểm tra** xem nhóm nhãn đã tồn tại trong Google Contacts chưa. Nếu không, **tạo mới**.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và **chọn một liên lạc mẫu** để kiểm tra.
  - Kiểm tra:
    - Liên lạc có được đồng bộ sang Google Contacts không?
    - Nhãn có được phân loại đúng không?
    - Trạng thái **"Added to Contacts"** trong Notion có được cập nhật không?
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để **báo cáo lỗi** hoặc **thông báo đồng bộ thành công**.
   - Ví dụ: Khi đồng bộ thất bại, gửi tin nhắn Slack với chi tiết lỗi.

2. **Lưu Log Đồng Bộ**:
   - Thêm **node Sticky Note** hoặc **Google Sheets** để **ghi lại lịch sử đồng bộ**, giúp theo dõi và debug dễ dàng.

3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node Set** kết hợp với **node HTTP Request** để gửi **báo cáo tổng hợp** về số lượng liên lạc đồng bộ hàng tháng qua email.

4. **Cập Nhật Nhãn Tự Động**:
   - Nếu nhãn trong Notion thay đổi, **cập nhật nhóm Google Contacts** bằng cách thêm **node Notion Trigger** theo dõi trường `Labels`.

5. **Sử Dụng API Key Notion (Nếu Không Dùng OAuth2)**:
   - Nếu các sếp không muốn sử dụng OAuth2, có thể **cấu hình API Key Notion** trong Credentials của n8n.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc nhập dữ liệu liên lạc thủ công**, đồng thời **đảm bảo dữ liệu luôn đồng bộ và chính xác** giữa Notion và Google Contacts. Với **cấu hình đơn giản** và **hoạt động tự động**, các sếp có thể tập trung vào công việc quan trọng hơn!

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình Notion + Google Contacts**.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
**🚀 Cần hỗ trợ thêm?** Hãy để lại bình luận hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community). Chúc các sếp thành công! 💪