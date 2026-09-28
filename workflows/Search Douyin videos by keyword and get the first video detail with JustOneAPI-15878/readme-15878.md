---
title: "🔍 Tự Động Hóa Tìm Kiếm Video TikTok Trung Quốc (Douyin) & Lấy Chi Tiết Video Đầu Tiên Với JustOneAPI - Không Cần Code"
description: "Workflow tự động hóa tìm kiếm video Douyin (TikTok Trung Quốc) theo từ khóa và lấy chi tiết video đầu tiên với API JustOneAPI, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và thu thập dữ liệu nhanh chóng. Hoàn toàn không cần viết code."
slug: "tu-dong-hoa-tim-kiem-video-douyin-justoneapi"
tags: [n8n, automation, market-research, justoneapi, douyin, no-code]
keywords: [n8n workflow douyin, tự động hóa tìm kiếm video tiktok trung quốc, justoneapi api, nghiên cứu thị trường tiktok, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Video Douyin & Lấy Chi Tiết Video Đầu Tiên Với JustOneAPI**

### **Giải Pháp Cho Các Sếp Nghiên Cứu Thị Trường TikTok Trung Quốc**
Bạn có bao giờ phải **tìm kiếm thủ công hàng trăm video Douyin** (TikTok Trung Quốc) để phân tích xu hướng, nội dung viral, hoặc nghiên cứu đối thủ? Hoặc phải **lấy chi tiết video** (like, share, duration, hashtags...) để xây dựng báo cáo? Thì workflow này sẽ **giải phóng bạn khỏi công việc mòn mỏi đó** với chỉ **một cú nhấp chuột**!

Với **JustOneAPI** và **n8n**, bạn có thể:
✅ **Tìm kiếm video Douyin theo từ khóa** (ví dụ: "sữa tắm", "thời trang", "du lịch").
✅ **Lấy chi tiết video đầu tiên** (tiêu đề, mô tả, số like, share, duration, hashtags...).
✅ **Lưu dữ liệu sạch** vào n8n để sử dụng lại hoặc xuất ra Excel/Google Sheets.
✅ **Hoạt động 24/7** nếu cài đặt trên VPS (self-hosted).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị giới hạn request, các sếp nên **cài n8n trên VPS riêng** (self-hosted).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tìm kiếm thủ công trên Douyin, chỉ cần nhập từ khóa là có kết quả.
- **Dữ liệu chính xác**: Lấy thông tin video đầu tiên (like, share, duration, hashtags...) một cách tự động.
- **Hoạt động liên tục**: Cài trên VPS để chạy 24/7, không giới hạn request.
- **Dữ liệu sạch**: Output được **lọc và định dạng** sẵn, dễ dàng xuất ra Excel/Google Sheets.
- **Nghiên cứu thị trường hiệu quả**: Phân tích xu hướng viral, nội dung hot trên Douyin một cách nhanh chóng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản JustOneAPI** (đăng ký tại [justoneapi.com](https://www.justoneapi.com/)).
✔ **API Key của JustOneAPI** (để cấu hình trong n8n).
✔ **n8n Workflow Editor** (cài đặt trên máy hoặc VPS).
✔ **Biết cách import workflow JSON** (hướng dẫn dưới đây).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Bước 1: **Tải workflow JSON** từ [link gốc](https://n8n.io/workflows/15878) hoặc copy toàn bộ JSON từ đây:
```json
{
  "nodes": {
    "1": {
      "parameters": {},
      "name": "Start Workflow Manually",
      "type": "manualTrigger",
      "typeOptions": {}
    },
    "2": {
      "parameters": {
        "data": {
          "justoneapi_key": "={{$flowData['justoneapi_key']}}",
          "keyword": "={{$flowData['keyword']}}"
        }
      },
      "name": "Set API and Search Parameters",
      "type": "set",
      "typeOptions": {}
    },
    "3": {
      "parameters": {
        "method": "POST",
        "url": "https://api.justoneapi.com/douyin/search",
        "body": {
          "keyword": "={{$flowData['keyword']}}",
          "page": 1,
          "count": 10
        },
        "headers": {
          "Authorization": "Bearer {{ $flowData['justoneapi_key'] }}"
        }
      },
      "name": "Fetch Douyin Video Search Results",
      "type": "httpRequest",
      "typeOptions": {}
    },
    "4": {
      "parameters": {
        "data": {
          "search_results": "={{$json['data']}}"
        }
      },
      "name": "Store Raw Search Results",
      "type": "set",
      "typeOptions": {}
    },
    "5": {
      "parameters": {
        "code": "// Extract video IDs from search results\nconst videoIds = [];\nconst results = $input.all()['search_results'];\nif (results && results.length > 0) {\n  results.forEach(item => {\n    if (item.video && item.video.id) {\n      videoIds.push(item.video.id);\n    }\n  });\n}\nreturn { videoIds: videoIds };\n"
      },
      "name": "Extract Video IDs from Search",
      "type": "code",
      "typeOptions": {}
    },
    "6": {
      "parameters": {
        "data": {
          "video_ids": "={{$json['videoIds']}}"
        }
      },
      "name": "Store Extracted Video IDs",
      "type": "set",
      "typeOptions": {}
    },
    "7": {
      "parameters": {
        "method": "GET",
        "url": "https://api.justoneapi.com/douyin/detail/{{$flowData['video_ids'][0]}}",
        "headers": {
          "Authorization": "Bearer {{ $flowData['justoneapi_key'] }}"
        }
      },
      "name": "Fetch First Video Details",
      "type": "httpRequest",
      "typeOptions": {}
    },
    "8": {
      "parameters": {
        "code": "// Build clean video detail output\nconst videoDetail = $input.all()['json'];\nreturn {\n  title: videoDetail.title,\n  description: videoDetail.description,\n  duration: videoDetail.duration,\n  like_count: videoDetail.like_count,\n  share_count: videoDetail.share_count,\n  hashtags: videoDetail.hashtags || [],\n  author: videoDetail.author,\n  url: videoDetail.url\n};\n"
      },
      "name": "Build Clean Video Detail",
      "type": "code",
      "typeOptions": {}
    },
    "9": {
      "parameters": {
        "data": {
          "clean_video_detail": "={{$json}}"
        }
      },
      "name": "Store Final Video Details",
      "type": "set",
      "typeOptions": {}
    }
  },
  "connections": {
    "manualTrigger": ["Set API and Search Parameters"],
    "Set API and Search Parameters": ["Fetch Douyin Video Search Results"],
    "Fetch Douyin Video Search Results": ["Store Raw Search Results"],
    "Store Raw Search Results": ["Extract Video IDs from Search"],
    "Extract Video IDs from Search": ["Store Extracted Video IDs"],
    "Store Extracted Video IDs": ["Fetch First Video Details"],
    "Fetch First Video Details": ["Build Clean Video Detail"],
    "Build Clean Video Detail": ["Store Final Video Details"]
  }
}
```
**Cách import:**
1. Mở **n8n Workflow Editor**.
2. Nhấn **"Import"** → **"From JSON"** → Dán JSON trên.
3. **Kích hoạt workflow** bằng nút **"Active"**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a. Cấu Hình Credentials JustOneAPI**
- Đi đến **Settings → Credentials → Add New Credential**.
- Chọn **HTTP Request** và đặt tên (ví dụ: `justoneapi`).
- Điền **API Key** từ JustOneAPI vào trường **`Authorization`** (dạng `Bearer YOUR_API_KEY`).
- Lưu và **gán credential này cho node `Fetch Douyin Video Search Results` và `Fetch First Video Details`**.

##### **b. Cấu Hình Tham Số Tìm Kiếm**
- Mở node **"Set API and Search Parameters"** (node ID `2`).
- Điền **API Key** vào biến `$flowData['justoneapi_key']` (đã được tự động gán nếu cấu hình credential).
- Điền **từ khóa tìm kiếm** vào `$flowData['keyword']` (ví dụ: `"sữa tắm"`).

##### **c. Kiểm Tra Output**
- Chạy **Test Run** để kiểm tra kết quả.
- Kiểm tra node **"Store Final Video Details"** để xem dữ liệu đã được **lọc và định dạng** như thế nào.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với từ khóa mẫu (ví dụ: `"thời trang"`).
2. Kiểm tra **output** ở node cuối (`Store Final Video Details`).
3. **Bật Active** workflow để sử dụng thường xuyên.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu dữ liệu vào Google Sheets/Excel**
   - Thêm node **Google Sheets** sau node `"Store Final Video Details"` để tự động lưu dữ liệu vào bảng tính.
   - Cấu hình **Sheet Name** và **Range** để dữ liệu được ghi đè hoặc thêm mới.

2. **Gửi báo cáo định kỳ qua Email/Slack**
   - Thêm node **Email** (n8n-nodes-base.email) hoặc **Slack** để gửi kết quả tìm kiếm hàng ngày/tuần.
   - Ví dụ: Gửi **top 3 video viral** về "sữa tắm" vào mỗi sáng thứ 2.

3. **Tự động hóa theo lịch**
   - Sử dụng **n8n Trigger (Polling)** thay vì **Manual Trigger** để workflow chạy tự động hàng ngày.
   - Cấu hình **interval** (ví dụ: 1 lần/ngày) trong node **Polling**.

4. **Lọc video theo tiêu chí**
   - Sửa node **"Extract Video IDs from Search"** để **lọc video có like > 100k** hoặc **duration > 30s**.
   - Ví dụ:
     ```javascript
     const videoIds = [];
     const results = $input.all()['search_results'];
     if (results && results.length > 0) {
       results.forEach(item => {
         if (item.video && item.video.id && item.video.like_count > 100000) {
           videoIds.push(item.video.id);
         }
       });
     }
     return { videoIds: videoIds };
     ```

5. **Xử lý lỗi API**
   - Thêm node **Set Error Handling** để khi API JustOneAPI lỗi, workflow sẽ **gửi thông báo Slack/Email** thay vì ngừng chạy.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc mòn mỏi tìm kiếm video Douyin thủ công**, giúp **nghiên cứu thị trường hiệu quả hơn** với chỉ **một cú nhấp chuột**. Các sếp có thể:
✔ **Tìm kiếm video theo từ khóa** (sản phẩm, xu hướng, đối thủ).
✔ **Lấy chi tiết video** (like, share, hashtags...) một cách tự động.
✔ **Lưu dữ liệu sạch** để phân tích sau.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa nghiên cứu thị trường Douyin của bạn!** 🚀

---
**🔗 [Tải workflow JSON](https://n8n.io/workflows/15878) | [Đăng ký JustOneAPI](https://www.justoneapi.com/)**