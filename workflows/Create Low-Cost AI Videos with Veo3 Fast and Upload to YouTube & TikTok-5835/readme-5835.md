---
title: "🎥 Tự Động Hóa Sáng Tạo Video AI Rẻ Tiền với Veo3 Fast + Upload YouTube & TikTok (Không Code)"
description: "Workflow tự động hóa hoàn toàn miễn phí giúp các sếp tạo video AI chất lượng cao với chi phí thấp bằng Veo3 Fast, tự động upload lên YouTube và TikTok, đồng thời tự động sinh tiêu đề SEO bằng GPT-4o. Giảm thời gian sản xuất video từ 6h xuống 5 phút!"
slug: "tieu-tao-video-ai-veo3-fast-upload-youtube-tiktok"
tags: [n8n, automation, content-creation, ai-video, youtube-automation, tiktok-automation, google-sheets, openai, multimodal-ai]
keywords: [tự động hóa video AI, Veo3 Fast, upload YouTube tự động, TikTok automation, tạo video AI rẻ tiền, GPT-4o tự động sinh tiêu đề, n8n workflow video]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video AI Rẻ Tiền với Veo3 Fast + Upload YouTube & TikTok (Không Code)**

## **🔥 Nỗi Đau Của Các Sếp Trong Sáng Tạo Video AI**
Hiện nay, việc tạo video AI chất lượng cao thường đòi hỏi:
✅ **Chi phí cao** (mô hình AI đắt tiền như Sora, Pika Labs)
✅ **Thời gian lâu** (từ 30 phút đến 6 giờ để chờ AI sinh video)
✅ **Khó quản lý** (phải theo dõi từng bước thủ công trên nhiều nền tảng)
✅ **Không tự động hóa** (upload YouTube/TikTok phải làm thủ công)

