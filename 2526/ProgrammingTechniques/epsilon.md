Rất vui được giải thích cho bạn. Đây là một trong những khái niệm quan trọng nhất khi làm việc với số thực (`float` và `double`) trong lập trình.

Lý do đơn giản là: **Máy tính không thể lưu trữ hầu hết các số thực một cách chính xác tuyệt đối.**

---

### 1. 😵 Vấn đề: "Sai số xấp xỉ"

Giống như trong hệ thập phân (hệ 10), chúng ta không thể viết chính xác số $1/3$ (chúng ta viết $0.33333...$ và phải làm tròn ở đâu đó), máy tính trong hệ nhị phân (hệ 2) cũng không thể biểu diễn chính xác các số như `0.1` hay `0.2`.

* Máy tính lưu `0.1` có thể trông giống như: `0.10000000000000001`
* Máy tính lưu `0.2` có thể trông giống như: `0.20000000000000002`

Khi bạn cộng `0.1 + 0.2`, kết quả *có thể* là `0.30000000000000003`.
Nhưng số `0.3` mà máy tính lưu *có thể* lại là `0.29999999999999998`.

**Vì vậy, phép so sánh `(0.1 + 0.2) == 0.3` sẽ trả về `false`.**

### 2. ❌ Tại sao `a == 0` thất bại?

Trong bài tập của bạn, giả sử `a` là kết quả của một phép tính (ví dụ: `1.0 - 0.5 - 0.5`). Về mặt toán học, kết quả là `0`.

Nhưng trên máy tính, phép tính đó có thể cho ra một con số *siêu nhỏ*, ví dụ:
* `0.0000000000000001` (một số dương rất nhỏ)
* hoặc `-0.0000000000000001` (một số âm rất nhỏ)

Cả hai số này đều *không bằng 0*. Vì vậy, nếu bạn dùng `if (a == 0)`, chương trình sẽ gần như luôn luôn bị sai.

### 3. ✅ Giải pháp: `fabs(a) < EPSILON`

Thay vì hỏi: "a có *bằng* 0 không?", chúng ta hỏi một câu thực tế hơn: "a có *đủ gần* 0 hay không?"



Chúng ta định nghĩa một "ngưỡng chấp nhận" (tolerance) được gọi là **EPSILON**.

* **`EPSILON`**: Là một số siêu nhỏ do chúng ta tự định nghĩa, ví dụ `1e-6` (tức là $1 \times 10^{-6}$ hay `0.000001`). Đây là sai số mà chúng ta chấp nhận được.
* **`fabs(a)`**: Đây là hàm "giá trị tuyệt đối" (absolute value). Chúng ta dùng nó vì `a` có thể là số âm rất nhỏ (như `-0.00000001`). `fabs(a)` sẽ trả về `0.00000001`.
* **`fabs(a) < EPSILON`**: Phép so sánh này có nghĩa là: "Giá trị tuyệt đối của `a` (tức là khoảng cách từ `a` đến `0`) có nhỏ hơn ngưỡng chấp nhận của chúng ta không?".

Nếu `fabs(a)` nhỏ hơn `EPSILON`, chúng ta coi `a` chính là `0`.

> **Quy tắc vàng:** Không bao giờ so sánh hai số thực bằng `==` hoặc `!=`.
>
> * Thay vì `a == b`, hãy dùng: `fabs(a - b) < EPSILON`
> * Thay vì `a == 0`, hãy dùng: `fabs(a) < EPSILON`