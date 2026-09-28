---
title: "🚀 **Tự Động Hóa Pipeline Review Nội Dung Mạng Xã Hội Với Google Gemini & Google Sheets (Human-in-the-Loop)**"
description: "Workflow tự động hóa hoàn chỉnh giúp các nhà marketing và content creator tạo, đánh giá và xuất bản nội dung mạng xã hội chất lượng cao với sự kết hợp giữa AI (Google Gemini) và con người. Giảm thời gian review từ 30 phút/lần xuống còn 5 phút, đồng thời đảm bảo tính nhất quán và phù hợp với brand."
slug: "tieu-dong-hoa-pipeline-review-noi-dung-mang-xa-hoi-google-gemini"
tags: [n8n, automation, content-creation, ai-summarization, google-gemini, google-sheets, human-in-the-loop, social-media]
keywords: [tự động hóa nội dung mạng xã hội, google gemini n8n, review content tự động, pipeline content creation, ai + con người, workflow n8n google sheets]
---

# 🚀 **Tự Động Hóa Pipeline Review Nội Dung Mạng Xã Hội Với Google Gemini & Google Sheets**

## **Giới Thiệu: Giải Pháp Để Nội Dung Mạng Xã Hội Được Tạo Ra Chất Lượng, Nhanh Chóng Và Đúng Brand**
Các sếp đã từng phải mất **30 phút/lần** để review và chỉnh sửa nội dung mạng xã hội? Hay phải lo lắng về việc nội dung không phù hợp với brand, không hấp dẫn người dùng, hoặc không tuân thủ quy tắc của từng nền tảng? **Workflow này sẽ thay đổi tất cả!**

Với **3 AI Agent chuyên biệt (Sofia, Marcus, Taylor)** kết hợp với **con người trong vòng lặp review**, các sếp có thể:
✅ **Tạo 3 góc nhìn nội dung khác nhau** (Sofia) và lựa chọn góc phù hợp nhất.
✅ **Viết bản copy hoàn chỉnh** (Marcus) với hashtag, hướng dẫn thiết kế hình ảnh, và đảm bảo phù hợp với từng nền tảng.
✅ **Đánh giá chất lượng** (Taylor) theo tiêu chí brand alignment, độ dài, và tuân thủ quy tắc nền tảng.
✅ **Xuất bản nội dung** vào Google Sheets với tất cả thông tin chi tiết, sẵn sàng để chia sẻ hoặc xuất bản.

**Kết quả?** Nội dung **chất lượng cao, tiết kiệm thời gian, và không bao giờ bị lỗi brand** – tất cả chỉ với **5 phút review/con người** thay vì 30 phút!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian review**: Giảm từ 30 phút/lần xuống còn **5 phút** với vòng lặp feedback tự động.
- **Nội dung phù hợp brand 100%**: AI (Taylor) kiểm tra brand alignment và tuân thủ quy tắc nền tảng trước khi xuất bản.
- **Feedback hiệu quả**: AI **học từ phản hồi** của con người và tạo ra nội dung cải tiến trong lần tiếp theo.
- **Dễ dàng quản lý nhiều khách hàng**: Thêm khách hàng mới vào Google Sheets là xong – **không cần chỉnh sửa workflow**.
- **Xuất bản tự động**: Nội dung đã được phê duyệt sẽ tự động ghi vào Google Sheets, sẵn sàng để chia sẻ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
#### **1. Google Sheets (2 Tab Cần Thiết)**
- **Tab "Clients"**: Chứa thông tin khách hàng, brand guide, và các quy tắc tone cho từng nền tảng (LinkedIn, X/Twitter, Instagram).
  - Cột cần thiết: `client`, `brand_name`, `brand_guide`, `tone_linkedin`, `tone_x`, `tone_instagram`, `language_avoid`, `visual_style`, `key_messages`.
- **Tab "Approved Posts"**: Lưu trữ nội dung đã được phê duyệt với tất cả thông tin chi tiết.
  - Cột cần thiết: `brief_id`, `client`, `platform`, `content_type`, `approved_angle`, `post_copy`, `hashtags`, `visual_direction`, `sofia_iterations`, `marcus_iterations`, `approved_at`, `status`.

#### **2. API Credentials**
- **Google Sheets OAuth2**: Để workflow có thể đọc và ghi dữ liệu vào Sheets.
- **Google Gemini API**: Để AI (Sofia, Marcus, Taylor) hoạt động.

