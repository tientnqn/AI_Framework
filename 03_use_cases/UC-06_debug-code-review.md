# UC-06 — Hỗ Trợ Debug & Code Review

> **Mục tiêu:** Phát hiện bug tiềm ẩn, cải thiện chất lượng code, và rút ngắn thời gian debug.

---

## Bối cảnh

AI giỏi đọc code và nhận diện pattern — nhưng không biết runtime behavior thực tế. Hiệu quả nhất khi dùng như "senior reviewer" để soi code trước khi merge, hoặc làm rubber duck khi debug bí.

---

## Prompt Templates

### Debug lỗi cụ thể
```
Tôi đang gặp lỗi sau:
- Error message: [copy nguyên văn]
- Context: [mô tả ngắn đang làm gì, dữ liệu đầu vào là gì]
- Đã thử: [những gì đã thử]

[DÁN CODE LIÊN QUAN]

Phân tích nguyên nhân có thể và đề xuất cách fix.
Nếu cần thêm thông tin để chẩn đoán, hỏi tôi trước.
```

### Code Review
```
Review đoạn code dưới đây. Tập trung vào:
1. Bug tiềm ẩn hoặc edge case chưa xử lý
2. Security issues (injection, auth, data exposure)
3. Performance bottleneck
4. Readability và maintainability
5. Đề xuất refactor nếu có (kèm lý do)

Ngôn ngữ: [Python/Java/...] | Context: [mô tả ngắn]

[DÁN CODE VÀO ĐÂY]
```

### Giải thích code
```
Giải thích đoạn code dưới đây cho [Junior Dev / Senior Dev / non-technical stakeholder].
Tập trung vào: logic chính, tại sao viết vậy, side effect tiềm ẩn.

[DÁN CODE VÀO ĐÂY]
```

### Viết unit test
```
Viết unit test cho function dưới đây.
Framework: [Jest / pytest / JUnit / ...]
Bao gồm: happy path, edge cases, error cases.
Nếu cần mock, chỉ rõ cần mock gì.

[DÁN CODE VÀO ĐÂY]
```

---

## Workflow đề xuất

```
Debug:
1. Copy error + code liên quan → AI phân tích nguyên nhân
2. Thử fix theo gợi ý → nếu vẫn lỗi, cung cấp thêm log/context
3. Lặp tối đa 3 vòng — nếu vẫn không ra, cần debug thủ công

Code Review:
1. Chạy AI review trước khi tạo PR
2. Fix các issues rõ ràng
3. Các issues cần bàn thêm → comment vào PR để team review
```

---

## Giới hạn cần nhớ

```
⚠️ AI không chạy code thực — không detect runtime errors
⚠️ AI không biết business logic nội bộ — cần cung cấp context
⚠️ Với security-critical code: bắt buộc có human security review
⚠️ Không paste credential, API key, PII vào prompt
```

---

*Hoàn thành `03_use_cases/`. Tiếp theo: [`04_evaluation.md`](../04_evaluation.md) — Đánh giá chất lượng output AI.*
