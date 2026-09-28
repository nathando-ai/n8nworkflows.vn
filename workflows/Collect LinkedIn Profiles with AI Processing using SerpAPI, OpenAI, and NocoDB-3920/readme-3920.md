---
title: "🔍 Tự Động Học LinkedIn Profile + Xử Lý AI: Tải Excel & Lưu Trữ NocoDB Miễn Phí (SerpAPI + OpenAI)"
description: "Workflow tự động hóa tìm kiếm, xử lý và lưu trữ hồ sơ LinkedIn theo từ khóa/địa điểm, chuyển đổi số lượng follower từ dạng '3.3k+' thành số nguyên, và xuất ra Excel + NocoDB. Giúp doanh nghiệp tiết kiệm 10-15h/tháng trong nghiên cứu thị trường và tuyển dụng."
slug: "tu-dong-hoa-tim-kiem-linkedin-ai"
tags: [n8n, automation, sales, ai-marketing, nocodb, serpapi, openai]
keywords: [n8n workflow linkedin, tự động hóa tìm kiếm linkedin, xử lý ai follower linkedin, lưu trữ linkedin nocodb, serpapi n8n]
---

# 🚀 **Tự Động Học LinkedIn Profile + Xử Lý AI: Từ Tìm Kiếm Đến Excel & NocoDB**