#### **3. Dữ Liệu Brief Đầu Vào**
- Các trường cần thiết trong **Brief Intake Form**:
  - `Client` (tên khách hàng)
  - `Platform` (LinkedIn, X/Twitter, Instagram)
  - `Content Type` (bài viết, video, story)
  - `Topic Hint` (gợi ý chủ đề)
  - `Tone Note` (tone mong muốn)

---
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/16018](https://n8n.io/workflows/16018).
- **Bước 2**: Vào **n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3**: Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được thiết kế theo **3 giai đoạn review** (Sofia → Marcus → Taylor) với **vòng lặp feedback tự động**. Dưới đây là các node quan trọng cần cấu hình:

##### **🔹 Phase 0: Intake & Config (Lấy Dữ Liệu & Cấu Hình)**
- **Node "Brief Intake Form"**:
  - Cấu hình **form trigger** để nhận dữ liệu từ khách hàng (Client, Platform, Content Type, Topic Hint, Tone Note).
  - **Lưu ý**: Đảm bảo các trường này **khớp với cột trong Google Sheets "Clients"**.

- **Node "Client DB Lookup (Sheets)"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Điền **Sheet Name**: `Clients`.
  - **Key Parameters**:
    - `range`: `Clients!A2:I` (đảm bảo bắt đầu từ dòng 2 để tránh header).
    - `query`: `SELECT * WHERE client = "{{$json['client']}}"` (lấy dữ liệu khách hàng theo tên).

- **Node "Config — Brand + Brief"**:
  - Đây là **node "Set"** để gộp tất cả dữ liệu vào một biến duy nhất.
  - **Lưu ý**: Không cần chỉnh sửa gì, chỉ cần đảm bảo dữ liệu đầu vào đầy đủ.

##### **🔹 Phase 1: Sofia (Strategy) — Tạo 3 Góc Nhìn Nội Dung**
- **Node "Sofia Research Agent"**:
  - Chọn **credentials**: `googlePalmApi` (Google Gemini).
  - **Prompt Template** (được định sẵn trong workflow):
    ```json
    "You are Sofia, a content strategy AI. Generate 3 unique angles for the following brief:
    - Client: {{client}}
    - Platform: {{platform}}
    - Content Type: {{content_type}}
    - Topic Hint: {{topic_hint}}
    - Tone Note: {{tone_note}}
    - Brand Guide: {{brand_guide}}
    - Key Messages: {{key_messages}}
    - Language to Avoid: {{language_avoid}}
    Format each angle as JSON with these fields: title, insight, hook, why_it_fits, platform_fit."
    ```
  - **Lưu ý**: Nếu muốn thay đổi tone của AI, chỉnh sửa **`tone_note`** trong Brief Intake Form.

- **Node "Sofia Route Decision" (Switch)**:
  - Cấu hình **routing** dựa trên phản hồi của con người:
    - **Approved Angle**: Chuyển sang **Marcus (Creative)**.
    - **Revise**: Feedback được gửi lại cho **Sofia** để tạo góc nhìn mới.
    - **Reject**: Dừng workflow (hoặc có thể chuyển sang giai đoạn khác nếu cần).

##### **🔹 Phase 2: Marcus (Creative) — Viết Bản Copy & Hướng Dẫn Thiết Kế**
- **Node "Marcus — Creative Agent"**:
  - Chọn **credentials**: `googlePalmApi`.
  - **Prompt Template**:
    ```json
    "You are Marcus, a social media copywriter. Take the approved angle:
    - Title: {{approved_angle.title}}
    - Insight: {{approved_angle.insight}}
    - Hook: {{approved_angle.hook}}
    And create a full social post for {{platform}} with:
    - Post copy ({{character_limit}} characters)
    - Hashtags (3-5)
    - Visual direction (describe what the image should look like)
    - Composition pattern (e.g., 'Rule of Thirds')
    Follow brand guide: {{brand_guide}} and tone: {{tone_platform}}."
    ```
  - **Lưu ý**: Thay đổi `{{character_limit}}` theo quy tắc của nền tảng (ví dụ: LinkedIn ~1000 ký tự, Instagram ~220 ký tự).

- **Node "Save Post Draft" (Code)**:
  - Đây là **node Code** để **parse** output của Marcus thành JSON.
  - **Lưu ý**: Không cần chỉnh sửa nếu workflow đã được cấu hình đúng.

##### **🔹 Phase 3: Taylor (Quality Review) — Đánh Giá & Xuất Bản**
- **Node "Taylor — Review Agent"**:
  - Chọn **credentials**: `googlePalmApi`.
  - **Prompt Template**:
    ```json
    "You are Taylor, a quality assurance AI. Audit the following post for:
    - Brand alignment (1-5 score)
    - Platform compliance (character count, hashtag rules)
    - Quality flags (list issues)
    Return a structured JSON with:
    - ai_summary
    - character_count
    - quality_flags
    - brand_alignment_score
    - recommendation (APPROVE / REVISE_TO_MARCUS / REJECT_TO_SOFIA)
    - reasoning
    - feedback_for_team
    - final_score (1-10)"
    ```
  - **Lưu ý**: AI sẽ **không xuất bản nội dung** nếu không được phê duyệt.

- **Node "Log Published Post" (Google Sheets)**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: `Approved Posts`.
  - **Key Parameters**:
    - `range`: `Approved Posts!A2:L` (đảm bảo bắt đầu từ dòng 2).
    - `values`: Điền theo cấu trúc:
      ```json
      {
        "brief_id": "{{$json['brief_id']}}",
        "client": "{{$json['client']}}",
        "platform": "{{$json['platform']}}",
        "content_type": "{{$json['content_type']}}",
        "approved_angle": "{{$json['approved_angle']}}",
        "post_copy": "{{$json['post_copy']}}",
        "hashtags": "{{$json['hashtags']}}",
        "visual_direction": "{{$json['visual_direction']}}",
        "sofia_iterations": "{{$json['sofia_iterations']}}",
        "marcus_iterations": "{{$json['marcus_iterations']}}",
        "approved_at": "{{$json['approved_at']}}",
        "status": "APPROVED"
      }
      ```

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu:
  - Điền thông tin vào **Brief Intake Form** (ví dụ: Client = "ABC Corp", Platform = "LinkedIn", Topic Hint = "Tối ưu hóa thời gian làm việc").
  - Chạy workflow và theo dõi **vòng lặp feedback** (Sofia → Marcus → Taylor).
- **Bước 2**: Khi mọi thứ hoạt động ổn định, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hiệu Quả Hơn**]
- **📌 Thêm Slack/Telegram Notifications**:
  - Sử dụng **node Slack/Telegram Webhook** để thông báo khi nội dung được phê duyệt hoặc yêu cầu review.
  - Ví dụ: Khi **Taylor** đưa ra quyết định, gửi tin nhắn: *"Post đã được AI đánh giá. Vui lòng phê duyệt tại [link review]."*

