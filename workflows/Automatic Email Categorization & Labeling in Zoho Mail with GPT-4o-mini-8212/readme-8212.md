---
title: "🤖 Tự Động Hóa Phân Loại & Nhãn Email Zoho Mail Với GPT-4o-mini - Giảm 90% Thời Gian Quản Lý Email"
description: "Workflow tự động phân loại và gán nhãn cho email Zoho Mail dựa trên AI GPT-4o-mini, giúp các sếp tự động hóa quản lý email, giảm thiểu rác thải thông tin và tối ưu hóa công việc hàng ngày. Kết quả: Inbox sạch sẽ, email được phân loại chính xác theo chủ đề (Hỗ trợ, Tài chính, HR, Leads...) chỉ trong vài giây."
slug: "tieu-dong-hoa-phan-loai-nhan-email-zoho-mail-gpt-4o-mini"
tags: [n8n, automation, zoho-mail, ai-summarization, gpt-4o-mini, text-classification, no-code]
keywords: [tự động hóa email zoho, phân loại email bằng ai, gpt-4o-mini n8n, quản lý email tự động, nhãn email zoho, workflow n8n zoho mail]
---

# 🚀 **Tự Động Hóa Phân Loại & Nhãn Email Zoho Mail Với GPT-4o-mini**

### **Giải pháp AI cho các sếp quản lý email bị ngập tràn**
Hàng ngày, các sếp phải mất **từ 1-2 tiếng** để phân loại, đánh nhãn và chuyển tiếp email giữa các bộ phận (Hỗ trợ, Tài chính, HR, Leads...). Kết quả? **Inbox bị rối loạn, thông tin quan trọng bị bỏ qua, và hiệu suất công việc giảm sút.**

Workflow này **sử dụng AI GPT-4o-mini** để tự động phân loại email mới vào Zoho Mail và gán nhãn phù hợp, giúp các sếp:
✅ **Tiết kiệm 90% thời gian** quản lý email.
✅ **Giảm rác thải thông tin** với hệ thống nhãn tự động.
✅ **Tối ưu hóa công việc** bằng cách tự động chuyển tiếp email đến bộ phận đúng.
✅ **Không cần code** – chỉ cần cấu hình và chạy.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn tài nguyên của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân loại email** theo chủ đề (Hỗ trợ, Tài chính, HR, Leads...) chỉ trong **vài giây**.
- **Gán nhãn AI chính xác** với độ chính xác cao (thông qua GPT-4o-mini).
- **Giảm thiểu rác thải thông tin** bằng cách loại bỏ email không quan trọng.
- **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.
- **Kết hợp với Slack/Telegram** để thông báo email mới (mẹo nâng cao).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Zoho Mail** với **API access** được kích hoạt.
2. **Zoho OAuth Credentials** (để lấy token truy cập).
3. **API Key OpenRouter** (để sử dụng mô hình GPT-4o-mini).
4. **Thiết lập IMAP** cho Zoho Mail (để workflow đọc email mới).
5. **Danh sách nhãn (labels) sẵn sàng** trong Zoho Mail (ví dụ: "Support", "Billing", "HR", "Leads").
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8212](https://n8n.io/workflows/8212) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8212) và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **15 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu hình Zoho Mail (Bắt buộc)**
| Node | Thao tác cần làm |
|------|------------------|
| **Get Access Token** | Điền **Zoho OAuth Credentials** (tạo từ [Zoho Developer Console](https://api-console.zoho.com/)). |
| **Set Account ID** | Nhập **Account ID** của Zoho Mail (thường là email của bạn). |
| **Get Labels** | Node này tự động lấy danh sách nhãn từ Zoho Mail. **Không cần chỉnh**. |
| **Label name to ID map** (Node Code) | **Không cần chỉnh**, node này tự động tạo bản đồ từ tên nhãn → ID nhãn. |

##### **B. Cấu hình AI (GPT-4o-mini)**
| Node | Thao tác cần làm |
|------|------------------|
| **OpenRouter Chat Model** | Điền **API Key OpenRouter** vào **credentials** (`openRouterApi`). |
| **Text Classifier** | Node này sử dụng mô hình GPT-4o-mini để phân loại email. **Không cần chỉnh**, nhưng các sếp có thể tùy chỉnh **prompt** trong node này nếu muốn. |

##### **C. Phân loại & Gán nhãn**
| Node | Thao tác cần làm |
|------|------------------|
| **Set Support Category** | Node này **không hoạt động** mặc định (để test). Sau khi test thành công, các sếp **bật node** này và các node tương tự (`Billing`, `HR`, `Leads`). |
| **Add Label to the email** | **Bật node này** sau khi đã test thành công để tự động gán nhãn cho email. |

##### **D. Test Run Trước Khi Bật**
- **Không bật node "Add Label to the email"** khi test đầu tiên.
- **Sử dụng test data** (email mẫu) để kiểm tra phân loại.
- **Kiểm tra log** trong node **Merge** để xem AI phân loại như thế nào.

#### **3. Kích hoạt ⚡️**
1. **Test run** với email mẫu (ví dụ: email hỗ trợ, email tài chính).
2. **Bật node "Add Label to the email"** sau khi xác nhận phân loại chính xác.
3. **Bật workflow** và **chờ email mới** để test tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo email mới được phân loại.
   - Ví dụ: *"Email mới từ [Tên Khách Hàng] đã được phân loại vào nhãn 'Hỗ trợ'."*

2. **Lưu log phân loại**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử phân loại.
   - Giúp các sếp **theo dõi hiệu suất** của AI.

3. **Tùy chỉnh prompt AI**
   - Trong node **Text Classifier**, các sếp có thể **sửa prompt** để AI phân loại chính xác hơn.
   - Ví dụ:
     ```json
     "prompt": "Phân loại email này vào một trong các nhãn sau: 'Support', 'Billing', 'HR', 'Leads'. Nếu email không thuộc bất kỳ nhãn nào, trả về 'Uncategorized'."
     ```

4. **Sử dụng nhiều mô hình AI**
   - Thay thế GPT-4o-mini bằng **mô hình khác** (ví dụ: Mistral, Llama) nếu OpenRouter không phù hợp.

5. **Tự động chuyển tiếp email**
   - Thêm node **Zoho Mail Forward** để chuyển email vào folder riêng (ví dụ: "Support", "Billing").
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhàn nhạt là phân loại email, đồng thời **tăng cường hiệu quả công việc** với AI GPT-4o-mini. **Chỉ cần 10 phút cấu hình**, các sếp đã có thể **tự động hóa 90% công việc quản lý email**.

👉 **Bắt đầu ngay!**
1. Import workflow.
2. Cấu hình Zoho OAuth và OpenRouter API.
3. Test với email mẫu.
4. **Bật tự động hóa!**

**Hãy chia sẻ kết quả của bạn trong comment dưới đây!** 🚀