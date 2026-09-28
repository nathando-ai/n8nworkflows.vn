---
title: "🚀 Tự Động Hóa Xác Minh & Phân Loại Lead Tư Vấn Với GPT-4.1-mini, Slack & Google Sheets - Không Cần Code!"
description: "Workflow tự động nhận lead từ form, phân loại chất lượng bằng AI, phân phối ngay cho đội ngũ phù hợp và gửi email xác nhận tự động - tiết kiệm 80% thời gian làm thủ công."
slug: "tieu-dong-hoa-xac-minh-phan-loai-lead-tu-vien-tu-vấn"
tags: [n8n, automation, ai-automation, lead-generation, google-sheets, slack-integration]
keywords: [tự động hóa lead tư vấn, phân loại lead bằng AI, n8n workflow, tự động hóa email, Slack alert]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead Tư Vấn Với AI - Không Cần Code!**

### **Giải pháp cho các sếp bị "ngập" lead không chất lượng**
Bạn đã bao giờ phải:
- **Làm thủ công** phân loại hàng trăm lead mỗi ngày?
- **Mất thời gian** xác định lead nào thực sự có giá trị?
- **Phân phối lead** cho đội ngũ không đúng dịch vụ?
- **Quên gửi email xác nhận** cho khách hàng?

Workflow này **tự động hóa toàn bộ quy trình** từ nhận lead đến phân loại, phân phối và gửi email - **không cần viết một dòng code nào!** Dùng AI GPT-4.1-mini phân loại lead, Slack thông báo ngay cho đội ngũ phù hợp, và Google Sheets lưu trữ dữ liệu chi tiết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** làm thủ công phân loại lead.
✅ **Chọn lead chất lượng** bằng AI (GPT-4.1-mini) với độ chính xác cao.
✅ **Phân phối tự động** lead cho đội ngũ tư vấn, kế toán hoặc Fractional CFO phù hợp.
✅ **Gửi email xác nhận** tự động cho khách hàng (không quên nữa!).
✅ **Lưu trữ lead** trên Google Sheets với định dạng chuyên nghiệp.
✅ **Thông báo Slack** ngay khi có lead mới hoặc lead ưu tiên cao.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Gmail).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini).
3. **Credentials Slack** (để gửi thông báo).
4. **Form nhận lead** (có thể là Typeform, Google Form hoặc Webhook trực tiếp).
5. **Google Sheet** đã tạo sẵn với cấu trúc dữ liệu phù hợp (các sếp sẽ được hướng dẫn chi tiết).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12761](https://n8n.io/workflows/12761) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **17 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node "Client Intake Form" (Webhook)**
- **Cấu hình:**
  - Chọn **HTTP Trigger** (Webhook).
  - Đặt **URL** để nhận dữ liệu từ form (ví dụ: `https://của-bạn.n8n.cloud/webhook/lead-form`).
  - **Lưu ý:** Các sếp cần **bật CORS** nếu form từ bên ngoài.

##### **🔹 Node "Workflow Configuration" (Set)**
- **Cấu hình:**
  - Điền **tên dịch vụ** (Consulting, Accounting, Fractional CFO) và **mức độ ưu tiên** (Low/Medium/High).
  - Ví dụ:
    ```json
    {
      "serviceType": "Consulting",
      "priority": "Medium"
    }
    ```

##### **🔹 Node "OpenAI Model - Lead Classifier" (lmChatOpenAi)**
- **Cấu hình:**
  - **API Key OpenAI:** Điền vào **Credentials** trong n8n.
  - **Model:** Chọn **gpt-4.1-mini** (rẻ và hiệu quả).
  - **Prompt:** Sử dụng **Lead Classification Schema** (node tiếp theo) để AI phân loại lead.
  - **Lưu ý:** Nếu API Key hết hạn, workflow sẽ **ngừng hoạt động**.

##### **🔹 Node "Lead Classification Schema" (outputParserStructured)**
- **Cấu hình:**
  - Định nghĩa **schema** cho AI phân loại lead:
    ```json
    {
      "type": "object",
      "properties": {
        "isQualified": { "type": "boolean" },
        "serviceType": { "type": "string" },
        "priority": { "type": "string" }
      }
    }
    ```
  - **Lưu ý:** Schema này **phải khớp** với yêu cầu phân loại lead của doanh nghiệp.

##### **🔹 Node "AI Lead Classifier" (Agent)**
- **Cấu hình:**
  - Chọn **OpenAI** làm provider.
  - **Prompt:** Sử dụng template mặc định hoặc tùy chỉnh:
    ```
    "Analyze the lead data and classify it into:
    - Service Type: Consulting/Accounting/Fractional CFO
    - Priority: Low/Medium/High
    - Is Qualified: true/false"
    ```

##### **🔹 Node "Filter Lead Quality" (If)**
- **Cấu hình:**
  - **Điều kiện:** `{{ $json["isQualified"] }} === true`
  - **Nếu true:** Lead được phân loại là chất lượng, tiến hành phân phối.
  - **Nếu false:** Lead bị loại bỏ (có thể gửi email từ chối tự động).

##### **🔹 Node "Route by Service Type" (Switch)**
- **Cấu hình:**
  - **Case 1:** `{{ $json["serviceType"] }} === "Consulting"` → Gửi đến **Notify Team - Consulting**.
  - **Case 2:** `{{ $json["serviceType"] }} === "Accounting"` → Gửi đến **Notify Team - Accounting**.
  - **Case 3:** `{{ $json["serviceType"] }} === "Fractional CFO"` → Gửi đến **Notify Team - Fractional CFO**.

##### **🔹 Node "Notify Team - [Service]" (Slack)**
- **Cấu hình:**
  - **Credentials Slack:** Điền **Token** từ Slack API.
  - **Channel:** Chọn channel phù hợp (ví dụ: `#consulting-leads`).
  - **Message Template:**
    ```
    "🚀 **New Lead - {{ $json["serviceType"] }}**
    - **Name:** {{ $json["name"] }}
    - **Email:** {{ $json["email"] }}
    - **Priority:** {{ $json["priority"] }}"
    ```

##### **🔹 Node "Log Qualified Lead" (Google Sheets)**
- **Cấu hình:**
  - **Credentials Google:** Đăng nhập và cấp quyền.
  - **Sheet Name:** Chọn sheet đã tạo sẵn (ví dụ: `Lead Database`).
  - **Range:** `A1` (để ghi dữ liệu từ hàng đầu tiên).
  - **Data:** Chọn tất cả trường từ lead (name, email, serviceType, priority...).

##### **🔹 Node "OpenAI Model - Email Writer" (lmChatOpenAi)**
- **Cấu hình:**
  - **Prompt:** Sử dụng template để tạo email xác nhận:
    ```
    "Create a professional email acknowledging the lead's inquiry.
    - **Subject:** Thank you for your inquiry about {{ $json["serviceType"] }}
    - **Body:** [Template xác nhận]"
    ```

##### **🔹 Node "Send Acknowledgment Email" (Gmail)**
- **Cấu hình:**
  - **Credentials Gmail:** Đăng nhập và cấp quyền.
  - **From:** Địa chỉ email của doanh nghiệp.
  - **To:** `{{ $json["email"] }}`
  - **Subject:** `{{ $json["subject"] }}` (tự động lấy từ lead).

##### **🔹 Node "Check High Urgency" (If)**
- **Cấu hình:**
  - **Điều kiện:** `{{ $json["priority"] }} === "High"`
  - **Nếu true:** Gửi **Executive Alert** trên Slack.

##### **🔹 Node "Executive Alert - High Urgency" (Slack)**
- **Cấu hình:**
  - **Channel:** `#executive-alerts` (hoặc channel ưu tiên cao).
  - **Message:**
    ```
    "⚠️ **HIGH URGENCY LEAD**
    - **Name:** {{ $json["name"] }}
    - **Service:** {{ $json["serviceType"] }}
    - **Email:** {{ $json["email"] }}"
    ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một lead mẫu qua **Webhook** và kiểm tra:
     - AI có phân loại đúng không?
     - Slack có thông báo không?
     - Email có gửi được không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Zapier/Integromat** để nhận lead từ nhiều nguồn (Facebook, LinkedIn, Website).
2. **Lưu log hoạt động** trên Google Sheets để theo dõi hiệu suất.
3. **Tự động gửi báo cáo hàng tuần** về lead mới qua email (sử dụng **n8n + Gmail**).
4. **Cài đặt AI Agent** để tự động trả lời lead không chất lượng (ví dụ: "Xin lỗi, chúng tôi không hỗ trợ dịch vụ này").
5. **Sử dụng Google Analytics** để theo dõi nguồn lead hiệu quả nhất.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **tăng chất lượng lead** nhờ AI. **Không cần code**, chỉ cần **cài đặt và chạy** là xong!

👉 **Bắt đầu ngay:**
1. **Import workflow** từ [n8n.io/workflows/12761](https://n8n.io/workflows/12761).
2. **Cấu hình các node** theo hướng dẫn trên.
3. **Bật Active** và **nhận lead tự động**!

**Nếu có vấn đề**, các sếp có thể tham khảo [hỗ trợ n8n](https://community.n8n.io/) hoặc liên hệ với tôi để được hỗ trợ chi tiết! 🚀

---
**#TựĐộngHóa #LeadGeneration #AIAutomation #n8n #NoCode**