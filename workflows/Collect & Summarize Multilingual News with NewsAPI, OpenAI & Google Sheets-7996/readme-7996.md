---
title: "🌍 Tự Động Hái & Tóm Tắt Tin Tức Đa Ngôn Ngữ (Tiếng Anh & Nhật) Với NewsAPI + OpenAI – Không Cần Code!"
description: "Workflow tự động thu thập tin tức từ 2 ngôn ngữ (Anh/Nhật) theo từ khóa, tóm tắt bằng AI OpenAI và ghi dữ liệu vào Google Sheets – hoạt động tự động hàng ngày. Giúp các sếp tiết kiệm 10+ giờ/tháng tra cứu, tổng hợp tin tức quốc tế."
slug: "tu-dong-thu-tap-tom-tat-tin-tuc-ngon-ngu-multilingual"
tags: [n8n, automation, ai-summarization, news-collection, google-sheets, openai, multilingual]
keywords: [tự động hóa tin tức, tóm tắt tin tức bằng AI, thu thập tin tức tiếng Nhật, thu thập tin tức tiếng Anh, n8n workflow tự động, NewsAPI OpenAI]
---

# 🚀 **Tự Động Hái & Tóm Tắt Tin Tức Đa Ngôn Ngữ (Tiếng Anh & Nhật) – Không Cần Code!**

### **Giải pháp cho các sếp:**
Bạn có phải mất **10+ giờ/tháng** để tra cứu, đọc và tổng hợp tin tức từ **2 ngôn ngữ (Anh/Nhật)** để báo cáo cho ban lãnh đạo? Hay phải **lọc ra tin tức mới nhất** về ngành nghề của mình trong khi bị chìm trong luồng thông tin không cần thiết?

**Workflow này sẽ:**
✅ **Tự động thu thập tin tức** từ NewsAPI theo từ khóa của bạn (ví dụ: OpenAI, n8n, AI, blockchain...)
✅ **Tóm tắt bằng AI OpenAI** để bạn chỉ cần đọc **cốt lõi** trong 1 phút thay vì 1 giờ
✅ **Ghi dữ liệu vào Google Sheets** với cấu trúc sẵn sàng báo cáo
✅ **Hoạt động tự động hàng ngày** (không cần can thiệp thủ công)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** tra cứu tin tức thủ công.
- **Tóm tắt tin tức bằng AI** – chỉ đọc **cốt lõi** trong 1 phút thay vì 1 giờ.
- **Dữ liệu sẵn sàng báo cáo** – Google Sheets tự động cập nhật.
- **Hoạt động 24/7** – không cần can thiệp thủ công.
- **Hỗ trợ 2 ngôn ngữ** (Tiếng Anh & Nhật) – phù hợp cho doanh nghiệp quốc tế.
- **Cập nhật tự động** – không bỏ lỡ tin tức mới nhất.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu kết quả):
   - **Spreadsheet ID** (tìm trong liên kết chia sẻ Google Sheets).
   - **Sheet Name**:
     - Tab `01_Input` (để nhập từ khóa và đánh dấu "Yes/No" nếu cần tìm kiếm).
     - Tab `02_Output` (sẽ tự động ghi dữ liệu sau khi tóm tắt).
   - **Cấu trúc cột**:
     - `01_Input`: `Keyword` (từ khóa tìm kiếm) + `SearchRequired` (Yes/No).
     - `02_Output`: `Date`, `Keyword`, `Summary`, `URL`.

2. **API Key NewsAPI**:
   - [Đăng ký miễn phí tại NewsAPI](https://newsapi.org/) (đảm bảo có **plan Pro** để lấy đủ dữ liệu).

3. **API Key OpenAI** (nếu muốn tóm tắt bằng AI):
   - [Đăng ký tại OpenAI](https://platform.openai.com/) (đảm bảo có **tài khoản Pro** để sử dụng GPT-3.5/4).

4. **Credentials trong n8n**:
   - **Google Sheets OAuth2**: Cấu hình trong **n8n Credentials** (n8n → Credentials → Add → Google Sheets OAuth2).
   - **OpenAI API**: Cấu hình trong **n8n Credentials** (n8n → Credentials → Add → OpenAI).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/7996) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7996) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Schedule Trigger (Điều khiển thời gian chạy)**
- Mặc định: **Chạy hàng ngày lúc 13:00** (UTC).
- **Cách chỉnh**:
  - Nhấp vào node **Schedule Trigger** → **Edit**.
  - Chọn **Cron Expression**:
    - `0 0 13 * * ?` (lúc 13:00 hàng ngày).
    - Hoặc chỉnh theo giờ Việt Nam: `0 0 13 +8 * * ?` (UTC +8).

##### **B. Cấu hình Google Sheets**
- **Node "Get rows from sheet"**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Spreadsheet ID**: Nhập ID của **01_Input** (tìm trong liên kết chia sẻ Google Sheets).
  - **Sheet Name**: Nhập `01_Input`.

- **Node "Append rows to sheet"**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Nhập ID của **02_Output**.
  - **Sheet Name**: Nhập `02_Output`.
  - **Columns**: Đảm bảo có `Date`, `Keyword`, `Summary`, `URL`.

