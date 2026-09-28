---
title: "🔄 Chuyển đổi Notion ↔ Markdown Tự động: Giảm 90% Thời gian Chỉnh Sửa Văn Bản"
description: "Workflow này tự động chuyển đổi nội dung từ Notion sang Markdown và ngược lại, giúp các sếp tiết kiệm thời gian chỉnh sửa, đồng bộ hóa nội dung giữa hai nền tảng, và duy trì tính nhất quán cho tài liệu. Hỗ trợ cả định dạng phong phú (bold, links, lists...) mà không cần viết code."
slug: "chuyen-doi-notion-sang-markdown-va-nguoc-lai"
tags: [n8n, automation, notion, markdown, no-code, content-management]
keywords: [n8n workflow Notion, tự động hóa chuyển đổi văn bản, Notion sang Markdown tự động, đồng bộ hóa nội dung, tiết kiệm thời gian chỉnh sửa]
---

# 🔄 **Chuyển đổi Notion ↔ Markdown Tự động: Giải pháp Tiết kiệm Thời gian cho Các Sếp**

### **Nỗi đau thực tế của các sếp khi làm thủ công**
Các sếp thường phải mất **giờ đồng hồ** để chuyển đổi nội dung giữa Notion và Markdown, đặc biệt khi:
- Cần đồng bộ hóa tài liệu giữa Notion (để quản lý nội dung) và Markdown (để chia sẻ trên GitHub, blog, hoặc tài liệu kỹ thuật).
- Muốn **tối ưu hóa định dạng** (bold, links, lists, code blocks...) khi chuyển đổi sang Markdown.
- **Sửa đổi liên tục** và không muốn mất thời gian copy-paste thủ công.

