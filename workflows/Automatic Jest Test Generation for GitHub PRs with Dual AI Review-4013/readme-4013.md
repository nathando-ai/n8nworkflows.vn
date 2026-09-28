---
title: "🤖 **Tự Động Tạo Test Jest & Review PR trên GitHub với AI 2 Lần - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn sử dụng AI để sinh ra test Jest tự động từ PR diff, đồng thời review code bằng 2 mô hình OpenAI khác nhau, tiết kiệm thời gian dev lên đến 50%. Đáp ứng ngay cho các sếp engineering muốn nâng cao chất lượng code và giảm bớt công việc thủ công."
slug: "tu-dong-tao-test-jest-ai-review-pr-github"
tags: [n8n, automation, engineering, ai, github, test-automation]
keywords: [n8n workflow github, tự động hóa test jest, review code bằng ai, tự động hóa engineering, ai sinh test unit]
---

# 🚀 **Tự Động Tạo Test Jest & Review PR trên GitHub với AI 2 Lần - Không Cần Code!**

### **Nỗi đau của các sếp engineering**
Mỗi khi có một PR mới trên GitHub, các dev phải:
✅ **Tìm hiểu diff code** để viết test Jest thủ công (tốn thời gian và dễ lỗi).
✅ **Review code** bằng mắt thường, dẫn đến đánh giá không khách quan hoặc bỏ sót lỗi.
✅ **Chờ đợi feedback** từ đồng nghiệp, làm chậm quá trình merge.

**Workflow này giải quyết tất cả!** Sử dụng **AI (OpenAI + LangChain)** để:
✔ **Tự động sinh test Jest** từ diff code trong PR.
✔ **Review code 2 lần** bằng 2 mô hình AI khác nhau (o3-mini và gpt-4.1-mini) để đảm bảo độ chính xác cao.
✔ **Gửi comment tự động** lên PR, giúp dev hiểu rõ hơn về test và lỗi cần sửa.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian dev**: Giảm 50% công việc viết test thủ công.
- **Chất lượng code cao hơn**: AI phát hiện lỗi và đề xuất test tự động.
- **Review khách quan**: 2 mô hình AI khác nhau đánh giá code, giảm sai sót.
- **Hoạt động 24/7**: Workflow chạy tự động khi có PR mới, không cần can thiệp.
- **Tích hợp hoàn toàn**: Hoạt động trên GitHub, không cần cài đặt gì thêm.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản GitHub** với quyền **repo access** (để đọc PR và gửi comment).
2. **API Key OpenAI** (để sử dụng mô hình AI):
   - [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys) (mô hình `o3-mini` và `gpt-4.1-mini`).
3. **Node n8n** (self-hosted hoặc dùng phiên bản miễn phí trên [n8n.io](https://n8n.io/)).
4. **Repo GitHub** muốn tự động hóa (cần cấu hình webhook).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4013) hoặc copy JSON từ đây.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **20 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu hình GitHub Webhook**
- Node **"Webhook"** (node đầu tiên) cần liên kết với **GitHub**:
  - Mở **Settings → Webhooks → Add webhook** trên repo.
  - **Payload URL**: `https://<your-n8n-instance>/webhook/your-workflow-id`
  - **Content type**: `application/json`
  - **Events**: Chọn `Pull request` (hoặc `Pull request review comment` nếu muốn mở rộng).

##### **B. Cấu hình API OpenAI**
- Node **"o3-mini"** và **"gpt4.1-mini"** (mô hình AI):
  - Đi đến **Credentials → Add** → Chọn **OpenAI**.
  - Nhập **API Key** từ OpenAI (đã tạo ở bước chuẩn bị).
  - Chọn mô hình phù hợp:
    - `o3-mini` (rẻ hơn, tốc độ nhanh).
    - `gpt-4.1-mini` (độ chính xác cao hơn).

##### **C. Cấu hình PR & Diff Processing**
- Node **"GH - Get PR"** (GitHub):
  - Chọn **Repository** và **Credentials** (tài khoản GitHub).
  - Node **"GET .diff file"** (HTTP Request):
    - Điền URL mẫu: `https://api.github.com/repos/{owner}/{repo}/pulls/{pr_number}/files`.
    - Sử dụng **Dynamic Values** để lấy `owner`, `repo`, `pr_number` từ node trước.

- Node **"Splits text into array"** (Code):
  - Mở **Code Editor** → Sử dụng JavaScript để split diff thành mảng:
    ```javascript
    return { json: { diff: $input.all().diff.split('\n') } };
    ```

- Node **"Test Maker"** (Agent):
  - Đảm bảo **Prompt** được cấu hình để sinh test Jest từ diff:
    ```plaintext
    Tôi là một AI sinh test Jest. Từ diff code dưới đây, hãy tạo ra test Jest tương ứng.
    Input: {diff}
    Output: Test Jest (Jest + Mocking nếu cần).
    ```

- Node **"Code Reviewer"** (Agent):
  - Sử dụng **2 mô hình AI** để review:
    - `o3-mini`: Review nhanh, đề xuất test cơ bản.
    - `gpt4.1-mini`: Review chi tiết, phát hiện lỗi phức tạp.

##### **D. Gửi Comment Lên PR**
- Node **"POST Comments"** (HTTP Request):
  - URL mẫu: `https://api.github.com/repos/{owner}/{repo}/issues/{pr_number}/comments`.
  - Body JSON:
    ```json
    {
      "body": "Test Jest tự động:\n```\n{test}\n```\n\nReview AI:\n```\n{review}\n```"
    }
    ```

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Tạo một PR mẫu trên repo.
  - Chạy **Manual Trigger** trong n8n để kiểm tra workflow.
  - Kiểm tra **comment** được gửi lên PR có đúng không.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có PR mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có PR mới hoặc test tự động hoàn tất.
   - Ví dụ: `PR #123 đã tự động sinh test Jest và review code!`.

2. **Lưu log tự động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử test và review.
   - Giúp theo dõi tiến độ và chất lượng code dài hạn.

3. **Tích hợp với CI/CD**:
   - Nếu repo sử dụng **GitHub Actions**, có thể kết nối workflow này với pipeline để chạy test tự động trước khi merge.

4. **Cải thiện Prompt cho AI**:
   - Nếu test sinh ra không chính xác, điều chỉnh **Prompt** trong node **Test Maker** hoặc **Code Reviewer** để AI hiểu rõ hơn yêu cầu.

5. **Bộ lọc PR**:
   - Sử dụng node **Code (Filter)** để chỉ chạy workflow cho PR từ **branch cụ thể** (ví dụ: `feature/*`).
   - Mở **Code Editor** và thêm điều kiện:
     ```javascript
     return { json: { jsonpath: "$[?(@.pull_request.head.ref == 'feature/*')]" } };
     ```
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp engineering muốn:
✅ **Tiết kiệm thời gian** viết test thủ công.
✅ **Nâng cao chất lượng code** với review AI 2 lần.
✅ **Tự động hóa hoàn toàn** trên GitHub, không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình GitHub Webhook** và **API OpenAI**.
3. **Test với PR mẫu** và bật **Active**.
4. **Xem PR của mình tự động có test và review AI!**

👉 **Nếu cần hỗ trợ**, để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/community).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::