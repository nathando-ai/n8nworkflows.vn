---
title: "🌍 Tự Động Hóa Scrape & Tóm Tắt Tin Tức Ngành Công Nghiệp với Bright Data & OpenAI (Không Cần Code)"
description: "Workflow tự động hóa scrape tin tức Reuters về xung đột Israel-Iran, tóm tắt thông tin về vai trò của Hezbollah, và gửi báo cáo tự động đến nhóm phân tích. Giúp các sếp tiết kiệm thời gian và nhận được dữ liệu chính xác 24/7."
slug: "tieu-dong-hoa-scrape-tom-tat-tin-tuc-nganh-cong-nghiep"
tags: [n8n, automation, no-code, market-research, ai-summarization, bright-data, openai, gmail]
keywords: [tự động hóa n8n, scrape tin tức Reuters, tóm tắt tin tức AI, Hezbollah, Israel-Iran, Bright Data, OpenAI, tự động hóa báo cáo]
---

# 🚀 **Tự Động Hóa Scrape & Tóm Tắt Tin Tức Ngành Công Nghiệp với Bright Data & OpenAI**

## **Giới Thiệu**
Các sếp đang phải mất nhiều thời gian để theo dõi tin tức thị trường, đặc biệt là về xung đột Israel-Iran và vai trò của Hezbollah? Hay phải tốn công tóm tắt nội dung dài dòng của Reuters để gửi cho nhóm phân tích? **Workflow này giải quyết tất cả!**

Với **n8n**, Bright Data và OpenAI, các sếp chỉ cần **nhập URL bài báo**, hệ thống sẽ tự động:
✅ **Scrape** tin tức từ Reuters
✅ **Tóm tắt** bằng AI (GPT-4.1-mini)
✅ **Lọc** thông tin liên quan đến Hezbollah
✅ **Gửi báo cáo** tự động qua email cho nhóm Trends Team

**Kết quả?** Tiết kiệm **hàng giờ mỗi tuần**, giảm sai sót, và nhận được **dữ liệu chính xác, cấu trúc** để ra quyết định nhanh chóng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải scrape thủ công hoặc tóm tắt tin tức.
- **Dữ liệu chính xác**: AI lọc và tóm tắt nội dung chính xác về Hezbollah và xung đột Israel-Iran.
- **Báo cáo tự động**: Email được gửi ngay khi có tin tức mới, không cần can thiệp.
- **Cấu trúc dữ liệu**: Dữ liệu được định dạng JSON, dễ dàng tích hợp vào hệ thống phân tích.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (để scrape tin tức):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (sử dụng mã **1tndi4600b25** để hỗ trợ tạo nội dung miễn phí).
   - **API Key** của Bright Data MCP (cấu hình trong n8n dưới `mcpClientApi`).
2. **Tài khoản OpenAI**:
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key** (cấu hình trong n8n dưới `openAiApi`).
3. **Tài khoản Gmail** (để gửi báo cáo):
   - Cấu hình **OAuth2** trong n8n dưới `gmailOAuth2`.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí của n8n.io).
5. **Plugin LangChain** (đã tích hợp trong workflow, không cần cài thêm).
:::

---

## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5977) (hoặc sử dụng link gốc).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **3 phần chính**, các sếp cần chú ý cấu hình các node sau:

#### **📌 Phần 1: Khởi động & Nhập URL (Manual Trigger)**
- **🚦 Start Workflow (Manual Trigger)**:
  - **Không cần chỉnh sửa**, chỉ cần nhấn **Execute Workflow** khi muốn chạy.
- **🔗 Enter Reuters News URL**:
  - **Node `Set`**: Điền **URL bài báo Reuters** vào trường `url` (ví dụ: `https://www.reuters.com/...`).
  - **Lưu ý**: URL phải là bài báo liên quan đến **Israel-Iran** và **Hezbollah**.

