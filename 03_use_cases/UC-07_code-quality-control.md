# UC-07 — Kiểm Soát Chất Lượng & Bảo Mật Code

> **Mục tiêu:** Xây dựng cơ chế kiểm soát code 3 lớp — áp dụng nhất quán bất kể code do AI hay human viết.

---

## Nguyên tắc nền tảng

> **Không quan trọng code do ai viết — quan trọng là nó an toàn, đúng logic, và maintainable.**
> Mọi code đều phải đạt cùng một tiêu chuẩn trước khi vào production.

---

## Kiến trúc 3 lớp kiểm soát

```
Lớp 1 — AUTOMATED      Chạy tự động trong CI/CD pipeline
Lớp 2 — HUMAN REVIEW   Trước khi merge vào main branch
Lớp 3 — RUNTIME        Sau khi deploy lên môi trường thực
```

---

## Lớp 1 — Automated (CI/CD)

Chạy tự động mỗi khi có commit/PR — không cần can thiệp thủ công.

| Công cụ | Mục đích | Gợi ý tool |
|---------|---------|-----------|
| Static Analysis (SAST) | Phát hiện bug, code smell, security issue trong source code | SonarQube, Semgrep |
| Dependency Scan (SCA) | Kiểm tra thư viện bên thứ ba có lỗ hổng đã biết | Snyk, Dependabot, OWASP Dependency-Check |
| Secret Detection | Phát hiện credential, API key bị commit nhầm | GitGuardian, TruffleHog |
| Code Coverage | Đảm bảo unit test bao phủ đủ logic quan trọng | Coverage.py, JaCoCo |

**Nguyên tắc:** CI/CD pipeline phải **fail** nếu phát hiện critical issue — không merge được cho đến khi fix.

---

## Lớp 2 — Human Review (Pre-merge)

Checklist bắt buộc trước khi approve PR:

```
LOGIC & CORRECTNESS
□ Logic có đúng với yêu cầu nghiệp vụ không?
□ Các edge case quan trọng đã được xử lý chưa?
□ Error handling có đầy đủ và rõ ràng không?

SECURITY
□ Input có được validate trước khi xử lý không?
□ Có nguy cơ injection (SQL, command, prompt) không?
□ Authentication/authorization có được kiểm tra đúng chỗ không?
□ Dữ liệu nhạy cảm có bị log hoặc expose không?

PERFORMANCE
□ Có query/loop nào có thể gây bottleneck ở scale lớn không?
□ Có resource nào (connection, file) chưa được đóng/giải phóng không?

MAINTAINABILITY
□ Code có đủ rõ ràng để người khác đọc hiểu không?
□ Naming có nhất quán với codebase hiện tại không?
□ Có magic number hoặc hardcoded value nào cần refactor không?
```

**Với code AI-generated:** Tập trung đặc biệt vào phần **Logic & Security** — AI thường viết code trông đúng nhưng thiếu business context và edge case thực tế.

---

## Lớp 3 — Runtime Monitoring

Sau khi deploy, tiếp tục theo dõi:

| Loại | Mục đích | Gợi ý tool |
|------|---------|-----------|
| Application Monitoring | Phát hiện lỗi, anomaly trong runtime | Sentry, Datadog |
| Audit Log | Ghi lại các hành động quan trọng để trace khi có sự cố | ELK Stack |
| Penetration Testing | Kiểm tra bảo mật định kỳ từ góc nhìn attacker | OWASP ZAP, Burp Suite |
| Alerting | Cảnh báo ngay khi có chỉ số bất thường | PagerDuty, Grafana |

---

## Áp dụng với AI-assisted development

Khi dùng AI (ChatGPT, Gemini, Copilot) để viết code, thêm bước sau vào workflow:

```
1. AI sinh code
      ↓
2. Dev review theo checklist Lớp 2 TRƯỚC KHI commit
   (đừng commit rồi mới review — tốn công hơn)
      ↓
3. Commit → CI/CD chạy Lớp 1 tự động
      ↓
4. PR review → teammate confirm checklist Lớp 2
      ↓
5. Merge → Lớp 3 tiếp tục theo dõi
```

---

## Prompt hỗ trợ — Dùng AI để review code trước khi commit

```
Review đoạn code dưới đây trước khi tôi commit.
Tập trung vào:
1. Security vulnerability (injection, auth, data exposure)
2. Edge case chưa xử lý
3. Resource leak (connection, file, memory)
4. Điểm nào sẽ gây vấn đề khi scale lên 10x traffic

Với mỗi vấn đề: chỉ rõ dòng code, giải thích rủi ro, đề xuất fix.

[DÁN CODE VÀO ĐÂY]
```

---

## Lưu ý

- Lớp 1 là **safety net** — không thay thế được Lớp 2
- Tool chỉ phát hiện pattern đã biết — logic bug đặc thù của domain vẫn cần human review
- Với hệ thống banking: Lớp 3 (audit log + alerting) là bắt buộc theo yêu cầu tuân thủ
