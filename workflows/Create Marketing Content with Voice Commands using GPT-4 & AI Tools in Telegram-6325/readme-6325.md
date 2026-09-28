---
title: "🎙️ Tự Động Hóa Tạo Nội Dung Marketing Bằng Lệnh Nói (GPT-4 + AI) Trên Telegram - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn giúp các sếp tạo nội dung marketing (bài viết, bài post LinkedIn, hình ảnh, video) chỉ bằng giọng nói qua Telegram, tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-tao-noi-dung-marketing-bang-lenh-noi"
tags: [n8n, automation, content-creation, ai, telegram, gpt-4, no-code]
keywords: [n8n workflow content marketing, tự động hóa tạo nội dung bằng giọng nói, GPT-4 Telegram, tạo bài viết blog tự động, tạo hình ảnh video AI]
---

# 🚀 **Tạo Nội Dung Marketing Chỉ Bằng Lệnh Nói - Cứu Các Sếp Ra Khỏi "Blocker" Tạo Content**

Các sếp đã từng cảm thấy như thế này chưa?
- **"Tôi có ý tưởng nhưng không biết viết ra sao?"**
- **"Tạo hình ảnh/video đẹp mất quá nhiều thời gian?"**
- **"Cần bài viết blog nhưng lại không có thời gian nghiên cứu?"**
- **"Tôi muốn nội dung cá nhân hóa nhưng không đủ nguồn lực?"**

