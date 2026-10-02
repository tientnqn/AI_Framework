# 02.01 — Persona: Định Nghĩa Vai Trò & Hành Vi Agent

> **Mục tiêu:** Xác định agent là "ai", hành xử thế nào, và giới hạn vai trò của nó.

---

## 1. Persona là gì?

Persona = **system prompt nền** định nghĩa danh tính, chuyên môn, tone và hành vi mặc định của agent.  
Persona ảnh hưởng đến **mọi output** — thiết kế sai ở đây, mọi thứ phía sau đều lệch.

---

## 2. Bốn thành phần của một Persona

| Thành phần | Mô tả | Ví dụ |
|------------|-------|-------|
| **Role** | Agent đóng vai gì, có chuyên môn gì | "Senior Business Analyst chuyên lĩnh vực ngân hàng" |
| **Behavior** | Cách tiếp cận, phong cách làm việc | "Luôn hỏi lại nếu yêu cầu chưa rõ trước khi thực thi" |
| **Tone** | Phong cách giao tiếp | "Chuyên nghiệp, súc tích, không dùng jargon thừa" |
| **Boundary** | Điều agent không làm | "Không đưa ra quyết định cuối — chỉ phân tích và đề xuất" |

---

## 3. Template Persona

```markdown
## ROLE
Bạn là [vai trò] với chuyên môn về [lĩnh vực].
Bạn đang làm việc trong ngữ cảnh [mô tả tổ chức/dự án].

## BEHAVIOR
- [Hành vi 1 — ví dụ: luôn xác nhận yêu cầu trước khi thực thi]
- [Hành vi 2 — ví dụ: trình bày lý luận trước khi đưa ra kết luận]
- [Hành vi 3 — ví dụ: nêu giả định khi thông tin không đủ]

## TONE
[Mô tả phong cách giao tiếp phù hợp với đối tượng]

## BOUNDARY
- Bạn KHÔNG [hành động bị cấm 1]
- Bạy KHÔNG [hành động bị cấm 2]
- Khi gặp [tình huống X], bạn sẽ [hành động dự phòng]
```

---

## 4. Ví dụ thực tế — Agent hỗ trợ phân tích yêu cầu ngân hàng

```markdown
## ROLE
Bạn là Business Analyst chuyên về chuyển đổi số ngân hàng.
Bạn hỗ trợ team R&D phân tích và làm rõ yêu cầu từ khách hàng.

## BEHAVIOR
- Luôn phân tích yêu cầu theo 3 chiều: nghiệp vụ / kỹ thuật / tuân thủ
- Nếu yêu cầu mâu thuẫn hoặc thiếu thông tin, hỏi lại trước khi phân tích
- Trình bày assumption rõ ràng khi thiếu dữ liệu

## TONE
Chuyên nghiệp, trung lập, tập trung vào bằng chứng. Không đưa ý kiến cá nhân.

## BOUNDARY
- Không đưa ra quyết định kiến trúc hệ thống — chỉ phân tích yêu cầu
- Không cam kết timeline hoặc effort estimate
- Khi gặp câu hỏi pháp lý/compliance: cảnh báo cần tham chiếu chuyên gia
```

---

## 5. Lỗi Persona phổ biến

| Lỗi | Hậu quả | Cách sửa |
|-----|---------|----------|
| Role quá chung chung | Output generic | Chỉ định domain + ngữ cảnh cụ thể |
| Không có Boundary | Agent làm vượt phạm vi | Liệt kê rõ điều không được làm |
| Behavior mâu thuẫn | Agent hành xử không nhất quán | Test với edge case, tinh chỉnh |
| Tone không phù hợp đối tượng | Giao tiếp lệch kỳ vọng | Xác định rõ end-user của agent |

---

*Tiếp theo: [`02_tools.md`](./02_tools.md) — Tích hợp công cụ & khả năng của agent.*
