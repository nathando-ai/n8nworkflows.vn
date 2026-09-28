---
title: "🔍 **Tự Động Hóa Theo Dõi Backlinks Mới Với Google Sheets & Email Hàng Ngày - Không Cần Code!**"
description: "Workflow này tự động lấy backlinks mới từ DataForSEO, ghi vào Google Sheets và gửi báo cáo email hàng ngày. Giúp các sếp SEO tiết kiệm 10+ giờ/tháng theo dõi thủ công, đồng thời có dữ liệu chính xác về spam score, domain rating (DR), và loại backlink (dofollow/nofollow)."
slug: "tieu-dong-ho-tra-lai-backlinks-moi-voi-dataforseo-google-sheets"
tags: [n8n, automation, seo, dataforseo, google-sheets, gmail, market-research]
keywords: [n8n workflow backlinks, tự động hóa seo, lấy backlinks tự động, báo cáo backlinks hàng ngày, google sheets seo, email tự động seo]
---

# 🚀 **Tự Động Hóa Theo Dõi Backlinks Mới: Từ DataForSEO → Google Sheets → Email Hàng Ngày**

### **Nỗi Đau Của Các Sếp SEO Hiện Nay**
Theo dõi backlinks thủ công là một việc **tốn thời gian, dễ sai sót** và **không hiệu quả**. Các sếp phải:
- **Tra cứu backlinks** trên nhiều công cụ (Ahrefs, Moz, SEMrush...) mỗi ngày.
- **Ghi chép vào Excel/Google Sheets** bằng tay, dẫn đến lỗi nhập liệu.
- **Gửi báo cáo** cho team marketing bằng email, mất thêm thời gian chỉnh sửa.
- **Không biết** liệu backlink mới có chất lượng (spam score thấp, domain rating cao) hay không.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy backlinks mới** từ DataForSEO (API nhanh chóng, dữ liệu chính xác).
✅ **Ghi vào Google Sheets** với cấu trúc sạch sẽ (referring domain, spam score, DR, dofollow/nofollow).
✅ **Gửi email tự động** với link trực tiếp đến báo cáo hàng ngày.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần tra cứu thủ công hàng ngày.
- **Dữ liệu chính xác**: Backlinks mới được lọc theo spam score và domain rating.
- **Báo cáo tự động**: Email hàng ngày với link trực tiếp đến Google Sheets.
- **Dễ dàng theo dõi**: Cấu trúc bảng Google Sheets chuyên nghiệp, sẵn sàng chia sẻ với team.
- **Không cần code**: Cài đặt chỉ trong 15 phút, chạy 24/7 trên VPS.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản DataForSEO**:
   - [Đăng ký API Key](https://app.dataforseo.com/api-access) (miễn phí cho các plan cơ bản).
   - **Domain/URL** muốn theo dõi (ví dụ: `example.com`).
2. **Tài khoản Google Sheets**:
   - **Google Workspace** (nếu sử dụng Gmail doanh nghiệp).
   - **Bảng Google Sheets** mới hoặc đã có (sẽ tự động tạo nếu chưa có).
3. **Tài khoản Gmail**:
   - **OAuth 2.0** cho Gmail (để gửi email tự động).
   - **Email nhận báo cáo** (cần phải là địa chỉ Gmail chính thức).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/13694](https://n8n.io/workflows/13694) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không cần chỉnh sửa toàn bộ workflow** nếu đã import thành công.
- **Kích hoạt chế độ "Active"** sau khi cấu hình xong.
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **A. Cấu Hình DataForSEO (Lấy Backlinks)**
1. **Tạo connection DataForSEO**:
   - Vào **n8n Editor** → **Connections** → **Create Connection** → Chọn **DataForSEO**.
   - Điền:
     - **API Key** (từ [DataForSEO API Access](https://app.dataforseo.com/api-access)).
     - **Domain/URL** muốn theo dõi (ví dụ: `example.com`).
   - **Lưu connection** với tên `dataForSeoApi`.

2. **Cấu hình node "Get new backlinks"**:
   - Trong workflow, mở node **`Get new backlinks`**.
   - Chọn **credentials**: `dataForSeoApi` (đã tạo ở trên).
   - **Không cần chỉnh sửa thêm** (API sẽ tự lấy backlinks mới).

#### **B. Cấu Hình Google Sheets (Lưu Dữ Liệu)**
1. **Tạo connection Google Sheets**:
   - Vào **Connections** → **Create Connection** → Chọn **Google Sheets**.
   - **Login OAuth 2.0** và chọn tài khoản Google Workspace.
   - **Lưu connection** với tên `googleSheetsOAuth2Api`.

2. **Cấu hình node "Create spreadsheet"**:
   - Mở node **`Create spreadsheet`**.
   - Chọn **credentials**: `googleSheetsOAuth2Api`.
   - **Không cần chỉnh sửa** (n8n sẽ tự tạo bảng mới nếu chưa có).

3. **Cấu hình node "Append row in sheet"**:
   - Mở node **`Append row in sheet`**.
   - Chọn **credentials**: `googleSheetsOAuth2Api`.
   - **Sheet Name**: Đặt tên bảng (ví dụ: `Backlinks Daily Report`).
   - **Headers**: N8n sẽ tự động tạo từ dữ liệu DataForSEO (referring domain, spam score, DR, etc.).

#### **C. Cấu Hình Gmail (Gửi Email Báo Cáo)**
1. **Tạo connection Gmail**:
   - Vào **Connections** → **Create Connection** → Chọn **Gmail**.
   - **Login OAuth 2.0** và chọn tài khoản Gmail chính thức.
   - **Lưu connection** với tên `gmailOAuth2`.

2. **Cấu hình node "Send a message"**:
   - Mở node **`Send a message`**.
   - Chọn **credentials**: `gmailOAuth2`.
   - **To**: Điền email nhận báo cáo (ví dụ: `team-marketing@doanhnghiep.com`).
   - **Subject**: Đặt tiêu đề email (ví dụ: `🔍 Báo cáo Backlinks Mới - [Ngày tháng]`).
   - **Body**: Sử dụng **template HTML** để link trực tiếp đến Google Sheets:
     ```html
     <p>Xin chào,</p>
     <p>Dưới đây là báo cáo backlinks mới của <strong>[Domain]</strong>:</p>
     <p><a href="[LINK_TO_GOOGLE_SHEETS]">Xem báo cáo chi tiết</a></p>
     <p>Trân trọng,</p>
     <p>Automation Team</p>
     ```
   - **Lưu ý**: N8n sẽ tự động thay thế `[Domain]` và `[LINK_TO_GOOGLE_SHEETS]` khi chạy.

#### **D. Cấu Hình Schedule Trigger (Chạy Hàng Ngày)**
- Node **`Schedule Trigger`** đã được cấu hình sẵn để chạy **mỗi ngày lúc 8h sáng** (thời gian mặc định).
- **Không cần chỉnh sửa** trừ khi các sếp muốn thay đổi thời gian.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và chọn **Execute Once**.
   - Kiểm tra:
     - Backlinks có được lấy không?
     - Dữ liệu có ghi vào Google Sheets không?
     - Email có được gửi không?

2. **Bật chế độ Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Xóa Backlinks Trùng Lặp**
- Sử dụng **node `filter`** để lọc bỏ backlinks đã tồn tại trong Google Sheets.
- **Cách làm**:
  - Mở node **`Filter (has new backlinks)`**.
  - Thêm **condition**:
    ```json
    {
      "jsonpath": "$[*]",
      "operator": "notIn",
      "value": "$$.context.existingBacklinks"
    }
    ```
  - **Lưu ý**: Cần thêm một node **`googleSheets`** để lấy dữ liệu cũ trước khi filter.

### **2. Gửi Báo Cáo Đến Slack/Telegram**
- Thay thế node **`gmail`** bằng **`slack`** hoặc **`telegram`**.
- **Cách làm**:
  - Tạo connection Slack/Telegram trong **n8n**.
  - Thay đổi node **`Send a message`** thành **`slack.sendMessage`** hoặc **`telegram.sendMessage`**.
  - Cấu hình nội dung báo cáo tương tự như email.

### **3. Lưu Log Lịch Sử Cho Dễ Theo Dõi**
- Thêm **node `stickyNote`** để ghi lại lịch sử chạy workflow.
- **Cách làm**:
  - Mở node **`stickyNote`** (đã có trong workflow).
  - Chọn **credentials**: `stickyNote` (n8n sẽ tự tạo).
  - **Lưu ý**: Dữ liệu này sẽ được lưu trong **n8n Dashboard** để theo dõi.

### **4. Báo Cáo Thống Kê Hàng Tháng**
- Sử dụng **node `googleSheets`** để tạo **bảng tổng hợp** hàng tháng.
- **Cách làm**:
  - Thêm một **schedule trigger** chạy vào ngày 1 mỗi tháng.
  - Sử dụng **node `aggregate`** để tính toán:
    - Số lượng backlinks mới.
    - Domain rating trung bình.
    - Spam score thấp nhất.
  - Gửi báo cáo tổng hợp qua email.

---

## 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** cho các sếp SEO để tập trung vào **strategy** thay vì công việc thủ công. Với **DataForSEO + Google Sheets + Email tự động**, các sếp sẽ:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Có dữ liệu backlinks chính xác** (spam score, DR, dofollow).
✔ **Báo cáo tự động** hàng ngày/sáng.

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật chế độ Active** và **quên đi việc theo dõi backlinks thủ công!**

---
**🚀 Cần hỗ trợ?** Đăng ký **hỗ trợ kỹ thuật** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với DataForSEO qua [support@dataforseo.com](mailto:support@dataforseo.com).