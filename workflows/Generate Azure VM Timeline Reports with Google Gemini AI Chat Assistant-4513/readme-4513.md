---
title: "🚀 Tự động tạo báo cáo Timeline VM Azure với trợ lý AI Google Gemini"
description: "Workflow n8n giúp các sếp nhanh chóng tạo báo cáo chi tiết về hiệu suất, sự kiện và trạng thái của máy ảo Azure chỉ bằng một tin nhắn chat, không cần viết code."
slug: "tu-dong-tao-bao-cao-timeline-vm-azure-google-gemini"
tags: [n8n, automation, no-code, devops, ai, azure]
keywords: [n8n workflow, tự động hóa, Azure VM, Google Gemini, AI chat, DevOps]
---

# 🚀 Tự động tạo báo cáo Timeline VM Azure với trợ lý AI Google Gemini

Bạn đã từng phải **điều tra thủ công** từng máy ảo Azure để lấy thông số hiệu suất, sự kiện, và trạng thái?  
Việc mở portal, lọc log, sao chép dữ liệu rồi ghép lại thành một báo cáo đầy đủ **tốn hàng giờ** và dễ sai sót.  

Với workflow **Generate Azure VM Timeline Reports with Google Gemini AI Chat Assistant** (tác giả Adam Bertram), các sếp có thể **nhận báo cáo toàn diện chỉ trong vài giây** khi gửi một tin nhắn chat. Không cần viết code, không cần thao tác UI – mọi thứ được tự động hoá 100% bằng n8n và AI Google Gemini.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Báo cáo được tạo tự động trong vòng 30 giây.  
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ Azure Monitor API, không còn sai sót do nhập tay.  
- **Cá nhân hoá**: AI Gemini hiểu ngữ cảnh và tùy chỉnh báo cáo theo yêu cầu (ví dụ: “tóm tắt tuần qua” hoặc “chi tiết lỗi CPU”).  
- **Hoạt động liên tục**: Workflow chạy 24/7, sẵn sàng trả lời bất kỳ yêu cầu nào từ chat.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Azure** với quyền **Reader** hoặc **Monitoring Reader** trên subscription cần báo cáo.  
- **Azure Monitor OAuth2 API credential** trong n8n (client ID, client secret, tenant ID).  
- **Google Palm API credential** (API key) để sử dụng mô hình Gemini.  
- **Kênh chat** được hỗ trợ bởi n8n‑langchain (ví dụ: Slack, Microsoft Teams, Discord) – tạo webhook hoặc bot token tương ứng.  
- **n8n phiên bản ≥ 1.0** và các node `@n8n/n8n-nodes-langchain` đã được cài đặt.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc [đây](https://n8n.io/workflows/4513)).  
2. Mở n8n → **Workflows** → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Đặt tên cho workflow (mặc định: *Generate Azure VM Timeline Reports*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **When chat message received** (chatTrigger) | Lắng nghe tin nhắn từ kênh chat | - Chọn **Credential** (Slack/Discord…) <br> - Đặt **Channel ID** hoặc **Webhook URL** <br> - Kiểm tra **Event** = `message` |
| **Set Common Variables** (set) | Định nghĩa các biến chung cho Azure | - `subscriptionId` (ID subscription Azure) <br> - `resourceGroupName` (Tên resource group chứa VM) <br> - `vmName` (Tên VM muốn báo cáo) <br> - `timeRange` (ví dụ: `P7D` cho 7 ngày) |
| **Get Azure Resource Groups** (toolHttpRequest) | Lấy danh sách Resource Groups | - Credential: **Microsoft Azure Monitor OAuth2 API** <br> - Method: `GET` <br> - URL: `https://management.azure.com/subscriptions/{{ $json.subscriptionId }}/resourceGroups?api-version=2021-04-01` |
| **Get VM Information** (toolHttpRequest) | Thông tin cơ bản VM | - Credential: **Microsoft Azure Monitor OAuth2 API** <br> - URL: `https://management.azure.com/subscriptions/{{ $json.subscriptionId }}/resourceGroups/{{ $json.resourceGroupName }}/providers/Microsoft.Compute/virtualMachines/{{ $json.vmName }}?api-version=2022-08-01` |
| **Get VM Performance Stats** (toolHttpRequest) | Thống kê hiệu suất (CPU, Memory…) | - Credential: **Microsoft Azure Monitor OAuth2 API** <br> - URL: `https://management.azure.com/subscriptions/{{ $json.subscriptionId }}/resourceGroups/{{ $json.resourceGroupName }}/providers/Microsoft.Compute/virtualMachines/{{ $json.vmName }}/providers/microsoft.insights/metrics?metricnames=Percentage CPU,Network In Total,Network Out Total&timespan={{ $json.timeRange }}&api-version=2018-01-01` |
| **Get VM Events** (toolHttpRequest) | Lấy các sự kiện (restart, deallocate…) | - Credential: **Microsoft Azure Monitor OAuth2 API** <br> - URL: `https://management.azure.com/subscriptions/{{ $json.subscriptionId }}/resourceGroups/{{ $json.resourceGroupName }}/providers/Microsoft.Compute/virtualMachines/{{ $json.vmName }}/providers/microsoft.insights/eventCategories?api-version=2015-04-01` |
| **Get VM Instance View** (toolHttpRequest) | Trạng thái hiện tại (running, stopped…) | - Credential: **Microsoft Azure Monitor OAuth2 API** <br> - URL: `https://management.azure.com/subscriptions/{{ $json.subscriptionId }}/resourceGroups/{{ $json.resourceGroupName }}/providers/Microsoft.Compute/virtualMachines/{{ $json.vmName }}/instanceView?api-version=2022-08-01` |
| **Get Current Date** (toolCode) | Tạo timestamp cho báo cáo | - Code (JavaScript): `return { date: new Date().toISOString() };` |
| **Simple Memory** (memoryBufferWindow) | Lưu trữ lịch sử chat để AI có ngữ cảnh | - `Size` = 5 (lưu 5 tin nhắn gần nhất) |
| **Google Gemini Chat Model** (lmChatGoogleGemini) | Xử lý yêu cầu tạo báo cáo | - Credential: **Google Palm API** <br> - Model: `gemini-pro` (hoặc phiên bản mới nhất) <br> - Prompt mẫu (được truyền từ **AI Agent**) |
| **AI Agent** (agent) | Kết nối chat trigger → memory → Gemini → trả lời | - Chọn **Memory** = *Simple Memory* <br> - Chọn **LLM** = *Google Gemini Chat Model* <br> - Định nghĩa **Tool Calls**: `Get VM Information`, `Get VM Performance Stats`, `Get VM Events`, `Get VM Instance View`, `Get Current Date` |

> **Lưu ý:** Các URL Azure cần thay thế các biến `{{ $json.xxx }}` bằng giá trị thực tế từ node *Set Common Variables* hoặc output của các node trước.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn mẫu vào kênh chat, ví dụ:  
   ```
   @bot tạo báo cáo tuần này cho VM myVM trong resource group RG-Prod
   ```  
2. Kiểm tra log của từng node trong n8n để chắc chắn các API trả về dữ liệu hợp lệ.  
3. Khi mọi thứ ổn, bật **Active** cho workflow (nút toggle ở góc trên bên phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để gửi báo cáo dưới dạng file PDF/HTML.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại mỗi lần báo cáo (ngày, VM, thời gian thực hiện).  
- **Báo cáo định kỳ**: Dùng node `Cron` để tự động chạy workflow mỗi sáng thứ Hai, gửi báo cáo tuần cho team.  
- **Mở rộng công cụ**: Thêm `toolHttpRequest` để lấy **Cost Management** (chi phí) hoặc **Security Center alerts** cho báo cáo toàn diện hơn.  

### 📌 Kết luận
Với workflow này, các sếp có thể **đánh tan nỗi lo “tìm dữ liệu, ghép báo cáo”** chỉ bằng một câu lệnh chat. Hãy import ngay, cấu hình credential, và để AI Gemini lo phần còn lại – tiết kiệm thời gian, tăng độ chính xác và luôn có báo cáo cập nhật 24/7.  

**Áp dụng ngay hôm nay, để các sếp tập trung vào quyết định chiến lược, không còn bị cuốn vào công việc thủ công!**