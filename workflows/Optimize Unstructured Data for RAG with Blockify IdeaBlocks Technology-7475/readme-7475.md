---
title: "🧠 Tự Động Hóa Optimize Dữ Liệu Không Cấu Trúc cho RAG với Blockify IdeaBlocks (N8n + AI)"
description: "Workflow tự động hóa chuyển đổi dữ liệu không cấu trúc (PDF, TXT, slides) thành IdeaBlocks siêu cấu trúc, tăng độ chính xác RAG lên 78X, giảm dung lượng dữ liệu 97.5% - hoàn toàn không cần code!"
slug: "optimize-data-rag-blockify-n8n"
tags: [n8n, automation, ai-rag, multimodal-ai, blockify, openai, google-drive]
keywords: [n8n workflow tự động hóa, optimize dữ liệu không cấu trúc, RAG với Blockify, tăng độ chính xác AI 78 lần, tự động hóa dữ liệu doanh nghiệp]
---

# 🚀 **Tự Động Hóa Optimize Dữ Liệu Không Cấu Trúc cho RAG với Blockify IdeaBlocks**

### **Giải pháp siêu tốc cho doanh nghiệp: Chuyển dữ liệu rối loạn thành kiến thức siêu cấu trúc, tăng độ chính xác RAG lên 78X!**

