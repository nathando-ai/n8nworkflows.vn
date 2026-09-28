---
title: "🚀 Tự Động Hóa Tạo & Phê Duyệt Bài Đăng Social Media Với Google Sheets, Slack & Gemini AI (N8N)"
description: "Workflow hoàn chỉnh tự động hóa quy trình từ nghiên cứu chiến lược đến phê duyệt bài đăng social media với AI Gemini, Google Sheets và Slack - giảm thời gian 80% và đảm bảo nhất quán chất lượng. Phù hợp cho content agency, marketing team và doanh nghiệp cần quản lý nội dung chuyên nghiệp."
slug: "tieu-dong-hoa-tao-phieu-duyet-bai-dang-social-media"
tags: [n8n, automation, no-code, ai-automation, google-sheets, slack-integration, gemini-ai]
keywords: [n8n workflow social media, tự động hóa content marketing, gemini ai n8n, quản lý bài đăng social media, workflow phê duyệt nội dung]
---

# 🚀 **Tự Động Hóa Tạo & Phê Duyệt Bài Đăng Social Media Với AI Gemini, Slack & Google Sheets**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Hiện nay, quy trình tạo và phê duyệt bài đăng social media thường gặp phải những vấn đề sau:
- **Tốn thời gian quá lâu**: Từ nghiên cứu chủ đề đến viết nội dung, chỉnh sửa và phê duyệt có thể mất từ 1-3 ngày.
- **Không nhất quán**: Mỗi người có cách viết khác nhau, dẫn đến giọng điệu không đồng nhất.
- **Quá trình phê duyệt rườm rà**: Phải gửi qua email, Slack nhiều lần, mất nhiều thời gian phản hồi.
- **Không theo dõi được lịch sử**: Không biết bài đăng đã qua bao nhiêu vòng chỉnh sửa, ai đã phê duyệt.

