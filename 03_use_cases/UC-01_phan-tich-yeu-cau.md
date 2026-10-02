# UC-01 — Phân Tích Yêu Cầu Nghiệp Vụ

> **Mục tiêu:** Đọc, phân loại và làm rõ yêu cầu từ khách hàng ngân hàng nhanh hơn, ít bỏ sót hơn.

---

## Bối cảnh

Khách hàng ngân hàng thường cung cấp yêu cầu dưới dạng email, meeting notes, hoặc tài liệu Word không có cấu trúc. Team R&D mất nhiều thời gian để phân loại, làm rõ và chuẩn hóa trước khi thiết kế giải pháp.

---

## Prompt Template

```
Bạn là Business Analyst chuyên lĩnh vực ngân hàng.
Phân tích yêu cầu dưới đây và trả về kết quả theo cấu trúc:

1. FUNCTIONAL REQUIREMENTS — Liệt kê các yêu cầu chức năng, mỗi item một dòng
2. NON-FUNCTIONAL REQUIREMENTS — Hiệu năng, bảo mật, khả năng mở rộng
3. COMPLIANCE CONCERNS — Các điểm liên quan đến quy định SBV, AML, KYC (nếu có)
4. AMBIGUITIES — Những điểm chưa rõ, cần hỏi lại khách hàng
5. ASSUMPTIONS — Giả định bạn đã đưa ra khi phân tích

Nếu thiếu thông tin để phân tích, hỏi lại trước khi tiếp tục.

[DÁN NỘI DUNG YÊU CẦU VÀO ĐÂY]
```

---

## Ví dụ Output

```
1. FUNCTIONAL REQUIREMENTS
   - Hệ thống xác minh CCCD tự động qua OCR
   - So khớp ảnh chân dung với ảnh CCCD (liveness check)
   - Lưu kết quả xác minh vào hồ sơ KYC khách hàng

2. NON-FUNCTIONAL REQUIREMENTS
   - Thời gian xử lý < 3 giây / request
   - Độ chính xác OCR > 98%

3. COMPLIANCE CONCERNS
   - Cần xác nhận: dữ liệu sinh trắc học lưu trữ có tuân thủ Nghị định 13/2023 không?

4. AMBIGUITIES
   - Xử lý thế nào khi CCCD hết hạn?
   - Có hỗ trợ passport/CMND cũ không?

5. ASSUMPTIONS
   - Giả định chỉ áp dụng cho khách hàng cá nhân
```

---

## Lưu ý áp dụng

- Với tài liệu dài (>5 trang): dùng Gemini 1.5 Pro để tận dụng context window lớn
- Luôn review phần AMBIGUITIES trước khi gửi lại khách hàng
- Kết quả phân tích là **bản nháp** — cần BA hoặc tech lead confirm trước khi dùng chính thức