Workflow này **giải quyết tất cả vấn đề trên** bằng cách tự động hóa toàn bộ quy trình chuyển đổi **với định dạng hoàn toàn nguyên vẹn**, không cần viết một dòng code nào!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Đồng bộ hóa tự động** giữa Notion và Markdown (hoặc ngược lại).
- **Bảo toàn định dạng** (bold, links, danh sách, code blocks...) khi chuyển đổi.
- **Hoạt động 24/7** trên VPS, không cần can thiệp thủ công.
- **Dễ dàng mở rộng** để tích hợp với Slack, Telegram, hoặc gửi báo cáo định kỳ.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** và **API Key** của Notion:
   - Tạo API Key tại [Notion Developer Settings](https://www.notion.so/my-integrations).
   - Thêm credential `notionApi` trong n8n với:
     - **API Key**: Dán API Key từ Notion.
     - **Workspace URL**: `https://www.notion.so/workspaces/[YOUR_WORKSPACE_ID]` (thay `[YOUR_WORKSPACE_ID]` bằng ID workspace của bạn).
2. **Workflow Notion** (để trigger chuyển đổi):
   - Tạo một **Notion Page** hoặc **Database** và chia sẻ link với quyền **Read/Write** cho n8n.
3. **VPS Self-hosted** (khuyến nghị):
   - Để workflow chạy 24/7, các sếp nên cài n8n trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2901) hoặc copy toàn bộ JSON dưới đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "resource": "block",
          "operation": "getAll"
        },
        "name": "Notion Trigger",
        "type": "notionTrigger",
        "credentials": {
          "notionApi": "notion-api-credential"
        }
      },
      {
        "parameters": {},
        "name": "Notion",
        "type": "notion",
        "credentials": {
          "notionApi": "notion-api-credential"
        }
      },
      {
        "parameters": {
          "resource": "code"
        },
        "name": "Notion Node Blocks to Md",
        "type": "code"
      },
      {
        "parameters": {},
        "name": "Split Out",
        "type": "splitOut"
      },
      {
        "parameters": {
          "resource": "code"
        },
        "name": "Full Notion Blocks to Md",
        "type": "code"
      },
      {
        "parameters": {
          "resource": "code"
        },
        "name": "Md to Notion Blocks v3",
        "type": "code"
      },
      {
        "parameters": {
          "method": "POST",
          "url": "https://api.notion.com/v1/pages"
        },
        "name": "Add blocks as Children",
        "type": "httpRequest",
        "credentials": {
          "notionApi": "notion-api-credential"
        }
      },
      {
        "parameters": {
          "method": "GET",
          "url": "https://api.notion.com/v1/blocks/{BLOCK_ID}/children"
        },
        "name": "Get Child blocks",
        "type": "httpRequest",
        "credentials": {
          "notionApi": "notion-api-credential"
        }
      }
    ],
    "connections": {
      "notionTrigger": ["Notion"],
      "Notion": ["Notion Node Blocks to Md"],
      "Notion Node Blocks to Md": ["Split Out"],
      "Split Out": ["Full Notion Blocks to Md"],
      "Full Notion Blocks to Md": ["Md to Notion Blocks v3"],
      "Md to Notion Blocks v3": ["Add blocks as Children"],
      "Add blocks as Children": ["Get Child blocks"]
    }
  }
  ```
- **Import vào n8n Editor**:
  - Mở n8n và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
  - **Hoặc** copy/paste JSON vào **Create Workflow** → **Import from JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **2 phương pháp** để lấy dữ liệu Notion:
- **Phương pháp 1 (khuyến nghị)**: Sử dụng **Notion Node** (`n8n-nodes-base.notion`) để lấy dữ liệu block.
  - **Ưu điểm**: Dễ dàng cấu hình, hỗ trợ định dạng cơ bản (bold, links...).
  - **Nhược điểm**: Không hỗ trợ **rich text** (như code blocks, danh sách có dấu).
- **Phương pháp 2**: Sử dụng **HTTP Request** (`n8n-nodes-base.httpRequest`) để lấy dữ liệu block **rich text**.
  - **Ưu điểm**: Hỗ trợ **tất cả định dạng** (bold, links, code, lists...).
  - **Nhược điểm**: Cần cấu hình API URL và headers.

##### **Cấu hình chi tiết các node quan trọng**:
1. **Notion Trigger**:
   - Chọn **Trigger**: `notionTrigger`.
   - **Credentials**: Chọn `notionApi` (đã tạo trước đó).
   - **Lưu ý**: Workflow này sẽ **trigger** khi có sự thay đổi trong Notion (ví dụ: chỉnh sửa một page).

2. **Notion Node (lấy block)**:
   - **Operation**: `getAll`.
   - **Resource**: `block`.
   - **Credentials**: `notionApi`.
   - **Lưu ý**:
     - Nếu muốn lấy **rich text**, **bỏ qua node này** và sử dụng **HTTP Request** thay vào.

3. **Notion Node Blocks to Md (Code Node)**:
   - **Mã JavaScript**:
     ```javascript
     // Chuyển đổi block Notion sang Markdown
     const { blocks } = $input.all();
     const mdBlocks = blocks.map(block => {
       if (block.type === "paragraph") {
         return block.paragraph.rich_text.map(text => {
           if (text.type === "text") return text.text.content;
           else if (text.type === "link") return `[${text.text.content}](${text.link.url})`;
         }).join("");
       } else if (block.type === "heading_1") {
         return `# ${block.heading_1.rich_text[0].text.content}`;
       } else if (block.type === "heading_2") {
         return `## ${block.heading_2.rich_text[0].text.content}`;
       } else if (block.type === "bulleted_list_item") {
         return `- ${block.bulleted_list_item.rich_text[0].text.content}`;
       }
     }).join("\n");
     return { mdContent: mdBlocks };
     ```
   - **Lưu ý**: Nếu muốn hỗ trợ **code blocks**, **danh sách có dấu**, hoặc **links**, cần **cập nhật mã này**.

4. **Split Out**:
   - **Lưu ý**: Node này chia dữ liệu thành các block riêng lẻ để xử lý.

5. **Full Notion Blocks to Md (Code Node)**:
   - **Mã JavaScript** (cập nhật để hỗ trợ rich text):
     ```javascript
     // Chuyển đổi block Notion sang Markdown với rich text
     const { blocks } = $input.all();
     const mdBlocks = blocks.map(block => {
       if (block.type === "paragraph") {
         return block.paragraph.rich_text.map(text => {
           if (text.type === "text") return text.text.content;
           else if (text.type === "link") return `[${text.text.content}](${text.link.url})`;
           else if (text.type === "code") return \`\`\`${text.code.language || 'text'}\n${text.code.text}\n\`\`\``;
         }).join("");
       } else if (block.type === "code") {
         return \`\`\`${block.code.language || 'text'}\n${block.code.text}\n\`\`\``;
       } else if (block.type === "heading_1") {
         return `# ${block.heading_1.rich_text[0].text.content}`;
       } else if (block.type === "heading_2") {
         return `## ${block.heading_2.rich_text[0].text.content}`;
       } else if (block.type === "bulleted_list_item") {
         return `- ${block.bulleted_list_item.rich_text[0].text.content}`;
       }
     }).join("\n");
     return { mdContent: mdBlocks };
     ```
   - **Lưu ý**: Cập nhật mã này để hỗ trợ **tất cả định dạng**.

6. **Md to Notion Blocks v3 (Code Node)**:
   - **Mã JavaScript** (chuyển đổi Markdown sang block Notion):
     ```javascript
     // Chuyển đổi Markdown sang block Notion
     const { mdContent } = $input.all();
     const lines = mdContent.split("\n");
     const blocks = [];
     for (const line of lines) {
       if (line.startsWith("# ")) {
         blocks.push({
           type: "heading_1",
           heading_1: {
             rich_text: [{ type: "text", text: { content: line.substring(2) } }]
           }
         });
       } else if (line.startsWith("## ")) {
         blocks.push({
           type: "heading_2",
           heading_2: {
             rich_text: [{ type: "text", text: { content: line.substring(3) } }]
           }
         });
       } else if (line.startsWith("- ")) {
         blocks.push({
           type: "bulleted_list_item",
           bulleted_list_item: {
             rich_text: [{ type: "text", text: { content: line.substring(2) } }]
           }
         });
       } else if (line.startsWith("```")) {
         const codeBlock = line.substring(3);
         blocks.push({
           type: "code",
           code: {
             language: "text",
             text: codeBlock
           }
         });
       } else {
         blocks.push({
           type: "paragraph",
           paragraph: {
             rich_text: [{ type: "text", text: { content: line } }]
           }
         });
       }
     }
     return { blocks };
     ```

7. **Add blocks as Children (HTTP Request)**:
   - **Method**: `POST`.
   - **URL**: `https://api.notion.com/v1/pages/{PAGE_ID}/children` (thay `{PAGE_ID}` bằng ID page Notion muốn thêm block).
   - **Headers**:
     - `Content-Type`: `application/json`
     - `Notion-Version`: `2022-06-28`
     - `Authorization`: `Bearer {NOTION_API_KEY}`
   - **Body**:
     ```json
     {
       "children": $input.all().blocks
     }
     ```
   - **Lưu ý**: Cần **điền `PAGE_ID`** của page Notion muốn thêm block.