### **Nỗi Đau Của Các Sếp**
Tìm kiếm và phân tích hồ sơ LinkedIn thủ công là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp thường phải:
- **Tìm kiếm thủ công** trên Google với từ khóa cụ thể (ví dụ: "Chief Marketing Officer tại Hà Nội").
- **Lọc và sao chép** thông tin từ hàng trăm kết quả để phân tích.
- **Chuyển đổi số lượng follower** từ dạng "3.3k+" thành số nguyên (3300) để tính toán chính xác.
- **Lưu trữ và quản lý** dữ liệu một cách rối loạn trên Excel hoặc Google Sheets.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi dữ liệu không được tối ưu hóa để phân tích sâu.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10-15h/tháng** bằng cách tự động hóa tìm kiếm và xử lý dữ liệu.
✅ **Lấy được dữ liệu chính xác** với số lượng follower được chuyển đổi tự động (ví dụ: "500+" → 500).
✅ **Xem hồ sơ LinkedIn trong Excel** để tải xuống và phân tích offline.
✅ **Lưu trữ dữ liệu trong NocoDB** (cơ sở dữ liệu tương tự Airtable) để truy cập và phân tích dễ dàng.
✅ **Tránh bị chặn bởi Google** nhờ sử dụng **SerpAPI** (không cần sử dụng API chính thức của Google).
✅ **Cá nhân hóa thông tin công ty** bằng AI (OpenAI) từ nội dung LinkedIn.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (miễn phí tier):
   - Đăng ký tại [serpapi.com](https://serpapi.com/) và lấy **API Key**.
   - Hướng dẫn chi tiết: [n8n SerpAPI Docs](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolserpapi/).
2. **Tài khoản OpenAI** (miễn phí tier):
   - Đăng ký tại [openai.com](https://platform.openai.com/) và lấy **API Key**.
   - Chọn mô hình AI (gợi ý: **GPT-4o**).
3. **Tài khoản NocoDB**:
   - Đăng ký tại [nocodb.com](https://nocodb.com/) hoặc tự host.
   - Lấy **API Token** từ cài đặt tài khoản.
4. **Credentials trong n8n**:
   - Thiết lập 3 credentials trong n8n Editor:
     - `serpApi` (điền API Key từ SerpAPI).
     - `openAiApi` (điền API Key từ OpenAI).
     - `nocoDbApiToken` (điền token từ NocoDB).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Copy JSON từ [n8n.io/workflows/3920](https://n8n.io/workflows/3920) (mục "Template Code").
- **Bước 2:** Trong n8n Editor, chọn **"Import from JSON"** và dán JSON vào.
- **Bước 3:** Kiểm tra workflow đã import hoàn chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần chú ý cấu hình sau:

| **Node**                          | **Lưu Ý Cần Thiết**                                                                                                                                                                                                 | **Tham Số Cần Điền**                                                                                     |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **Manual Trigger**                | Khởi động workflow thủ công.                                                                                                                                                                               | -                                                                                                       |
| **Google search w/ SerpAPI**      | **Bắt buộc** thiết lập credentials `serpApi` và điền **API Key** từ SerpAPI.                                                                                                                           | `api_key`: [API Key từ SerpAPI]                                                                         |
| **Edit Fields**                   | Cấu hình **Search parameter** (từ khóa, địa điểm, số kết quả, ngôn ngữ). Ví dụ: `keyword="Chief Marketing Officer", location="Hà Nội", num=10`.                                                          | `keyword`: [Từ khóa tìm kiếm] <br> `location`: [Địa điểm] <br> `num`: [Số kết quả] (gợi ý: 10-20)       |
| **Discard meta data**             | Loại bỏ metadata không cần thiết (như liên kết quảng cáo).                                                                                                                                                     | -                                                                                                       |
| **LinkedIn profiles in Excel**    | **Không cần chỉnh**, chỉ cần **tải xuống** khi cần.                                                                                                                                                         | -                                                                                                       |
| **Turn search results into items**| Chuyển kết quả tìm kiếm thành **một danh sách cá nhân hóa** (mỗi profile là một item).                                                                                                                 | -                                                                                                       |
| **Company name & followers**       | **Bắt buộc** thiết lập credentials `openAiApi` và chọn mô hình AI (gợi ý: **GPT-4o**). Prompt đã được tối ưu hóa để trích xuất tên công ty và chuyển đổi số lượng follower.                          | `model`: `gpt-4o` <br> `prompt`: [Prompt mặc định] (không cần chỉnh nếu muốn kết quả nhanh)             |
| **Generate final data via merge** | Gộp dữ liệu từ các node trước thành **một bảng hoàn chỉnh**.                                                                                                                                                 | -                                                                                                       |
| **Store data in NocoDB**          | **Bắt buộc** thiết lập credentials `nocoDbApiToken` và chọn **table** đã tạo trước.                                                                                                                           | `table`: [Tên bảng trong NocoDB] <br> `operation`: `create` <br> `resources`: `row`                     |

#### **3. Kích Hoạt Workflow ⚡️**
- **Bước 1:** Điền **từ khóa** và **địa điểm** vào node `Edit Fields`.
- **Bước 2:** Chọn **"Run Workflow"** (hoặc kích hoạt **Manual Trigger**).
- **Bước 3:** Kiểm tra kết quả:
  - **Excel:** Mở node `LinkedIn profiles in Excel` và **tải xuống** file.
  - **NocoDB:** Kiểm tra bảng đã lưu dữ liệu (các cột: `NameInLinkedinProfile`, `NameOfCompany`, `followers_number`, ...).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** sau node `Store data in NocoDB` để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn: *"Workflow hoàn thành! Đã tìm thấy [số lượng] hồ sơ LinkedIn mới."*

2. **Lưu Log & Audit**:
   - Thêm node **Set** trước node `nocoDb` để ghi **thời gian chạy**, **từ khóa**, và **số kết quả** vào một cột `log` trong NocoDB.

3. **Tự Động Chạy Hàng Ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày (ví dụ: tìm kiếm mới nhất về "Chief Technology Officer tại TP.HCM").

4. **Cải Tiến Prompt OpenAI**:
   - Nếu muốn kết quả chính xác hơn, chỉnh sửa **prompt** trong node `Company name & followers` để yêu cầu AI:
     - Trích xuất **nền tảng công ty** (ví dụ: "Công ty công nghệ").
     - Loại bỏ **từ khóa không liên quan** (ví dụ: "Freelancer").

5. **Lọc Kết Quả Theo Đặc Trưng**:
   - Thêm node **Filter** sau `Turn search results into items` để loại bỏ hồ sơ không phù hợp (ví dụ: chỉ giữ những profile có `followers_number > 1000`).

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại trong nghiên cứu thị trường và tuyển dụng. Bằng cách kết hợp **SerpAPI** (tìm kiếm Google không bị chặn), **OpenAI** (xử lý AI), và **NocoDB** (lưu trữ dữ liệu), các sếp có thể:
- **Tìm kiếm và phân tích** hàng ngàn hồ sơ LinkedIn trong vài phút.
- **Tải dữ liệu xuống Excel** để phân tích sâu.
- **Lưu trữ và truy cập dữ liệu** một cách dễ dàng trên NocoDB.

**Hành động ngay!** Import workflow này vào n8n của mình và bắt đầu **tự động hóa nghiên cứu LinkedIn** từ hôm nay. 🚀

---
**💡 Lưu ý cuối cùng:**
- Nếu gặp vấn đề với **SerpAPI**, hãy kiểm tra **API Key** và **tài khoản miễn phí** có đủ hạn mức không.
- Đối với **OpenAI**, nếu dùng mô hình miễn phí, lưu ý **hạn mức request** (gợi ý: sử dụng mô hình `gpt-3.5-turbo` nếu cần tiết kiệm chi phí).
- **NocoDB** hỗ trợ tự host, các sếp có thể cài trên VPS để **không phụ thuộc vào dịch vụ cloud**.