- **📌 Lưu Log Tất Cả Các Vòng Lặp**:
  - Thêm **node Set** sau mỗi vòng lặp feedback để lưu **lịch sử chỉnh sửa** vào Google Sheets.
  - Cột mới trong "Approved Posts": `feedback_history` (lưu JSON của feedback).

- **📌 Tự Động Gửi Báo Cáo Định Kỳ**:
  - Sử dụng **node Schedule Trigger** để mỗi tuần tự động gửi báo cáo:
    - Số lượng nội dung đã xuất bản.
    - Thời gian trung bình review.
    - Thống kê phản hồi từ khách hàng.

- **📌 Kết Hợp Với Canva/Design Tools**:
  - Sau khi **Marcus** tạo **visual direction**, tự động gửi yêu cầu thiết kế đến Canva API hoặc công cụ design khác.

- **📌 Tăng Cường AI với Prompt Engineering**:
  - Nếu muốn AI **tạo nội dung dài hơn**, chỉnh sửa `character_limit` trong prompt của Marcus.
  - Nếu muốn AI **tránh từ khóa nhất định**, thêm vào `language_avoid` trong Google Sheets.
:::

---

### 📌 **Kết Luận: Đừng Bỏ Lỡ Cách Tạo Nội Dung Mạng Xã Hội Chất Lượng Mà Không Cần Code!**
Workflow này không chỉ **giảm thời gian review** mà còn **đảm bảo nội dung luôn phù hợp với brand**, **tuân thủ quy tắc nền tảng**, và **học từ mỗi phản hồi** của con người.

**Các sếp hãy thử ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Google Sheets + API.
3. **Test với dữ liệu mẫu** và bắt đầu tự động hóa!

**🎁 Đăng ký VPS TinoHost với mã giảm giá VPSN8N (giảm tới 39%)** để lưu trữ workflow ổn định:
👉 [TinoHost VPS](https://tino.vn/vps-n8n?affid=388)

**🚀 Hãy bắt đầu tự động hóa pipeline content của mình ngay hôm nay!** 🚀