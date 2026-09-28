---
title: "🚀 Tự Động Xác Minh TikTok Influencer Từ Username Với Dumpling AI + GPT-4 (Không Cần Code)"
description: "Workflow tự động hóa kiểm tra và phân loại TikToker có đủ tiêu chí (40+ video, 100K+ follower, 300K+ heart) từ username, kết quả lưu vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng trong việc tuyển chọn influencer."
slug: "tieu-dong-xac-min-tiktok-influencer-dumpling-ai-gpt4"
tags: [n8n, automation, no-code, tiktok-marketing, ai-multimodal, google-sheets]
keywords: [tự động hóa tiktok influencer, n8n workflow tiktok, kiểm tra tiktoker bằng ai, dumpling api tiktok, gpt4 phân loại influencer]
---

# 🚀 **Tự Động Xác Minh TikTok Influencer Từ Username Với Dumpling AI + GPT-4**

### **Giải quyết vấn đề gì?**
Các sếp đang phải **tìm kiếm và đánh giá thủ công hàng trăm TikToker** để chọn những người phù hợp cho chiến dịch marketing. Quá trình này tốn thời gian, dễ sai sót, và khó theo dõi kết quả. **Workflow này tự động hóa toàn bộ quy trình:**
✅ **Nhập username TikTok** → **Lấy dữ liệu profile** (Dumpling AI)
✅ **GPT-4 đánh giá** (40+ video, 100K+ follower, 300K+ heart)
✅ **Lưu kết quả vào Google Sheets** (cập nhật hoặc thêm mới)
✅ **Tiết kiệm 10+ giờ/tháng** cho đội ngũ marketing!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên TikTok.
- **Đánh giá chính xác**: GPT-4 tự động phân loại dựa trên tiêu chí cụ thể.
- **Dữ liệu cập nhật**: Lưu kết quả vào Google Sheets để theo dõi và phân tích.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp.
- **Cá nhân hóa**: Thêm tiêu chí đánh giá tùy chỉnh (ví dụ: engagement rate).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Dumpling AI** (để lấy dữ liệu profile TikTok):
   - API Key từ [Dumpling AI](https://dumpling.ai/) (miễn phí hoặc trả phí).
   - Tham số `httpHeaderAuth` trong node `Get TikTok Profile`.

2. **Tài khoản OpenAI** (để sử dụng GPT-4):
   - API Key từ [OpenAI](https://platform.openai.com/).
   - Tham số `openAiApi` trong node `Evaluate Profile Qualification`.

3. **Tài khoản Google Sheets**:
   - File Google Sheets đã cấu trúc với các cột:
     - `Tik Tok user` (username)
     - `User ID` (ID duy nhất của TikToker)
     - `Follower Count`
     - `Following Count`
     - `Heart Count`
     - `Video Count`
     - `Qualified?` (True/False)
   - Tham số `googleSheetsOAuth2Api` trong node `Check if User Already Exists` và `Add New TikTok User`.

4. **Form Trigger** (để nhận username từ người dùng):
   - Có thể là form web, Slack, hoặc Telegram (tùy chọn).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9126](https://n8n.io/workflows/9126) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình node `Get TikTok Profile (Dumpling AI)`**
- **Tham số quan trọng**:
  - **URL**: `https://api.dumpling.ai/v1/users/{username}` (thay `{username}` bằng `$node["Trigger on TikTok Username Form"]["json"]["username"]`).
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY_DUMPLING}` (điền API Key từ Dumpling AI).
    - `Content-Type`: `application/json`.
  - **Method**: `GET`.

##### **B. Cấu hình node `Evaluate Profile Qualification (GPT-4)`**
- **Tham số quan trọng**:
  - **Model**: `gpt-4` (hoặc `gpt-4-turbo` nếu có).
  - **Prompt**:
    ```plaintext
    You are an influencer qualification assistant. Evaluate if a TikTok user meets the following criteria:
    1. At least 40 videos
    2. 100,000+ followers
    3. 300,000+ hearts

    Return ONLY "Qualified for influencer outreach" if all criteria are met, otherwise return "Not qualified".

    Data to evaluate:
    {{
      $json["Follower Count"],
      $json["Video Count"],
      $json["Heart Count"]
    }}
    ```
  - **API Key**: Điền `openAiApi` từ tài khoản OpenAI.

##### **C. Cấu hình node `Check if User Already Exists`**
- **Tham số quan trọng**:
  - **File Google Sheets**: Chọn file đã cấu trúc.
  - **Range**: `Sheet1!A2:G` (giả sử dữ liệu từ hàng 2).
  - **Query**: `SELECT * WHERE User ID = "{{$node["Trigger on TikTok Username Form"]["json"]["userId"]}}"`.
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.

##### **D. Cấu hình node `Add New TikTok User to Sheet` và `Update Existing TikTok User`**
- **Tham số chung**:
  - **File Google Sheets**: Chọn file cùng với node trước.
  - **Range**: `Sheet1!A2:G` (để dữ liệu bắt đầu từ hàng 2).
  - **Credentials**: `googleSheetsOAuth2Api`.
- **Node `Add New TikTok User`**:
  - **Operation**: `append`.
  - **Data**:
    ```json
    {
      "Tik Tok user": "{{$node["Trigger on TikTok Username Form"]["json"]["username"]}}",
      "User ID": "{{$node["Trigger on TikTok Username Form"]["json"]["userId"]}}",
      "Follower Count": "{{$json["Follower Count"]}}",
      "Following Count": "{{$json["Following Count"]}}",
      "Heart Count": "{{$json["Heart Count"]}}",
      "Video Count": "{{$json["Video Count"]}}",
      "Qualified?": "{{$node["Evaluate Profile Qualification (GPT-4)"]["json"]["result"]}}"
    }
    ```
- **Node `Update Existing TikTok User`**:
  - **Operation**: `appendOrUpdate` (cập nhật nếu tồn tại).
  - **Data**: Cấu trúc tương tự như node `Add New`, nhưng thay `append` thành `appendOrUpdate`.

##### **E. Cấu hình node `Route Based on Existence` (Switch)**
- **Tham số quan trọng**:
  - **Condition 1**: `{{$node["Check if User Already Exists"]["json"]["rows"].length > 0}}` → Chọn node `Update Existing TikTok User`.
  - **Condition 2**: `{{!$node["Check if User Already Exists"]["json"]["rows"].length > 0}}` → Chọn node `Add New TikTok User`.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhập một username TikTok vào form trigger (ví dụ: `@phamngochau`).
   - Kiểm tra kết quả trong Google Sheets và node `Evaluate Profile Qualification`.

2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo kết quả cho team.
   - Ví dụ: Nếu `Qualified? = True`, gửi tin nhắn: `🎉 @username đã được xác minh là influencer!`.

2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi lại thời gian và kết quả của mỗi request.

3. **Báo cáo định kỳ**:
   - Sử dụng node `googleSheets` để tạo báo cáo tổng hợp (ví dụ: số lượng TikToker mới được thêm trong tháng).

4. **Tùy chỉnh tiêu chí đánh giá**:
   - Thay đổi prompt GPT-4 để thêm tiêu chí mới (ví dụ: engagement rate > 5%).

5. **Dùng Dumpling API miễn phí**:
   - Nếu không muốn trả phí, thử dùng API free tier của Dumpling (có giới hạn request).

---

### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa quy trình tuyển chọn TikTok influencer chỉ trong vài phút**, tiết kiệm thời gian và giảm thiểu sai sót. **Bắt đầu ngay bằng cách import và cấu hình theo hướng dẫn trên!**

👉 **Bấm "Active" và để workflow làm việc cho bạn!** 🚀

---
**Cần hỗ trợ?** Đăng câu hỏi trên [Community n8n](https://community.n8n.io/) hoặc liên hệ với tác giả [Yang](https://n8n.io/workflows/9126).