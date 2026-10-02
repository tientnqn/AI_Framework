# UC-05 — Chuẩn Bị Nội Dung Báo Cáo Lãnh Đạo

> **Mục tiêu:** Từ dữ liệu/thông tin thô → tóm tắt executive summary cho CTO/CEO ngân hàng.

---

## Bối cảnh

Lãnh đạo cấp cao cần thông tin nhanh, rõ, có thể ra quyết định ngay. Phần lớn thời gian chuẩn bị báo cáo là chuyển đổi từ ngôn ngữ kỹ thuật sang ngôn ngữ business — AI làm tốt việc này.

---

## Prompt Templates

### Executive Summary từ tài liệu kỹ thuật
```
Chuyển tài liệu kỹ thuật dưới đây thành executive summary
cho CTO/CEO ngân hàng (không có background kỹ thuật sâu).

Cấu trúc output:
- Vấn đề: [1-2 câu]
- Giải pháp đề xuất: [2-3 câu]
- Lợi ích kinh doanh: [3 bullet]
- Rủi ro cần lưu ý: [2-3 bullet]
- Quyết định cần từ lãnh đạo: [rõ ràng, cụ thể]

Giới hạn: không quá 250 từ. Không dùng jargon kỹ thuật.

[DÁN TÀI LIỆU VÀO ĐÂY]
```

### Cập nhật tiến độ dự án
```
Viết báo cáo tiến độ dự án [tên] cho buổi họp với lãnh đạo.

Thông tin đầu vào:
- Tiến độ thực tế: [%hoàn thành, milestone đã đạt]
- So với kế hoạch: [đúng hạn / trễ X ngày / sớm]
- Vấn đề đang gặp: [mô tả ngắn]
- Kế hoạch tiếp theo: [2 tuần tới làm gì]
- Cần hỗ trợ gì từ lãnh đạo: [nếu có]

Tone: thẳng thắn, không tô hồng, không bi quan thái quá.
Format: bullet points, không quá 1 trang A4.
```

### Đề xuất đầu tư / phê duyệt
```
Viết tờ trình đề xuất [tên đề xuất] cho Ban Lãnh đạo.

Thông tin:
- Bài toán cần giải quyết: [...]
- Giải pháp đề xuất: [...]
- Chi phí ước tính: [...]
- ROI / lợi ích kỳ vọng: [...]
- Timeline: [...]
- Rủi ro và biện pháp giảm thiểu: [...]

Cấu trúc: Bối cảnh → Đề xuất → Chi phí-Lợi ích → Rủi ro → Kiến nghị
Độ dài: không quá 1 trang. Ngôn ngữ: business, không kỹ thuật.
```

---

## Nguyên tắc viết cho lãnh đạo

```
✓ Kết luận trước, chi tiết sau (Pyramid Principle)
✓ Số liệu cụ thể > mô tả định tính
✓ Rủi ro phải nêu kèm biện pháp xử lý
✓ Luôn có "Lãnh đạo cần quyết định gì?" ở cuối
✗ Không dùng: "leverage", "synergy", "robust", "scalable" khi không cần thiết
✗ Không ẩn bad news — nêu thẳng kèm plan B
```

---

## Lưu ý áp dụng

- AI không biết culture nội bộ và mối quan hệ với lãnh đạo — tone cuối cùng do người viết quyết định
- Luôn review số liệu trước khi trình bày
- Dùng kết quả làm bản nháp, không gửi thẳng
