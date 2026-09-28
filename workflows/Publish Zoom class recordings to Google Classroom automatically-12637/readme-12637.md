---
title: "🎓 Tự Động Chuyển Góp Video Zoom Lớp Học Sang Google Classroom - Không Cần Code!"
description: "Học sinh và giáo viên tiết kiệm 100% thời gian ghi chép lại video Zoom vào Google Classroom với workflow tự động hóa này. Hỗ trợ tóm tắt nội dung bằng AI, chia sẻ tự động và quản lý file hiệu quả."
slug: "tieu-dong-chuyen-gop-video-zoom-sang-google-classroom"
tags: [n8n, tự động hóa giáo dục, Zoom, Google Classroom, AI Summarization, no-code]
keywords: [tự động hóa giáo dục, chuyển video Zoom sang Google Classroom, AI tóm tắt bài giảng, tự động chia sẻ lớp học, n8n workflow giáo dục]
---

# 🎓 **Tự Động Chuyển Góp Video Zoom Lớp Học Sang Google Classroom - Không Cần Code!**

### **Nỗi Đau Của Giáo Viên & Học Sinh**
Giáo viên phải mất **thời gian quý báu** để:
- **Tải video Zoom** từ Zoom Cloud sau mỗi buổi học.
- **Chỉnh sửa metadata** (tiêu đề, mô tả, thẻ) cho phù hợp với Google Classroom.
- **Tóm tắt nội dung** để học sinh dễ dàng theo dõi.
- **Chia sẻ lại** video vào Google Classroom, đồng thời **ghi chú** cho học sinh.

**Kết quả?** Thời gian quản lý lớp học bị "đè nặng", trong khi học sinh phải **tìm kiếm video** qua nhiều nơi khác nhau.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Với workflow này, **giáo viên và quản trị lớp học** sẽ:
✅ **Tiết kiệm 5-10 giờ/tuần** (tự động hóa toàn bộ quy trình).
✅ **Video được chia sẻ ngay lập tức** vào Google Classroom với **tiêu đề, mô tả và tóm tắt AI** tự động.
✅ **Quản lý file hiệu quả** (xóa video cũ, sắp xếp theo thứ tự thời gian).
✅ **Học sinh dễ dàng truy cập** video từ Google Classroom, không cần tìm kiếm ngoài Zoom.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài Khoản & API Keys:**
- **Tài khoản Zoom** (để lấy video từ Zoom Cloud).
- **Tài khoản Google Classroom** (để chia sẻ video).
- **Tài khoản OpenAI** (để tóm tắt nội dung video bằng AI).
- **Tài khoản Gmail** (nếu cần gửi thông báo cho học sinh).

📌 **Cấu Hình Cần Điền:**
- **ID Zoom Meeting** (để lấy video).
- **Google Classroom ID** (để chia sẻ).
- **Prompt AI** (để tóm tắt video).
- **Thời gian lưu trữ video** (xóa video cũ sau bao lâu).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/12637](https://n8n.io/workflows/12637).
- **Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
- **Bước 3:** Chọn **n8n Cloud** (nếu dùng miễn phí) hoặc **Self-hosted** (nếu tự cài).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **các node chính sau** (cần cấu hình kỹ):

| **Node**               | **Lưu Ý Cần Chỉnh**                                                                 |
|------------------------|--------------------------------------------------------------------------------------|
| **Webhook (n8n-nodes-base.webhook)** | Cần **bật Webhook** để nhận dữ liệu từ Zoom (hoặc sử dụng **HTTP Request** để gọi API Zoom). |
| **Gmail (n8n-nodes-base.gmail)** | **Chọn tài khoản Gmail** liên kết với Google Classroom.                          |
| **OpenAI (n8n-nodes-langchain.openAi)** | **Điền API Key OpenAI** và **cấu hình Prompt** để tóm tắt video.                  |
| **Google Classroom (n8n-nodes-base.httpRequest)** | **Cấu hình URL API** của Google Classroom (sử dụng **OAuth 2.0**).               |
| **Merge (n8n-nodes-base.merge)** | **Kết hợp dữ liệu** từ Zoom, AI và Google Classroom trước khi chia sẻ.              |
| **Switch (n8n-nodes-base.switch)** | **Chọn điều kiện** để xóa video cũ (nếu cần).                                      |

🔹 **Mẹo:**
- **Kiểm tra lại API Key** của Zoom và Google Classroom (nếu sai, workflow sẽ **không hoạt động**).
- **Test Run** trước khi bật **Active** để đảm bảo **không lỗi**.

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Nhấn **"Test Run"** với **dữ liệu mẫu** (ví dụ: video Zoom mẫu).
- **Bước 2:** Kiểm tra **Google Classroom** xem video đã được chia sẻ chưa.
- **Bước 3:** Nếu thành công, **bật Active** để workflow chạy **24/7**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
💡 **1. Gửi Thông Báo Cho Học Sinh**
- **Kết hợp với Slack/Telegram** để thông báo khi video mới được chia sẻ.
- **Sử dụng node `n8n-nodes-base.slack`** để gửi tin nhắn tự động.

💡 **2. Lưu Log Lịch Sử Chia Sẻ**
- **Sử dụng node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử chia sẻ video.
- **Kết hợp với Google Sheets** để theo dõi thống kê.

💡 **3. Tự Động Xóa Video Cũ**
- **Cấu hình node `n8n-nodes-base.crypto`** để xóa video Zoom sau **30 ngày** (tránh tốn dung lượng).

💡 **4. Tóm Tắt Bài Giảng Bằng AI**
- **Cải thiện Prompt OpenAI** để tóm tắt **chính xác hơn** (ví dụ: *"Tóm tắt bài giảng trong 3 điểm chính, không quá 200 từ"*).

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho giáo viên và quản trị lớp học, đồng thời **cải thiện trải nghiệm học tập** của học sinh bằng cách:
✔ **Video được chia sẻ ngay lập tức** vào Google Classroom.
✔ **Tóm tắt AI** giúp học sinh **nhận biết nội dung chính** nhanh chóng.
✔ **Quản lý file hiệu quả** (xóa video cũ, sắp xếp tự động).

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả giảng dạy!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?** Để lại bình luận bên dưới hoặc liên hệ với **Max** (tác giả workflow) qua [n8n.io](https://n8n.io).