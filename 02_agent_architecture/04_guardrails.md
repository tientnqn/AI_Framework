# 02.04 — Guardrails: Ràng Buộc, An Toàn & Kiểm Soát Agent

> **Mục tiêu:** Thiết kế các lớp kiểm soát để agent hoạt động đúng phạm vi, an toàn và có thể tin cậy.

---

## 1. Tại sao Guardrails quan trọng?

Agent có khả năng tự thực thi nhiều bước — **một sai lầm có thể dẫn đến chuỗi hành động sai**.  
Trong ngữ cảnh banking: dữ liệu nhạy cảm, tuân thủ pháp lý, và rủi ro vận hành đòi hỏi kiểm soát nghiêm ngặt hơn bình thường.

---

## 2. Ba lớp Guardrails

```
Layer 1 — INPUT GUARD      Kiểm soát đầu vào trước khi LLM xử lý
Layer 2 — PROCESS GUARD    Kiểm soát trong quá trình agent thực thi
Layer 3 — OUTPUT GUARD     Kiểm soát đầu ra trước khi trả về user
```

---

## 3. Chi tiết từng lớp

### Layer 1 — Input Guard
| Kiểm soát | Mô tả |
|-----------|-------|
| Input validation | Kiểm tra format, độ dài, ký tự đặc biệt |
| PII detection | Phát hiện và mask dữ liệu cá nhân trước khi đưa vào prompt |
| Prompt injection detection | Phát hiện lệnh cố tình override system prompt |
| Scope check | Yêu cầu có nằm trong phạm vi agent không? |

### Layer 2 — Process Guard
| Kiểm soát | Mô tả |
|-----------|-------|
| Human-in-the-loop | Yêu cầu xác nhận người dùng trước hành động rủi ro cao |
| Tool execution limit | Giới hạn số lần gọi tool trong một session |
| Loop detection | Phát hiện và dừng khi agent lặp vô hạn |
| Step timeout | Hủy nếu một bước mất quá nhiều thời gian |

### Layer 3 — Output Guard
| Kiểm soát | Mô tả |
|-----------|-------|
| PII scrubbing | Xóa thông tin nhạy cảm khỏi output |
| Factual grounding check | Kiểm tra output có dựa trên nguồn thực tế không |
| Confidence threshold | Từ chối trả lời nếu độ tin cậy quá thấp |
| Format validation | Đảm bảo output đúng cấu trúc mong đợi |

---

## 4. Human-in-the-Loop — Khi nào bắt buộc?

```
BẮT BUỘC có human approval trước khi thực thi:
  ✓ Hành động write/delete dữ liệu quan trọng
  ✓ Gọi API external có side effect
  ✓ Quyết định ảnh hưởng đến khách hàng cuối
  ✓ Khi agent có độ tin cậy thấp với task

KHÔNG cần human approval:
  ✓ Read-only queries
  ✓ Tạo bản nháp (user vẫn review trước khi dùng)
  ✓ Task lặp lại đã được kiểm chứng nhiều lần
```

---

## 5. Template Guardrails Config

```markdown
## GUARDRAILS: [Tên Agent]

**Input:**
- [ ] Validate input format trước khi xử lý
- [ ] Mask PII: [danh sách trường nhạy cảm]
- [ ] Từ chối nếu yêu cầu ngoài scope: [mô tả scope]

**Process:**
- Human approval bắt buộc cho: [danh sách action]
- Tool call limit per session: [N]
- Timeout per step: [X giây]

**Output:**
- Scrub trước khi trả về: [danh sách trường]
- Từ chối trả lời khi: [điều kiện]
- Luôn kèm disclaimer cho: [loại output]
```

---

## 6. Checklist Guardrails

```
□ Đã có Input Guard cho PII và prompt injection?
□ Đã xác định action nào cần human approval?
□ Đã có cơ chế phát hiện và thoát khỏi loop?
□ Đã có Output Guard loại bỏ dữ liệu nhạy cảm?
□ Đã test các attack vector phổ biến (injection, jailbreak)?
□ Đã có fallback rõ ràng khi guardrail bị trigger?
□ Đã log đủ thông tin để audit sau sự cố?
```

---

*Hoàn thành `02_agent_architecture/`. Tiếp theo: [`03_use_cases/`](../03_use_cases/) — Case thực tế R&D & banking.*
