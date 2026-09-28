---
title: "📄 Tự Động Hóa Phân Tích Rủi Ro Hợp Đồng PDF Với Form, AI Gemini, Google Sheets & Slack - Không Cần Code!"
description: "Workflow tự động hóa phân tích rủi ro trong hợp đồng PDF bằng Google Gemini, lưu kết quả vào Google Sheets và gửi cảnh báo Slack khi phát hiện rủi ro cao. Giúp các sếp tiết kiệm thời gian kiểm tra thủ công và giảm thiểu lỗ hổng pháp lý."
slug: "tieu-dong-hoa-phan-tich-rui-ro-hop-dong-pdf"
tags: [n8n, automation, no-code, google-gemini, google-sheets, slack-integration, ai-summarization]
keywords: [tự động hóa hợp đồng PDF, phân tích rủi ro hợp đồng, Google Gemini n8n, lưu hợp đồng vào Google Sheets, cảnh báo Slack tự động]
---

# 🚀 **Tự Động Hóa Phân Tích Rủi Ro Hợp Đồng PDF Với AI Gemini, Google Sheets & Slack**

Hiện nay, việc kiểm tra và phân tích hợp đồng PDF thủ công không chỉ tốn thời gian mà còn dễ bị bỏ sót các điều khoản rủi ro như điều kiện bất lợi, thiếu bảo vệ pháp lý hoặc các khoản phí ẩn. **Workflow này tự động hóa toàn bộ quy trình**, từ upload hợp đồng đến phân tích bằng AI Google Gemini, lưu kết quả vào Google Sheets và gửi cảnh báo Slack khi phát hiện rủi ro cao. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra từng hợp đồng thủ công.
- **Chính xác cao**: AI Google Gemini phát hiện rủi ro mà con người có thể bỏ sót.
- **Lưu trữ tự động**: Tất cả kết quả phân tích được lưu vào Google Sheets theo định kỳ.
- **Cảnh báo kịp thời**: Nhận thông báo Slack khi hợp đồng có rủi ro cao (score > 7).
- **Cá nhân hóa**: Đặt cài đặt riêng cho từng loại hợp đồng (ví dụ: tập trung vào điều khoản bảo mật).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Gemini API** (miễn phí với free tier).
2. **Google Sheets**:
   - Tạo một bảng mới tên là **"Contract Reviews"** (cấu trúc sẽ được tự động tạo khi chạy workflow đầu tiên).
   - Cung cấp quyền truy cập cho n8n (đăng ký OAuth 2.0).
