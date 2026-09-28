---
title: "🤖 Tự Động Xem Xét CV với OpenAI & PostgreSQL: 4 Bước AI Chaining - Giải Pháp HR Không Cần Code"
description: "Workflow tự động hóa xem xét CV bằng 4 prompt AI liên kết, lưu kết quả trực tiếp vào PostgreSQL. Giúp HR tiết kiệm 80% thời gian đánh giá, giảm thiểu sai sót và tạo ra báo cáo tổng hợp chuyên nghiệp cho mỗi vị trí tuyển dụng."
slug: "tieu-dong-xem-xet-cv-voi-openai-postgresql"
tags: [n8n, automation, hr, ai-summarization, postgresql, openai, no-code]
keywords: [tự động hóa xem xét cv, ai screening cv, workflow n8n hr, postgresql ai integration, openai prompt chaining]
---

# 🚀 **Tự Động Xem Xét CV với OpenAI & PostgreSQL: 4 Bước AI Chaining - Giải Pháp HR Không Cần Code**

### **Nỗi Đau Của Các Sếp HR**
Hàng ngày, các sếp HR phải:
- **Đọc hàng trăm CV** để tìm kiếm ứng viên phù hợp.
- **Đánh giá chủ quan** dựa vào kinh nghiệm, kỹ năng và trải nghiệm cá nhân.
- **Tạo báo cáo tổng hợp** để trình lên cấp trên, mất nhiều thời gian và dễ bị sai sót.
- **Phải nhớ lại** từng ứng viên sau khi đã xem xét, dẫn đến mất mát thông tin quan trọng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100% quá trình xem xét CV** với AI OpenAI.
✅ **Lưu trữ kết quả trực tiếp vào PostgreSQL**, không cần backend phức tạp.
✅ **Cung cấp báo cáo tổng hợp chuyên nghiệp** cho mỗi vị trí tuyển dụng.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Xem xét hàng trăm CV chỉ trong vài phút thay vì nhiều giờ.
- **Đánh giá khách quan**: AI phân tích CV theo tiêu chí cấu trúc, tránh chủ quan của con người.
- **Báo cáo tự động**: Tạo tổng hợp ứng viên phù hợp và điểm yếu chung cho từng vị trí.
- **Cập nhật liên tục**: Kết quả được lưu vào PostgreSQL, dễ dàng truy xuất và phân tích sau này.
- **Tối ưu hóa phỏng vấn**: AI đề xuất câu hỏi phỏng vấn cá nhân hóa cho từng ứng viên.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản OpenAI** với API Key (để sử dụng AI GPT-4.1-mini hoặc mô hình khác).
2. **Cơ sở dữ liệu PostgreSQL** với các bảng đã được tạo (xem **Schema SQL** dưới đây).
3. **Dữ liệu ban đầu**:
   - Các **vị trí tuyển dụng (jobs)** với mô tả chi tiết.
   - **CV của ứng viên** đã được chuyển thành văn bản (`cv_text`).
