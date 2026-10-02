# 02.03 — Memory: Quản Lý Ngữ Cảnh & Bộ Nhớ Agent

> **Mục tiêu:** Hiểu các loại memory, khi nào dùng loại nào, và cách thiết kế cho đúng.

---

## 1. Vấn đề cốt lõi

LLM **không có bộ nhớ tự nhiên** giữa các lần gọi — mỗi request là một tờ giấy trắng.  
Memory là cơ chế ta thiết kế để agent "nhớ" được thông tin cần thiết.

---

## 2. Bốn loại Memory

| Loại | Lưu ở đâu | Tồn tại bao lâu | Dùng khi nào |
|------|-----------|----------------|-------------|
| **In-context** | Trong prompt (conversation history) | Trong session | Hội thoại ngắn, thông tin tạm thời |
| **External (DB)** | Vector DB, SQL, file | Lâu dài | Kiến thức domain, tài liệu nội bộ |
| **Cache** | Lưu kết quả tool/query | Tạm thời | Tránh gọi tool lặp, tiết kiệm chi phí |
| **Episodic** | Log các session trước | Lâu dài | Agent cần "nhớ" lịch sử tương tác với user |

---

## 3. In-Context Memory — Quản lý conversation history

Đây là loại đơn giản nhất nhưng có giới hạn token. Cần quản lý chủ động:

```
Chiến lược xử lý khi context dài:

1. SUMMARIZE   — Tóm tắt các turn cũ, giữ turn gần nhất nguyên vẹn
2. SLIDING WINDOW — Chỉ giữ N turn gần nhất
3. SELECTIVE   — Chỉ giữ các turn có thông tin quan trọng (đã đánh dấu)
```

---

## 4. External Memory — RAG Pattern

Dùng khi agent cần truy xuất kiến thức từ tài liệu nội bộ (spec, policy, lịch sử ticket...):

```
User Query
    ↓
[Embedding Model] → Vector
    ↓
[Vector DB Search] → Top-K chunks liên quan
    ↓
[Inject vào prompt] → LLM trả lời dựa trên context tìm được
```

**Lưu ý khi triển khai RAG:**
- Chất lượng chunking ảnh hưởng trực tiếp đến chất lượng retrieval
- Cần metadata (nguồn, ngày, version) để agent biết context của tài liệu
- Luôn trả về source reference để người dùng có thể verify

---

## 5. Template — Memory Strategy cho một Agent

```markdown
## MEMORY DESIGN: [Tên Agent]

**In-context:**
- Giữ tối đa [N] turn gần nhất
- Summarize khi vượt [X] tokens
- Thông tin bắt buộc giữ nguyên: [list]

**External (nếu có):**
- Nguồn dữ liệu: [tên DB / tài liệu]
- Trigger retrieval khi: [điều kiện]
- Số chunks trả về: [K]

**Không lưu vào memory:**
- [Thông tin nhạy cảm — PII, credentials]
- [Thông tin chỉ dùng một lần]
```

---

## 6. Checklist Memory Design

```
□ Xác định loại memory phù hợp với use case?
□ Đã có chiến lược xử lý khi context vượt giới hạn token?
□ Đã loại trừ thông tin nhạy cảm (PII, secret) khỏi memory?
□ External memory có metadata đủ để trace nguồn gốc?
□ Đã test hành vi khi memory rỗng (first-time user)?
```

---

*Tiếp theo: [`04_guardrails.md`](./04_guardrails.md) — Ràng buộc, an toàn và kiểm soát agent.*
