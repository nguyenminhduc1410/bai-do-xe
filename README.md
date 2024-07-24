# Bãi đỗ xe

Dùng cho để thực hiện các chức năng của bãi xe





## Chức năng

- In danh sách xe trong bãi
- Kiểm tra một xe có trong bãi hay không
- Cho xe ra, vào bãi
- Đếm số xe máy có trong bãi
- Tính tiền xe khi ra khỏi bãi
- Tính tổng tiền của bãi xe từ lúc bắt đầu hoạt động


## Input

Khối đầu tiên chứa thông tin về các lượt gửi xe được cho theo các dòng định dạng như sau:
<hh:mm:ss> <plate>: là xe có biển số <plate> đã vào bãi vào lúc <hh:mm:ss> của ngày hiện tại. Trường hợp xe đạp không biển số <plate> có giá trị xxxx-000.01 với 4 kí tự đầu luôn là xxxx, 5 số cuối là mã số của vé được phát.
Kết thúc khối đầu tiên là 1 dòng chứa dấu *

Khối thứ 2 chứa chuỗi các lệnh hoặc chuỗi lệnh, mỗi lệnh trên một hàng, kết thúc bằng dấu ***








## Ví dụ



```bash
Input
10:30:24 31K1-123.45
11:30:24 xxxx-000.01
*
list
***
Output
02:30:24 31K1-123.45
11:30:24 xxxx-000.01

```

##
