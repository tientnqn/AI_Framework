# UC-04 — Hỗ Trợ Nghiên Cứu Công Nghệ

> **Mục tiêu:** Tổng hợp và so sánh các giải pháp/công nghệ theo tiêu chí định sẵn, rút ngắn thời gian research.

---

## Bối cảnh

Team R&D thường phải evaluate nhiều công nghệ trước khi đề xuất giải pháp. AI giúp tổng hợp thông tin nhanh và cấu trúc hóa so sánh — nhưng cần verify với nguồn thực tế trước khi ra quyết định.

---

## Prompt Templates

### So sánh công nghệ/giải pháp
```
So sánh [A] và [B] cho bài toán [mô tả bài toán].

Ngữ cảnh: [mô tả hệ thống, scale, ràng buộc]
Tiêu chí đánh giá: [hiệu năng / chi phí / độ phức tạp / ecosystem / security / ...]

Trả về bảng so sánh theo từng tiêu chí + nhận xét tổng hợp.
Nêu rõ giả định và điểm cần verify thêm.
```

### Nghiên cứu nhanh một công nghệ
```
Tổng quan về [tên công nghệ/framework/pattern] cho đối tượng là
Senior Developer đã có nền tảng kỹ thuật tốt.

Trả về:
1. Là gì, giải quyết bài toán gì
2. Kiến trúc cốt lõi (3-5 điểm chính)
3. Ưu điểm và nhược điểm thực tế
4. Khi nào nên dùng / không nên dùng
5. Các công cụ/dự án nổi bật đang dùng
6. Tài nguyên học thêm (docs, paper, repo)
```

### Đánh giá fit cho dự án cụ thể
```
Chúng tôi đang xây dựng [mô tả hệ thống].
Yêu cầu kỹ thuật: [list]
Ràng buộc: [ngân sách, team skill, timeline, compliance]

Đánh giá xem [công nghệ X] có phù hợp không.
Phân tích theo: technical fit / team fit / risk / long-term maintainability.
Kết luận: Nên dùng / Không nên / Cần thêm thông tin để quyết định.
```

---

## Workflow đề xuất

```
1. Prompt tổng quan → hiểu bức tranh chung
2. Prompt so sánh → thu hẹp xuống 2-3 lựa chọn
3. Prompt đánh giá fit → áp vào ngữ cảnh thực tế
4. Verify các điểm quan trọng với official docs / benchmark thực tế
5. Tổng hợp thành technology evaluation report
```

---

## Lưu ý áp dụng

- AI có knowledge cutoff — với công nghệ mới (<6 tháng), kết hợp web search hoặc đọc release notes trực tiếp
- Số liệu benchmark từ AI cần verify — thường là số liệu tham khảo, không phải đo thực tế
- Dùng kết quả làm **khung thảo luận** với team, không làm quyết định đơn lẻ
