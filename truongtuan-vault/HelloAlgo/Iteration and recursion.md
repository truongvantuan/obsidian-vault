## Iteration

> Là quá trình lặp lại một task cho đến khi điều kiện lặp không còn thỏa mãn
### For loop

Syntax:
```java

for ([initialization]; condition; update) {  
    // Code to be executed in each iteration  
}

for (int i = 0, j = 10; i < j; i++, j--) {
    // Code to be executed in each iteration
}

for ( ; ; ) {

}
```

- initialization:
	- khởi tạo loop controll variable
	- được khởi tạo 1 lần trước loop khởi chạy
	- optional, lúc này khởi tạo loop controll variable trước `for`
- condition:
	- kiểm tra condition trước mỗi lần lặp.
	- optional
- update:
	- chạy update loop controll variable sau mỗi lần loop
	- optional
- Số lần lặp được biết trước.
- Độ phức tạp tuyến tính với kích thước input
- `break;` thoát vòng lặp

### While loop

- 