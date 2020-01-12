---
layout: post
published: true
title: 'Euclid mở rộng và ứng dụng'
subtitle: 'Math&Algo are best friend forever!'
date: '2019-07-07'
tags:
- num theory
- basic
---

Hey, I'm muoii!
	
Bài viết này mình sẽ viết về một số ứng dụng của giải thuật [Euclid mở rộng](https://vi.wikipedia.org/wiki/Gi%E1%BA%A3i_thu%E1%BA%ADt_Euclid_m%E1%BB%9F_r%E1%BB%99ng)
	
Để có thể hiểu được bài viết một cách rõ ràng hơn, bạn nên đọc [giải thuật Euclid](https://vi.wikipedia.org/wiki/Gi%E1%BA%A3i_thu%E1%BA%ADt_Euclid) - giúp tìm gcd(a,b) trong O(log(max(a,b))

--------------------------------------------------------------------------------------------------------------------------------

## Phương trình Diophantine: ax + by = gcd(a,b)
	
**Cho a,b khác 0, d = gcd(a,b), tìm cặp nghiệm nguyên (x,y) của phương trình: ax + by = c**
	
	- Điều kiện có nghiệm của phương trình trên là: c≡0 (mod d)
	
	- Có thể giải phương trình trên ta đưa về nó về phương trình k.(ax + by) = k.d (k=c/d),
	
	lúc này, vấn đề chúng ta đặt ra là giải phương trình ax + by = d (=gcd(a,b))
	
	Ta có thể giải phương trình này bằng giải thuật *Euclid mở rộng*:
	
		+ Ý tưởng: Dựa trên thuật toán Euclid song song với việc 
			
		duy trì ba giá trị m,n,r duy trì luôn 3 cặp số biểu diễn chúng: 
			
			m = a.x𝑚 + b.y𝑚
			
			n = a.x𝑛 + b.y𝑛
			
			r = 𝑎.x𝑟 + 𝑏.x𝑟

		```
		/// demo:
		
			m = a; (xm, ym) = (1, 0); //m = a = a * 1 + b * 0
		
			n = b; (xn, yn) = (0, 1); //n = b = a * 0 + b * 1
		
			while (n ≠ 0)
			{ 
				q = m / n; 
				
				r = m – q * n; 
				
				///r = m -qn =  ax𝑚 + by𝑚 − q(ax𝑛 + by𝑛)
				///  =  a(x𝑚 − qx𝑛 = x𝑟) + b(y𝑚 − qy𝑛 = y𝑟)
				
				(xr, yr) = (xm, ym) - q * (xn, yn); 
				
				m = n;  (xm, ym) = (xn, yn); 
				
				n = r; (xn, yn) = (xr, yr);
				
			}
			
			Output d = gcd(a,b) = m = a.x𝑚 + b.y𝑚;
			
		```
		
	*optimization: nhận xét: vs phương trình ax+by=d,*
	*ta chỉ cần giải x thì có thể biết được y =(d - ax)/b*
	
	*Dưới đây là code của muoii để tìm x của phương trình trên:*
	
``` c++

/// muoii
/// O(log(max(a,b)))

int diophante(const int &m,const int &xm,const int &n,const int &xn)
{
    if(n==0) return xm;
    return diophante(n,xn,m%n,xm-xn*(m/n));
}
/// ax + by = gcd(a,b) = d
/// (x0,y0) = (diophante(a,1,b,0),y0=(d-ax0)/b
/// (x,y) = (x0 + k*lcm(a,b)/a,y0 - k*lcm(a,b)/b)	(k is sig int)
```
	*Challenge: chứng minh họ nghiệm của ax+by=gcd(a,b):*
	*(x,y) = (x0 + k*lcm(a,b)/a,y0 - k*lcm(a,b)/b)	(k is sig int)*
	
	*Gợi ý: 𝑎𝑥 + 𝑏𝑦 = 𝑎(𝑥 + 𝑝) + 𝑏(𝑦 − 𝑞) = d
	
--------------------------------------------------------------------------------------------------------------------------------

## Giải hệ phương trình đồng dư:

*Cho hệ phương trình đồng dư:*
		
	*Cho dãy số nguyên a1,a2,...,an và b1,b2,...,bn,*
	*tìm x sao cho:* **x mod a[i] = b[i] (Vi)**
		
		
- Bài toán có thể giải bằng [định lý số dư TQ](https://vi.wikipedia.org/wiki/%C4%90%E1%BB%8Bnh_l%C3%BD_s%E1%BB%91_d%C6%B0_Trung_Qu%E1%BB%91c) nếu gcd(a[i],a[j])=1 (V i<>j)
	
- Ta sẽ giải bài toán này bằng *Euclid mở rộng* cho dạng tổng quát:
	
		- Xét hệ phương trình: x mod a1 = b1 và x mod a2 = b2
, 
		- x = a1.y + b1 = a2.z + b2  <=> a1.y + a2.(-z) = b2-b1
		
		(với cặp số nguyên y,z nào đó)
		
		- Đặt x0 = a1.y + b1 hoặc x0 = a2.z + b2
		
		- Họ nghiệm: x ≡ x0 (mod lcm(𝑎1,𝑎2))
		
	* Challenge: hãy cài đặt chương trình giải hệ phương trình đồng dư bằng Euclid mở rộng*
	
--------------------------------------------------------------------------------------------------------------------------------

*Mong bài viết hữu ích cho bạn đọc!*

*muoii*
	