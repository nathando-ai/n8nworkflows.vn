---
title: "🚀 Tự Động Hóa Theo Dõi Tin AWS + Tạo Nội Dung LinkedIn Chuyên Nghiệp Với Claude 3 & Feishu (Không Cần Code)"
description: "Workflow tự động hóa thu thập tin tức AWS hàng ngày, phân tích bằng AI Claude 3 Sonnet, lưu trữ trong Feishu Bitable và xuất bản tự động lên LinkedIn sau khi được phê duyệt. Giúp các sếp tiết kiệm 10+ giờ/tháng và xây dựng nội dung chuyên nghiệp 24/7."
slug: "tieu-dong-ho-tin-tuc-aws-va-tao-noi-dung-linkedin"
tags: [n8n, automation, aws, linkedin, ai-claude-3, feishu, content-creation, no-code]
keywords: [tự động hóa tin tức aws, tạo nội dung linkedin tự động, ai claude 3 sonnet, workflow n8n aws, phân tích tin tức bằng ai, feishu bitable tự động hóa]
---

# 🚀 **Tự Động Hóa Theo Dõi Tin AWS + Tạo Nội Dung LinkedIn Chuyên Nghiệp Với Claude 3 & Feishu**

Hiện nay, các sếp trong lĩnh vực **Cloud Computing** phải mất **gần 10 giờ/tuần** để:
- Theo dõi tin tức AWS mới nhất từ các nguồn RSS chuyên nghiệp.
- Phân tích nội dung để rút ra **điểm quan trọng**, **tác động kinh doanh**, và **cách ứng dụng thực tế**.
- Chuyển đổi tin tức thành **nội dung LinkedIn** thu hút, chuyên nghiệp, và phù hợp với brand voice.
- Phê duyệt và xuất bản nội dung một cách thủ công, dễ gây lỗi và mất thời gian.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập** tin tức AWS hàng ngày từ RSS.
✅ **Phân tích bằng AI Claude 3 Sonnet** (mô hình tiên tiến nhất của AWS Bedrock) để tạo **tóm tắt 200 từ**, **đánh giá mức độ quan trọng**, và **phân tích tác động kinh doanh**.
✅ **Lưu trữ trong Feishu Bitable** với hệ thống **phê duyệt thủ công** để đảm bảo chất lượng.
✅ **Tạo và xuất bản tự động** lên LinkedIn khi nội dung được phê duyệt, kèm theo **hashtag chuyên nghiệp** và **call-to-action** hiệu quả.

---
## 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc theo dõi và phân tích tin tức.
- **Nội dung LinkedIn chuyên nghiệp** được tối ưu hóa cho engagement, với **tóm tắt AI**, **phân tích kỹ thuật**, và **gợi ý hashtag**.
- **Phê duyệt thủ công** để đảm bảo chất lượng trước khi xuất bản.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Xây dựng uy tín chuyên môn** với nội dung liên tục, cập nhật và có giá trị.
:::

---
## 🔧 **Yêu cầu cần thiết**

:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
- **Tài khoản AWS** với quyền truy cập **AWS Bedrock** (để sử dụng mô hình Claude 3 Sonnet).
- **Tài khoản Feishu** (để tạo **Bitable** lưu trữ tin tức và **automation webhook**).
- **Tài khoản LinkedIn Developer** (để xuất bản nội dung lên trang công ty).
- **Tài khoản n8n Self-hosted** (do các node Feishu và AWS yêu cầu cài đặt cộng đồng).

### **2. Thiết lập cơ sở hạ tầng**
- **VPS cho n8n** (để chạy 24/7):
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

