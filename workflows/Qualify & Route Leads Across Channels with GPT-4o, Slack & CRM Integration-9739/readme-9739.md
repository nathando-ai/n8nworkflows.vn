---
title: "🚀 Tự Động Hóa Xác Minh & Phân Loại Lead Tự Động Với GPT-4o, Slack & CRM (HubSpot/Salesforce) - Không Cần Code!"
description: "Workflow này tự động nhận lead từ email, form, phân tích nội dung bằng AI GPT-4o, tính điểm lead, phân loại theo khu vực và tự động chuyển đến HubSpot/Salesforce + thông báo Slack. Giúp các sếp tiết kiệm 10+ giờ/năm và giảm thiểu lead rớt."
slug: "tu-dong-hoa-xac-minh-phan-loai-lead-voi-gpt-4o-slack-crm"
tags: [n8n, automation, lead-nurturing, ai-summarization, crm-integration, gpt-4o, slack, hubspot, salesforce]
keywords: [tự động hóa lead, phân loại lead bằng AI, n8n workflow, CRM tự động, GPT-4o tự động hóa, lead scoring, Slack notification]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead Tự Động Với GPT-4o, Slack & CRM**

## **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Làm thủ công** kiểm tra hàng chục lead từ email, form website, hoặc CRM.
- **Phân loại lead** dựa trên thông tin mơ hồ, mất thời gian và dễ sai sót.
- **Chuyển lead** đến bộ phận phù hợp (Sales, Marketing) mà không có tiêu chí rõ ràng.
- **Đợi AI** để tổng hợp thông tin lead, mất thời gian và chi phí cao.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận lead** từ email (Gmail) hoặc form webhook.
✅ **Phân tích lead** bằng GPT-4o, tính điểm lead (0-100) dựa trên ngành nghề, quy mô doanh nghiệp, vị trí, vấn đề và ngân sách.
✅ **Phân loại lead** theo khu vực (territory) và chuyển tự động đến **HubSpot** hoặc **Salesforce**.
✅ **Gửi thông báo Slack** cho team Sales khi có lead mới phù hợp.
✅ **Lưu log** lead thành công và thất bại vào **Google Sheets** để theo dõi.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/năm** không phải làm thủ công phân loại lead.
- **Tăng độ chính xác** lên 95% nhờ AI phân tích tự động.
- **Cá nhân hóa lead** với điểm số (lead score) giúp Sales ưu tiên lead có tiềm năng cao.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Kết nối nhiều kênh** (email, form, Slack, CRM) vào một hệ thống duy nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **Gmail**: Tạo **Service Account** (để trigger từ email) hoặc sử dụng **Gmail API** (cần quyền truy cập vào email doanh nghiệp).
   - **Google Sheets**: Tạo **2 sheet riêng biệt**:
     - **Sheet "Leads"** (để lưu lead thành công).
     - **Sheet "Failed Leads"** (để lưu lead không hợp lệ).
   - **OpenAI API Key**: Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - **HubSpot/Salesforce**:
     - Tạo **API Key** (Developer App) trong HubSpot hoặc Salesforce.
     - Chọn **CRM phù hợp** (HubSpot hoặc Salesforce, không thể dùng cả hai cùng lúc).
   - **Slack**:
     - Tạo **App Slack** và lấy **Bot Token** (để gửi thông báo).
     - Chọn **Channel Slack** để nhận thông báo lead mới.
