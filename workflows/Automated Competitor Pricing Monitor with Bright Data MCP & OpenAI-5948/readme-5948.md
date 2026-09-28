---
title: "🚀 **Tự Động Hóa Theo Dõi Giá Thay Đổi ClickUp Với AI & Bright Data MCP - Không Cần Code!**"
description: "Workflow n8n tự động so sánh, phân tích và cập nhật giá ClickUp trên Google Sheets mỗi khi có thay đổi, tiết kiệm thời gian và giảm thiểu sai sót cho các sếp marketing & kinh doanh."
slug: "tieu-dong-hoa-theo-doi-gia-clickup-voi-ai-bright-data"
tags: [n8n, automation, market-research, ai-summarization, bright-data, google-sheets, openai]
keywords: [n8n workflow tự động hóa, theo dõi giá ClickUp, AI scraping, Bright Data MCP, tự động cập nhật Google Sheets, không cần code]
---

# **🚀 Tự Động Hóa Theo Dõi Giá ClickUp Với AI & Bright Data MCP - Không Cần Code!**

## **💡 Giới Thiệu**
Bạn đã bao giờ phải mất nhiều giờ để thủ công theo dõi giá của ClickUp hoặc các công cụ SaaS khác? Hay phải lo lắng rằng giá đã thay đổi nhưng bạn không kịp cập nhật? **Workflow này giải quyết tất cả những vấn đề đó!**

Với **n8n + Bright Data MCP + OpenAI**, bạn có thể **tự động hóa việc theo dõi giá ClickUp**, so sánh với dữ liệu cũ, và **cập nhật tự động lên Google Sheets** mỗi khi có thay đổi. **Không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Chính xác 100%**: AI tự động phân tích và so sánh giá, tránh sai sót con người.
- **Cập nhật tự động**: Dữ liệu luôn mới nhất trên Google Sheets.
- **Dễ dàng mở rộng**: Theo dõi nhiều công cụ khác (Notion, Airtable, Monday.com) chỉ bằng cách thay đổi tham số.
- **Bảo mật**: Sử dụng **Bright Data MCP** để tránh bị chặn bởi bot protection.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **Tài khoản Bright Data MCP** (đăng ký [tại đây](https://get.brightdata.com/1tndi4600b25) để hỗ trợ tạo nội dung miễn phí)
✅ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/api-keys))
✅ **Google Sheets** với cấu trúc dữ liệu để lưu trữ lịch sử giá (mẫu có thể tham khảo trong workflow)
✅ **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud)
:::

---

## **🚀 Cách Import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5948](https://n8n.io/workflows/5948) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON vào và nhấn **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **🔹 Node 1: Trigger (Schedule Trigger)**
- **Cài đặt lịch chạy**: Chọn **daily/weekly** tùy nhu cầu (ví dụ: chạy hàng ngày lúc 8h sáng).
- **Lưu ý**: Nếu dùng phiên bản cloud, chọn **Active** sau khi cấu hình xong.

#### **🔹 Node 2: Set Search Parameters**
- **Điền URL của trang giá ClickUp** (ví dụ: `https://clickup.com/pricing`).
- **Thêm tên công cụ** (ví dụ: `"ClickUp"`).
- **Lưu ý**: Nếu muốn theo dõi nhiều công cụ, sao chép workflow và thay đổi tham số này.

#### **🔹 Node 3: Retrieve Pricing Data (Google Sheets)**
- **Chọn Google Sheets OAuth2 API** đã cấu hình trước.
- **Chọn Sheet và Range** (ví dụ: `Sheet1!A1:D100`).
- **Lưu ý**: Sheet phải có cột `price` để so sánh sau này.

#### **🔹 Node 4: AI Agent (Core Logic)**
- **MCP Client Tool**:
  - Chọn **mcpClientApi** đã cấu hình.
  - **Operation**: Đảm bảo chọn `executeTool`.
  - **Lưu ý**: Nếu không có API Key MCP, đăng ký tại [Bright Data](https://get.brightdata.com/1tndi4600b25).
- **LLM Brain (OpenAI)**:
  - Chọn **openAiApi** và **model = gpt-4o-mini**.
  - **Prompt mặc định** đã được tối ưu, không cần chỉnh sửa (nếu muốn thay đổi, chỉnh ở **keyParameters**).
- **Structured Output Parser**:
  - Đảm bảo **format JSON** đúng với cấu trúc:
    ```json
    { "plan_name": "Business", "price": "$12", "key_features": [...] }
    ```

#### **🔹 Node 5: If Price Changes**
- **Cấu hình logic so sánh**:
  - So sánh `json["price"].old` vs `json["price"].new`.
  - Nếu khác nhau → **true** → cập nhật Google Sheets.
  - Nếu giống nhau → **false** → bỏ qua.

#### **🔹 Node 7: Update Google Sheet**
- **Chọn Sheet và Range** tương tự như Node 3.
- **Operation**: Chọn `update`.
- **Lưu ý**: Đảm bảo **ID Sheet và OAuth2 API** đúng.

---

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
  - Kiểm tra **Google Sheets** xem có cập nhật không.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

## **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH MỞ RỘNG WORKFLOW]
- **Gửi thông báo Slack/Telegram khi giá thay đổi**:
  - Thêm **Slack/Telegram Node** sau **If Price Changes** (nếu true).
  - Cấu hình message: `Giá ClickUp đã thay đổi từ $X sang $Y!`.
- **Lưu lịch sử thay đổi**:
  - Thêm **Google Sheets (Append Row)** sau **Update Google Sheet** để lưu toàn bộ lịch sử.
- **Theo dõi nhiều công cụ**:
  - Sao chép workflow và thay đổi **Set Search Parameters** cho Notion, Airtable, Monday.com...
- **Tạo báo cáo định kỳ**:
  - Sử dụng **Google Apps Script** để tự động tạo báo cáo từ Google Sheets.
- **Bảo mật dữ liệu**:
  - Mật mã hóa API Key bằng **n8n Secrets Management**.
:::

---

## **📌 Kết luận**
Workflow này **giúp các sếp tự động hóa việc theo dõi giá ClickUp một cách hoàn toàn không cần code**, tiết kiệm thời gian và giảm thiểu sai sót. **Bắt đầu ngay hôm nay!**

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Đăng ký Bright Data MCP** (nếu chưa có) → [Tại đây](https://get.brightdata.com/1tndi4600b25).
2. **Import workflow** vào n8n và cấu hình theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả trên Google Sheets!
:::

---
**Cần hỗ trợ?** Liên hệ với tác giả Yaron Been qua:
🔗 [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
📺 [YouTube](https://www.youtube.com/@YaronBeen/videos)