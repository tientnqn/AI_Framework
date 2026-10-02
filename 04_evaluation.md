# 04 — Evaluation: Đánh Giá Chất Lượng Output AI

> **Mục tiêu:** Biết khi nào tin output AI, khi nào cần kiểm tra lại, và cách cải thiện khi output kém.

---

## 1. Tại sao cần Evaluation?

AI luôn trả lời tự tin — kể cả khi sai. Không có framework đánh giá, team sẽ hoặc **over-trust** (dùng output sai) hoặc **under-trust** (không khai thác được giá trị AI).

---

## 2. Ba câu hỏi đánh giá output

Sau mỗi output AI, tự hỏi:

```
1. ĐÚNG không?       — Thông tin có chính xác, có thể verify không?
2. ĐỦ không?         — Có bao quát đủ yêu cầu, không bỏ sót case quan trọng?
3. DÙNG ĐƯỢC không?  — Có phù hợp ngữ cảnh, đối tượng, và mục đích sử dụng?
```

---

## 3. Ma trận đánh giá theo loại output

| Loại output | Tiêu chí chính | Mức độ cần verify |
|-------------|---------------|------------------|
| Phân tích kỹ thuật | Logic chặt chẽ, coverage đủ | Cao — tech lead review |
| Tài liệu nghiệp vụ | Đúng domain, không mơ hồ | Cao — BA/domain expert review |
| Code / debug | Chạy đúng, không security issue | Rất cao — test + security review |
| Báo cáo lãnh đạo | Số liệu đúng, tone phù hợp | Trung bình — author review |
| Brainstorm / ý tưởng | Đa dạng, có giá trị khai thác | Thấp — team thảo luận |
| Tóm tắt tài liệu | Không bỏ sót ý chính | Trung bình — so với nguồn gốc |

---

## 4. Dấu hiệu output cần làm lại

```
🚩 Trả lời quá chung chung, không có ngữ cảnh cụ thể
🚩 Tự mâu thuẫn trong cùng một output
🚩 Số liệu không có nguồn hoặc không thể verify
🚩 Bỏ qua ràng buộc đã nêu trong prompt
🚩 Không đề cập đến edge case hoặc rủi ro nào
🚩 Tone/format không phù hợp đối tượng
```

---

## 5. Vòng lặp cải thiện output

```
Output kém → Chẩn đoán nguyên nhân → Điều chỉnh prompt → Thử lại

Nguyên nhân phổ biến:
├── Thiếu context  → Bổ sung ngữ cảnh, ràng buộc
├── Role sai       → Thay đổi hoặc làm rõ role
├── Task quá rộng  → Tách nhỏ, dùng prompt chaining
├── Format mơ hồ   → Chỉ định format output cụ thể
└── Model không phù hợp → Thử tool/model khác
```

---

## 6. Evaluation theo vòng đời tài liệu

```
DRAFT      — AI tạo bản nháp         → Chấp nhận 70-80% accuracy
REVIEW     — Human review & chỉnh    → Nâng lên 95%+
PUBLISH    — Tài liệu chính thức     → 100% human-verified
```

> ⚠️ Không bao giờ publish tài liệu quan trọng mà chưa qua bước REVIEW.

---

## 7. Checklist đánh giá trước khi dùng output

```
□ Thông tin có thể verify với nguồn độc lập không?
□ Có logic gap hoặc edge case bị bỏ qua không?
□ Output có phù hợp với đối tượng sử dụng không?
□ Nếu output sai và được dùng → hậu quả là gì? (đánh giá rủi ro)
□ Đã có người có chuyên môn review chưa (nếu high-stakes)?
```

---

## 8. Nguyên tắc chung

> **Output AI tốt đến đâu phụ thuộc vào khả năng đánh giá của bạn.**  
> Nếu bạn không đủ năng lực đánh giá output trong một domain — đừng dùng AI độc lập trong domain đó.

---

*Hoàn thành bộ khung `AI-Working-Framework`. Xem tổng quan tại [`00_mindset.md`](./00_mindset.md).*
