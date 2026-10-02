# UC-02 — Sinh Tài Liệu Kỹ Thuật

> **Mục tiêu:** Từ requirement hoặc mô tả ngắn → tự động tạo bản nháp ADR, technical spec, API doc.

---

## Bối cảnh

Viết tài liệu kỹ thuật tốn thời gian nhưng cấu trúc thường lặp lại. AI có thể tạo bản nháp 80% — team chỉ cần review và điền phần domain-specific.

---

## Prompt Templates

### ADR (Architecture Decision Record)
```
Viết ADR cho quyết định kiến trúc sau:
- Bối cảnh: [mô tả vấn đề cần giải quyết]
- Quyết định: [giải pháp đã chọn]
- Các lựa chọn đã cân nhắc: [A, B, C]

Format chuẩn ADR:
## Status
## Context
## Decision
## Consequences (Positive / Negative / Risks)
## Alternatives Considered
```

### Technical Spec
```
Viết technical spec cho tính năng: [tên tính năng]
Đối tượng đọc: Developer + Tech Lead

Thông tin đầu vào:
- Mục tiêu: [...]
- Luồng chính: [...]
- Tech stack: [...]
- Ràng buộc: [...]

Format output:
## Overview
## Architecture Diagram (mô tả bằng text nếu không có tool vẽ)
## Data Model
## API Endpoints
## Error Handling
## Open Questions
```

### API Documentation
```
Viết API documentation cho endpoint sau:
- Method + Path: [POST /api/v1/kyc/verify]
- Mục đích: [...]
- Request body: [mô tả hoặc JSON mẫu]
- Response: [mô tả hoặc JSON mẫu]
- Error codes: [...]

Format: OpenAPI-style, ngôn ngữ tiếng Anh, ví dụ thực tế.
```

---

## Workflow đề xuất

```
1. Cung cấp thông tin đầu vào (bullet points cũng được)
2. AI sinh bản nháp
3. Tech lead review, điền các phần AI không biết (số liệu, quyết định nội bộ)
4. Lưu vào repo tài liệu
```

---

## Lưu ý áp dụng

- AI không biết quyết định nội bộ, lịch sử dự án — phải cung cấp thủ công
- Phần **Consequences/Risks** trong ADR cần human review kỹ nhất
- Dùng ChatGPT cho ADR/spec; Gemini nếu cần đọc tài liệu đầu vào dài
