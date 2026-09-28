---
title: "🚀 Tự Động Hóa Yêu Cầu Kết Nối LinkedIn Cá Nhân Hóa AI - Từ Google Sheets Với Gemini (Không Cần Code)"
description: "Workflow tự động hóa gửi yêu cầu kết nối LinkedIn cá nhân hóa, dựa trên dữ liệu từ Google Sheets và trí tuệ nhân tạo Gemini, giúp các sếp tiết kiệm thời gian và tăng tỷ lệ chấp nhận lên đến 30%. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tu-dong-hoa-yeu-cau-ket-noi-linkedin-ai-google-sheets-gemini"
tags: [n8n, automation, no-code, lead-nurturing, ai-personalized, linkedin-automation, google-sheets, gemini-ai]
keywords: [tự động hóa linkedin, gửi yêu cầu kết nối tự động, gemini ai linkedin, google sheets automation, lead nurturing no-code, connectsafely ai]
---

# 🚀 **Tự Động Hóa Yêu Cầu Kết Nối LinkedIn Cá Nhân Hóa AI - Từ Google Sheets Với Gemini**

### **Giải pháp cho các sếp bán hàng, tuyển dụng và doanh nghiệp muốn chuyển từ "cold outreach" sang chiến lược "inbound engagement" hiệu quả**

Hãy tưởng tượng một hệ thống **tự động hóa hoàn toàn** gửi yêu cầu kết nối LinkedIn **cá nhân hóa 100%**, dựa trên thông tin chi tiết của từng người dùng, mà không cần viết một dòng code nào. Thay vì gửi hàng trăm tin nhắn chung chung, các sếp có thể **tăng tỷ lệ phản hồi lên đến 30%** bằng cách kết hợp:
✅ **Dữ liệu từ Google Sheets** (danh sách tiềm năng, trạng thái, thông tin liên hệ)
✅ **Trí tuệ nhân tạo Gemini** (tạo nội dung cá nhân hóa dựa trên hồ sơ LinkedIn)
✅ **API ConnectSafely.AI** (trích xuất thông tin chi tiết từ LinkedIn)
✅ **Tự động hóa 24/7** (không cần can thiệp thủ công)

