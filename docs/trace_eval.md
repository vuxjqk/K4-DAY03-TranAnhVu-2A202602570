# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Trần Anh Vũ  
> **Mã Sinh Viên / Mã Học viên:** 2A202602570  
> **Chủ đề Lựa chọn:** Trợ lý Hỗ trợ Kỹ thuật IT Helpdesk: Tra cứu ticket sự cố mạng, tài khoản và tạo yêu cầu hỗ trợ kỹ thuật.  

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 4 / 5 | Bài toán có thể yêu cầu Agent thực hiện nhiều bước liên tiếp: xác định người dùng → tra cứu ticket → kiểm tra trạng thái/loại sự cố → quyết định hướng xử lý → tạo ticket mới hoặc cập nhật ticket. Tuy nhiên, không phải mọi yêu cầu đều cần nhiều bước nên chưa nên chấm 5/5. |
| **2. Tool Interaction** | 5 / 5 | Agent cần tương tác với nhiều công cụ thông qua MCP Server, chẳng hạn get_user, search_tickets, get_ticket, create_ticket, update_ticket. Các tool có thể truy cập database hoặc hệ thống Helpdesk bên ngoài. |
| **3. Dynamic Decision** | 5 / 5 | Đây là điểm mạnh nhất của đề tài. Bước tiếp theo phụ thuộc vào kết quả của bước trước. Ví dụ: nếu ticket đang OPEN thì tra cứu thêm; nếu RESOLVED thì thông báo kết quả; nếu chưa có ticket phù hợp thì tạo yêu cầu hỗ trợ mới. |
| **4. Long Horizon Goal** | 4 / 5 | Một yêu cầu phức tạp có thể cần Agent duy trì mục tiêu qua nhiều bước, ví dụ: “Kiểm tra sự cố mạng của tôi, nếu chưa có ticket thì tạo ticket ưu tiên cao và trả mã ticket”. Tuy nhiên, bài lab quy mô nhỏ nên chưa thực sự cần một horizon quá dài. |
| **TỔNG ĐIỂM AGENTIC FIT** | **18 / 20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Wi-Fi trên máy tính không kết nối được thì tôi nên kiểm tra những gì trước?",
    "action_type": "FINAL_ANSWER",
    "thought": "Gemini phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Khi máy tính không kết nối được Wi-Fi, bạn nên thực hiện các bước kiểm tra cơ bản sau đây trước khi gửi yêu cầu hỗ trợ kỹ thuật:\n\n1. **Kiểm tra công tắc Wi-Fi & Chế độ máy bay (Airplane Mode):**\n   * Đảm bảo tính năng Wi-Fi trên máy tính đang được bật.\n   * Kiểm tra xem máy tính có đang bật **Airplane Mode** (Chế độ máy bay) hay không và hãy tắt nó đi.\n\n2. **Kiểm tra kết nối trên các thiết bị khác:**\n   * Dùng điện thoại hoặc máy tính khác thử kết nối vào cùng mạng Wi-Fi đó.\n   * *Nếu thiết bị khác cũng không vào được:* Sự cố có thể xuất phát từ Router/Modem hoặc đường truyền mạng chung.\n   * *Nếu thiết bị khác vẫn vào được:* Sự cố nằm ở máy tính của bạn.\n\n3. **Quên mạng (Forget Network) và kết nối lại:**\n   * Vào phần cài đặt Wi-Fi trên máy tính, chọn mạng Wi-Fi đang gặp lỗi -> chọn **Forget** (Quên mạng).\n   * Sau đó chọn lại mạng Wi-Fi và nhập lại mật khẩu.\n\n4. **Khởi động lại máy tính & Modem/Router:**\n   * **Khởi động lại máy tính:** Giúp xóa các bộ nhớ tạm và làm mới lại các dịch vụ mạng.\n   * **Khởi động lại Router/Modem Wi-Fi** (nếu bạn đang ở nhà hoặc có quyền truy cập thiết bị): Tắt nguồn, đợi khoảng 10–15 giây rồi bật lại.\n\n5. **Sử dụng công cụ chẩn đoán sự cố mạng tự động:**\n   * **Windows:** Nhấp chuột phải vào biểu tượng mạng ở góc dưới bên phải màn hình -> chọn **Diagnose network problems** (hoặc *Troubleshoot problems*).\n   * **macOS:** Giữ phím `Option` và nhấp vào biểu tượng Wi-Fi trên thanh menu -> chọn **Open Wireless Diagnostics**.\n\n6. **Tắt và bật lại Card mạng (Network Adapter):**\n   * Trên Windows: Vào `Control Panel` > `Network and Sharing Center` > `Change adapter settings` > Nhấp chuột phải vào card Wi-Fi chọn **Disable**, chờ 5 giây rồi nhấp chuột phải chọn **Enable**.\n\n---\n Nếu đã thử các bước trên nhưng vẫn không kết nối được, bạn hãy cung cấp thêm thông tin (Tên hệ điều hành, thông báo lỗi nếu có) để IT Helpdesk hỗ trợ bạn chi tiết hơn nhé!",
    "latency_ms": 8531.75
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [X] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 5 lượt.
- **Kết quả đẩy Repo nộp bài:** [X] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