Workflow này **giải quyết tất cả** bằng cách kết hợp **GPT-4, AI Multimodal và Telegram** để các sếp chỉ cần **nói yêu cầu** là hệ thống tự động:
✅ **Viết bài viết blog** (cấu trúc hoàn chỉnh, SEO-friendly)
✅ **Tạo bài post LinkedIn** (cá nhân hóa, thu hút)
✅ **Sinh hình ảnh/ảnh thô** (phù hợp với nội dung)
✅ **Chỉnh sửa hình ảnh** (tối ưu hóa cho mạng xã hội)
✅ **Tạo video ngắn** (dùng AI voice + video generation)
✅ **Gửi kết quả về Telegram** (cập nhật liên tục)

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công (không cần viết, chỉnh sửa, tìm hình).
- **Nội dung chuyên nghiệp** (cấu trúc rõ ràng, SEO-optimized, phù hợp với brand voice).
- **Cá nhân hóa hoàn toàn** (AI hiểu yêu cầu cụ thể của sếp qua giọng nói).
- **Hoạt động 24/7** (không cần can thiệp, chỉ cần kích hoạt workflow).
- **Kết hợp nhiều format** (text, image, video) từ một lệnh duy nhất.
- **Lưu lịch sử** (gắn kết với Google Sheets để theo dõi tất cả nội dung tạo ra).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ/API          | Mô Tả                                                                 | Link Đăng Ký                                                                 |
|----------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Telegram Bot**     | Bot để nhận lệnh giọng nói và gửi kết quả.                           | [@BotFather](https://t.me/BotFather) (tạo bot và lấy `API Token`)          |
| **OpenRouter**       | API để gọi GPT-4 (thay thế OpenAI).                                    | [openrouter.ai](https://openrouter.ai/) (mã giảm giá: **OPENROUTER10** - 10%) |
| **Tavily**           | AI search để hỗ trợ nghiên cứu cho bài viết.                           | [tavily.com](https://tavily.com/) (mã giảm giá: **TAVILYN8N** - 15%)        |
| **PiAPI**            | API tạo video từ text (nếu muốn tạo video).                           | [piapi.ai](https://piapi.ai/) (mã giảm giá: **PIAPIN8N** - 20%)            |
| **Runway**           | API xử lý video (nếu muốn chỉnh sửa video).                          | [runwayml.com](https://runwayml.com/)                                       |
| **ElevenLabs**       | API tạo giọng nói AI cho video.                                       | [elevenlabs.io](https://elevenlabs.io/) (mã giảm giá: **ELEVENN8N** - 12%)  |

### **2. Workflow Con Lẻ (Cần Import Đầu)**
Các sếp phải **import 6 workflow con** này trước:
1. **Video** (tạo video từ text)
2. **LinkedIn Post** (tạo bài post LinkedIn)
3. **Blog Post** (tạo bài viết blog)
4. **Create Image** (sinh hình ảnh từ text)
5. **Edit Image** (chỉnh sửa hình ảnh)
6. **Search Images** (tìm kiếm hình ảnh phù hợp)

👉 **Lấy file JSON** từ [n8n.io/workflows/6325](https://n8n.io/workflows/6325) và import vào n8n Editor.

### **3. Template Cần Download**
| Template               | Mô Tả                                                                 | Link                                                                       |
|------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Creatomate Image**   | Mẫu hình ảnh chuẩn cho marketing (tải từ Free Skool Community).         | [Tải tại đây](https://creatomate.com/) (tìm kiếm "Free Skool Community") |
| **Google Sheets Log**  | Bảng theo dõi tất cả nội dung tạo ra (cần kết nối với n8n).           | [Mở file](https://docs.google.com/spreadsheets/d/1wQxM9cAwewCigPH22KDidMu_i9j_dx4MHEa5rmJiw5I/edit?usp=sharing) |

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
:::note[BƯỚC CHUẨN BỊ]
- Các sếp cần **n8n Self-hosted** (không dùng phiên bản cloud) để workflow hoạt động 24/7.
- **Cài đặt n8n trên VPS** (khuyến nghị dùng VPS TinoHost hoặc Xeon 4GB):
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

#### **Hướng Dẫn Import**
1. **Tải file JSON** của workflow chính từ [n8n.io/workflows/6325](https://n8n.io/workflows/6325).
2. **Import vào n8n Editor**:
   - Mở n8n Editor → **Import Workflow** → Chọn file JSON.
   - **Không chỉnh sửa workflow chính**, chỉ import workflow con (6 workflow trên).
3. **Kết nối workflow con**:
   - Mở từng workflow con (Video, LinkedIn Post, Blog Post,...) → **Settings** → **Workflow** → Chọn **Import Workflow** → Chọn file JSON tương ứng.
   - **Liên kết các node** trong workflow chính với workflow con bằng cách:
     - Đặt tên node trong workflow chính **khớp với tên workflow con** (ví dụ: node `Video` trong workflow chính phải liên kết với workflow `Video` đã import).
     - Sử dụng **`toolWorkflow`** node để gọi workflow con.

#### **Cách Kết Nối Workflow Con**
- Trong workflow chính, tìm node có tên **`Video`**, **`LinkedIn Post`**, **`Blog Post`**,... → Nhấp **Settings** → **Workflow** → Chọn workflow con tương ứng.
- **Lưu ý**: Các workflow con **không tự động liên kết**, các sếp phải **thiết lập manual** bằng cách:
  - Mở workflow con → Tìm node đầu tiên (ví dụ: node `Set` trong workflow `Blog Post`) → **Settings** → **Workflow** → Chọn workflow chính.
  - **Cấu hình `Execution`** để workflow con chạy khi được gọi từ workflow chính.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Credentials**
| Node               | Credential Cần Thiết       | Hướng Dẫn Cấu Hình                                                                 |
|--------------------|----------------------------|------------------------------------------------------------------------------------|
| **Telegram**       | `telegramApi`              | Điền `API Token` từ BotFather vào n8n Credentials.                                |
| **OpenRouter**     | `openRouterApi`            | Điền `API Key` từ OpenRouter vào n8n Credentials.                                  |
| **OpenAI (Transcribe)** | `openAiApi`       | Điền `API Key` từ OpenAI (nếu muốn transcribe giọng nói).                         |
| **Tavily**         | `tavilyApi`                | Điền `API Key` từ Tavily vào n8n Credentials.                                      |
| **PiAPI/Runway/ElevenLabs** | API Key tương ứng | Điền vào từng workflow con (Video, Edit Image,...) theo hướng dẫn trên canvas. |

#### **B. Cấu Hình Node Quan Trọng**
1. **Node `Telegram Trigger`**:
   - **Credentials**: Chọn `telegramApi`.
   - **Update**: Bật **`Update`** để workflow phản hồi khi nhận lệnh.
   - **Chat ID**: Điền `chat_id` của bot Telegram (lấy từ `/getUpdates` trong Telegram Bot API).

2. **Node `Download Voice File`**:
   - **Credentials**: Chọn `telegramApi`.
   - **Resource**: Đặt là `file` để tải file âm thanh từ Telegram.

3. **Node `Transcribe Audio`**:
   - **Credentials**: Chọn `openAiApi`.
   - **Operation**: Đặt là `transcribe`.
   - **Resource**: Đặt là `audio` và chọn file âm thanh từ node trước.

4. **Node `Marketing Team Agent`**:
   - **Tools**: Đảm bảo tất cả **toolWorkflow** (Video, Blog Post,...) được liên kết đúng.
   - **Memory**: Kết nối với node `Simple Memory` để lưu lịch sử đối thoại.

5. **Node `Set 'Text'`**:
   - **Expression**: Đặt giá trị mặc định cho text (ví dụ: `"Tạo bài viết blog về marketing AI"`).

6. **Node `Google Sheets` (nếu sử dụng)**:
   - **Credentials**: Thêm `googleSheetsApi` và kết nối với file Google Sheets Log.
   - **Sheet Name**: Đặt là `Content Log` (tên sheet trong file mẫu).

#### **C. Cấu Hình Workflow Con**
- **Video Workflow**:
  - Thêm `PiAPI API Key`, `Runway API Key`, `ElevenLabs API Key` vào **Settings** → **Credentials**.
  - Kiểm tra node `Video` có gọi đúng API không.
- **Blog Post / LinkedIn Post**:
  - Thêm `Tavily API Key` vào **Settings** → **Credentials**.
  - Kiểm tra node `Search Images` có kết nối với Tavily không.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Gửi lệnh giọng nói đến bot Telegram (ví dụ: *"Tạo bài viết blog về tự động hóa n8n"*).
   - Kiểm tra workflow có chạy không bằng cách:
     - Mở **Execution History** trong n8n Editor.
     - Xem log của từng node (đặc biệt là `Marketing Team Agent` và `Telegram`).
2. **Bật Active**:
   - Sau khi test thành công, **bật `Active`** cho workflow chính và workflow con.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM THÊM ĐỂ TĂNG HIỆU QUẢ]
1. **Tích Hợp Slack/Telegram Cập Nhật**:
   - Thêm node `Slack` hoặc `Telegram` sau node `Set 'Text'` để gửi thông báo khi hoàn thành.
   - Ví dụ: *"Bài viết đã tạo xong! Link: [đường dẫn]"*.

2. **Lưu Log Tất Cả Lệnh**:
   - Kết nối node `Google Sheets` sau node `Telegram` để ghi lại tất cả yêu cầu và kết quả.
   - Cấu trúc cột: `Ngày Gửi`, `Lệnh`, `Kết Quả`, `Trạng Thái`, `Link`.

3. **Tạo Menu Lệnh Giọng Nói**:
   - Thêm node `Switch` sau `Transcribe Audio` để phân loại lệnh:
     - Nếu lệnh chứa *"bài viết"* → Gọi workflow `Blog Post`.
     - Nếu lệnh chứa *"hình ảnh"* → Gọi workflow `Create Image`.
     - Nếu lệnh chứa *"video"* → Gọi workflow `Video`.

4. **Cập Nhật API Key Tự Động**:
   - Sử dụng node `Set` để cập nhật API Key nếu hết hạn (ví dụ: OpenRouter).
   - Ví dụ: Tạo một workflow nhỏ để check API Key và tự động refresh.

5. **Tạo Template Cá Nhân Hóa**:
   - Tạo một file `JSON` lưu các template nội dung (ví dụ: bài viết mẫu, post LinkedIn mẫu).
   - Node `Set` có thể đọc file này để khởi tạo text mặc định.

6. **Báo Cáo Định Kỳ**:
   - Sử dụng node `Set` + `Telegram` để gửi báo cáo tuần/month về:
     - Số lượng nội dung tạo ra.
     - Thời gian trung bình tạo 1 nội dung.
     - Top chủ đề phổ biến.

---
## 📌 **Kết Luận: Đừng Chờ Đợi - Tự Động Hóa Ngay!**
Workflow này **không chỉ tiết kiệm thời gian**, mà còn **mang lại chất lượng nội dung chuyên nghiệp** mà các sếp khó có thể đạt được bằng cách làm thủ công. Với **GPT-4 và AI Multimodal**, hệ thống hiểu yêu cầu của sếp một cách sâu sắc và tạo ra nội dung **phù hợp với brand voice**, **SEO-friendly**, và **cá nhân hóa**.

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Đăng ký VPS** (n8n Self-hosted) từ [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).
2. **Import workflow** và cấu hình credentials theo hướng dẫn.
3. **Test với 1 lệnh giọng nói** và xem kết quả!
4. **Tích hợp Google Sheets** để theo dõi tất cả nội dung tạo ra.

**Chỉ cần