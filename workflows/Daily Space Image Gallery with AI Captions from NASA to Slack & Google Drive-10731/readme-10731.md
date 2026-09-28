---
title: "🚀 Tự Động Hóa Bảng Ảnh Vũ Trụ NASA Hàng Ngày Với AI Caption - Gửi Slack & Lưu Google Drive"
description: "Workflow tự động lấy 3 ảnh vũ trụ đẹp nhất từ NASA (Trái Đất, Sao Hỏa, Thư viện) hàng ngày, tạo caption AI độc đáo bằng GPT-4.1-mini, và gửi kết quả sang Slack + lưu bản sao trên Google Drive - hoàn toàn không cần code!"
slug: "tieu-dong-hoa-bang-anh-nasa-ai-caption-slack-google-drive"
tags: [n8n, automation, no-code, ai-caption, nasa-api, google-drive, slack-integration, multimodal-ai]
keywords: [n8n workflow tự động hóa, lấy ảnh NASA hàng ngày, AI tạo caption tiếng Nhật, gửi Slack tự động, lưu Google Drive, tự động hóa nội dung vũ trụ]
---

# 🚀 **Tự Động Hóa Bảng Ảnh Vũ Trụ NASA Hàng Ngày Với AI Caption - Gửi Slack & Lưu Google Drive**

## **🌌 Nỗi Đau Của Các Sếp Trong Nội Dung Vũ Trụ**
Bạn có bao giờ phải:
- **Tìm kiếm thủ công** ảnh vũ trụ đẹp nhất hàng ngày từ NASA để chia sẻ trên Slack?
- **Viết caption** bằng tay, mất thời gian và không thể đảm bảo tính sáng tạo?
- **Quên lưu bản sao** để tham khảo sau này?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động lấy 3 ảnh NASA** (Trái Đất, Sao Hỏa, Thư viện) hàng ngày
✅ **Tạo caption AI** độc đáo bằng GPT-4.1-mini (ngôn ngữ Nhật Bản)
✅ **Gửi kết quả sang Slack** với định dạng đẹp mắt
✅ **Lưu bản sao trên Google Drive** để tham khảo sau

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30 phút/ngày** so với làm thủ công
- **Caption AI độc đáo** thay vì copy-paste từ NASA
- **Hoạt động tự động** 24/7, không cần can thiệp
- **Lưu trữ an toàn** trên Google Drive
- **Chia sẻ ngay trên Slack** với định dạng chuyên nghiệp
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **API Key NASA** (đăng ký tại [NASA API](https://api.nasa.gov/))
✔ **Credentials Slack** (OAuth Token từ [Slack API](https://api.slack.com/apps))
✔ **Credentials Google Drive** (Service Account JSON từ [Google Cloud](https://developers.google.com/drive/api/v3/quickstart/python))
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys))
✔ **Mã Slack Channel** (ví dụ: `#space-gallery`)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10731](https://n8n.io/workflows/10731)
- **Nhấn "Import"** trong n8n Editor
- **Hoặc copy/paste** JSON vào tab "Import" của n8n

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình NASA API Key**
- **Node: "Workflow Configuration" (type: set)**
  - Thêm biến `NASA_API_KEY` với giá trị là API Key của bạn

##### **B. Cấu Hình Slack**
- **Node: "Post to Slack1" (type: slack)**
  - Chọn **Credentials** đã đăng ký trước
  - Điền **Channel Name** (ví dụ: `#space-gallery`)
  - **Thiết lập Block Kit** (nếu muốn thay đổi layout)

##### **C. Cấu Hình Google Drive**
- **Node: "Google Drive: Save Summary" (type: googleDrive)**
  - Chọn **Credentials** từ Google Service Account
  - Điền **Folder ID** (để lưu file vào thư mục cụ thể)

##### **D. Cấu Hình OpenAI**
- **Node: "OpenAI Chat Model3" (type: lmChatOpenAi)**
  - Chọn **Credentials** từ OpenAI API Key
  - **Không cần thay đổi** model `gpt-4.1-mini` (đã tối ưu cho caption ngắn)

##### **E. Thiết Lập Lịch Trình Chạy**
- **Node: "Daily 10:00 - Start Poll" (type: scheduleTrigger)**
  - **Không cần chỉnh** (đã cấu hình chạy hàng ngày lúc 10:00 UTC)

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu (nút "Run Workflow")
- **Kiểm tra Slack** và **Google Drive** để xác nhận
- **Bật Active** khi mọi thứ hoạt động ổn

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thay đổi ngôn ngữ caption**
   - Trong **node "OpenAI Chat Model3"**, thay `gpt-4.1-mini` thành `gpt-4` (nếu muốn caption dài hơn)
   - **Prompt nâng cao**: `Tạo caption ngắn (50 ký tự) về ảnh này, phong cách thơ Nhật Bản, không có từ "tuyệt vời"`

2. **Gửi báo cáo định kỳ**
   - Thêm **node "Set" mới** sau "Google Drive: Save Summary" để gửi email báo cáo hàng tuần

3. **Kết hợp với Telegram**
   - Thêm **node Telegram Bot** để gửi ảnh cùng caption sang nhóm Telegram

4. **Lưu log hoạt động**
   - Thêm **node "Sticky Note"** để ghi lại lỗi nếu workflow bị crash

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc tạo nội dung vũ trụ hàng ngày, đồng thời **tăng tính chuyên nghiệp** với caption AI độc đáo. **Hãy áp dụng ngay** và chia sẻ bảng ảnh NASA đẹp nhất trên Slack mỗi sáng!

👉 **Bắt đầu tự động hóa ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/10731) và cài đặt VPS với mã giảm giá **VPSN8N**! 🚀