**Workflow này giải quyết tất cả đó!** Với sự kết hợp giữa **AI Gemini** (nghiên cứu chiến lược), **Google Sheets** (quản lý dữ liệu), **Slack** (phê duyệt thực thời) và **n8n**, các sếp có thể:
✅ **Tạo bài đăng trong 10 phút** thay vì 1-3 ngày
✅ **Phê duyệt chỉ bằng 1 cú click** trên Slack
✅ **Theo dõi toàn bộ lịch sử chỉnh sửa** trong Google Sheets
✅ **Đảm bảo nhất quán giọng điệu** nhờ AI
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian từ nghiên cứu đến phê duyệt.
- **Chất lượng cao nhất**: AI Gemini nghiên cứu xu hướng, đề xuất góc nhìn sáng tạo.
- **Phê duyệt nhanh chóng**: Thay vì email, chỉ cần **click vào Slack** để phê duyệt hoặc yêu cầu chỉnh sửa.
- **Quản lý dễ dàng**: Tất cả dữ liệu được lưu trữ trong **Google Sheets** với lịch sử chi tiết.
- **Hoạt động tự động**: Không cần can thiệp thủ công, hoạt động liên tục 24/7.
- **Cá nhân hóa**: Mỗi bài đăng được tối ưu cho từng platform (Facebook, Instagram, LinkedIn...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (đã cài đặt **Google Sheets OAuth2** trong n8n).
2. **Tài khoản Slack** (đã cài đặt **Slack API** với scope `chat:write`).
3. **Tài khoản Gmail** (nếu cần gửi email cho IT khi có khách hàng mới).
4. **API Key Google Gemini** (để sử dụng AI Gemini trong workflow).
5. **API Key Anthropic** (nếu muốn sử dụng Claude AI làm lựa chọn thay thế).
6. **Tài khoản Flux/Recraft** (để tạo hình ảnh tự động, nếu cần).
7. **Google Drive** (để tải xuống **template Google Sheets** đã chuẩn bị).

👉 **Lưu ý quan trọng**:
- **Không cần biết code** - workflow hoàn toàn **no-code**.
- **Cần VPS để chạy 24/7** (Self-hosted n8n).
  :::info[Gợi ý hạ tầng cho n8n]
  Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
  :::
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **77 nodes** và cấu trúc phức tạp. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/16161](https://n8n.io/workflows/16161) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::warning[LƯU Ý]
- **Không copy/paste trực tiếp từ trang web** (sẽ bị lỗi do format JSON không đúng).
- **Sử dụng tab "Import"** trong n8n Editor để tải file JSON.
:::

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Sau khi import, các sếp phải **cấu hình lại các node quan trọng** như sau:

##### **A. Cấu Hình Google Sheets**
1. **Tải template Google Sheets** từ:
   👉 [Google Drive Templates](https://drive.google.com/drive/folders/1uhw8HB5r3Q4UrkHv63PyxKpH5Fk7mSzq)
2. **Import vào Google Drive** của mình.
3. **Cấu hình OAuth2** trong n8n:
   - Đi đến **Credentials** → **Add New Credential** → **Google Sheets OAuth2**.
   - Chọn **Google Sheets** trong các node cần thiết (ví dụ: `DB - Log Brief`, `Get Post Angles`, `DB - Log Approved`...).
   - **Chọn sheet đúng** trong mỗi node (ví dụ: `Brief Log`, `Post Angles`, `Approved Posts`...).

##### **B. Cấu Hình Slack**
1. **Tạo Slack App** và cấp quyền:
   - Đi đến [Slack API](https://api.slack.com/apps) → Tạo một **new app**.
   - Cấp quyền **`chat:write`** và **`commands`**.
   - Invite app vào **channel** cần sử dụng (ví dụ: `#social-media`).
2. **Cấu hình Slack API trong n8n**:
   - Đi đến **Credentials** → **Add New Credential** → **Slack API**.
   - Nhập **Token** và **Channel ID** (lấy từ Slack App).
   - **Cấu hình tất cả node Slack** (ví dụ: `IT Mssg`, `Approved Mssg`, `Post Angles new`...) với **Channel ID** tương ứng.
3. **Tạo bookmark "CREATE NEW BRIEF"** trong Slack:
   - Đi đến **Slack** → **Bookmarks** → Tạo một bookmark mới.
   - Gán link đến **Brief Intake Form** (node `Brief Intake Form` trong workflow).

##### **C. Cấu Hình AI (Google Gemini & Anthropic)**
1. **Google Gemini**:
   - Đi đến **Credentials** → **Add New Credential** → **Google Palm API**.
   - Nhập **API Key** từ [Google AI Studio](https://makersuite.google.com/).
   - Cấu hình node `Google Gemini Chat Model` và `Google Gemini Chat Model2`.
2. **Anthropic (Claude AI - lựa chọn thay thế)**:
   - Đi đến **Credentials** → **Add New Credential** → **Anthropic API**.
   - Nhập **API Key** từ [Anthropic](https://www.anthropic.com/).
   - Cấu hình node `Anthropic Chat Model` (nếu muốn sử dụng).

##### **D. Cấu Hình Webhook**
Workflow này sử dụng **webhook** để truyền dữ liệu giữa các giai đoạn:
1. **Lấy URL webhook** từ node:
   - `Marcus Webhook` → Copy **URL** (ví dụ: `https://your-n8n-url/webhook/Marcus`).
   - `Taylor Webhook` → Copy **URL** (ví dụ: `https://your-n8n-url/webhook/Taylor`).
   - `Taylor-Marcus Revise` → Copy **URL** (ví dụ: `https://your-n8n-url/webhook/marcus-revise`).
2. **Cấu hình lại node `To Marcus` và `To Taylor`**:
   - Đi đến node `To Marcus` → Thay đổi **URL** thành URL webhook của `Marcus Webhook`.
   - Đi đến node `To Taylor` → Thay đổi **URL** thành URL webhook của `Taylor Webhook`.
   - Đi đến node `Taylor-Marcus Revise` → Thay đổi **URL** thành URL webhook của `Taylor-Marcus Revise`.

##### **E. Cấu Hình Flux/Recraft (nếu cần tạo hình ảnh)**
1. **Đăng ký tài khoản Flux/Recraft** (mô hình miễn phí hoặc trả phí).
2. **Cấu hình node `Flux`**:
   - Đi đến node `Flux` → Thay đổi **URL API** và **API Key** theo hướng dẫn của Flux.
   - **Lưu ý**: Nếu không cần tạo hình ảnh, có thể **xóa node này** và các node liên quan.

##### **F. Cấu Hình Email (nếu có khách hàng mới)**
1. **Cấu hình Gmail OAuth2**:
   - Đi đến **Credentials** → **Add New Credential** → **Gmail OAuth2**.
   - Chọn **Gmail** trong node `Email to IT - New Client`.
   - **Cấu hình email mẫu** trong node này (chủ đề, nội dung, người nhận).

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Execute Workflow** và chọn **Manual Trigger** (`When clicking ‘Execute workflow’`).
   - Điền thông tin vào **Brief Intake Form** (node `Brief Intake Form`).
   - Theo dõi quá trình trên **Slack** và **Google Sheets**.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với các tool khác**:
   - **Canva API** để tự động tạo banner từ text.
   - **Buffer/Hootsuite API** để lên lịch bài đăng.
   - **Google Analytics** để theo dõi hiệu suất bài đăng.

2. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node `Set` + `Google Sheets`** để tạo báo cáo tuần/month về số lượng bài đăng, lượt phê duyệt, thời gian xử lý.

3. **Cá nhân hóa thông báo Slack**:
   - Thay vì thông báo chung, **tạo các channel riêng** cho mỗi người phê duyệt (Sofia, Marcus, Taylor) và gửi thông báo riêng.

4. **Lưu log chi tiết**:
   - Sử dụng **node `StickyNote`** để ghi chú thêm vào Google Sheets khi có yêu cầu chỉnh sửa đặc biệt.

5. **Tích hợp với CRM**:
   - Nếu sử dụng **HubSpot, Salesforce**, có thể lấy thông tin khách hàng tự động vào form intake.

6. **Sử dụng AI để tối ưu nội dung**:
   - Sau khi phê duyệt, **AI có thể tự động đề xuất hashtag, keyword** phù hợp cho từng platform.

7. **Tự động chuyển đổi bài đăng sang nhiều ngôn ngữ**:
   - Sử dụng **Google Translate API** để tạo phiên bản đa ngôn ngữ.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa toàn bộ quy trình từ **nghiên cứu chiến lược** đến **phê duyệt và đăng bài** trên social media. Với sự hỗ trợ của **AI Gemini, Google Sheets và Slack**, các sếp không chỉ tiết kiệm **thời gian và công sức** mà còn **đảm bảo chất lượng cao nhất** cho nội dung.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** và bắt đầu tự động hóa!

👉 **Xem video demo** của workflow: [https://youtu.be/rJ5n9Nq9CSc](https://youtu.be/rJ5n9Nq9CSc)

---
**Chia sẻ và đánh giá nếu bạn thấy hữu ích!** 🚀