#### **📌 Phần 2: AI Scrape & Tóm Tắt (Agent + OpenAI + Bright Data)**
- **🤖 Agent: Scrape Reuters News**:
  - **Không cần chỉnh sửa**, AI Agent sẽ tự động:
    - **Scrape** nội dung từ URL đã nhập.
    - **Lọc** thông tin về **Hezbollah** và xung đột Israel-Iran.
  - **Cấu hình trong Agent**:
    - **Tool `MCP Client Tool`** (Bright Data):
      - **Credentials**: Chọn `mcpClientApi` (đã cấu hình trước).
      - **Operation**: Đảm bảo chọn `executeTool`.
    - **OpenAI Chat Model**:
      - **Model**: Đã mặc định là `gpt-4.1-mini` (tiết kiệm chi phí).
      - **Credentials**: Chọn `openAiApi` (API Key OpenAI).
    - **Output Parser**:
      - **Auto-fixing**: Đảm bảo chọn `outputParserAutofixing`.
      - **Structured Output**: Chọn `outputParserStructured` để định dạng JSON.

#### **📌 Phần 3: Gửi Báo cáo qua Email (Gmail)**
- **✉️ Send Insights to Trends Team (Gmail)**:
  - **Credentials**: Chọn `gmailOAuth2` (tài khoản Gmail đã cấu hình).
  - **Email To**: Điền địa chỉ email của **nhóm Trends Team** (ví dụ: `team@doanhnghiep.com`).
  - **Subject**: Đặt tiêu đề email như `"Tóm tắt tin tức Israel-Iran - Hezbollah"`.
  - **Body**: Sử dụng **JSON structured** từ node trước (AI đã tóm tắt).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** và nhập URL bài báo mẫu.
   - Kiểm tra **Output** để đảm bảo:
     - Dữ liệu scrape được chính xác.
     - Email được gửi thành công.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi ý Nâng Cao**
:::tip[CÁCH LÀM THÊM ĐỂ TĂNG CƯỜNG HỆ THỐNG]
1. **Tự động scrape nhiều bài báo**:
   - Sử dụng **Webhook** thay vì Manual Trigger để nhận URL từ **Slack/Telegram**.
   - Ví dụ: Khi có tin tức mới trên Slack, workflow tự động scrape và gửi báo cáo.

2. **Lưu log scrape**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử scrape.
   - Cấu hình node `Set` để ghi dữ liệu vào sheet.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để scrape và gửi email **hàng ngày/tuần**.
   - Ví dụ: Scrape tất cả tin tức mới về Israel-Iran từ Reuters vào 8h sáng.

4. **Tích hợp với Slack**:
   - Thay vì email, gửi báo cáo qua **Slack** bằng node `slack`.
   - Cấu hình **webhook Slack** trong n8n.

5. **Cải thiện prompt AI**:
   - Nếu muốn AI tóm tắt chi tiết hơn về **Hezbollah**, chỉnh sửa **prompt** trong node `lmChatOpenAi`:
     ```json
     {
       "role": "user",
       "content": "Tóm tắt bài báo này về vai trò của Hezbollah trong xung đột Israel-Iran. Đảm bảo bao gồm: \n
       - Mối quan hệ với Iran \n
       - Hành động quân sự gần đây \n
       - Ảnh hưởng đến an ninh khu vực \n
       - Dự đoán tương lai"
     }
     ```
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần theo dõi tin tức thị trường một cách **tự động, chính xác và tiết kiệm thời gian**. Với **Bright Data** scrape tin tức, **OpenAI** tóm tắt nội dung, và **Gmail** gửi báo cáo, các sếp không phải lo lắng về việc mất thời gian hoặc sai sót trong quá trình phân tích.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá trên).
2. **Import workflow** và cấu hình tài khoản.
3. **Test và bật Active** để nhận báo cáo tự động hàng ngày!

**Cần hỗ trợ?** Liên hệ với tác giả qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**Chúc các sếp thành công với tự động hóa!** 🚀