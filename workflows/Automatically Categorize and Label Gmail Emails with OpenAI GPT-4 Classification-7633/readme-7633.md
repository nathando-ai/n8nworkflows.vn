---
title: "🚀 Tự Động Phân Loại & Gắn Nhãn Email Gmail bằng OpenAI GPT‑5"
description: "Workflow n8n tự động lấy email mới, dùng GPT‑5 phân loại và gắn nhãn (Ưu tiên, Cá nhân, Khuyến mãi) chỉ trong vài giây, không cần viết code."
slug: "tu-dong-phan-loai-email-gmail-openai"
tags: [n8n, automation, no-code, AI, Gmail, OpenAI]
keywords: [n8n workflow, tự động hóa, phân loại email, OpenAI GPT, Gmail label]
---

# 🚀 Tự Động Phân Loại & Gắn Nhãn Email Gmail bằng OpenAI GPT‑5

Bạn có bao giờ mở Gmail và thấy hàng trăm email lộn xộn, phải mất thời gian lọc “ưu tiên”, “cá nhân” hay “khuyến mãi”?  
Việc làm này không chỉ tốn công sức mà còn dễ bỏ sót những email quan trọng.  
**Workflow này** sẽ giải quyết hoàn toàn vấn đề: mỗi 5 phút, n8n sẽ tự động kéo 10 email mới nhất, dùng mô hình GPT‑5 phân loại và gắn nhãn tương ứng ngay trong Gmail – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải mở Gmail, đọc, rồi tự gắn nhãn.  
- **Độ chính xác cao**: AI phân loại dựa trên nội dung tiêu đề + thân email.  
- **Inbox luôn gọn gàng**: Email được tự động xếp vào “Ưu tiên”, “Cá nhân”, “Khuyến mãi”.  
- **Hoạt động liên tục**: Chạy mỗi 5 phút, không ngừng cập nhật.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Gmail** (có quyền OAuth2 để đọc và gắn nhãn).  
- **API Key OpenAI** (đăng ký tại https://platform.openai.com).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Credentials** trong n8n:  
  - `gmailOAuth2` – kết nối Gmail.  
  - `openAiApi` – kết nối OpenAI.  
- **Label trong Gmail**: tạo trước các nhãn “IMPORTANT”, “CATEGORY_PERSONAL”, “CATEGORY_PROMOTIONS” (hoặc tùy chỉnh).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc https://n8n.io/workflows/7633) hoặc sao chép nội dung JSON.  
2. Vào **n8n Editor → Import → From File** (hoặc **From Clipboard**) và dán JSON.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|--------|
| **Schedule Trigger** | `Every 5 minutes` (hoặc tùy ý) | Đảm bảo không gây quá tải API Gmail. |
| **Gmail - Get Emails** | - **Operation**: `getAll` <br> - **Maximum Results**: `10` <br> - **Query**: `newer_than:5m` | Lấy tối đa 10 email trong 5 phút qua. |
| **Loop Over Items** (splitInBatches) | **Batch Size**: `1` | Xử lý từng email một để AI phân loại chính xác. |
| **Label Classifier** (textClassifier) | - **Model**: `OpenAI Chat Model` (được liên kết ở node phía dưới) <br> - **Categories**: `High Priority`, `Personal`, `Promotions` (có thể đổi tên) <br> - **Prompt**: “Phân loại email này thành một trong các danh mục: High Priority, Personal, Promotions. Trả về chỉ tên danh mục.” | Đây là “trí tuệ” quyết định nhãn. |
| **OpenAI Chat Model** | - **Credentials**: `openAiApi` <br> - **Model**: `gpt-5` (hoặc `gpt-4` nếu chưa có quyền gpt‑5) | Đảm bảo quota API đủ. |
| **Add Label (High Priority)** | - **Operation**: `addLabels` <br> - **Resource**: `thread` <br> - **Label ID**: ID của nhãn “IMPORTANT” | Lấy ID nhãn từ Gmail → Settings → Labels → “Manage labels”. |
| **Add Label (Personal)** | Tương tự, **Label ID** của “CATEGORY_PERSONAL”. |
| **Add Label (Promotions)** | Tương tự, **Label ID** của “CATEGORY_PROMOTIONS”. |
| **Sticky Note** (nếu có) | Dùng để ghi chú nội bộ, không ảnh hưởng workflow. | Tùy chọn. |

> **⚠️ Lưu ý quan trọng:**  
> - Đảm bảo **các node Add Label** được nối sau node `Label Classifier` bằng **IF** hoặc **Switch** dựa trên giá trị `category` trả về.  
> - Kiểm tra **quota** OpenAI và **limit** Gmail API (5000 yêu cầu/ngày cho tài khoản cá nhân).  

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra với dữ liệu mẫu.  
2. Kiểm tra Gmail: các email mới nhất đã được gắn nhãn đúng.  
3. Bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: dùng node `Slack` hoặc `Telegram` để gửi thông báo khi email được gắn nhãn “High Priority”.  
- **Lưu log vào Google Sheets**: mỗi lần phân loại, ghi lại `emailId`, `subject`, `category`, `timestamp`.  
- **Tùy chỉnh Prompt**: bổ sung ví dụ mẫu trong `Label Classifier` để AI hiểu ngữ cảnh doanh nghiệp (ví dụ: “Email từ HR → Personal”).  
- **Mở rộng nhãn**: Thêm các node `Add Label` cho các danh mục khác như “Finance”, “Support”.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **đánh tan nỗi lo inbox hỗn loạn**, giảm thời gian xử lý email xuống mức tối thiểu và luôn luôn có hộp thư được sắp xếp thông minh. Hãy triển khai ngay trên n8n, tùy chỉnh nhãn và danh mục phù hợp với doanh nghiệp của bạn – và để AI làm phần còn lại! 🚀