Hiện nay, doanh nghiệp thường gặp phải vấn đề dữ liệu không cấu trúc (PDF, Word, slides, transcript) lớn và rối loạn, khiến hệ thống RAG (Retrieval-Augmented Generation) của AI gặp khó khăn trong việc trả lời chính xác và hiệu quả. **Workflow này tự động hóa quá trình chuyển đổi dữ liệu không cấu trúc thành IdeaBlocks siêu cấu trúc của Blockify**, giúp:
- **Tăng độ chính xác trả lời của AI lên 78X** so với phương pháp chunk truyền thống.
- **Giảm dung lượng dữ liệu xuống chỉ 2.5%** so với nguyên bản, tiết kiệm chi phí lưu trữ và tính toán.
- **Tự động hóa toàn bộ quy trình** từ tải file lên Google Drive đến tạo vector store cho RAG, không cần viết một dòng code nào.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tăng độ chính xác trả lời của AI lên 78X** (so với phương pháp chunk truyền thống).
✅ **Giảm dung lượng dữ liệu xuống 2.5%** (tiết kiệm chi phí lưu trữ và tính toán).
✅ **Tự động hóa toàn bộ quy trình** từ tải file đến tạo vector store cho RAG.
✅ **Cải thiện chất lượng dữ liệu đầu vào** cho hệ thống RAG, giảm hallucination (trả lời sai) của AI.
✅ **Hoàn toàn không cần code**, chỉ cần cấu hình các node trong n8n.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để tải file .TXT lên).
2. **API Key của Blockify** (đăng ký miễn phí tại [https://console.blockify.ai/signup](https://console.blockify.ai/signup)).
3. **API Key của OpenAI** (để sử dụng OpenAI Embeddings và Chat Models).
4. **File .TXT hoặc dữ liệu không cấu trúc** (PDF, Word, slides) cần được chuyển đổi.
5. **n8n Self-hosted** (để chạy workflow 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7475](https://n8n.io/workflows/7475) hoặc copy/paste JSON từ trang này vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của n8n).
  2. Nhấn **Import** và chọn file JSON đã tải.
  3. Hoặc nhấn **Create Workflow** → **Import from JSON** và dán JSON vào.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **15 node** chính, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node "Download .TXT File for Ingest" (Google Drive)**
- **Cấu hình**:
  - Chọn **credentials**: `googleDriveOAuth2Api` (đã cấu hình trước khi import).
  - Điền **Google Drive ID** của file .TXT cần tải xuống.
  - **Operation**: `download`.

#### **🔹 Node "Blockify Ingest API" (HTTP Request)**
- **Cấu hình**:
  - **Credentials**: `httpBearerAuth` (điền API Key của Blockify).
  - **URL**: `https://api.blockify.ai/ingest` (hoặc URL mới nhất từ Blockify).
  - **Headers**:
    - `Content-Type`: `application/json`.
    - `Authorization`: `Bearer <API_KEY>`.
  - **Body**:
    ```json
    {
      "text": "{{$json.chunkedText}}",
      "model": "gpt-4.1-nano",
      "temperature": 0.7
    }
    ```
    (Thay `{{$json.chunkedText}}` bằng dữ liệu từ node trước).

#### **🔹 Node "Embeddings OpenAI" (OpenAI Embeddings)**
- **Cấu hình**:
  - **Credentials**: `openAiApi` (đã cấu hình trước).
  - **Model**: `text-embedding-ada-002` (hoặc model mới nhất).
  - **Input**: Dữ liệu từ node `Extract IdeaBlocks from API Response`.

#### **🔹 Node "OpenAI Chat Model" (Chat Trigger)**
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4.1-nano` (hoặc model khác phù hợp).
  - **Prompt**: Sử dụng template từ Blockify để tạo IdeaBlocks.

#### **🔹 Node "Chunk Text" (Code)**
- **Cấu hình**:
  - **Script**:
    ```javascript
    // Chunk text với kích thước 1,000 ký tự và overlap 100 ký tự
    const chunkSize = 1000;
    const overlap = 100;
    const text = $input.all()[0].json.text;
    const chunks = [];

    for (let i = 0; i < text.length; i += chunkSize - overlap) {
      const chunk = text.slice(i, i + chunkSize);
      chunks.push({ text: chunk });
    }

    return chunks;
    ```

#### **🔹 Node "Simple IdeaBlock Vector Store" (Vector Store InMemory)**
- **Cấu hình**:
  - **Vector Store**: `SimpleIdeaBlockVectorStore` (tự động tạo từ node trước).

#### **🔹 Node "AI Agent" (Agent)**
- **Cấu hình**:
  - **Agent Type**: `langchain.agent`.
  - **Tools**: Chọn các tool liên quan đến Blockify và OpenAI.

---
### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Execute Workflow** và kiểm tra kết quả.
   - Đảm bảo các node hoạt động liên tục và không có lỗi.
2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi kích hoạt.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi tạo IdeaBlocks, gửi kết quả lên Slack/Telegram thông báo hoàn tất.
   - **Node sử dụng**: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log hoạt động**:
   - Sử dụng node `n8n-nodes-base.manualTrigger` để lưu log vào Google Sheets hoặc database.
   - **Node sử dụng**: `n8n-nodes-base.googleSheets`.

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow phụ để gửi báo cáo tổng hợp về số lượng IdeaBlocks tạo ra hàng tháng.
   - **Node sử dụng**: `n8n-nodes-base.email`.

4. **Tối ưu hóa cho nhiều file**:
   - Sử dụng node `n8n-nodes-base.splitInBatches` để xử lý nhiều file đồng thời.
   - **Node sử dụng**: `n8n-nodes-base.splitInBatches`.

5. **Sử dụng Blockify Distill**:
   - Nếu muốn tối ưu hóa dữ liệu thêm, kết hợp với **Blockify Distill** để rút gọn dữ liệu còn 1-2% dung lượng.
   - **Link**: [https://iternal.ai/blockify](https://iternal.ai/blockify).
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp muốn tự động hóa quá trình chuyển đổi dữ liệu không cấu trúc thành kiến thức siêu cấu trúc, tăng độ chính xác của RAG lên **78X** và giảm dung lượng dữ liệu xuống **2.5%**. **Không cần code**, chỉ cần cấu hình các node trong n8n là xong!

**Hãy áp dụng ngay workflow này và biến dữ liệu rối loạn của doanh nghiệp thành một hệ thống RAG hiệu quả, tiết kiệm chi phí và tăng độ chính xác!** 🚀

---
### **🔗 Tài liệu tham khảo**
- [Blockify Official Website](https://iternal.ai/blockify)
- [Blockify API Documentation](https://console.blockify.ai/docs)
- [n8n Workflow](https://n8n.io/workflows/7475)