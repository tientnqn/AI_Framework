# 00 — Mindset: Tư Duy Làm Việc Với AI

> **Mục tiêu file này:** Xây dựng nền tảng tư duy đúng trước khi đi vào kỹ thuật.  
> Không có mindset đúng, kỹ thuật tốt cũng cho kết quả tệ.

---

## 1. AI là gì trong bối cảnh làm việc của bạn?

AI (LLM như ChatGPT, Gemini) **không phải**:
- Công cụ tìm kiếm nâng cao
- Chuyên gia có thể tin tuyệt đối
- Hệ thống thực thi logic chính xác như code

AI **là**:
- **Cộng sự tư duy** — giỏi tổng hợp, phác thảo, phản biện nhanh
- **Accelerator** — rút ngắn thời gian từ ý tưởng đến bản nháp đầu tiên
- **Rubber duck thông minh** — giúp bạn làm rõ suy nghĩ khi đặt câu hỏi đúng

**Hệ quả thực tế:** Bạn vẫn là người ra quyết định. AI tăng tốc và mở rộng năng lực — không thay thế phán đoán của bạn.

---

## 2. Ba sự thay đổi tư duy cốt lõi

### 2.1 Từ "Hỏi để lấy đáp án" → "Hỏi để tư duy tốt hơn"

| Tư duy cũ | Tư duy mới |
|-----------|-----------|
| "AI cho mình câu trả lời đúng" | "AI giúp mình đặt câu hỏi đúng hơn" |
| Copy output và dùng ngay | Dùng output làm điểm khởi đầu, rồi tinh chỉnh |
| Prompt một lần, kỳ vọng hoàn hảo | Lặp lại nhiều vòng, mỗi vòng tốt hơn |

### 2.2 Từ "Dùng AI như tool" → "Cộng tác với AI như peer"

Khi làm việc với một đồng nghiệp giỏi, bạn:
- Cung cấp đủ ngữ cảnh
- Nói rõ kỳ vọng đầu ra
- Phản hồi khi kết quả chưa đúng hướng

Làm việc với AI cũng vậy. **Chất lượng output phụ thuộc vào chất lượng input của bạn.**

### 2.3 Từ "Sợ AI thay thế" → "Chủ động định hình vai trò"

Người bị thay thế không phải là người dùng AI — mà là người không biết cách làm việc cùng AI.

Trong R&D, AI không thay thế được:
- Hiểu sâu domain (banking, hệ thống legacy, quy trình nghiệp vụ)
- Phán đoán về rủi ro và trade-off kỹ thuật
- Trách nhiệm với sản phẩm và khách hàng

AI thay thế được: công việc lặp lại, tổng hợp thông tin, phác thảo đầu tiên.

---

## 3. Giới hạn cần nhớ — để không bị "ảo tưởng AI"

```
⚠️  AI tự tin kể cả khi sai (hallucination)
⚠️  AI không có ngữ cảnh nội bộ của bạn trừ khi bạn cung cấp
⚠️  AI bị ảnh hưởng bởi cách bạn đặt câu hỏi (framing bias)
⚠️  AI không cập nhật real-time (tùy model, có knowledge cutoff)
⚠️  AI không hiểu "ý ngầm" — cần nói rõ kỳ vọng
```

**Nguyên tắc kiểm soát:** Output nào ảnh hưởng đến sản phẩm hoặc khách hàng → bắt buộc có người review.

---

## 4. Khung tư duy khi bắt đầu một task với AI

Trước khi mở ChatGPT/Gemini, tự hỏi 3 câu:

```
1. Mình muốn AI làm gì CỤ THỂ trong task này?
   (Viết? Phân tích? Phản biện? Tóm tắt? Sinh ý tưởng?)

2. AI cần biết gì để làm đúng?
   (Ngữ cảnh, ràng buộc, định dạng output, đối tượng đọc?)

3. Mình sẽ đánh giá output theo tiêu chí nào?
   (Để biết khi nào "đủ tốt" và khi nào cần làm lại)
```

> 📌 **Checklist nhanh trước khi prompt:**
> - [ ] Tôi đã xác định rõ loại output mong muốn
> - [ ] Tôi đã cung cấp đủ ngữ cảnh cần thiết
> - [ ] Tôi biết tiêu chí để đánh giá kết quả

---

## 5. Ví dụ minh họa — cùng một task, hai mindset khác nhau

**Task:** Phân tích rủi ro khi tích hợp AI vào quy trình KYC ngân hàng.

---

**❌ Mindset cũ — hỏi để lấy đáp án:**
```
"Rủi ro khi dùng AI trong KYC là gì?"
```
→ Output: danh sách generic, copy từ internet, không có giá trị thực tế.

---

**✅ Mindset mới — cộng tác để tư duy tốt hơn:**
```
"Tôi đang thiết kế giải pháp AI hỗ trợ KYC cho ngân hàng thương mại
tại Việt Nam. Hệ thống sẽ tự động xác minh giấy tờ và đánh giá
hành vi giao dịch.

Hãy phân tích các rủi ro theo 3 nhóm:
(1) Rủi ro kỹ thuật/model
(2) Rủi ro tuân thủ pháp lý (SBV, FATF)
(3) Rủi ro vận hành khi triển khai

Với mỗi rủi ro, đề xuất biện pháp kiểm soát cụ thể."
```
→ Output: có cấu trúc, có ngữ cảnh Việt Nam, dùng được làm nền cho báo cáo.

---

## 6. Nguyên tắc vàng của team

> **"AI làm bản nháp — bạn làm bản cuối."**
>
> **"Prompt tệ → output tệ. Đừng đổ lỗi cho AI."**
>
> **"Nếu bạn không thể đánh giá output, bạn chưa hiểu đủ task đó."**

---

*Tiếp theo: [`01_prompting_guide.md`](./01_prompting_guide.md) — Kỹ thuật prompting từ cơ bản đến nâng cao.*
