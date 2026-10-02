# 02.02 — Tools: Tích Hợp Công Cụ & Khả Năng Agent

> **Mục tiêu:** Định nghĩa agent được dùng công cụ gì, khi nào, và kiểm soát ra sao.

---

## 1. Tool là gì?

Tool = khả năng agent **thực thi hành động ra thế giới bên ngoài** — gọi API, đọc file, truy vấn DB, chạy code...  
Không có tool, agent chỉ là chatbot. Có tool, agent mới thực sự "làm việc".

---

## 2. Phân loại Tool

| Nhóm | Ví dụ | Mức độ rủi ro |
|------|-------|--------------|
| **Read-only** | Truy vấn DB, đọc file, gọi API GET | Thấp |
| **Write** | Tạo file, ghi DB, gọi API POST/PUT | Trung bình |
| **Execute** | Chạy code, gọi webhook, trigger workflow | Cao |
| **External** | Gọi service bên thứ ba, internet search | Trung bình–Cao |

> ⚠️ **Nguyên tắc least privilege:** Chỉ cấp tool thực sự cần — không cấp thừa.

---

## 3. Template định nghĩa Tool

```markdown
## TOOL: [Tên tool]

**Mô tả:** [Tool làm gì]
**Khi nào dùng:** [Điều kiện trigger]
**Input:** [Tham số đầu vào, kiểu dữ liệu]
**Output:** [Định dạng trả về]
**Giới hạn:** [Rate limit, timeout, dữ liệu không được truyền vào]
**Fallback:** [Xử lý khi tool lỗi hoặc không có kết quả]
```

---

## 4. Ví dụ thực tế — Agent tra cứu thông tin khách hàng ngân hàng

```markdown
## TOOL: search_customer

**Mô tả:** Tra cứu thông tin khách hàng từ core banking system
**Khi nào dùng:** Khi user cung cấp CIF hoặc số tài khoản và yêu cầu thông tin KH
**Input:** { "cif": string } hoặc { "account_number": string }
**Output:** { name, account_status, segment, last_transaction_date }
**Giới hạn:**
  - Không trả về số dư tài khoản
  - Không dùng với input chưa được xác thực
**Fallback:** Nếu không tìm thấy → thông báo user và dừng, không đoán mò
```

---

## 5. Tool Selection Logic

Khi agent nhận một yêu cầu, LLM cần quyết định:

```
1. Task này có cần tool không?
   → Nếu không: trả lời trực tiếp

2. Cần tool nào?
   → Khớp yêu cầu với danh sách tool được phép

3. Đủ thông tin để gọi tool chưa?
   → Nếu thiếu: hỏi user trước khi gọi

4. Kết quả tool có đủ để trả lời không?
   → Nếu không: gọi thêm tool hoặc thông báo giới hạn
```

---

## 6. Checklist khi thêm Tool mới

```
□ Tool này thực sự cần thiết cho mục tiêu agent?
□ Đã định nghĩa rõ input/output và kiểu dữ liệu?
□ Đã xác định mức độ rủi ro và cơ chế kiểm soát?
□ Đã có fallback khi tool lỗi?
□ Đã test với input biên (null, sai format, quá lớn)?
□ Có cần human approval trước khi thực thi không?
```

---

*Tiếp theo: [`03_memory.md`](./03_memory.md) — Quản lý ngữ cảnh & bộ nhớ agent.*
