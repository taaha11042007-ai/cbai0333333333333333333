# ShopeeFood Checkout

## 1. Giới thiệu

Đây là bài tập xây dựng phân hệ quyết toán đơn hàng ShopeeFood bằng ngôn ngữ C.

Chương trình có nhiệm vụ:

- Kiểm tra tính hợp lệ của đơn hàng.
- Xác định đơn hàng có nằm trong giờ cao điểm hay không.
- Tính phụ phí giao hàng.
- Kiểm tra điều kiện giảm phí giao hàng.
- Tính phí giao hàng thực tế.
- Tính tổng tiền thanh toán.

Chương trình được xây dựng theo phương pháp Flag-based Arithmetic, sử dụng các biểu thức Boolean trả về giá trị 0 hoặc 1 để thực hiện tính toán mà không sử dụng cấu trúc rẽ nhánh.

## 2. Input

Chương trình nhận 6 thông tin:

| Dữ liệu | Kiểu | Ý nghĩa |
|---|---|---|
| order_id | int | Mã đơn hàng |
| subtotal | int | Giá trị tiền món ăn, đơn vị VNĐ |
| distance_km | float | Khoảng cách giao hàng |
| booking_hour | int | Giờ đặt hàng từ 0 đến 23 |
| is_store_open | int | 1 là quán mở, 0 là quán đóng |
| inventory_qty | int | Số lượng tồn kho |

## 3. Quy tắc nghiệp vụ

### Cước phí cơ bản

Phí giao hàng cơ bản:

15000 VNĐ.

### Phụ phí giờ cao điểm

Giờ cao điểm:

- Từ 11h đến 13h.
- Hoặc từ 18h đến 20h.

Nếu nằm trong giờ cao điểm:

10000 VNĐ.

Ngược lại:

0 VNĐ.

### Giảm phí giao hàng

Nếu subtotal >= 100000 VNĐ:

Giảm 15000 VNĐ phí giao hàng.

Ngược lại:

0 VNĐ.

### Điều kiện đơn hàng hợp lệ

Đơn hàng hợp lệ khi:

- Quán đang mở.
- Tồn kho lớn hơn 0.
- Khoảng cách giao hàng không vượt quá 15 km.
- Giờ đặt hàng nằm trong khoảng 0 đến 23.
- Giá trị món ăn không âm.
- Khoảng cách giao hàng lớn hơn 0.
- Trạng thái quán chỉ nhận giá trị 0 hoặc 1.

## 4. Công thức tính toán

Cờ giờ cao điểm:

is_peak_hour =
((booking_hour >= 11 && booking_hour <= 13) ||
 (booking_hour >= 18 && booking_hour <= 20));

Cờ giảm phí:

is_freeship_eligible = (subtotal >= 100000);

Cờ đơn hàng hợp lệ:

is_valid_order =
(is_store_open == 1) &&
(inventory_qty > 0) &&
(distance_km <= 15.0) &&
(booking_hour >= 0 && booking_hour <= 23) &&
is_valid_input;

Phụ phí:

surcharge = is_peak_hour * 10000;

Giảm phí:

discount = is_freeship_eligible * 15000;

Phí giao hàng thực tế:

final_delivery_fee =
is_valid_order * (base_fee + surcharge - discount);

Tổng tiền thanh toán:

total_payment =
is_valid_order * (subtotal + final_delivery_fee);

Do các biểu thức Boolean có giá trị 0 hoặc 1 nên có thể sử dụng phép nhân để bật hoặc tắt một khoản chi phí mà không cần dùng if/else.

## 5. Constraint

Chương trình không sử dụng:

- if
- else
- switch-case
- toán tử ba ngôi ?:
- for
- while
- do-while
- array
- struct
- hàm tự định nghĩa

Chương trình chỉ sử dụng kiến thức cơ bản:

- int
- float
- printf
- scanf
- Toán tử số học
- Toán tử so sánh
- Toán tử logic &&, ||, !

## 6. Biên dịch

Sử dụng GCC:

```bash
gcc -Wall -Wextra -std=c11 main.c -o main