Workflow này **không chỉ tiết kiệm thời gian mà còn giúp xây dựng mối quan hệ chân thực**, thay vì gửi tin nhắn "cold" không hiệu quả.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** so với việc gửi yêu cầu thủ công.
- **Tỷ lệ chấp nhận tăng 20-30%** nhờ nội dung cá nhân hóa.
- **Hoạt động liên tục 24/7** mà không cần can thiệp.
- **Dữ liệu theo dõi rõ ràng** trên Google Sheets (trạng thái, tin nhắn đã gửi).
- **Không cần kỹ năng code** – chỉ cần cấu hình các node trong n8n.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ConnectSafely.AI** (để trích xuất dữ liệu LinkedIn):
   - [Đăng ký miễn phí tại đây](https://connectsafely.ai) và lấy **API Key**.
   - Tham số `Bearer YOUR_TOKEN_HERE` sẽ được sử dụng trong node `Fetch LinkedIn Profile`.

2. **Google Sheets** với các cột bắt buộc:
   | Cột Tên          | Mô tả                                  |
   |-------------------|----------------------------------------|
   | `First Name`      | Tên của tiềm năng                     |
   | `LinkedIn Url`    | Link hồ sơ LinkedIn (vd: `linkedin.com/in/nguyenvana`) |
   | `Tagline`         | Mô tả ngắn gọn trong hồ sơ (nếu có)   |
   | `Status`          | Trạng thái: `PENDING` (chờ xử lý), `IN PROGRESS`, `DONE` |
   | `Message`         | Tin nhắn đã gửi (nếu có)              |

3. **Google Gemini API Key**:
   - [Đăng ký tại Google AI Studio](https://makersuite.google.com/app/apikey) và lấy `API Key` để kết nối với node `Google Gemini`.

4. **Credentials trong n8n**:
   - **Google Sheets OAuth2**: Cấu hình trong `n8n Credentials` để đọc/giữi tin.
   - **HTTP Bearer Auth**: Điền `Bearer YOUR_CONNECTSAFELY_API_KEY` cho node `Fetch LinkedIn Profile`.
   - **Google Gemini API Key**: Điền vào node `Google Gemini`.

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [n8n.io/workflows/11420](https://n8n.io/workflows/11420) (chọn "Export as JSON").
2. Trong **n8n Dashboard**, chọn **"Import"** và dán JSON vào.
   *Hoặc*:
   - Mở **n8n Editor**, chọn **"Create Workflow from JSON"** và dán nội dung.

:::note[LƯU Ý]
- **Không sao chép toàn bộ JSON** từ trang n8n.io (do có thể có phần metadata không cần thiết). Chỉ sao chép phần `nodes` và `connections`.
- Nếu import từ file, **xác nhận lại cấu trúc** các node sau import.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Credentials**
Các node quan trọng cần cấu hình kỹ lưỡng:

| **Node**                     | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Get Pending Prospect**      | Chọn **Google Sheets OAuth2** đã cấu hình trước.                                   | -                                             |
| **Mark as In Progress**      | Cùng sheet và credentials với node trên.                                           | -                                             |
| **Fetch LinkedIn Profile**   | Chọn **HTTP Bearer Auth** và điền `Bearer YOUR_CONNECTSAFELY_API_KEY`.              | `URL`: `https://api.connectsafely.ai/v1/profile/{linkedin_url}` |
| **Google Gemini**             | Điền **API Key** từ Google AI Studio.                                             | `API Key`: `YOUR_GOOGLE_GEMINI_API_KEY`       |
| **Send Connection Request**  | Tham số `URL` sẽ tự động xây dựng từ API ConnectSafely.AI (không cần chỉnh).     | -                                             |
| **Mark as Complete**         | Cùng sheet và credentials với node `Get Pending Prospect`.                          | -                                             |

#### **B. Cấu hình Google Sheets**
1. **Chọn Sheet và Range**:
   - Trong node `Get Pending Prospect` và `Mark as In Progress/Complete`, chọn:
     - **Sheet Name**: Tên của file Google Sheets.
     - **Range**: `Sheet1!A1:E1000` (đảm bảo bao gồm tất cả cột và dữ liệu).
   - **Filter**: Thêm điều kiện `Status = "PENDING"` để chỉ lấy dữ liệu chờ xử lý.

2. **Cấu hình cột `Status`**:
   - Workflow sẽ tự động cập nhật trạng thái từ `PENDING` → `IN PROGRESS` → `DONE`.
   - **Không chỉnh sửa cột này thủ công** để tránh xung đột.

#### **C. Cấu hình AI Prompt (Node `Generate Personalized Message`)**
Node này sử dụng **Agent + Gemini** để tạo tin nhắn cá nhân hóa. Các sếp cần chỉnh sửa **system prompt** để phù hợp với phong cách cá nhân:
```json
{
  "systemMessage": "Bạn là một chuyên gia bán hàng LinkedIn. Tạo một tin nhắn kết nối cá nhân hóa, ngắn gọn (5-7 câu) dựa trên thông tin sau:
  - Tên: {{First Name}}
  - LinkedIn URL: {{LinkedIn Url}}
  - Tagline: {{Tagline}}
  Tin nhắn phải:
  1. Chào tên họ (vd: 'Chào [Tên],').
  2. Nêu 1 điểm chung (vd: 'Tôi thấy bạn đang làm việc tại [Công ty], một startup rất hot trong lĩnh vực [ngành]!').
  3. Giới thiệu ngắn về mình và mục đích kết nối (vd: 'Tôi là [Tên], chuyên giúp doanh nghiệp [giải pháp]...').
  4. Kêu gọi hành động mềm dẻo (vd: 'Tôi rất thích những gì bạn chia sẻ về [chủ đề]. Có thể chia sẻ thêm về kinh nghiệm của bạn không?').
  5. Kết thúc bằng lời mời kết nối và lời cảm ơn.
  Đừng sử dụng template chung chung!"
}
```
:::tip[Mẹo nâng cao]
- Thêm **thông tin cá nhân** của các sếp (vd: công ty, sản phẩm, giá trị cốt lõi) vào prompt để tăng tính chân thực.
- Nếu muốn **tăng độ dài tin nhắn**, điều chỉnh tham số `temperature` trong node `Google Gemini` (giá trị từ 0.1 đến 1.0).
:::

#### **D. Cấu hình Schedule Trigger**
- Node `Run Every Minute` sẽ chạy workflow mỗi phút.
- **Không cần chỉnh** nếu muốn chạy liên tục. Nếu muốn chạy ít hơn (vd: 1 lần/h), chỉnh `cron` thành `0 * * * *` (mỗi giờ).

#### **E. Cấu hình Random Delay (1-5 min)**
Node `Random Delay` giúp workflow **trông tự nhiên hơn** khi gửi yêu cầu. Các sếp có thể:
- **Giữ mặc định** (1-5 phút) để tránh bị LinkedIn flag là bot.
- **Chỉnh thời gian** trong node `wait` (vd: `min: 2`, `max: 10`).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với 1 dữ liệu mẫu:
   - Chọn node `Manual Trigger` và nhấn **"Execute Workflow"**.
   - Kiểm tra:
     - Dữ liệu từ Google Sheets có được lấy đúng không?
     - Tin nhắn AI có hợp lý không?
     - Yêu cầu kết nối có được gửi thành công không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.
   - Kiểm tra **Google Sheets** để xác nhận trạng thái `Status` được cập nhật từ `PENDING` → `DONE`.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Slack/Telegram để báo cáo**
Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để:
- **Báo cáo thành công/thất bại** mỗi khi gửi yêu cầu.
- **Gửi tin nhắn mẫu** đã tạo cho các sếp review trước khi gửi.

**Cách làm**:
1. Thêm node `Slack` sau node `Send Connection Request`.
2. Cấu hình:
   - **Webhook URL**: Lấy từ Slack App (cài đặt tại [api.slack.com/apps](https://api.slack.com/apps)).
   - **Message**: `📩 Yêu cầu kết nối đã gửi cho [First Name]! Tin nhắn: {{Message}}`.

### **2. Lưu log hoạt động vào Google Sheets**
Thêm cột mới trong Google Sheets như:
- `Sent At` (thời gian gửi)
- `Response` (phản hồi từ LinkedIn, nếu có)
- `Status Code` (mã trạng thái API)

### **3. Tăng tỷ lệ thành công với AI**
- **Đào sâu dữ liệu LinkedIn**: Sử dụng node `Fetch LinkedIn Profile` để lấy thêm thông tin (vd: ngành nghề, kinh nghiệm) và thêm vào prompt.
- **A/B Testing**: Tạo 2 phiên bản prompt khác nhau và so sánh tỷ lệ chấp nhận.
- **Sử dụng LangChain Agent**: Nếu muốn nâng cao tính logic của AI, các sếp có thể tùy chỉnh **tool use** trong node `agent`.

### **4. Xử lý lỗi tự động**
Thêm node `n8n-nodes-base.if` để:
- **Nếu `Status Code` = 429 (Too Many Requests)**, chờ 5 phút trước khi retry.
- **Nếu `LinkedIn Url` không hợp lệ**, chuyển trạng thái thành `ERROR` và thông báo qua Slack.

---
## 📌 **Kết luận**
Workflow này **không chỉ tự động hóa gửi yêu cầu kết nối LinkedIn mà còn biến nó thành một hệ thống "inbound lead generation" hiệu quả**, giúp các sếp:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược.
✔ **Tăng tỷ lệ phản hồi** nhờ nội dung cá nhân hóa.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay**:
1. **Chuẩn bị dữ liệu** trên Google Sheets và API keys.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và phản hồi**: Các sếp có thể comment bên dưới hoặc liên hệ với tác giả [ConnectSafely](https://connectsafely.ai) để cải tiến workflow! 🚀