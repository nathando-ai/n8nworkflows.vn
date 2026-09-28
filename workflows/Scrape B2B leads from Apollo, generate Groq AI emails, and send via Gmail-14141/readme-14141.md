---
title: "🚀 Tự Động Hóa Outreach B2B Tối Đa: Scrape Leads Từ Apollo → AI Tạo Email → Gửi Vía Gmail (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tìm kiếm, enrich và liên lạc với leads B2B tiềm năng chỉ trong vài giây, tiết kiệm 10+ giờ/tháng làm thủ công. Sử dụng AI Groq để tạo email cá nhân hóa và Gmail để gửi tự động."
slug: "tieu-dong-hoa-outreach-b2b-apollo-groq-gmail"
tags: [n8n, automation, lead-generation, ai-cold-email, groq, google-sheets, gmail]
keywords: [tự động hóa outreach b2b, scrape leads apollo, ai tạo email cá nhân hóa, workflow n8n lead generation, tự động gửi email gmail]
---

# 🚀 **Tự Động Hóa Outreach B2B Từ A-Z: Scrape Leads → AI Tạo Email → Gửi Vía Gmail (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Trong Outreach B2B**
Làm thủ công outreach B2B là một công việc **mệt mỏi, tốn thời gian và thiếu hiệu quả**:
- **Tìm kiếm leads** trên Apollo hay LinkedIn mất **giờ đồng hồ** mỗi ngày.
- **Tạo email cá nhân hóa** cho từng lead là **khó khăn và không đồng nhất**, dẫn đến tỷ lệ mở thấp.
- **Gửi email thủ công** dễ bị **quên hoặc sai thời điểm**, ảnh hưởng đến hiệu suất.
- **Kiểm tra duplicate leads** và **cập nhật trạng thái** là công việc **lặp đi lặp lại**, gây mất tập trung.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động scrape leads** từ Apollo với thông tin chi tiết (email, số điện thoại, LinkedIn, thông tin công ty).
✅ **AI Groq tự động tạo email cá nhân hóa** dựa trên thông tin của từng lead (job title, công ty, ngành nghề).
✅ **Gửi email tự động qua Gmail** với thời gian cooldown hợp lý để tránh bị đánh dấu là spam.
✅ **Lưu tất cả dữ liệu** vào Google Sheets với trạng thái cập nhật (Pending → Mail Generated → Sent).
✅ **Tránh duplicate leads** để không lãng phí nguồn lực.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** làm thủ công tìm kiếm và gửi email.
- **Tỷ lệ chuyển đổi cao hơn** nhờ email cá nhân hóa bởi AI.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dữ liệu leads sạch và cập nhật** trong Google Sheets, dễ dàng theo dõi.
- **Tránh bị chặn email** nhờ thời gian cooldown tự động.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apollo.io** (để scrape leads):
   - **API Key** (đăng ký tại [Apollo.io Developer Portal](https://www.apollo.io/developer-portal/)).
   - **Header Auth** trong n8n (cấu hình trong **Credentials** của node `Apollo — Search Leads` và `Apollo — Enrich Lead Data`).

2. **Google Sheets** (để lưu leads và email):
   - **File Google Sheets** với **cấu trúc cột chuẩn** (các sếp sẽ được hướng dẫn sau).
   - **OAuth2 Credential** trong n8n (cấu hình trong **Credentials** của các node `googleSheets`).

3. **Groq API Key** (để sử dụng AI tạo email):
   - **Đăng ký tại [Groq Console](https://console.groq.com/)** và lấy **API Key**.
   - Cấu hình trong **Credentials** của node `Groq LLM (Fast AI)`.

4. **Tài khoản Gmail** (để gửi email tự động):
   - **OAuth2 Credential** trong n8n (cấu hình trong **Credentials** của node `Send Cold Email via Gmail`).
   - **Không sử dụng Gmail cá nhân** (nên dùng tài khoản công ty để tránh bị chặn).

5. **Prompt AI cá nhân hóa** (để Groq tạo email):
   - Các sếp cần **cập nhật template email** trong node `AI Cold Email Writer` (hướng dẫn chi tiết sau).
---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. **Tải file JSON** từ [n8n Workflows](https://n8n.io/workflows/14141) (ấn nút **Export**).
2. Trong **n8n Editor**, chọn **Import** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n Workflows](https://n8n.io/workflows/14141).
2. Trong **n8n Editor**, chọn **Import** → **Paste JSON** và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 trigger** chính (hướng dẫn chi tiết trong phần **Ghi Chú** của tác giả):
- **Trigger 1 (Form Trigger)**: Dùng để **nhập thông tin tìm kiếm leads** (job title, location, số lượng leads).
- **Trigger 2 (Manual Trigger)**: Dùng để **chạy AI tạo email và gửi** cho tất cả leads có trạng thái **Pending**.

#### **🔹 Cấu Hình Căn Bản (Cần Thực Hiện Trước Khi Chạy)**
| **Node** | **Thao Tác Cần Làm** | **Lưu Ý** |
|----------|----------------------|------------|
| **Apollo — Search Leads** | Điền **API Key** vào `httpHeaderAuth` (Credentials). | Sử dụng **API Key** từ Apollo.io. |
| **Apollo — Enrich Lead Data** | Sử dụng cùng **API Key** như trên. | Đảm bảo **cooldown 2s** để không bị Apollo chặn. |
| **Groq LLM (Fast AI)** | Điền **Groq API Key** vào `groqApi` (Credentials). | Model mặc định: `qwen/qwen3-32b` (mô hình mạnh mẽ). |
| **Gmail OAuth2** | Kết nối **tài khoản Gmail** (không dùng Gmail cá nhân). | Cần **cho phép quyền** trong Gmail. |
| **Google Sheets OAuth2** | Kết nối **Google Sheets** và chọn **file** chứa leads. | **Cấu trúc cột bắt buộc** (hướng dẫn sau). |
| **Form Trigger (Trigger 1)** | Cấu hình **form** với 3 trường: `Job Title`, `Location`, `Number of Leads`. | Sử dụng node `formTrigger` để người dùng nhập thông tin. |
| **Manual Trigger (Trigger 2)** | Chỉnh **node `When clicking Execute Workflow`** để chạy khi cần. | Dùng để **kích hoạt AI tạo email và gửi**. |

#### **🔹 Cấu Trúc Google Sheets Bắt Buộc**
File Google Sheets phải có **các cột sau** (để workflow hoạt động):
| **Tên Cột** | **Loại Dữ liệu** | **Mô Tả** |
|-------------|------------------|------------|
| `Lead ID` | Text | ID duy nhất của lead (tự động tạo). |
| `Job Title` | Text | Vị trí công việc của lead. |
| `Company` | Text | Tên công ty của lead. |
| `Email` | Text | Email của lead (do Apollo enrich). |
| `Phone` | Text | Số điện thoại (nếu có). |
| `LinkedIn URL` | Text | Link LinkedIn (nếu có). |
| `Location` | Text | Địa chỉ công ty/lead. |
| `Status` | Text | Trạng thái: `Pending` (chờ email), `Mail Generated` (email đã tạo), `Sent` (đã gửi). |
| `Email Subject` | Text | Tiêu đề email (do AI tạo). |
| `Email Body` | Text | Nội dung email (do AI tạo). |

**Lưu ý:**
- **Sheet Name** phải là **`Leads`** (hoặc chỉnh trong node `Fetch Leads from Sheet`).
- **Tab đầu tiên** của file phải là **`Leads`**.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Chạy **Trigger 1 (Form Trigger)** với thông tin mẫu (ví dụ: `Job Title = "Sales Manager"`, `Location = "Hà Nội"`, `Number of Leads = 5`).
   - Kiểm tra **Google Sheets** xem có **leads mới được enrich** không.
   - Chạy **Trigger 2 (Manual Trigger)** để **AI tạo email và gửi**.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, **bật chế độ Active** trong n8n Editor.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM ĐỂ WORKFLOW HỢP LÝ VỚI DOANH NGHIỆP CỦA CÁC SẺP**]
1. **Tối ưu Prompt AI cho Email**:
   - **Cập nhật template email** trong node `AI Cold Email Writer` để phù hợp với **branding** của công ty.
   - Ví dụ:
     ```json
     "prompt": "Tạo một email cold outreach cá nhân hóa cho lead có thông tin sau:\n
     - Job Title: {{Job Title}}\n
     - Company: {{Company}}\n
     - Industry: {{Industry}}\n
     - Email: {{Email}}\n
     Email phải:\n
     1. Giới thiệu công ty của tôi là {{Your Company}} chuyên về {{Your Industry}}.\n
     2. Nêu rõ **1 lợi ích cụ thể** mà lead có thể nhận được từ dịch vụ của tôi.\n
     3. Kết thúc bằng **CTA mạnh mẽ** như: 'Hãy liên hệ với tôi qua email này để chúng ta thảo luận chi tiết!'"
     ```

2. **Lưu Log & Theo Dõi Hiệu Quả**:
   - Thêm **node `stickyNote`** để ghi lại **lịch sử hoạt động** (ví dụ: số leads scrape, số email gửi thành công).
   - Sử dụng **Google Sheets** để **vẽ biểu đồ** theo dõi tỷ lệ mở email.

3. **Kết Hợp Với Slack/Telegram**:
   - Thêm **node `slack`** hoặc `telegram` để **báo cáo kết quả** khi workflow hoàn thành.
   - Ví dụ: `Tự động scrape 10 leads mới từ Apollo! Email đã được tạo và gửi cho 5 lead.`

4. **Thêm Thời Gian Cooldown Tùy Chỉnh**:
   - Nếu **Gmail bị chặn**, tăng thời gian cooldown trong node `Wait — Email Cooldown` (ví dụ: từ 60s → 300s).

5. **Dùng API Key Miễn Phí (Nếu Groq Quá Đắt)**:
   - Thay thế Groq bằng **LLM miễn phí** như **Mistral** hoặc **Gemini** (cần cập nhật node `lmChatGroq`).

6. **Tự Động Xóa Leads Sau Thời Gian**:
   - Thêm **node `code`** để xóa leads có trạng thái `Sent` sau **30 ngày** để giữ sạch Google Sheets.
---

## 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Outreach Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** và **quan hệ khách hàng** thay vì làm thủ công outreach. Với **AI Groq** tạo email cá nhân hóa và **Gmail tự động gửi**, tỷ lệ chuyển đổi sẽ **tăng gấp đôi** so với cách làm thủ công.

### **🔥 Bước Đầu Tiên: Cài Đặt Hệ Thống**
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS** thay vì dùng phiên bản miễn phí (có giới hạn).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).

---
### **🚀 Hành Động Tiếp Theo**
1. **Import workflow** và cấu hình **credentials** theo hướng dẫn.
2. **Test với 5-10 leads** để đảm bảo hoạt động.
3. **Bật Active** và **để workflow chạy tự động** mỗi khi có yêu cầu.
4. **Theo dõi kết quả** trong Google Sheets và **cập nhật prompt AI** để tối ưu hiệu quả.

**💡 Lời Khuyên Cuối Cùng:**
- **Không dùng Gmail cá nhân** để gửi email (dễ bị chặn).
- **Cập nhật API Key** định kỳ để tránh bị Apollo/Groq chặn.
- **Tối ưu prompt AI** để email càng cá nhân hóa càng tốt.

**Bắt đầu tự động hóa outreach của mình ngay hôm nay!** 🚀