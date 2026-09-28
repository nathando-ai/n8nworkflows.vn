---
title: "🚀 Tự động hóa tạo video quảng cáo sản phẩm bằng AI với GPT-4o, Fal.ai & gotoHuman"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn diện quy trình sáng tạo nội dung, sinh ảnh và video quảng cáo sản phẩm bằng AI, kết hợp kiểm duyệt thông minh từ con người qua gotoHuman."
slug: "tao-video-quang-cao-san-pham-ai-fal-ai-gotohuman"
tags: [n8n, automation, ai-video, gotohuman, fal-ai, openai, content-creation]
keywords: [n8n workflow, tạo video ai, fal.ai, gotohuman, gpt-4o, tự động hóa marketing, content creation]
---

# 🚀 Tự động hóa tạo video quảng cáo sản phẩm bằng AI với GPT-4o, Fal.ai & gotoHuman

Các sếp đang làm trong lĩnh vực thương mại điện tử hoặc marketing chắc hẳn đều hiểu cảm giác "đau đầu" mỗi tuần khi phải lên ý tưởng, thiết kế hình ảnh, dựng video và viết caption để đăng lên mạng xã hội. Việc làm thủ công này tốn vô thời gian mà đôi khi AI tạo ra nội dung lại "lệch pha" với thương hiệu. 

Giải pháp ư? Hãy để workflow n8n này "gánh" thay các sếp 100% công đoạn từ A-Z: Tự động lên ý tưởng, viết tagline, sinh hình ảnh, chuyển ảnh thành video, chèn chữ qua Cloudinary và đặc biệt là có **cổng kiểm duyệt của con người (Human-in-the-loop)** thông qua **gotoHuman** để đảm bảo thành phẩm hoàn hảo nhất trước khi xuất bản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 4 giai đoạn:** Từ lên ý tưởng chiến dịch, tạo tagline thông minh (tự học hỏi từ các mẫu được duyệt trước đó), sinh ảnh gốc qua Fal.ai, đến biến ảnh thành video chuyển động sinh động.
- **Kiểm soát tuyệt đối với gotoHuman:** Không lo AI "phóng khoác" hay sai lệch thông tin sản phẩm. Mọi bước quan trọng đều chờ người quản lý phê duyệt hoặc chỉnh sửa trực tiếp.
- **Tối ưu thời gian:** Thay vì mất hàng ngày, giờ đây việc sản xuất chuỗi video quảng cáo hàng tuần chỉ diễn ra trong vài phút click chuột.
- **Tích hợp linh hoạt:** Kết hợp mượt mà giữa OpenAI (GPT-4o-mini), Fal.ai, Cloudinary và giao diện review trực quan của gotoHuman.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Đã cài sẵn node `@gotohuman/n8n-nodes-gotohuman`).
- **Tài khoản OpenAI API Key** (Dùng cho GPT-4o-mini ideation & tagline).
- **Tài khoản Fal.ai** (Dùng để generate Image & Video).
- **Tài khoản Cloudinary** (Dùng để chèn text/tagline lên ảnh và video).
- **Tài khoản gotoHuman** (Dùng làm giao diện kiểm duyệt nội dung).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Trước tiên, hãy đảm bảo các sếp đã cài đặt node `gotoHuman` vào n8n trước khi import template (nếu chưa có, hãy kéo thả một node gotoHuman vào một canvas trống).
- Import file JSON của workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 47 nodes và chia làm các chặng rõ ràng, các sếp cần chú ý cấu hình các thông số sau:

- **Cài đặt gotoHuman:** 
  - Tạo tài khoản gotoHuman, lấy API Key và thêm vào credentials của n8n.
  - Trong giao diện gotoHuman, hãy import các review template bằng danh sách ID sau (copy toàn bộ chuỗi ngăn cách bằng dấu phẩy): `Z7V1jyImY1pho9eY039R,0GBaOCWd27tqV562kkCL,E2wlCVPWmk2UnLHVt4uu,DitPdbIapS4rBxBTIYGt,Z2T7nFwkXVFQlD6z50eV`
  - Liên kết Webhook URL từ node `Remote manual trigger` trong n8n vào phần cài đặt template "Create Campaign" trên gotoHuman.
  
- **Cấu hình Fal.ai (Node: `Fal.ai Image Gen` & `Fal.ai Video Gen`):**
  - Chọn `Generic Credential Type` > `Header Auth` 
  - Name: `Authorization` | Value: `Key YOUR-API-KEY` (Lấy từ tài khoản Fal.ai của các sếp).

- **Cấu hình Cloudinary (Nodes upload ảnh/video):**
  - Lấy Cloud/Environment Name từ tài khoản Cloudinary.
  - Tạo một Upload Preset mới tại Cloudinary Settings > Upload, đặt chế độ signing là **Unsigned**, đặt tên thư mục asset và lưu lại.
  - Điền tên Environment và Upload Preset vào các node Cloudinary tương ứng trong n8n.

- **Các node AI Agent & LLM:**
  - Chọn credentials OpenAI cho các node `LLM` và `LLM1` (sử dụng `gpt-4o-mini`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách kích hoạt thủ công từ `Schedule Trigger` hoặc `Remote manual trigger`.
- Kiểm tra các bước review trên giao diện gotoHuman.
- Sau khi mọi thứ chạy trơn tru, hãy bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động đăng bài:** Ở node cuối cùng (`Homework: Post it` / NoOp), các sếp có thể thay thế bằng node kết nối trực tiếp với Facebook Page, TikTok, Instagram hoặc YouTube để tự động đăng video ngay khi được phê duyệt.
- **Lưu trữ dữ liệu:** Thêm một node Google Sheets hoặc Airtable để ghi log lại toàn bộ các ý tưởng và video đã được duyệt nhằm phục vụ cho việc báo cáo.
- **Mở rộng kênh thông báo:** Tích hợp thêm node Telegram hoặc Slack để gửi thông báo về điện thoại ngay khi có một task mới chờ con người phê duyệt trên gotoHuman.

### 📌 Kết luận
Tự động hóa sáng tạo nội dung không còn là điều gì đó quá xa vời hay tốn kém. Bằng cách kết hợp sức mạnh tổng hợp của AI hiện đại và sự kiểm soát chặt chẽ từ con người thông qua workflow này, các sếp hoàn toàn có thể làm chủ quy trình sản xuất truyền thông chuyên nghiệp cho doanh nghiệp của mình. Chúc các sếp "lên đồ" thành công!