##### **C. Cấu hình NewsAPI (Thu thập tin tức)**
- **Node "HTTP Request (EN)"** (Tiếng Anh):
  - **URL**: `https://newsapi.org/v2/everything`
  - **Query Parameters**:
    - `q`: `$json["Keyword"]` (từ khóa từ Google Sheets).
    - `language`: `en` (ngôn ngữ Anh).
    - `apiKey`: Nhập **API Key NewsAPI** của bạn.
  - **Headers**:
    - `Accept`: `application/json`.

- **Node "HTTP Request (JP)"** (Tiếng Nhật):
  - **URL**: `https://newsapi.org/v2/everything`
  - **Query Parameters**:
    - `q`: `$json["Keyword"]` (từ khóa từ Google Sheets).
    - `language`: `ja` (ngôn ngữ Nhật).
    - `apiKey`: Nhập **API Key NewsAPI** của bạn.

##### **D. Cấu hình OpenAI (Tóm tắt tin tức)**
- **Node "Summarize with OpenAI"**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có).
  - **Prompt**:
    ```json
    "Tóm tắt tin tức này trong 3 câu ngắn gọn. Đảm bảo bao gồm:
    - Điểm chính của bài viết.
    - Thông tin quan trọng về chủ đề.
    - Liên kết nguồn gốc (URL).
    Tin tức: {{$json["article"]}}"
    ```
  - **Temperature**: 0.7 (để AI không quá sáng tạo).

##### **E. Cấu hình Code Nodes (Split Articles)**
- **Node "Split Articles (EN)"**:
  - **Code**:
    ```javascript
    return {
      json: {
        article: $input.all()[0].json.body.articles.map(article => article.title + "\n" + article.description + "\n" + article.url).join("\n\n")
      }
    };
    ```
- **Node "Split Articles (JP)"**:
  - **Code**:
    ```javascript
    return {
      json: {
        article: $input.all()[0].json.body.articles.map(article => article.title + "\n" + article.description + "\n" + article.url).join("\n\n")
      }
    };
    ```

##### **F. Cấu hình If Condition (Kiểm tra "SearchRequired")**
- **Node "If Search Required"**:
  - **Condition**: `$json["SearchRequired"] === "Yes"`.
  - Nếu `Yes` → Chạy **HTTP Request (EN)** và **HTTP Request (JP)**.
  - Nếu `No` → Bỏ qua và chuyển sang **Merge Articles**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra logic):
   - Nhấp vào nút **Run Workflow** và chọn **Test Run**.
   - Nhập dữ liệu mẫu vào **01_Input** (ví dụ: `Keyword = "AI", SearchRequired = "Yes"`).
   - Kiểm tra **02_Output** xem có ghi dữ liệu không.

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấp vào **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Tin tức mới về [Keyword] đã được tóm tắt và lưu vào Google Sheets!"`.

2. **Lưu Log Dữ liệu**:
   - Thêm node **Set** trước khi **Append rows to sheet** để lưu thêm thông tin như:
     ```json
     {
      "Log": "Tin tức về " + $json["Keyword"] + " đã được xử lý vào " + new Date().toISOString()
     }
     ```
   - Sau đó, ghi vào một **tab mới** trong Google Sheets để theo dõi lịch sử.

3. **Tự động Gửi Báo Cáo Email**:
   - Sử dụng node **Email** (ví dụ: Gmail) để gửi báo cáo hàng tuần cho ban lãnh đạo.
   - Ví dụ: Gửi **Google Sheets** dưới dạng PDF hoặc Excel.

4. **Tăng Số Lượng Từ Khóa**:
   - Thêm nhiều hàng vào **01_Input** để thu thập tin tức về nhiều chủ đề khác nhau (ví dụ: "Blockchain", "n8n", "ChatGPT").

5. **Chỉnh Sửa Prompt OpenAI**:
   - Nếu muốn tóm tắt chi tiết hơn, chỉnh **Prompt** trong node OpenAI:
     ```json
     "Tóm tắt tin tức này chi tiết trong 5 câu, bao gồm:
     - Bối cảnh của bài viết.
     - Điểm quan trọng nhất.
     - Thông tin mới nhất.
     - Liên kết nguồn gốc.
     Tin tức: {{$json["article"]}}"
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc thủ công** tra cứu, đọc và tổng hợp tin tức. Bằng cách **tự động thu thập, tóm tắt bằng AI và lưu vào Google Sheets**, các sếp có thể:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Nhận báo cáo tin tức quốc tế** (Anh/Nhật) một cách nhanh chóng.
✔ **Cập nhật liên tục** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm từ khóa** vào **01_Input**.
3. **Bật Active** và để AI làm việc cho bạn!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/7996) và bắt đầu tự động hóa ngay! 🚀

---
**Chia sẻ & phản hồi:**
Nếu có thắc mắc hoặc muốn cải tiến workflow, hãy để lại bình luận dưới đây. Các sếp cũng có thể **customize** workflow này để phù hợp với ngành nghề của mình! 💡