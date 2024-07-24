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
## Các câu lệnh
1. list: in ra danh sách xe trong bãi, theo thứ tự của input. Lưu ý chỉ trả về biển số.
2. find <plate>: tìm xe có biển số <plate> có trong bãi hay không. Ví dụ: find 31K1-123.45: in ra chỉ số của xe trong danh sách nếu tìm thấy, -1 nếu không tìm thấy
3. in <hh:mm:ss> <plate>: lúc <hh:mm:ss> cho xe biển số <plate> vào bãi. Ví dụ: in 10:00:02 31K1-123.45 trả về 0 nếu lỗi (xe đang trong bãi), 1 nếu thành công
4. out <hh:mm:ss> <plate>: lúc <hh:mm:ss> cho xe biển số <plate> ra. Ví dụ: out 03:04:56 31K1-123.45 trả về 0 nếu lỗi (xe không có trong bãi), 1 nếu thành công
5. cnt-moto: đếm số xe máy đang có trong bãi
6. bill <hh:mm:ss> <plate>: tính tiền gửi xe cho xe có biển <plate>. nếu không tìm thấy xe trong bãi trả về -1. Chú ý, chỉ tính tiền, xe vẫn ở trong bãi, không cho xe ra khỏi bãi.
7. billall: tính tổng số tiền gửi xe thu được từ khi bắt đầu chạy chương trình, việc thu tiền được thực hiện khi xe ra khỏi bãi.








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

## In danh sách xe trong bãi
```bash
void listxe(){
    for(int i=0;i<baixe.size();i++){
        baixe[i].in();
    }
}
```
## Kiểm tra một xe có trong bãi hay không

```bash
int check (string plate){
    for(int i=0;i<baixe.size();i++){
        if(baixe[i].laybienso()==plate){	
        	return i;
		}
	}
		return -1;
 }
```

## Cho xe ra, vào bãi
```bash
## Cho xe vào bãi 

int processVehicleEntry(string time, string plate) {
    	bool check=false;
        for(int i=0;i<baixe.size();i++){
        	if(baixe[i].laybienso()==plate){
        		check=true;
			}
		}
		if(check==true){
			return 0;
		}
		else{
			baixe.push_back(phuongtien(time,plate));
			return 1;
		}
	}
## Cho xe ra khỏi bãi
int layxera(string time,string plate){
	    for(int i=0;i<baixe.size();i++){
       		if(baixe[i].laybienso()==plate){
       			int fee=calculateFee(plate, baixe[i].laybienso(), time);
       			totalEarnings =totalEarnings+ fee;
       			baixe.erase(baixe.begin()+i);
       			return 1;
			}
	   }
	   return 0;
	}

```
## Đếm số xe máy có trong bãi
```bash
int countMotorcycles() {
        int count = 0;
        for (int i=0;i<baixe.size();i++) {
            if (baixe[i].laybienso().substr(0, 4) != "xxxx") {
                count++;
            }
        }
        return count;
    }

```

## Tính tiền xe khi ra khỏi bãi
```bash
int calculateFee(string plate, string entryTime, string exitTime) {
        
        bool isBike = (plate.substr(0, 4) == "xxxx");

        if (isDaytime(entryTime) && isDaytime(exitTime)) {
            return isBike ? 1 : 3;
        } else if (isNighttime1(entryTime) && isNighttime1(exitTime)) {
            return isBike ? 2 : 5;
        } else if (isNighttime1(entryTime) && isDaytime(exitTime)) {
            return isBike ? 3 : 8;
        }
		else if (isNighttime1(exitTime) && isDaytime(entryTime)) {
            return isBike ? 3 : 8;
        }
		else if (isNighttime2(entryTime) && isNighttime2(exitTime)) {
            return isBike ? 2 : 5;
        } else if (isNighttime2(entryTime) && isDaytime(exitTime)) {
            return isBike ? 3 : 8;
        } 
		else if (isNighttime2(exitTime) && isDaytime(entryTime)) {
            return isBike ? 3 : 8;
        }
		else { 
            return isBike ? 5 : 13;
        }

    }


    int getBill(string time, string plate) {
        for(int i=0;i<baixe.size();i++){
        	if(baixe[i].laybienso()==plate){
        		return calculateFee(plate, baixe[i].laybienso(), time);
			}
		}
		return -1;
    }
```
## Tính tổng tiền của bãi xe từ lúc bắt đầu hoạt động
```bash
int getTotalEarnings() {
        return totalEarnings;
    }
```