2. **Dữ liệu mẫu (nếu test)**:
   - Một email mẫu từ khách hàng (nếu dùng trigger Gmail).
   - Một form webhook mẫu (nếu dùng Form Submission).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/9739](https://n8n.io/workflows/9739) (chọn "Export").
2. **Mở n8n Editor** (n8n.io) → **Import** → Chọn file JSON vừa tải.
3. **Chọn phiên bản n8n** phù hợp (n8n 1.x hoặc 2.x, tùy vào phiên bản của bạn).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/9739](https://n8n.io/workflows/9739) (chọn "Export" → "Copy JSON").
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON**.
3. **Xác nhận import** và chuyển sang tab **Configuration**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 phần chính** cần cấu hình kỹ lưỡng:

#### **🟡 Intake & Configuration (Nhận Dữ liệu & Cấu Hình)**
| **Node**               | **Cần Chỉnh Gì?**                                                                 | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Email Trigger**      | Chọn **Gmail Trigger** → Cấu hình:                                             | - Chọn **Event Type**: "New Email" (hoặc "New Email in Inbox").          |
|                        | - **Label**: Chọn nhãn email cần theo dõi (ví dụ: "Leads").                     | - **Thêm điều kiện**: Nếu muốn chỉ lấy email từ người gửi cụ thể, thêm **filter** trong node `code`. |
| **Form Submission**    | Chọn **Webhook** → Điền **Path**: `648db646-76c1-44b4-bab0-5955971721e5` (không đổi). | - **Test Webhook**: Sau khi import, mở tab **Webhooks** trong n8n → **Test** với payload mẫu. |
| **Merge Inputs**       | Kiểm tra **Merge Strategy**: "Array" (để gộp email và form).                   | - Nếu chỉ dùng email, có thể bỏ qua node này.                             |
| **Workflow Configuration** | Điền **các trường sau**:                                                   | - **CRM Type**: Chọn **HubSpot** hoặc **Salesforce** (không thể đổi sau). |
|                        | - **HubSpot/Salesforce API Key** (từ Developer App).                          | - **Slack Channel ID** (tìm trong Slack App Settings → Features → Slack Channel). |
|                        | - **Google Sheets ID** (tìm trong Google Sheets → Share → "Copy link" → ID sau `/d/`). | - **OpenAI API Key** (từ OpenAI Dashboard).                              |
|                        | - **Lead Score Threshold** (giá trị mặc định: **50**, có thể điều chỉnh).       | - **Territory Mapping** (nếu cần phân vùng, điền theo định dạng: `{"Vietnam": "Asia", "USA": "North America"}`). |

#### **🧠 AI Extraction & Scoring (Phân Tích & Tính Điểm Lead)**
| **Node**               | **Cần Chỉnh Gì?**                                                                 | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Validate Input Data** | Kiểm tra **code** trong node (nếu có sai sót, sửa để phù hợp với dữ liệu của bạn). | - Nếu lead thiếu trường bắt buộc (ví dụ: `company`, `budget`), nó sẽ bị log vào **Failed Leads**. |
| **Extract Lead Data with AI** | Điền **Prompt AI** trong node OpenAI: | - **Prompt mẫu** (có thể chỉnh sửa): |
|                        | > "Analyze the following lead data and extract key details:
> - Company: [company]
> - Size: [size]
> - Industry: [industry]
> - Role: [role]
> - Problem: [problem]
> - Region: [region]
> - Budget: [budget]
> Return JSON with structured data and a lead score (0-100) based on the following criteria:
> - High budget (100-500k) = +30
> - Mid-size company (50-500 employees) = +20
> - Clear problem statement = +25
> - Sales role = +15
> - Asia region = +10
> Format response as:
> ```json
> {
>   "company": "[extracted_company]",
>   "size": "[extracted_size]",
>   "industry": "[extracted_industry]",
>   "role": "[extracted_role]",
>   "problem": "[extracted_problem]",
>   "region": "[extracted_region]",
>   "budget": "[extracted_budget]",
>   "lead_score": [calculated_score]
> }
> ```" | - **Model**: Chọn **GPT-4o** (hoặc GPT-4 nếu không có).                          |
|                        | - **Temperature**: 0.7 (để AI không quá ngẫu nhiên).                            | - **Test AI**: Gửi một lead mẫu vào node `webhook` → Kiểm tra output AI.   |
| **Calculate Lead Score** | Kiểm tra **code** tính điểm (nếu cần chỉnh sửa logic).                         | - Điểm tối đa là **100**, tối thiểu **0**.                                |

#### **📨 Routing & Notifications (Phân Loại & Thông Báo)**
| **Node**               | **Cần Chỉnh Gì?**                                                                 | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Route by Territory** | Chọn **Switch Case** → Điền **mapping territory** (ví dụ: `{{$node["Workflow Configuration"].json["territoryMapping"]["Vietnam"]}}`). | - Nếu không cần phân vùng, có thể bỏ qua node này.                      |
| **Create HubSpot Contact** | Điền **API Key HubSpot** và **mapping fields** (ví dụ: `email` → `email`, `name` → `firstName`). | - **Test HubSpot**: Chạy một lead mẫu → Kiểm tra trong HubSpot.          |
| **Create Salesforce Lead** | Điền **API Key Salesforce** và **mapping fields** (tương tự HubSpot).           | - **Test Salesforce**: Chạy một lead mẫu → Kiểm tra trong Salesforce.     |
| **Post to Slack**      | Điền **Slack Token** và **Channel ID**.                                            | - **Message Template**: Có thể chỉnh sửa để thông báo chi tiết hơn.      |
| **Log to Google Sheets** | Điền **Google Sheets ID** và **sheet name**: "Leads".                            | - **Columns**: Đảm bảo sheet có cột: `email`, `name`, `company`, `lead_score`, `createdAt`. |
| **Log Failed Leads**   | Điền **Google Sheets ID** và **sheet name**: "Failed Leads".                       | - **Columns**: Đảm bảo sheet có cột: `email`, `error`, `timestamp`.       |

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra không có lỗi):
   - Chọn **Run Workflow** → Chọn **Email Trigger** hoặc **Form Submission Webhook**.
   - Gửi một **lead mẫu** (ví dụ: email hoặc payload JSON).
   - Kiểm tra:
     - **Slack**: Có thông báo lead mới không?
     - **HubSpot/Salesforce**: Có lead mới được tạo không?
     - **Google Sheets**: Lead được log vào "Leads" hay "Failed Leads"?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Workflow Status** từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với ZoomInfo/Apollo**:
   - Thêm node **ZoomInfo API** để enrich lead với thông tin công ty chi tiết (ví dụ: size, revenue).
   - **Cách làm**: Sử dụng node `httpRequest` để gọi API ZoomInfo và merge vào lead trước khi chuyển đến CRM.

