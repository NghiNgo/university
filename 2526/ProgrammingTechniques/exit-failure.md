Trong C++, `return 0` và `return -1` từ hàm `main()` là các **mã thoát (exit codes)** mà chương trình của bạn gửi lại cho hệ điều hành khi nó kết thúc.

Nói một cách đơn giản:

  * `return 0;` ➡️ Báo hiệu chương trình đã **thực thi thành công**.
  * `return -1;` (hoặc bất kỳ số nào khác 0) ➡️ Báo hiệu chương trình đã kết thúc và **gặp lỗi**.

-----

### 🚀 `return 0;` (Trạng thái Thành công)

Đây là quy ước chuẩn trong lập trình. Khi hàm `main()` của bạn trả về `0`, nó đang gửi một thông điệp đến hệ điều hành (hoặc bất kỳ quy trình nào đã khởi chạy nó) rằng: "Tôi đã chạy xong và mọi thứ đều ổn, không có lỗi gì xảy ra."

### ⚠️ `return -1;` (Trạng thái Thất bại / Lỗi)

Khi hàm `main()` trả về một giá trị **khác 0** (ví dụ như `-1`, `1`, `2`, v.v.), nó báo hiệu rằng chương trình đã kết thúc một cách bất thường hoặc đã gặp phải một lỗi trong quá trình thực thi.

  * **Tại sao lại quan trọng?** Hệ điều hành hoặc các script (ví dụ như tệp batch `.bat` trên Windows hoặc Bash script `.sh` trên Linux/macOS) có thể kiểm tra mã thoát này.
  * **Ví dụ:** Một script có thể chạy chương trình A. Nếu chương trình A trả về `0` (thành công), script sẽ tiếp tục chạy chương trình B. Nhưng nếu chương trình A trả về `1` (lỗi), script có thể dừng lại và báo lỗi mà không chạy chương trình B.
  * **Các mã lỗi khác nhau:** Bạn có thể sử dụng các giá trị khác 0 khác nhau để chỉ định *loại* lỗi. Ví dụ:
      * `return 1;` có thể có nghĩa là "Không tìm thấy tệp".
      * `return 2;` có thể có nghĩa là "Không đủ bộ nhớ".
      * `return -1;` thường là một mã lỗi chung chung.

-----

### 💡 Cách thực hành tốt (Best Practice)

Thay vì phải nhớ `0` là thành công và `-1` hay `1` là thất bại, C++ (giống như C) cung cấp hai hằng số được xác định trước trong thư viện `<cstdlib>`. Việc sử dụng chúng làm cho code của bạn rõ ràng và dễ đọc hơn:

  * `EXIT_SUCCESS`: Hằng số này đảm bảo tương đương với `0`.
  * `EXIT_FAILURE`: Hằng số này đảm bảo là một giá trị khác 0 (thường là `1`), biểu thị cho thất bại.

Đây là một ví dụ về cách thực hành tốt:

```cpp
#include <iostream>
#include <cstdlib> // Cần thiết để sử dụng EXIT_SUCCESS và EXIT_FAILURE
#include <fstream> // Ví dụ về việc mở tệp

int main() {
    std::ifstream file("non_existent_file.txt");

    if (!file.is_open()) {
        std::cerr << "Lỗi: Không thể mở tệp!" << std::endl;
        // Báo cho hệ điều hành biết rằng đã có lỗi xảy ra
        return EXIT_FAILURE; 
    }

    // ... (Làm gì đó với tệp)

    std::cout << "Chương trình chạy thành công." << std::endl;
    // Báo cho hệ điều hành biết mọi thứ đều ổn
    return EXIT_SUCCESS; 
}
```

**Tóm lại:** Luôn `return EXIT_SUCCESS;` (hoặc `return 0;`) khi chương trình của bạn chạy đúng, và `return EXIT_FAILURE;` (hoặc một số khác 0) khi có lỗi xảy ra.