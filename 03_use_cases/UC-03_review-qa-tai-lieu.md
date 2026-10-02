# UC-03 — Review & QA Tài Liệu

> **Mục tiêu:** Phát hiện lỗ hổng logic, thiếu sót compliance, và điểm mơ hồ trong spec/design trước khi triển khai.

---

## Bối cảnh

Review tài liệu thủ công dễ bỏ sót, đặc biệt với tài liệu dài. AI giỏi phát hiện inconsistency, missing cases, và điểm chưa được xử lý — giúp team review nhanh hơn và sâu hơn.

---

## Prompt Templates

### Review Logic & Completeness
```
Bạn là Senior Software Architect.
Review tài liệu thiết kế dưới đây và chỉ ra:

1. LOGIC GAPS — Luồng xử lý có lỗ hổng hoặc edge case chưa được xử lý
2. MISSING CASES — Tình huống nào có thể xảy ra nhưng tài liệu chưa đề cập
3. CONTRADICTIONS — Các điểm mâu thuẫn nhau trong tài liệu
4. UNCLEAR POINTS — Những phần mơ hồ, có thể hiểu theo nhiều cách

Với mỗi vấn đề: nêu vị trí, mô tả vấn đề, đề xuất cách xử lý.

[DÁN TÀI LIỆU VÀO ĐÂY]
```

### Review Compliance (Banking)
```
Bạn là chuyên gia compliance ngân hàng tại Việt Nam.
Review tài liệu sau và xác định các điểm có thể vi phạm hoặc
cần chú ý về:
- Quy định SBV (Ngân hàng Nhà nước)
- AML/CFT (chống rửa tiền)
- Bảo vệ dữ liệu cá nhân (Nghị định 13/2023)
- PCI-DSS (nếu liên quan đến thanh toán)

Với mỗi điểm: trích dẫn phần trong tài liệu, nêu rủi ro, đề xuất điều chỉnh.

[DÁN TÀI LIỆU VÀO ĐÂY]
```

### Review API Contract
```
Review API contract dưới đây:
1. Các endpoint có đặt tên nhất quán không? (RESTful conventions)
2. Error handling có đủ các case quan trọng không?
3. Authentication/authorization có được mô tả rõ không?
4. Có breaking change nào so với version cũ không? [đính kèm version cũ nếu có]
5. Response schema có thiếu field quan trọng không?

[DÁN API CONTRACT VÀO ĐÂY]
```

---

## Workflow đề xuất

```
1. Chạy review logic trước → fix các lỗi cơ bản
2. Chạy review compliance → escalate nếu có điểm nghi ngờ
3. Tổng hợp tất cả issues vào một danh sách
4. Assign cho người phụ trách từng issue
5. Re-review sau khi fix
```

---

## Lưu ý áp dụng

- AI không biết quy định pháp lý cụ thể của Việt Nam 100% chính xác → **bắt buộc có legal/compliance review với tài liệu quan trọng**
- Dùng Gemini 1.5 Pro cho tài liệu dài (>20 trang)
- Output của AI là **danh sách gợi ý** — không phải kết luận cuối cùng
