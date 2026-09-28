---
title: "🚀 Tự động tạo bản tin sáng lập & danh sách tiềm năng từ Hacker News bằng GPT‑4o & Gmail"
description: "Workflow n8n thu thập tin tức Hacker News, lọc các startup sáng lập, tạo bản tin và gửi email tự động qua Gmail, đồng thời lưu lead vào Google Sheets."
slug: "tu-dong-tao-ban-tin-hacker-news-gpt4o-gmail"
tags: [n8n, automation, no-code, market-research, ai, email]
keywords: [n8n workflow, tự động hóa, Hacker News, GPT-4o, Gmail, lead generation]
---

# 🚀 Tự động tạo bản tin sáng lập & danh sách tiềm năng từ Hacker News bằng GPT‑4o & Gmail

Doanh nghiệp công nghệ thường phải **đánh mất hàng giờ** mỗi ngày để lướt Hacker News, lọc những startup mới, ghi chú thông tin liên hệ và soạn email gửi tới đội sales. Công việc này không chỉ tốn thời gian mà còn dễ sai sót, khiến các cơ hội tiềm năng bị bỏ lỡ.

**Workflow này** sẽ giải quyết toàn bộ quy trình **100 % tự động**:
1. **Lên lịch** chạy mỗi ngày.
2. **Thu thập** các bài viết mới trên Hacker News qua SerpAPI.
3. **Phân tích** nội dung bằng GPT‑4o để xác định các startup sáng lập và trích xuất thông tin quan trọng.
4. **Lưu** dữ liệu lead vào Google Sheets.
5. **Soạn & gửi** bản tin tóm tắt qua Gmail tới danh sách người nhận.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở Hacker News, copy‑paste, và soạn email thủ công.  
- **Độ chính xác cao**: GPT‑4o phân tích nội dung, lọc chỉ những startup thực sự phù hợp.  
- **Dữ liệu luôn cập nhật**: Leads được ghi vào Google Sheets ngay khi xuất hiện.  
- **Gửi bản tin tự động**: Đội sales nhận email mỗi sáng, sẵn sàng liên hệ ngay.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (self‑hosted hoặc cloud).  
- **API key của SerpAPI** (để truy vấn Hacker News).  
- **Credentials Gmail** (OAuth2 hoặc App Password).  
- **Google Cloud Project** với **Google Sheets API** bật và credentials JSON.  
- **Azure OpenAI endpoint & API key** (để sử dụng mô hình GPT‑4o).  
- **MCP Client Tool** (nếu dùng LangChain MCP).  
- **Google Sheet** đã tạo sẵn với các cột: `Date`, `Title`, `URL`, `Founder`, `Email`, `Notes`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows**.  
2. Nhấn **Import** → **Upload JSON** và chọn file `founder-digest-hackernews.json` (hoặc copy toàn bộ JSON vào ô **Import from Clipboard**).  
3. Nhấn **Import** để workflow xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **Schedule Trigger** | Khởi chạy tự động mỗi ngày | Chọn **Cron**: `0 8 * * *` (8h sáng GMT+7) hoặc tùy lịch muốn. |
| **SerpAPI** (`n8n-nodes-serpapi.serpApi`) | Tìm kiếm “Hacker News” mới nhất | - **API Key**: nhập key SerpAPI.<br>- **Engine**: `google`. <br>- **Query**: `site:news.ycombinator.com "show hn"`.<br>- **Num Results**: `20`. |
| **Code** (`n8n-nodes-base.code`) | Lọc URL, tiêu đề, trích xuất nội dung | Đảm bảo **JavaScript** trả về mảng object `{title, url, content}`. |
| **LangChain Agent** (`@n8n/n8n-nodes-langchain.agent`) | Gọi GPT‑4o để xác định startup & founder | - **Credentials**: Azure OpenAI.<br>- **Model**: `gpt-4o`.<br>- **Prompt**: “Identify if the article describes a newly founded startup. If yes, extract founder name, email (if present), and a short description.” |
| **Aggregate** (`n8n-nodes-base.aggregate`) | Gom lại các lead thành một mảng | Chọn **Mode**: `Merge` → **Field to Merge**: `data`. |
| **Google Sheets** (`n8n-nodes-base.googleSheets`) | Ghi lead vào sheet | - **Credentials**: Google Service Account.<br>- **Spreadsheet ID**: ID của sheet đã tạo.<br>- **Sheet Name**: `Leads`.<br>- **Operation**: `Append`. |
| **Gmail** (`n8n-nodes-base.gmail`) | Gửi bản tin qua email | - **Credentials**: Gmail OAuth2.<br>- **To**: danh sách email (có thể dùng **Expression** để lấy từ Google Sheet).<br>- **Subject**: `📈 Founder Digest – {{ $now.format("DD/MM/YYYY") }}`.<br>- **Body**: chèn HTML template, dùng **Expression** để lặp qua leads. |
| **MCP Client Tool** (`@n8n/n8n-nodes-langchain.mcpClientTool`) | (Nếu dùng) Kết nối tới LangChain MCP | Điền **Endpoint** và **API Key** của MCP. |
| **LM Chat Azure OpenAI** (`@n8n/n8n-nodes-langchain.lmChatAzureOpenAi`) | (Tùy chọn) Truy vấn trực tiếp Azure OpenAI | Cấu hình **Endpoint**, **API Key**, **Deployment Name** (`gpt-4o`). |
| **Sticky Note** | Ghi chú mô tả workflow | Không cần cấu hình, chỉ để tham khảo. |

> **Lưu ý:** Mỗi node sử dụng **Credentials** riêng; hãy tạo chúng trong **n8n > Credentials** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log của từng node, đặc biệt node **Code** và **LangChain Agent** để chắc chắn dữ liệu được trích xuất đúng.  
2. Nếu mọi thứ ổn, bật **Active** (góc phải trên) để workflow chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo nhanh khi có lead mới.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để ghi lại JSON raw vào S3 hoặc Google Drive, phục vụ audit.  
- **Báo cáo tuần**: Thêm node **Schedule Trigger** (hàng tuần) + **Google Docs** để tổng hợp số lượng lead, tỷ lệ chuyển đổi, gửi email báo cáo.  
- **Filtration nâng cao**: Sử dụng **IF** node để chỉ lưu lead có email hợp lệ hoặc có mức độ “high confidence” từ GPT‑4o.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn mất công** lướt Hacker News, **tự động thu thập** các startup tiềm năng, **lưu trữ** vào Google Sheets và **gửi bản tin** ngay trong hộp thư Gmail. Hãy triển khai ngay hôm nay, để đội sales luôn có nguồn lead “sẵn sàng gọi” mỗi sáng!