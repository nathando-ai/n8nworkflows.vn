---
title: "🚀 Tự Động Hóa Phân Tích Gọi Điện Bán Hàng với AI Azure + CRM: CallForge - 05"
description: "Workflow tự động hóa phân tích cuộc gọi bán hàng từ Gong.io, sử dụng Azure AI để trích xuất thông tin quan trọng cho Sales, Marketing và Product, đồng bộ hóa tự động vào CRM và Notion. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng và cải thiện chất lượng dữ liệu."
slug: "tieu-dong-hoa-phan-tich-goi-dien-banh-hang-azure-crm"
tags: [n8n, automation, sales, crm, ai, azure-openai, gong-io, notion, salesforce, no-code]
keywords: [n8n workflow phân tích gọi điện, tự động hóa sales gong.io, azure ai trong n8n, đồng bộ hóa crm với notion, workflow ai cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Phân Tích Gọi Điện Bán Hàng với AI Azure + CRM: CallForge - 05**

### **Giải pháp AI tự động hóa phân tích cuộc gọi bán hàng từ Gong.io**
Các sếp đang mất nhiều thời gian thủ công để phân tích cuộc gọi bán hàng từ Gong.io? Thường xuyên gặp phải vấn đề:
- **Thông tin quan trọng bị bỏ lỡ** vì phải đọc thủ công hàng trăm cuộc gọi.
- **Dữ liệu không đồng bộ** giữa Salesforce, Notion và các bộ phận khác.
- **Tốn thời gian** để trích xuất thông tin cho Sales, Marketing và Product.
- **Không tối ưu hóa** từ cuộc gọi để cải thiện chiến lược bán hàng.

**CallForge - 05** là workflow tự động hóa **100% không cần code**, sử dụng **Azure AI (GPT-4o-mini)** để phân tích cuộc gọi từ Gong.io, trích xuất thông tin quan trọng và đồng bộ hóa tự động vào **Salesforce, Notion** cho 3 bộ phận: **Sales, Marketing và Product**. Kết quả? **Tiết kiệm 10+ giờ/tháng**, dữ liệu chính xác và đồng bộ, cùng với khả năng mở rộng cho nhiều cuộc gọi.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa phân tích cuộc gọi**: AI trích xuất thông tin từ transcript, giảm thời gian thủ công từ **10+ giờ/tháng** xuống **0**.
- **Dữ liệu đồng bộ hóa tự động**: Thông tin từ cuộc gọi được gửi ngay vào **Salesforce (Sales)**, **Notion (Marketing & Product)**.
- **Cải thiện chất lượng dữ liệu**: AI xử lý sai sót (ví dụ: tên khách hàng sai phát âm) và chuẩn hóa thông tin.
- **Khả năng mở rộng**: Xử lý hàng loạt cuộc gọi, không giới hạn số lượng.
- **Không phụ thuộc vào nhân viên**: Hoạt động **24/7**, không cần can thiệp thủ công.
- **Tích hợp AI tiên tiến**: Sử dụng **Azure OpenAI (GPT-4o-mini)** để phân tích sâu và trích xuất dữ liệu cấu trúc.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gong.io**:
   - API Key của Gong.io để lấy transcript cuộc gọi.
   - Cấu hình **Webhook** trong Gong.io để gửi dữ liệu vào n8n.
2. **Tài khoản Azure OpenAI**:
   - **API Key** và **Endpoint** của Azure OpenAI (đăng ký tại [Azure Portal](https://portal.azure.com/)).
  . **Tài khoản CRM/Salesforce**:
   - **API Key** và **Credentials** để đồng bộ hóa dữ liệu.
4. **Tài khoản Notion**:
   - **Token Notion** và **Database ID** để lưu trữ dữ liệu Marketing/Product.
5. **n8n Self-hosted**:
   - Workflow này yêu cầu **n8n chạy trên VPS** để hoạt động 24/7 (không thể dùng n8n Cloud).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3035](https://n8n.io/workflows/3035) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Kích hoạt workflow** bằng cách bấm **Active** ở góc trên bên phải.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **3 AI Agent** riêng biệt (Sales, Marketing, Product) và **3 sub-workflow** để đồng bộ hóa dữ liệu. Dưới đây là các bước **cấu hình bắt buộc**:

#### **A. Cấu hình Azure OpenAI (2 node)**
- **Node**: `Azure OpenAI Chat Model` (3 node tương tự, tên khác nhau).
- **Tham số cần điền**:
  - **Credentials**: Chọn `azureOpenAiApi` (tạo mới trong **Credentials** của n8n).
    - API Key: Nhập từ Azure Portal.
    - Endpoint: Nhập URL của Azure OpenAI (ví dụ: `https://<your-resource-name>.openai.azure.com/`).
  - **Model**: Đặt là `gpt-4o-mini` (đã cấu hình sẵn).
  - **Temperature**: Giữ mặc định (0.7) hoặc điều chỉnh theo yêu cầu.

#### **B. Cấu hình Webhook (n8n-nodes-base.executeWorkflowTrigger)**
- **Node**: `Execute Workflow Trigger`.
- **Tham số cần điền**:
  - **HTTP Method**: `POST`.
  - **Path**: Nhập URL webhook của **Gong.io** (đã cấu hình trước khi import).
  - **Credentials**: Chọn `gongIoApi` (tạo mới trong **Credentials** của n8n).
    - API Key: Nhập từ Gong.io.
  - **Body**: Đảm bảo nhận được dữ liệu từ Gong.io (thường là JSON với transcript cuộc gọi).

#### **C. Cấu hình User Prompt (n8n-nodes-base.set)**
- **Node**: `Create User Prompt`.
- **Tham số cần chỉnh sửa**:
  - **JSON Path**: Điền vào `$.userPrompt` (hoặc tương tự, tùy thuộc vào cấu trúc dữ liệu từ Gong.io).
  - **Nội dung Prompt**: Sửa để phù hợp với yêu cầu phân tích của doanh nghiệp (ví dụ: yêu cầu AI trích xuất **tên khách hàng, sản phẩm đề cập, vấn đề gặp phải, thời gian cuộc gọi**).
    ```json
    {
      "instruction": "Analyze the following call transcript and extract structured data for Sales, Marketing, and Product teams. Standardize names and key details. Output in JSON format.",
      "transcript": "$$.json.transcript"
    }
    ```

#### **D. Cấu hình Sub-workflow (n8n-nodes-base.executeWorkflow)**
Workflow này sử dụng **3 sub-workflow** riêng biệt:
1. **Sales Data Processor** → Đồng bộ hóa vào **Salesforce**.
2. **Marketing Data Processor** → Đồng bộ hóa vào **Notion**.
3. **Product Data Processor** → Đồng bộ hóa vào **Notion**.

- **Node**: `Sales Data Processor`, `Marketing Data Processor`, `Product Data Processor`.
- **Tham số cần điền**:
  - **Workflow ID**: Nhập ID của sub-workflow tương ứng (tạo mới trong n8n hoặc sử dụng sub-workflow đã có).
  - **Credentials**: Chọn `salesforceApi` (Salesforce) hoặc `notionApi` (Notion).
  - **Data**: Đảm bảo dữ liệu từ AI Agent được truyền vào sub-workflow (kiểm tra **JSON Path** trong node `Merge all processed data`).

#### **E. Cấu hình Notion & Salesforce**
- **Notion**:
  - Tạo **Database** trong Notion và lấy **Database ID**.
  - Trong **Credentials Notion**, điền:
    - **Token**: Nhập từ Notion API (tạo tại [Notion API](https://www.notion.so/my-integrations)).
    - **Database ID**: Nhập ID của database bạn muốn đồng bộ.
- **Salesforce**:
  - Tạo **Connected App** và lấy **Consumer Key** và **Consumer Secret**.
  - Trong **Credentials Salesforce**, điền:
    - **Client ID**: Consumer Key.
    - **Client Secret**: Consumer Secret.
    - **Username & Password**: Tài khoản Salesforce.

#### **F. Cấu hình Queue Logic (n8n-nodes-base.set)**
- **Node**: `Success Status Generated`.
- **Lưu ý**: Nếu workflow thất bại (ví dụ: do **rate limiting của Notion**), nó sẽ tự động **re-run** cho các cuộc gọi còn lại. Đảm bảo:
  - **Node `Data Recall Sales`**, `Data Recall Marketing` và `Data Recall Product`** được cấu hình đúng **JSON Path** để lưu trữ dữ liệu cho lần re-run.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **cuộc gọi mẫu** từ Gong.io vào webhook.
   - Kiểm tra **Output** của workflow để đảm bảo dữ liệu được trích xuất và đồng bộ hóa chính xác.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.email** hoặc **Slack** để gửi **báo cáo tổng hợp** về kết quả phân tích hàng ngày/tuần.
   - Ví dụ: "Top 3 sản phẩm được đề cập trong tuần", "Tỷ lệ thành công của Sales".

2. **Tích hợp với CRM khác**:
   - Nếu sử dụng **HubSpot** hoặc **Zoho CRM**, có thể thay thế node Salesforce bằng **HubSpot API** hoặc **Zoho API**.

3. **Lưu log cho audit**:
   - Sử dụng **n8n-nodes-base.httpRequest** để gửi log vào **Google Sheets** hoặc **AWS S3** để theo dõi lịch sử.

4. **Tối ưu hóa Prompt**:
   - Nếu AI không trích xuất chính xác, hãy **cập nhật Prompt** trong node `Create User Prompt` để rõ ràng hơn về yêu cầu.

5. **Xử lý lỗi tự động**:
   - Thêm **n8n-nodes-base.if** để kiểm tra lỗi và **retry** tự động nếu API bị lỗi.

6. **Tích hợp với Zoom/Teams**:
   - Nếu muốn phân tích cuộc gọi từ **Zoom** hoặc **Microsoft Teams**, có thể thay thế node Gong.io bằng **Zoom API** hoặc **Teams API**.

---

## 📌 **Kết luận**
**CallForge - 05** là **workflow tự động hóa hoàn chỉnh** để phân tích cuộc gọi bán hàng từ Gong.io, đồng bộ hóa dữ liệu vào **Salesforce, Notion** và sử dụng **Azure AI** để trích xuất thông tin chính xác. Với workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** không cần phân tích thủ công.
✅ **Cải thiện chất lượng dữ liệu** với AI xử lý sai sót.
✅ **Đồng bộ hóa tự động** giữa Sales, Marketing và Product.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (Gong.io, Azure, Salesforce, Notion).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test Run** và bật **Active** để tự động hóa ngay!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/3035) và bắt đầu tự động hóa doanh nghiệp của mình!