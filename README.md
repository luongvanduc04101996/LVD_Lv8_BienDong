# I.Khái niệm  

## a/Biến động
   * Là các biến được tạo ra lúc chạy chương trình, tùy theo nhu cầu. 
   * Do vậy, mà số biến này hoàn toàn không được xác định từ trước.
   * Các biến được tạo ra như vậy được gọi là các biến động. Các biến động không có tên (vì việc đặt tên thực chất là gán cho nó một địa chỉ xác định).  
   
## b/Cách tạo ra biến động và truy nhập đến biến động
* Việc tạo ra biến động và xóa nó đi (để thu hồi lại bộ nhớ) được thực hiện nhờ các hàm như malloc() và free() đã có sẵn trong stdlib.h 
* Việc truy nhập đến biến động được tiến hành nhờ các biến con trỏ. 
* Các biến con trỏ được định nghĩa như các biến tĩnh ( được khai báo ngay từ đầu trong phần khai báo biến)
và được dùng để chứa địa chỉ các biến động. 
* **vd**:	
```  
int *p; /* Khai báo biến con trỏ p*/  
			p= (int *) malloc(100);/* Tạo biến động*/  
	Ðoạn chương trình trên sẽ cấp phát 100 bytes trong bộ nhớ và gán địa chỉ khối bộ nhớ này cho p  
```
# II.	Cấp phát và giải phóng bộ nhớ động (các hàm thuộc stdlib.h và alloc.h) 
## a/Cấp phát bộ nhớ động bằng hàm malloc() 
* Cú pháp: `void *malloc(size_t size)`  
**Chức năng:** Hàm malloc cấp phát một vùng nhớ có kích thước là size.  
* **Trong đó:**   
 * size là một giá trị kiểu size_t (là một kiểu dữ liệu định sẵn trong thư viện stdlib.h, ta có thể khai báo kiểu unsigned cũng được).  
 * Hàm này trả về con trỏ kiểu void chứa địa chỉ ô nhớ đầu của vùng nhớ được cấp phát. Nếu không đủ vùng nhớ để cấp phát nó sẽ trả về 
giá trị NULL, vì vậy ta phải kiểm tra giá trị trả về khi sử dụng hàm malloc.  
* **vd:**  
```
# include ``<stdlib.h>``  
# include ``<conio.h>``  
void main () /* Ham chinh */  
{  
void *v;  
if ((v=malloc(100))==NULL)  
{ printf("Khong du bo nho");  
exit(1); }  
printf("Bo nho da duoc cap phat");  
getch();  
}  
```
## b/Cấp phát bộ nhớ động bằng hàm calloc() 
* **Cú pháp:** 
`(datatype *) calloc(n, sizeof(object));`  
**Chức năng:** cấp phát bộ nhớ động cho các kiểu dữ liệu (có thể là những kiểu dữ liệu không phải kiểu cơ sở)  
* **Trong đó:**  
datatype *) là kiểu con trỏ trỏ tới kiểu dữ liệu datatype. n là số lượng object thuộc kiểu datatype mà ta cần cấp phát bộ nhớ.
Kiểu datatype có thể là những kiểu dữ liệu mới do người lập trình sáng tạo ra.  
* **vd:**  
```
struct sv {  
char ht[30];  
unsigned int tuoi;  
unsigned int diem; } /* Khai báo cấu trúc */  
struct sv *p_sv;/* Khai báo con trỏ sv*/  
Cấp phát bộ nhớ cho 10 người:  
calloc(10, sizeof(struct sv)); 
```
## c/Cấp phát bộ nhớ động bằng hàm relloc() 
* **Cú pháp:** `(datatype *) realloc(buf _p, newsize);`   
 **Chức năng:** Hàm cấp phát lại bộ nhớ  
* **Trong đó:**  
 * buf_p là con trỏ đang trỏ đến vùng ô nhớ đã được cấp phát từ trước.  
 * newsize là kích thước mới cần cấp phát, có thể to hoặc nhỏ hơn.  

## d/Giải phóng bộ nhớ bằng hàm free
* **Cú pháp**  
`void free( void *prt)`
	* Hàm free giải phóng vùng nhớ được trỏ đến bởi con trỏ ptr. 
	* Nếu con trỏ ptr = NULL thì hàm free không làm gì cả.
