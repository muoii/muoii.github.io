---
layout: post
published: true
title: 'Chạy trốn nỗi đau'
subtitle:
date: '2020-05-17'
---

## ĐỊNH NGHĨA:
	
*define:* Một hàm f(n) (nϵN) được coi là **hàm nhân tính** ([Multiplicative Function](https://en.wikipedia.org/wiki/Multiplicative_function)) nếu:
	
#f(xy) = f(x)×f(y)   (xϵN,yϵN và gcd(x,y)=1)
	

## Dirichlet Convolution:

*Với f,g là hai hàm nhân tính, ta có thể xây dựng hàm nhân tính mới:
	
	
	.
	
			    (f×g)(n)=∑d|n: f(d)×g(n/d)

			*chú thích: d|n: d là ước của n*

	*chứng minh:*

	- Cho a,b với gcd(a,b)=1 --> ước của ab có dạng d=rs (r|a và s|b)

	- Ta có:

		(f×g)(ab)= ∑r|a,s|b: f(rs)g(ab/rs)
					
				 = ∑r|a,s|b: f(r)×f(s) × g(a/r)×g(b/s)
				 
				 =( ∑r|a: f(r)×g(a/r) ) × ( ∑s|b: f(s)g(b/s) 
				 
				 =(f×g)(a) × (f×g)(b)

		=> (f×g) cũng là hàm nhân tính.
	
## ỨNG DỤNG
	
#1. Bài toán: Cho n≤10^6, tính tất cả các giá trị f(i) (i,n ϵ N và i<=n)
	
	Lộ trình giải:
	
	- *Chứng minh f là hàm nhân tính.*
	
	- *Xác định công thức cho f(p^k) với p là số nguyên tố.*
	
	- *Sử dụng sàng để tính mọi f(i) (i<=n) trong O(nlogn):*
	
	``` c++
	///demo:
	
	
	```
	
#2. Bài toán: Cho n≤10^12, tính f(n) (n ϵ N)
	
	Lộ trình giải:
	
	- *Chứng minh f là hàm nhân tính.*
	
	- *Xác định công thức cho f(p^k) với p là số nguyên tố.*
	
	- *Phân tích n thành thừa số nguyên tố để tính f(n) trong O(sqrt(n)):*
	
	``` c++
	///demo:
	
	
	```
	
## CÁC HÀM NHÂN TÍNH THƯỜNG GẶP

- f(n)= 1,

- f_k(n)= nk (k=const)

- f_k(n)= ∑d]n: dk (k=const)

- f_k(n)= gcd(n,k) (k=const)

- f(n)= phi(n)

- [mobius(n)](http://vnoi.info/wiki/translate/quora/mobius-function)


-----------------------------------------------------------------------------------------------------------------------------


Nguồn tham khảo: [wikipedia](https://en.wikipedia.org/wiki/Multiplicative_function) [vnoi wiki](http://vnoi.info/wiki/algo/math/multiplicative-function) 
