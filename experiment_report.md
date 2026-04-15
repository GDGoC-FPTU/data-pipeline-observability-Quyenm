# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600481
**Name:** Nguyễn Mạnh Quyền 
**Date:** 2026-04-15  

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| **Clean Data** (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Phản hồi chính xác và hữu ích. Laptop được xác định đúng là mặt hàng điện tử hàng đầu. |
| **Garbage Data** (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Hoàn toàn sai. Agent đề xuất một giá trị ngoại lệ cực đoan rõ ràng không phải là sản phẩm thực tế. |

---

## 2. Phân tích & nhận xét

### Tại sao Agent trả lời sai khi dùng Garbage Data?

Khi dùng garbage data, Agent cho ra kết quả sai hoàn toàn vì dữ liệu đầu vào chứa nhiều vấn đề nghiêm trọng về cấu trúc và nội dung:

1.  **Outliers (Giá trị ngoại lệ):** Sự xuất hiện của "Nuclear Reactor" với mức giá cực lớn ($999,999) đã đánh lừa logic tìm kiếm của Agent. Agent chỉ đơn thuần quét qua các con số lớn nhất mà không có khả năng phân biệt được đây là một thực thể phi lý trong danh mục mua sắm thông thường.
2.  **Duplicate IDs (Trùng lặp ID):** Việc tồn tại nhiều bản ghi có cùng ID (ví dụ id=1 xuất hiện hai lần) gây ra sự nhiễu loạn thông tin, làm cho tập dữ liệu mất đi tính nhất quán và duy nhất.
3.  **Wrong Data Types (Sai kiểu dữ liệu):** Trường "price" chứa giá trị dạng chữ ("ten dollars") thay vì số khiến Agent không thể thực hiện các phép toán so sánh hoặc tính toán trung bình một cách chính xác.
4.  **Null Values (Giá trị rỗng):** Các bản ghi bị thiếu ID hoặc Category nhưng vẫn lọt qua bộ lọc làm giảm độ tin cậy của toàn bộ hệ thống. 

Tất cả những yếu tố trên chứng minh rằng nếu không có bước tiền xử lý và validation, Agent sẽ bị "mù quáng" tin vào dữ liệu sai lệch, dẫn đến các quyết định gây hại.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** **Đồng ý hoàn toàn.**

Dù bạn có viết một Prompt cực kỳ chi tiết, logic và chặt chẽ đến đâu, nếu dữ liệu đầu vào là "rác" thì kết quả trả ra vẫn sẽ là "rác". Bài thí nghiệm này khẳng định nguyên tắc cốt lõi: **"Garbage In, Garbage Out"**. 

Một AI Agent thông minh cần được xây dựng trên một nền tảng dữ liệu sạch (Clean Data). Việc đầu tư vào quy trình ETL và kiểm soát chất lượng dữ liệu (Data Quality Control) quan trọng hơn nhiều so với việc chỉ cố gắng tối ưu câu lệnh điều hướng, vì dữ liệu chính là "nguồn tri thức" duy nhất mà Agent dựa vào để thực hiện nhiệm vụ.