3. **Slack Workspace**:
   - Tạo một channel riêng để nhận cảnh báo (ví dụ: `#contract-alerts`).
   - Cung cấp **API Token Slack** (tạo tại [API Apps Slack](https://api.slack.com/apps)).
4. **Form Upload PDF**:
   - Sử dụng node **Form Trigger** để tạo liên kết upload hợp đồng (sẽ được hướng dẫn chi tiết dưới đây).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow đã được chia sẻ trên [n8n Community](https://n8n.io/workflows/13671). Các sếp có thể:
- **Tải JSON** và import vào n8n Editor:
  1. Mở n8n Editor.
  2. Nhấn **Import Workflow** → Chọn file JSON tải từ link trên.
  3. Hoặc **Copy/Paste JSON** từ [đây](https://n8n.io/workflows/13671) vào Editor (nhấn **Import** ở góc trên bên phải).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node** chính. Dưới đây là hướng dẫn cấu hình chi tiết:

##### **A. Upload Contract Form (formTrigger)**
- **Cách hoạt động**: Tạo một liên kết upload PDF cho đội ngũ pháp lý.
- **Lưu ý**:
  - Node này sẽ tự động tạo một form upload. Các sếp **không cần chỉnh sửa gì** ngoài việc chia sẻ liên kết form với team.
  - **Lưu ý quan trọng**: Sau khi import, nhấn **Run** để tạo liên kết form. Sau đó, copy liên kết này để chia sẻ với người dùng (ví dụ: `https://your-n8n-instance.com/form/76d78a1e-7b97-47eb-94a4-48ee4ae35635`).

##### **B. Extract PDF Text (code)**
- **Cách hoạt động**: Trích xuất văn bản từ file PDF upload.
- **Lưu ý**:
  - Node này sử dụng **Python** để extraxt text. **Không cần chỉnh sửa** nếu đã import JSON chính xác.
  - Nếu gặp lỗi, kiểm tra **credentials** của node **Form Trigger** đã được cấu hình đúng.

##### **C. Analyze Contract (chainLlm) + Gemini Chat Model (lmChatGoogleGemini)**
- **Cách hoạt động**: Google Gemini phân tích hợp đồng và đánh giá rủi ro (score 1-10).
- **Lưu ý**:
  1. **Cấu hình API Key Google Gemini**:
     - Đăng ký tại [Google AI Studio](https://aistudio.google.com/).
     - Copy **API Key** và thêm vào **Credentials** của node `lmChatGoogleGemini`:
       - Nhấn **Add Credential** → Chọn **Google Gemini** → Điền API Key.
  2. **Chỉnh sửa Prompt (nếu cần)**:
     - Mở node `Analyze Contract` → Tab **Code** → Sửa phần `prompt` để tập trung vào loại rủi ro cụ thể (ví dụ: điều khoản bảo mật, thời hạn hợp đồng).
     - Ví dụ:
       ```json
       "prompt": "Analyze this contract for risky clauses, unfavorable terms, and missing protections. Assign a risk score from 1-10 based on the following criteria: [danh sách tiêu chí của bạn]. Return results in JSON format."
       ```

##### **D. Parse Risk Results (code)**
- **Cách hoạt động**: Chuyển đổi kết quả phân tích của Gemini thành định dạng dễ đọc.
- **Lưu ý**:
  - Node này **không cần chỉnh sửa** nếu import JSON chính xác.
  - Nếu muốn thêm logic mới, mở tab **Code** và chỉnh sửa phần `JSON.parse()`.

##### **E. Log Review to Sheets (googleSheets)**
- **Cách hoạt động**: Lưu tất cả kết quả phân tích vào Google Sheets.
- **Lưu ý**:
  1. **Cấu hình Google Sheets**:
     - Tạo một bảng mới tên **`Contract Reviews`** (cấu trúc sẽ tự động tạo khi chạy workflow đầu tiên).
     - Cung cấp quyền truy cập cho n8n:
       - Mở [Google Cloud Console](https://console.cloud.google.com/).
       - Tạo **OAuth 2.0 Client ID** và đăng ký cho n8n.
     - Trong node `googleSheets`:
       - Chọn **Operation**: `appendOrUpdate`.
       - Chọn **Sheet Name**: `Contract Reviews`.
       - Chọn **Range**: `Sheet1!A1` (hoặc tự động tạo).

##### **F. Check Risk Level (if) + Send Risk Alert (slack)**
- **Cách hoạt động**: Nếu rủi ro > 7, gửi cảnh báo Slack.
- **Lưu ý**:
  1. **Cấu hình Slack**:
     - Tạo **API Token Slack** tại [API Apps Slack](https://api.slack.com/apps).
     - Trong node `slack`:
       - Chọn **Credential**: `Slack` (nhấn **Add Credential** → Điền **API Token**).
       - Chọn **Channel**: `#contract-alerts` (hoặc channel của bạn).
       - Chỉnh sửa **Message Template** (nếu muốn thay đổi nội dung cảnh báo):
         ```json
         "text": "⚠️ **High-Risk Contract Alert** ⚠️\nContract: {{ $node["Extract PDF Text"].json["fileName"] }}\nRisk Score: {{ $node["Parse Risk Results"].json["riskScore"] }}/10\nDetails: {{ $node["Parse Risk Results"].json["riskDetails"] }}"
         ```
  2. **Điều chỉnh ngưỡng rủi ro**:
     - Mở node `Check Risk Level` → Tab **Conditions** → Chỉnh `score > 7` thành giá trị phù hợp (ví dụ: `score > 5`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Upload một file PDF mẫu (ví dụ: hợp đồng mẫu) vào form.
   - Kiểm tra kết quả trong Google Sheets và Slack.
2. **Bật Active**:
   - Nhấn **Active** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[NÂNG CAO WORKFLOW]
1. **Thêm Log Lịch Sử**:
   - Sử dụng node **Sticky Note** để lưu lịch sử phân tích (ví dụ: ngày upload, người upload).
2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Trigger** (n8n-nodes-base.trigger) để gửi báo cáo tổng hợp hàng tuần qua email (node `n8n-nodes-base.email`).
3. **Kết hợp với Notion**:
   - Thay vì Google Sheets, sử dụng node **Notion** để lưu kết quả vào một database Notion.
4. **Phân Loại Hợp Đồng**:
   - Sử dụng node **Code** để phân loại hợp đồng theo loại (ví dụ: hợp đồng lao động, hợp đồng mua bán) và gửi cảnh báo khác nhau.
5. **Tích Hợp với Microsoft Teams**:
   - Thay vì Slack, sử dụng node **Microsoft Teams** để gửi cảnh báo.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ pháp lý** khỏi công việc kiểm tra hợp đồng thủ công, đồng thời **giảm thiểu rủi ro pháp lý** nhờ AI Google Gemini. **Chỉ cần 10 phút setup**, các sếp đã có một hệ thống tự động hóa hoàn chỉnh, hoạt động 24/7.

**Hành động ngay!**
1. Import workflow từ [n8n Community](https://n8n.io/workflows/13671).
2. Cấu hình Google Gemini, Google Sheets và Slack theo hướng dẫn.
3. Chia sẻ liên kết form với team và **bắt đầu tự động hóa ngay!**

---
**💡 Cần hỗ trợ?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định và liên hệ với chúng tôi qua [Facebook](https://facebook.com/n8n.vn) nếu có thắc mắc!