**Workflow này giải quyết tất cả!** Sử dụng **Veo3 Fast** (mô hình AI video rẻ tiền của Google) kết hợp với **GPT-4o** để tự động:
✔ **Tạo video AI chất lượng** trong 5 phút (thay vì 6 giờ)
✔ **Upload tự động lên YouTube & TikTok**
✔ **Sinh tiêu đề SEO tối ưu** bằng AI
✔ **Quản lý toàn bộ trên Google Sheets** (không cần code)

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 90% thời gian**: Từ 6 giờ tạo video thủ công xuống **5 phút tự động hóa**.
- **Chi phí thấp hơn 80%**: Sử dụng mô hình **Veo3 Fast** (rẻ hơn Sora/Pika Labs gấp 10 lần).
- **Tự động hóa hoàn toàn**: Video được tạo → upload YouTube/TikTok → sinh tiêu đề SEO **một lần nhấn nút**.
- **Quản lý trung tâm**: Tất cả dữ liệu video được lưu trên **Google Sheets**, dễ theo dõi và mở rộng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets, Google Drive, YouTube).
2. **API Key Veo3 Fast** (từ [Fal.ai](https://fal.ai/)) – **Miễn phí** (dùng mô hình `google/veo3-fast`).
3. **API Key Upload-Post** (để upload YouTube) – **10 upload miễn phí/tháng** ([Đăng ký](https://app.upload-post.com/)).
4. **Tài khoản TikTok** (nếu muốn upload TikTok, cần **upgrade plan**).
5. **Google Sheet mẫu** (sẽ hướng dẫn sau).
6. **N8n Self-hosted** (để workflow chạy 24/7) – 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5835](https://n8n.io/workflows/5835).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/5835](https://n8n.io/workflows/5835).
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán mã.

---

### **2. Cấu Hình Cần Thiết (BẮT BUỘC CHỈNH)**
Workflow gồm **16 node**, nhưng các node quan trọng nhất cần cấu hình như sau:

#### **📌 Node 1: Google Sheets (Mẫu)**
- **Tạo Google Sheet theo mẫu** ([Download mẫu](https://docs.google.com/spreadsheets/d/1pcoY9N_vQp44NtSRR5eskkL5Qd0N0BGq7Jh_4m-7VEQ/edit?usp=sharing)).
- **Cột cần điền**:
  - **PROMPT**: Mô tả chi tiết video (ví dụ: *"Video giới thiệu sản phẩm iPhone 15 Pro Max"*).
  - **DURATION**: Thời lượng video (ví dụ: `30` giây).
  - **VIDEO**: **Không điền** (sẽ tự động điền sau khi video tạo xong).
  - **TITLE**: **Không điền** (sẽ tự động sinh tiêu đề SEO bằng GPT-4o).
  - **YOUTUBE_URL**: **Không điền** (sẽ tự động điền sau khi upload YouTube).

- **Cấu hình node "Get new video"**:
  - **Credentials**: Chọn **Google Sheets** đã tạo.
  - **Sheet Name**: `Video Prompts`.
  - **Range**: `Sheet1!A:D` (để lấy dữ liệu từ cột PROMPT, DURATION, VIDEO, TITLE).

#### **📌 Node 2: API Key Veo3 Fast (Fal.ai)**
- **Tạo tài khoản** tại [Fal.ai](https://fal.ai/) và lấy **API Key**.
- **Cấu hình node "Create Video"**:
  - **Method**: `POST`.
  - **URL**: `https://api.fal.ai/generations/veo3-fast`.
  - **Headers**:
    - `Authorization`: `Key YOUR_API_KEY_HERE` (điền API Key từ Fal.ai).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "prompt": "{{$node["Get new video"].json["PROMPT"]}}",
      "duration": "{{$node["Get new video"].json["DURATION"]}}"
    }
    ```

#### **📌 Node 3: Tải Video từ Veo3 Fast**
- **Cấu hình node "Get Url Video"**:
  - **Method**: `GET`.
  - **URL**: `{{$node["Create Video"].json["result"]["url"]}}` (lấy URL video từ response của Veo3).
  - **Headers**: Không cần thiết (nếu là GET).

- **Cấu hình node "Get File Video"**:
  - **Method**: `GET`.
  - **URL**: `{{$node["Get Url Video"].json["url"]}}` (lấy file video từ URL).
  - **Response Type**: `Buffer` (để lưu video dưới dạng file).

#### **📌 Node 4: Upload Video lên Google Drive**
- **Cấu hình node "Upload Video"**:
  - **Credentials**: Chọn **Google Drive** đã kết nối.
  - **File**: `{{$node["Get File Video"].json["body"]}}` (file video từ Veo3).
  - **Folder**: Chọn **Folder** muốn lưu video (ví dụ: `Video AI`).
  - **File Name**: `{{$node["Get new video"].json["PROMPT"]}}.mp4` (tên file tự động sinh từ PROMPT).

#### **📌 Node 5: Sinh Tiêu Đề SEO bằng GPT-4o**
- **Cấu hình node "Generate title"**:
  - **Credentials**: Chọn **OpenAI** (đã kết nối API Key).
  - **Model**: `gpt-4o` (hoặc `gpt-4` nếu không có).
  - **Prompt**:
    ```
    Tạo tiêu đề YouTube SEO cho video AI về "{{$node["Get new video"].json["PROMPT"]}}".
    Tiêu đề phải:
    1. Đặc biệt và hấp dẫn (sử dụng từ khóa hot).
    2. Có từ khóa chính: "{{$node["Get new video"].json["PROMPT"].split(' ')[0]}}".
    3. Dài khoảng 50-70 ký tự.
    4. Không có spam hoặc từ ngữ quá khích.
    ```
  - **Max Tokens**: `100`.

#### **📌 Node 6: Upload Video lên YouTube (Upload-Post)**
- **Cấu hình node "HTTP Request" (Upload YouTube)**:
  - **Method**: `POST`.
  - **URL**: `https://api.upload-post.com/v1/upload`.
  - **Headers**:
    - `Authorization`: `Apikey YOUR_UPLOAD_POST_API_KEY` (điền API Key từ [Upload-Post](https://app.upload-post.com/)).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "url": "{{$node["Get Url Video"].json["url"]}}",
      "title": "{{$node["Generate title"].json["choices"][0].message.content}}",
      "description": "Video AI tự động tạo bởi n8n + Veo3 Fast. Chi tiết: {{$node["Get new video"].json["PROMPT"]}}",
      "tags": ["AI", "Video", "{{$node["Get new video"].json["PROMPT"].split(' ')[0]}}"],
      "category": "People & Blogs"
    }
    ```

#### **📌 Node 7: Upload Video lên TikTok (Nếu Có Plan Paid)**
- **Cấu hình node "Upload on TikTok"**:
  - **Method**: `POST`.
  - **URL**: `https://api.tiktok.com/oauth2/v2/access_token` (nếu cần OAuth) hoặc API TikTok Business API (nếu có).
  - **Lưu ý**: **Phiên bản miễn phí không hỗ trợ TikTok**, cần **upgrade plan** để upload TikTok.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Test Workflow"** và điền vào Google Sheets:
     - **PROMPT**: *"Video giới thiệu sản phẩm iPhone 15 Pro Max"*
     - **DURATION**: `30`
   - Kiểm tra từng node để đảm bảo không có lỗi.

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động.

3. **Cấu Hình Schedule Trigger**:
   - **Node "Schedule Trigger"**: Đặt lịch chạy **tối đa 5 phút/lần** (để tránh bị giới hạn API).
   - **Lịch chạy**: Ví dụ: `0 0 * * *` (chạy hàng ngày lúc 00:00).

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM ĐẸP HƠN**]
1. **Tự động sinh thumbnail**:
   - Sử dụng **node OpenAI** để sinh thumbnail từ PROMPT, sau đó upload lên Google Drive.

2. **Gửi thông báo Slack/Telegram khi video hoàn thành**:
   - Thêm **node "HTTP Request"** để gửi thông báo khi video upload xong.

3. **Lưu log hoạt động**:
   - Sử dụng **node "Sticky Note"** để ghi lại lịch sử video đã tạo.

4. **Tạo báo cáo định kỳ**:
   - Sử dụng **node "Google Sheets"** để cập nhật thống kê video đã tạo (số lượng, lượt view, engagement).

5. **Kết hợp với YouTube Studio API**:
   - Tự động cập nhật metadata (mô tả, tags) cho video mới.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy content** thay vì làm thủ công. Với chi phí thấp và hiệu suất cao, **Veo3 Fast + n8n** là giải pháp **tự động hóa video AI hoàn hảo** cho các doanh nghiệp và creator.

**🚀 Hành động ngay!**
1. **Đăng ký VPS TinoHost** để self-host n8n: [👉 Đăng ký với mã giảm giá VPSN8N](https://tino.vn/vps-n8n?affid=388).
2. **Import workflow** và bắt đầu tạo video AI tự động.
3. **Chia sẻ kết quả** với bạn bè để cùng tự động hóa!

---
**💡 Lưu ý cuối cùng**:
- **Veo3 Fast có giới hạn free tier**, các sếp nên theo dõi tài khoản để không bị ngừng dịch vụ.
- **Upload-Post miễn phí chỉ cho 10 video/tháng**, nên lên kế hoạch upload.
- **Nếu muốn upload TikTok**, cần **upgrade plan** (từ ~$10/tháng).

**Hãy tự động hóa ngay hôm nay!** 🚀