- **Cài đặt các node cộng đồng**:
  - [`n8n-nodes-feishu-lite`](https://www.npmjs.com/package/n8n-nodes-feishu-lite) (cho Feishu Bitable).
  - [`@n8n/n8n-nodes-langchain`](https://www.npmjs.com/package/@n8n/n8n-nodes-langchain) (cho AI Agent và mô hình Claude 3).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/8733](https://n8n.io/workflows/8733).
- **Bước 2:** Trong **n8n Editor**, chọn **Import** → Chọn file JSON vừa tải.
- **Bước 3:** Xác nhận import và chuyển sang **mode "Edit"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Thiết lập Credentials cho các Node**
| **Node**               | **Credentials cần thiết**               | **Hướng dẫn cấu hình**                                                                 |
|------------------------|------------------------------------------|-----------------------------------------------------------------------------------------|
| **AWS Bedrock Chat**   | `aws` (IAM User với quyền Bedrock)      | - Tạo **IAM User** trong AWS với chính sách `AmazonBedrockFullAccess`.                  |
|                        |                                          | - Tạo **Access Key & Secret Key** và thêm vào n8n dưới **Credentials → AWS**.             |
| **Feishu Bitable**     | `feishuCredentialsApi`                  | - Tạo **Developer App** trên Feishu và cấp quyền **Bitable API**.                     |
|                        |                                          | - Thêm **App ID**, **App Secret**, và **Bot Token** vào n8n dưới **Credentials → Feishu**. |
| **LinkedIn**           | `linkedInOAuth2Api`                     | - Tạo **LinkedIn Developer App** và cấp quyền **Post to Company Page**.              |
|                        |                                          | - Thêm **Client ID**, **Client Secret**, và **Redirect URI** vào n8n.                  |
| **Webhook (Flow 2)**   | Path: `e4878fda-90b9-4503-8410-6ec14a3dc1ed` | - **Không thay đổi path** này, phải giữ nguyên để Feishu webhook hoạt động.          |

#### **🔹 Cấu hình Feishu Bitable**
- **Bước 1:** Tạo **Bitable mới** trên Feishu với cấu trúc bảng như sau:
  | Column Name       | Type      | Required |
  |-------------------|-----------|----------|
  | title             | Text      | ✅        |
  | pubDate           | Date      | ✅        |
  | summary           | Text      | ✅        |
  | keywords          | Text      | ✅        |
  | rating            | Select    | ✅        | (Low/Medium/High) |
  | link              | URL       | ✅        |
  | approval_status   | Select    | ✅        | (Pending/Approved/Rejected) |

- **Bước 2:** Trong **Feishu Automation**, tạo **automation mới**:
  - **Trigger:** "When field value changes" → Chọn `approval_status`.
  - **Condition:** `approval_status equals "Approved"`.
  - **Action:** Gửi **HTTP POST** đến URL webhook trong Flow 2 (không thay đổi path).

#### **🔹 Cấu hình Scheduled Trigger**
- Node **Scheduled Trigger** chạy **mỗi ngày lúc 8h PM** (thời gian Việt Nam).
- **Không cần chỉnh sửa** thời gian này, trừ khi các sếp muốn điều chỉnh.

#### **🔹 Cấu hình RSS Reader**
- Node **RSS Reader** sử dụng **RSS feed AWS chính thức**:
  - Ví dụ: [AWS Blog RSS](https://feeds.awsblog.com/awsblog).
  - **Không cần thay đổi** URL mặc định trong node, trừ khi các sếp muốn theo dõi nguồn khác.

#### **🔹 Cấu hình AI Agent & Claude 3**
- Node **AWS Bedrock Chat Model** sử dụng mô hình `anthropic.claude-3-sonnet-20240229-v1:0`.
- **Prompt mặc định** đã được tối ưu hóa để phân tích tin tức AWS. **Không nên chỉnh sửa** trừ khi các sếp có yêu cầu đặc biệt.

---
### **3. Kích hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với dữ liệu mẫu để kiểm tra:
  - Node **RSS Reader** thu thập được tin tức không?
  - Node **AI Agent** phân tích và tạo ra **summary** và **keywords** không?
  - Node **Feishu Bitable** lưu trữ dữ liệu không?
- **Bước 2:** Sau khi kiểm tra thành công, **bật Active** workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Tối ưu hóa nội dung LinkedIn**
- **Thêm hình ảnh/ảnh minh họa**: Sử dụng node **Image Generation** (nếu cần) để tạo hình ảnh từ tin tức.
- **Kết hợp với Slack/Telegram**: Sau khi xuất bản, gửi thông báo lên Slack/Telegram để đồng bộ đội nhóm.
- **Lưu log hoạt động**: Sử dụng node **Code** để ghi log vào file CSV hoặc database để theo dõi hiệu suất.

### **🔹 Phân tích hiệu quả**
- **Node Code Debugger**: Sử dụng để kiểm tra và debug dữ liệu từ RSS trước khi phân tích.
- **Thêm node Email Notification**: Gửi email báo cáo hàng tuần cho team về tin tức đã xuất bản và phản hồi.

### **🔹 Mở rộng cho nhiều nguồn tin**
- **Thêm RSS feed khác**: Ví dụ: AWS Startups, AWS Events, hoặc tin tức từ các nhà cung cấp Cloud khác (Azure, GCP).
- **Dùng node **Set** để lưu trữ nhiều URL RSS** và chuyển đổi thành một danh sách.

### **🔹 Tích hợp với CRM**
- **Gửi tin tức cho khách hàng VIP**: Sau khi phân tích, gửi tin tức quan trọng cho khách hàng qua email hoặc CRM (HubSpot, Salesforce).

---
## 📌 **Kết luận**

Workflow này không chỉ **tự động hóa toàn bộ quy trình** từ thu thập tin tức đến xuất bản LinkedIn, mà còn **tăng cường chất lượng nội dung** bằng AI Claude 3 Sonnet và **giảm thiểu rủi ro** với hệ thống phê duyệt thủ công.

**Hành động ngay hôm nay:**
1. **Đăng ký VPS** để self-host n8n (mã giảm giá **VPSN8N**).
2. **Thiết lập AWS Bedrock, Feishu, và LinkedIn Developer**.
3. **Import workflow** và chạy thử với dữ liệu mẫu.
4. **Bật Active** và bắt đầu tự động hóa nội dung LinkedIn của mình!

**🚀 Cùng xây dựng nội dung chuyên nghiệp, liên tục và hiệu quả mà không cần code!**