8. **Get Child blocks (HTTP Request)**:
   - **Method**: `GET`.
   - **URL**: `https://api.notion.com/v1/blocks/{BLOCK_ID}/children` (thay `{BLOCK_ID}` bằng ID block muốn lấy con block).
   - **Headers**:
     - `Notion-Version`: `2022-06-28`
     - `Authorization`: `Bearer {NOTION_API_KEY}`
   - **Lưu ý**: Node này **không bắt buộc** nhưng có thể dùng để lấy block con.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Run** với một **Notion Page** mẫu.
   - Kiểm tra kết quả Markdown và Notion có **đồng bộ** không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH MỞ RỘNG THÊM]
1. **Gửi Markdown qua Slack/Telegram**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để gửi kết quả Markdown vào chat nhóm.
2. **Lưu log chuyển đổi**:
   - Thêm node `n8n-nodes-base.file` để lưu **log** của mỗi lần chuyển đổi vào file CSV hoặc JSON.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để **chạy workflow hàng ngày** và gửi báo cáo tổng hợp qua email.
4. **Tích hợp với GitHub**:
   - Sử dụng node `n8n-nodes-base.github` để **push** Markdown vào repository GitHub tự động.
5. **Chuyển đổi nhiều page Notion**:
   - Sử dụng node `n8n-nodes