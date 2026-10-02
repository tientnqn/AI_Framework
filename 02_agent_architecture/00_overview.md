# 02.00 — Agent Architecture: Tổng Quan

> **Mục tiêu:** Hiểu agent là gì, gồm những thành phần nào, và khi nào nên xây dựng agent.

---

## 1. Agent là gì?

Agent = AI có khả năng **tự lập kế hoạch và thực thi nhiều bước** để hoàn thành mục tiêu, thay vì chỉ trả lời một câu hỏi đơn lẻ.

```
Chatbot thường:  Input → [LLM] → Output

Agent:           Goal → [LLM] → Plan → [Tool/Action] → Observe
                              ↑__________________________|
                              (lặp lại đến khi hoàn thành)
```

---

## 2. Năm thành phần cốt lõi

| Thành phần | Vai trò | File chi tiết |
|------------|---------|--------------|
| **Persona** | Định nghĩa vai trò, hành vi, tone của agent | `01_persona.md` |
| **Tools** | Công cụ agent được phép sử dụng | `02_tools.md` |
| **Memory** | Cách agent lưu và truy xuất ngữ cảnh | `03_memory.md` |
| **Guardrails** | Ràng buộc, giới hạn, kiểm soát an toàn | `04_guardrails.md` |
| **Orchestration** | Logic điều phối luồng thực thi | *(nằm trong overview này)* |

---

## 3. Khi nào nên xây Agent?

**Nên xây agent khi task:**
- Có nhiều bước phụ thuộc nhau
- Cần gọi tool ngoài (API, database, file system)
- Cần lặp lại dựa trên kết quả trung gian

**Không cần agent khi:**
- Task một bước, output đơn giản → dùng prompt thường
- Không có tool nào cần gọi
- Độ trễ và chi phí không cho phép

> ⚠️ Agent phức tạp hơn prompt thường rất nhiều. Đừng over-engineer.

---

## 4. Vòng đời thực thi của một Agent

```
1. GOAL        — Nhận mục tiêu từ user
2. PLAN        — LLM phân tích và lập kế hoạch các bước
3. ACT         — Gọi tool hoặc thực thi hành động
4. OBSERVE     — Nhận kết quả từ tool
5. REFLECT     — LLM đánh giá: đã xong chưa? Cần điều chỉnh không?
6. REPEAT/END  — Lặp lại hoặc trả kết quả cuối cho user
```

---

## 5. Checklist thiết kế agent

```
□ Đã xác định rõ mục tiêu agent cần đạt được?
□ Đã liệt kê các tool agent được phép dùng?
□ Đã định nghĩa điều kiện dừng (success/failure)?
□ Đã có guardrails cho các hành động rủi ro cao?
□ Đã xác định cần loại memory nào?
□ Đã test với edge case và input bất thường?
```

---

*Tiếp theo: [`01_persona.md`](./01_persona.md) — Định nghĩa vai trò và hành vi agent.*