4. **VPS hoặc máy chủ** để chạy n8n 24/7 (khuyến nghị **Self-hosted** để đảm bảo bảo mật và hiệu suất).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13876](https://n8n.io/workflows/13876) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
  2. Nhấn **Import** và chọn file JSON đã tải.
  3. Chọn **Workflow** từ danh sách và nhấn **Import**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **21 node**, nhưng các bước quan trọng nhất cần chú ý:

#### **A. Cấu Hình Credentials**
- **OpenAI API**:
  - Đi đến **Settings > Credentials** trong n8n.
  - Tạo **mới credential** với tên `openAiApi`.
  - Điền **API Key** từ tài khoản OpenAI của bạn.
  - Chọn **Model**: `gpt-4.1-mini` (hoặc mô hình khác nếu muốn cải thiện độ chính xác).

- **PostgreSQL**:
  - Tạo **mới credential** với tên `postgres`.
  - Điền thông tin kết nối:
    - **Host**: Địa chỉ IP hoặc tên máy chủ PostgreSQL.
    - **Port**: Thường là `5432`.
    - **Database**: Tên cơ sở dữ liệu.
    - **Username** và **Password**.
    - **SSL Mode**: `require` (nếu kết nối qua internet).

#### **B. Cấu Hình Webhook**
- Node **"Receive CVs"** (Webhook):
  - **Path**: `cv-analyze` (không cần thay đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần thiết (webhook công khai).

#### **C. Cấu Hình Prompts AI**
Workflow sử dụng **4 prompt AI** liên kết:
1. **Prompt 0**: Trích xuất **mô tả công việc cấu trúc** từ mô tả vị trí (chỉ chạy nếu `gabarito` trong bảng `jobs` là `null`).
2. **Prompt 1**: Đánh giá điểm số ứng viên (0-100) dựa trên tiêu chí công việc.
3. **Prompt 2**: Xác định **điểm mạnh và điểm yếu** của ứng viên.
4. **Prompt 3**: Tạo **câu hỏi phỏng vấn cá nhân hóa**.
5. **Prompt 4**: Tạo **báo cáo tổng hợp** khi tất cả ứng viên được xử lý.

- **Lưu ý**:
  - Các prompt đã được tối ưu sẵn, nhưng các sếp có thể **cập nhật nội dung** trong node **OpenAI** nếu cần.
  - Để cải thiện độ chính xác, có thể **thay thế mô hình** từ `gpt-4.1-mini` sang `gpt-4` (mặc dù chi phí cao hơn).

#### **D. Cấu Hình PostgreSQL**
- **Bảng cần tạo** (xem **Schema SQL** dưới đây).
- **Query trong node PostgreSQL**:
  - Các query đã được viết sẵn, nhưng các sếp nên **kiểm tra lại** để phù hợp với cấu trúc cơ sở dữ liệu của mình.
  - Ví dụ:
    ```sql
    -- Query trong "Fetch Job and Candidates"
    SELECT * FROM jobs WHERE id = $1;
    SELECT * FROM candidates WHERE job_id = $1 AND status = 'pending';
    ```

#### **E. Cấu Hình Loop Candidates**
- Node **"Loop Candidates"** (Split in Batches):
  - **Batch Size**: Đặt số lượng ứng viên xử lý cùng một lúc (ví dụ: `5`).
  - **Lưu ý**: Nếu số lượng ứng viên quá lớn, có thể **tăng batch size** để tăng tốc độ.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **gói dữ liệu mẫu** đến webhook:
     ```json
     {
       "job_id": 1,
       "candidate_ids": [1, 2, 3]
     }
     ```
   - Kiểm tra kết quả trong **PostgreSQL** để đảm bảo dữ liệu được lưu trữ chính xác.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN THÊM**]
1. **Gửi kết quả qua Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **"Save Analysis"** để thông báo kết quả cho team.
   - Ví dụ: Khi một ứng viên đạt điểm cao, gửi tin nhắn tự động.

2. **Lưu log hoạt động**:
   - Thêm node **Code** sau node **"Save Analysis"** để ghi log vào bảng mới trong PostgreSQL.
   - Có thể sử dụng **n8n-nodes-base.dateTime** để ghi thời gian xử lý.

3. **Tạo báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.schedule** để chạy workflow hàng tuần và gửi báo cáo tổng hợp qua email.
   - Thêm node **Email** (ví dụ: Gmail, SendGrid) để gửi báo cáo tự động cho HR.

4. **Tối ưu hóa Prompts**:
   - Nếu muốn cải thiện độ chính xác, các sếp có thể **thêm ví dụ** vào Prompt 0 và Prompt 1.
   - Ví dụ:
     ```json
     {
       "instruction": "Dưới đây là mô tả công việc của vị trí Marketing Manager. Trích xuất các tiêu chí cần thiết và gán trọng số cho từng tiêu chí.",
       "examples": [
         {
           "input": "Mô tả công việc...",
           "output": "{\"requirements\": [...], \"weights\": {...}}"
         }
       ]
     }
     ```

5. **Kết hợp với Google Sheets**:
   - Thay vì lưu vào PostgreSQL, các sếp có thể **lưu kết quả vào Google Sheets** bằng node **Google Sheets**.
   - Tiện lợi cho việc chia sẻ với team không có quyền truy cập vào cơ sở dữ liệu.

---

## 🗄️ **Schema SQL Cần Thiết**
Dưới đây là **các bảng PostgreSQL** cần tạo để workflow hoạt động:
```sql
-- Tạo bảng jobs (lưu thông tin vị trí tuyển dụng)
CREATE TABLE jobs (
  id SERIAL PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT NOT NULL,
  gabarito JSONB,  -- Lưu kết quả trích xuất từ Prompt 0
  status VARCHAR(20) DEFAULT 'draft',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Tạo bảng candidates (lưu thông tin ứng viên)
CREATE TABLE candidates (
  id SERIAL PRIMARY KEY,
  job_id INTEGER REFERENCES jobs(id) ON DELETE CASCADE,
  name VARCHAR(255),
  filename VARCHAR(255),
  cv_text TEXT,  -- Nội dung CV đã chuyển thành văn bản
  status VARCHAR(20) DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Tạo bảng analyses (lưu kết quả phân tích AI)
CREATE TABLE analyses (
  id SERIAL PRIMARY KEY,
  candidate_id INTEGER REFERENCES candidates(id) ON DELETE CASCADE,
  job_id INTEGER REFERENCES jobs(id) ON DELETE CASCADE,
  score INTEGER,  -- Điểm số từ 0-100
  nivel_aderencia VARCHAR(20),  -- Mức độ phù hợp
  justificativa_score TEXT,  -- Lý do cho điểm số
  pontos_fortes JSONB,  -- Điểm mạnh của ứng viên
  gaps_criticos JSONB,  -- Điểm yếu quan trọng
  gaps_secundarios JSONB,  -- Điểm yếu thứ yếu
  perguntas_entrevista JSONB,  -- Câu hỏi phỏng vấn
  score_criterios JSONB,  -- Điểm theo từng tiêu chí
  created_at TIMESTAMP DEFAULT NOW(),
  CONSTRAINT analyses_candidate_unique UNIQUE (candidate_id)
);

-- Tạo bảng job_summaries (lưu báo cáo tổng hợp)
CREATE TABLE job_summaries (
  id SERIAL PRIMARY KEY,
  job_id INTEGER REFERENCES jobs(id) ON DELETE CASCADE,
  total_analisados INTEGER,  -- Tổng số ứng viên phân tích
  recomendados JSONB,  -- Danh sách ứng viên được khuyến nghị
  destaque TEXT,  -- Điểm nổi bật của ứng viên
  gap_comum TEXT,  -- Điểm yếu chung của ứng viên
  resumo TEXT,  -- Tóm tắt tổng hợp
  created_at TIMESTAMP DEFAULT NOW(),
  CONSTRAINT job_summaries_job_id_key UNIQUE (job_id)
);
```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc mệt mỏi là xem xét CV thủ công. Bằng cách sử dụng **AI OpenAI và PostgreSQL**, nó tự động:
✔ **Phân tích CV** theo tiêu chí cấu trúc.
✔ **Đánh giá điểm số** và đề xuất câu hỏi phỏng vấn.
✔ **Tạo báo cáo tổng hợp** cho từng vị trí tuyển dụng.
✔ **Lưu trữ dữ liệu** một cách an toàn và dễ truy cập.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n** trên VPS và import workflow.
2. **Cấu hình PostgreSQL** và OpenAI API.
3. **Test với dữ liệu mẫu** và bắt đầu tự động hóa quá trình tuyển dụng của bạn!

**Nếu có bất kỳ câu hỏi nào**, các sếp có thể tham khảo [documentation chính thức của n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/discord). **Chúc các sếp thành công!** 🚀