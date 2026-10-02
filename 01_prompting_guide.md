# 01 — Prompting Guide: Kỹ Thuật Làm Việc Với AI

> **Mục tiêu file này:** Nắm vững các kỹ thuật prompting từ cơ bản đến nâng cao,  
> áp dụng được ngay vào công việc R&D và bối cảnh banking.

---

## 1. Anatomy của một prompt tốt

Một prompt hiệu quả thường có đủ 5 thành phần sau:

```
[ROLE]     — AI đóng vai gì? Có chuyên môn gì?
[CONTEXT]  — Bối cảnh, ngữ cảnh nội bộ, thông tin nền
[TASK]     — Yêu cầu cụ thể cần làm
[FORMAT]   — Định dạng output mong muốn
[CONSTRAINT] — Ràng buộc, giới hạn, điều cần tránh
```

**Không cần đủ 5 thành phần mọi lúc** — task đơn giản chỉ cần TASK + FORMAT.  
Nhưng task phức tạp mà thiếu ROLE + CONTEXT → output sẽ generic và không dùng được.

---

## 2. Các kỹ thuật prompting theo cấp độ

### Level 1 — Basic: Rõ ràng và có cấu trúc

**Nguyên tắc:** Nói rõ bạn muốn gì, muốn format nào, cho ai.

```
❌ "Viết email cho khách hàng về tiến độ dự án"

✅ "Viết email cập nhật tiến độ dự án AI cho CTO ngân hàng.
   Dự án đang trễ 2 tuần do thay đổi yêu cầu từ phía khách hàng.
   Tone: chuyên nghiệp, thẳng thắn, không xin lỗi quá mức.
   Độ dài: không quá 150 từ."
```

---

### Level 2 — Role Prompting: Định nghĩa chuyên môn

**Nguyên tắc:** Gán cho AI một vai trò có chuyên môn cụ thể → output sâu hơn, đúng góc nhìn hơn.

```
"Bạn là một Solution Architect với 10 năm kinh nghiệm triển khai
hệ thống AI trong lĩnh vực ngân hàng tại Đông Nam Á.
Hãy đánh giá kiến trúc sau từ góc độ scalability và compliance..."
```

> ⚠️ **Lưu ý:** Role prompting không làm AI "biết thêm" — nó định hướng  
> góc nhìn và phong cách trả lời. Vẫn cần verify thông tin domain-specific.

---

### Level 3 — Chain of Thought (CoT): Bắt AI suy luận từng bước

**Nguyên tắc:** Với bài toán phân tích hoặc ra quyết định, yêu cầu AI trình bày lý luận trước khi kết luận.

```
"Phân tích xem giải pháp A hay B phù hợp hơn cho bài toán này.
Hãy suy luận từng bước:
1. Liệt kê tiêu chí đánh giá quan trọng nhất
2. Đánh giá từng giải pháp theo từng tiêu chí
3. Kết luận có lý giải rõ ràng"
```

**Khi nào dùng:** So sánh giải pháp kỹ thuật, đánh giá rủi ro, ra quyết định có nhiều trade-off.

---

### Level 4 — Few-shot Prompting: Dạy bằng ví dụ

**Nguyên tắc:** Cung cấp 2–3 ví dụ input/output mẫu → AI học pattern và áp dụng nhất quán.

```
"Phân loại các yêu cầu sau theo mức độ ưu tiên (High/Medium/Low).

Ví dụ:
- 'Hệ thống đăng nhập bị lỗi khi có >1000 users' → High
- 'Đổi màu nút Submit' → Low
- 'Báo cáo cuối tháng chạy chậm 30 giây' → Medium

Bây giờ phân loại:
- 'API KYC timeout sau 5 phút xử lý'
- 'Thêm tooltip vào form nhập liệu'
- 'Model AI có accuracy giảm 3% so với baseline'"
```

**Khi nào dùng:** Phân loại, gán nhãn, viết theo style nhất định, format lại dữ liệu.

---

### Level 5 — Iterative Refinement: Làm việc theo vòng lặp

**Nguyên tắc:** Không kỳ vọng output hoàn hảo từ lần đầu. Prompt → Review → Tinh chỉnh.

```
Vòng 1: Prompt tổng quát để có bản nháp
         ↓
Vòng 2: "Phần X chưa đúng vì [lý do]. Hãy điều chỉnh theo hướng Y."
         ↓
Vòng 3: "Giữ phần A và B, viết lại phần C theo format bảng."
         ↓
Vòng n: Đến khi output đạt tiêu chí đã định
```

> 📌 **Mẹo:** Đừng bắt đầu prompt mới mỗi lần — giữ nguyên conversation  
> để AI có đủ context của các vòng trước.

---

### Level 6 — Prompt Chaining: Chia task lớn thành chuỗi

**Nguyên tắc:** Task phức tạp → tách thành các bước nhỏ, output của bước trước là input của bước sau.

```
Task: Viết báo cáo đánh giá giải pháp AI cho ngân hàng

Bước 1 → "Liệt kê các tiêu chí đánh giá quan trọng nhất (output: danh sách)"
Bước 2 → "Dùng tiêu chí trên, đánh giá [Giải pháp A] (output: bảng điểm)"
Bước 3 → "Dùng tiêu chí trên, đánh giá [Giải pháp B] (output: bảng điểm)"
Bước 4 → "Tổng hợp so sánh và viết phần kết luận + khuyến nghị"
```

**Khi nào dùng:** Báo cáo dài, phân tích đa chiều, quy trình có nhiều bước phụ thuộc nhau.