2. **Gửi Email Tự Động Cho Lead**:
   - Thêm node **Gmail Send Email** sau khi lead được tạo trong HubSpot/Salesforce.
   - **Template Email**: Sử dụng **node `code`** để động thái hóa email (ví dụ: chào tên lead, đề cập đến vấn đề của họ).

3. **Báo Cáo Định Kỳ**:
   - Thêm node **Google Sheets** để tạo **báo cáo hàng tuần/monthly** về lead score, territory, và ROI.
   - **Cách làm**: Sử dụng **node `schedule`** (n8n Pro) hoặc **Google Calendar Trigger** để chạy báo cáo tự động.

4. **Phân Loại Lead Theo Ngành Nghề**:
   - Tăng cường **prompt AI** để phân loại lead theo ngành (ví dụ: Fintech, E-commerce) và chuyển đến bộ phận chuyên biệt.
   - **Ví dụ**: Nếu lead là ngành **Fintech**, chuyển đến team Sales Fintech trong HubSpot.

5. **Lưu Log AI Response**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu **tất cả response AI** (để review sau).
   - **Cách làm**: Sử dụng node `set` để lưu response vào biến, rồi append vào Google Drive.

6. **Tích Hợp với Zapier/Make**:
   - Nếu không muốn tự host n8n, có thể chạy workflow trên **n8n Cloud** (miễn phí cho 1 workflow).
   - **Lưu ý**: Một số node như **Salesforce** hoặc **Google Sheets** có giới hạn trên n8n Cloud.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa 100% quá trình nhận, phân tích và phân loại lead**.
✔ **Tiết kiệm thời gian** để tập trung vào việc bán hàng chứ không phải làm thủ công.
✔ **Tăng hiệu quả Sales** nhờ lead được đánh giá và phân loại chính xác.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với lead mẫu** trước khi chuyển sang hoạt động thực tế.
3. **Bật Active** và để nó chạy