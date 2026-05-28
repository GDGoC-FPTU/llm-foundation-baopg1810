# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature tăng từ 0.0 lên 1.5, các câu trả lời trở nên đa dạng, sáng tạo và nhiều chi tiết bất ngờ hơn, nhưng tính nhất quán giảm dần. Ở mức nhiệt độ thấp (0.0 - 0.5), phản hồi rất logic và tập trung vào các sự thật chính xác, trong khi ở mức quá cao (1.5), câu trả lời có xu hướng dài dòng, lặp từ hoặc sinh ra các câu từ thiếu tự nhiên.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature thấp, dao động từ 0.0 đến 0.2. Chatbot hỗ trợ khách hàng yêu cầu sự chính xác tuyệt đối, nhất quán và tin cậy về thông tin sản phẩm hoặc chính sách dịch vụ; đặt nhiệt độ thấp giúp giảm thiểu tối đa hiện tượng "ảo tưởng" (hallucination) của mô hình.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> GPT-4o đắt hơn GPT-4o-mini đúng **33.33 lần**. 
> *Giải thích chi tiết:* 
> - Chi phí Input: $5.00 / $0.150 = 33.33 lần.
> - Chi phí Output: $20.00 / $0.600 = 33.33 (đúng 100/3) lần.
> Do tỷ lệ chi phí của cả Input và Output đều là 33.33, nên với bất kỳ tỷ lệ phân bổ token nào, chi phí cho workload của GPT-4o luôn đắt gấp 33.33 lần so với GPT-4o-mini.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> - **GPT-4o xứng đáng:** Khi cần phân tích tài liệu phức tạp, xử lý logic suy luận nhiều bước đòi hỏi sự chính xác cao (ví dụ: tư vấn pháp lý, phân tích lỗi bảo mật mã nguồn).
> - **GPT-4o-mini tốt hơn:** Khi cần xử lý các tác vụ phân loại đơn giản, tần suất lớn, cần phản hồi nhanh như phân loại ý định người dùng (intent classification), tóm tắt ý chính của tin nhắn chat, trích xuất dữ liệu thô từ văn bản.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng chatbot giao tiếp trực tiếp với người dùng cuối, nơi Time to First Token (TTFT) quyết định trải nghiệm phản hồi nhanh chóng, giúp người dùng đọc thông tin ngay khi nó được sinh ra thay vì cảm thấy ứng dụng bị "đơ". Ngược lại, non-streaming phù hợp hơn cho các tác vụ ngầm chạy tự động (background jobs) như xử lý dữ liệu hàng loạt (batch processing), phân tích cảm xúc (sentiment analysis) để ghi log, hoặc khi kết quả đầu ra cần đi qua một bước hậu xử lý lập trình (ví dụ: parse JSON, kiểm tra lỗi cú pháp) trước khi hiển thị.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