---

## 3. ChatGPT vs Gemini — Điểm khác biệt thực tế

| Tiêu chí | ChatGPT (GPT-4o) | Gemini (1.5 Pro/Flash) |
|----------|-----------------|----------------------|
| **Độ sâu lý luận** | Mạnh, CoT tự nhiên | Tốt, đặc biệt với dữ liệu có cấu trúc |
| **Context window** | 128K tokens | 1M tokens (1.5 Pro) — lợi thế rõ với doc dài |
| **Xử lý tài liệu dài** | Tốt | Vượt trội khi cần đọc cả file lớn |
| **Coding & technical** | Rất mạnh | Tốt, tích hợp tốt với Google ecosystem |
| **Multimodal (ảnh, file)** | GPT-4o tốt | Gemini 1.5 mạnh hơn với video/audio |
| **Tiếng Việt** | Tốt | Tốt, đang cải thiện nhanh |
| **Tích hợp workflow** | ChatGPT + plugins/GPTs | Gemini + Google Workspace |

**Khuyến nghị thực tế cho R&D team:**

```
Dùng ChatGPT khi:
→ Viết code, debug, review architecture
→ Brainstorm ý tưởng, phác thảo tài liệu
→ Cần lý luận phức tạp, nhiều bước

Dùng Gemini khi:
→ Phân tích tài liệu dài (spec, contract, log)
→ Làm việc với Google Docs/Sheets/Slides
→ Cần xử lý nhiều file cùng lúc
```

---

## 4. Các lỗi prompting phổ biến — và cách tránh

| Lỗi | Biểu hiện | Cách sửa |
|-----|-----------|----------|
| **Quá mơ hồ** | "Phân tích cái này cho tôi" | Chỉ rõ: phân tích theo tiêu chí gì, output dạng nào |
| **Quá dài dòng** | Prompt 500 từ cho task đơn giản | Chỉ giữ thông tin AI thực sự cần |
| **Thiếu ngữ cảnh** | AI không biết bạn đang làm gì | Cung cấp bối cảnh dự án, đối tượng, ràng buộc |
| **Kỳ vọng một lần hoàn hảo** | Không hài lòng rồi bỏ cuộc | Dùng iterative refinement |
| **Không chỉ định format** | Output dài, lan man, khó dùng | Nói rõ: bảng, bullet, số từ, heading |
| **Hỏi nhiều thứ cùng lúc** | AI trả lời sơ sài mọi thứ | Tách thành nhiều prompt riêng biệt |

---

## 5. Template prompt cho các task phổ biến trong R&D

### 5.1 — Phân tích kỹ thuật
```
Bạn là [vai trò chuyên môn].
Bối cảnh: [mô tả ngắn về hệ thống/dự án]
Yêu cầu: Phân tích [X] theo các khía cạnh: [a], [b], [c]
Ràng buộc: [ngữ cảnh đặc thù, quy định cần tuân thủ]
Output: Bảng so sánh + nhận xét tổng hợp + khuyến nghị
```

### 5.2 — Review tài liệu / thiết kế
```
Hãy review [loại tài liệu] dưới đây.
Tập trung vào: [điểm cần review — logic, completeness, risk, clarity]
Với mỗi vấn đề tìm thấy: nêu vấn đề, giải thích tại sao, đề xuất cách sửa.
[Dán nội dung tài liệu vào đây]
```

### 5.3 — Brainstorm giải pháp
```
Bối cảnh: [mô tả bài toán]
Ràng buộc: [ngân sách, thời gian, tech stack, compliance]
Yêu cầu: Đề xuất 3–5 hướng giải quyết khác nhau.
Với mỗi hướng: mô tả ngắn, ưu điểm, nhược điểm, độ phức tạp triển khai.
Không cần chọn hướng tốt nhất — tôi sẽ tự đánh giá.
```

### 5.4 — Viết tài liệu kỹ thuật
```
Viết [loại tài liệu: ADR / RFC / spec / README] cho [tên tính năng/hệ thống].
Đối tượng đọc: [developer / architect / PM / khách hàng]
Thông tin đầu vào: [mô tả ngắn hoặc bullet points]
Format: [heading chuẩn của loại tài liệu đó]
Tone: [kỹ thuật / business / hỗn hợp]
```

### 5.5 — Chuẩn bị nội dung cho lãnh đạo
```
Tóm tắt [nội dung] cho [CTO/CEO ngân hàng].
Họ cần biết: Vấn đề là gì, ảnh hưởng gì, chúng ta làm gì, cần quyết định gì.
Format: Executive summary không quá 200 từ + 3 bullet điểm hành động.
Tránh: jargon kỹ thuật, chi tiết implementation.
```

---

## 6. Checklist — Trước khi gửi prompt

```
□ Đã xác định rõ loại task (viết / phân tích / brainstorm / review / tóm tắt)?
□ Đã cung cấp đủ ngữ cảnh cho AI hiểu bối cảnh?
□ Đã chỉ định format output mong muốn?
□ Đã nêu ràng buộc hoặc điều cần tránh?
□ Task có đủ nhỏ để một prompt xử lý tốt không?
  → Nếu không: tách ra, dùng Prompt Chaining
□ Đã chọn đúng tool (ChatGPT hay Gemini) cho task này?
```

---

*Tiếp theo: [`02_agent_architecture/00_overview.md`](./02_agent_architecture/00_overview.md) — Tổng quan kiến trúc Agent.*
