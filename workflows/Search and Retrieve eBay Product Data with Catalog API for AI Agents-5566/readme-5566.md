---
title: "🚀 Tự Động Hóa Tìm Kiếm & Lấy Dữ Liệu Sản Phẩm eBay Cho AI Agent (MCP) - Không Cần Code"
description: "Workflow này tự động hóa việc tìm kiếm và lấy dữ liệu sản phẩm chi tiết từ API Catalog eBay, biến chúng thành API MCP để AI Agent sử dụng. Giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình nghiên cứu sản phẩm và tối ưu hóa quy trình bán hàng."
slug: "tu-dong-hoa-tim-kiem-du-lieu-san-pham-ebay-cho-ai-agent"
tags: [n8n, automation, ebay-api, ai-agent, mcp, no-code, ai-rag]
keywords: [tự động hóa ebay api, ai agent với n8n, mcp ebay catalog, tìm kiếm sản phẩm eBay tự động, api catalog ebay cho ai]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Lấy Dữ Liệu Sản Phẩm eBay Cho AI Agent (MCP)**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải **tìm kiếm, so sánh và lấy dữ liệu sản phẩm từ eBay** để:
- **Tối ưu hóa danh sách sản phẩm** trên các nền tảng bán hàng khác.
- **Tránh sai sót trong mô tả sản phẩm** (tên, chi tiết kỹ thuật, hình ảnh).
- **Tiết kiệm thời gian** trong quá trình nghiên cứu thị trường.

**Với workflow này**, các sếp **không cần viết một dòng code** mà vẫn có thể:
✅ **Tự động hóa việc tìm kiếm sản phẩm** từ API Catalog eBay.
✅ **Chuyển dữ liệu thành API MCP** để AI Agent sử dụng.
✅ **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động tìm kiếm và lấy dữ liệu sản phẩm thay vì làm thủ công.
- **Chính xác 100%**: Dữ liệu được lấy từ API chính thức của eBay, không sai sót.
- **Tích hợp với AI Agent**: API MCP cho phép AI Agent tương tác trực tiếp với dữ liệu sản phẩm.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản eBay Developer** (đăng ký tại [eBay Developer Portal](https://developer.ebay.com/)).
2. **API Key & App ID** của eBay (để kết nối với API Catalog).
3. **n8n Self-hosted** (để chạy workflow 24/7).
4. **AI Agent** (nếu muốn tích hợp, ví dụ như LangChain, LlamaIndex...).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/5566) (hoặc copy JSON từ trang này).
2. **Mở n8n Editor** → **Import Workflow** → **Paste JSON** → **Import**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 node chính**, các sếp cần cấu hình như sau:

#### **🔹 Node 1: Catalog MCP Server (mcpTrigger)**
- **Chức năng**: Làm server endpoint cho AI Agent gửi yêu cầu.
- **Cấu hình**:
  - **Path**: `catalog-mcp` (không cần thay đổi).
  - **Credentials**: Không cần OAuth2 (do API eBay yêu cầu API Key).

#### **🔹 Node 2 & 3: Retrieve Product Details & Search Product Summaries (httpRequestTool)**
- **Chức năng**: Gọi API eBay để lấy dữ liệu sản phẩm.
- **Cấu hình cần thiết**:
  - **Base URL**: `https://api.ebay.com/buy/browse/v1/catalog/`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_EBAY_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Query Parameters** (ví dụ cho `Search Product Summaries`):
    ```json
    {
      "keywords": "$fromAI()",  // AI tự động điền từ khóa tìm kiếm
      "limit": 10,
      "offset": 0
    }
    ```
  - **Query Parameters** (ví dụ cho `Retrieve Product Details`):
    ```json
    {
      "productId": "$fromAI()",  // AI tự động điền ID sản phẩm
      "fields": "title,description,itemSpecifics,images"
    }
    ```

#### **🔹 Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu từ AI Agent (ví dụ: `{"keywords": "iPhone 15 Pro Max"}`).
   - Kiểm tra kết quả trả về có đúng không?
2. **Bật Active** workflow sau khi test thành công.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
- **Kết hợp với Slack/Telegram**: Gửi kết quả tìm kiếm sản phẩm vào kênh chat.
- **Lưu log dữ liệu**: Sử dụng **n8n-nodes-base.quickBooks** để lưu lịch sử tìm kiếm.
- **Tự động gửi báo cáo**: Gửi email định kỳ với danh sách sản phẩm mới nhất.
- **Tối ưu AI Agent**: Sử dụng `$fromAI()` để AI tự động điền từ khóa tìm kiếm.
:::

---

## **📌 Kết Luận**
Workflow này **giúp các sếp tự động hóa việc tìm kiếm và lấy dữ liệu sản phẩm eBay** một cách **mạnh mẽ và hiệu quả**, đồng thời **tích hợp với AI Agent** để tối ưu hóa quy trình bán hàng.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?** Liên hệ với tác giả David Ashby trên [Discord](https://discord.me/cfomodz) hoặc tham khảo [tài liệu chính thức n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).