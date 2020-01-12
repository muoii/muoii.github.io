---
layout: post
published: true
title: 'Số học cơ bản'
subtitle: 'Math&Algo are best friend forever!'
date: '2019-10-22'
tags:
- num theory
- basic
---

## SỐ NGUYÊN TỐ - PRIME NUMBER
	
**define: n is prime <=> n>1 && size(set(divisor(n)))=2**
	
**1. Kiểm tra theo định nghĩa:**
	
- n là số nguyên tố <=> n>1 và n có đúng 2 ước số <=> n<=1 hoặc n có >2 ước số:
	
``` c++
///muoii
/// O(sqrt(n))
bool prime(const int &n)
{
	if(n<=1) return false;

	for(int i=2;i*i<=n;i++)
		if(n%i==0)
			return false;

	return true;
}
```
	*optimization with clause: "n>=5 && n is prime" => n=6k±1 (k is unsig int)
	*Challenge: Hãy suy nghĩ cách sử dụng thuật toán trên để phân tích một số thành thừa số nguyên tố*
	*Gợi ý: ước đầu tiên của n là một số nguyên tố |n>1|*
		
**2. Sàng nguyên tố Eratosthenes:**
		
[Giải thuật sàng Eratosthenes - wikipedia](https://vi.wikipedia.org/wiki/S%C3%A0ng_Eratosthenes)
	
``` c++
///muoii
/// O(nlogn)
void sieve(const int &maxn)
{
	prime[0]=prime[1]=0;
	for(int i=2;i<maxn;i++) prime[i]=1;

	for(int i=2;i*i<maxn;i++)
		if(prime[i])
			for(int j=i*i;j<maxn;j+=i)
				prime[j]=0;
				
}
```
	*Challenge: Hãy suy nghĩ cách sử dụng sàng Eratosthenes để phân tích một số thành thừa số nguyên tố*
	*Gợi ý: lưu lại ước số nguyên tố đầu tiên/cuối cùng của n |n>1|, có thể phân tích n thành thừa số nguyên tố trong O(log(n))*
	
**3. Định lí Wilson:** *(n-1)! ≡ n-1* <=> *(n-1)!+1 ≡ 0* (mod n) <=> n is prime (n>1)
	
*Prove:*
	
	- "Nếu n!+1 chia hết cho n thì n là số nguyên tố" là điều hiển nhiên.
	
	Vì khi đó n sẽ nguyên tố cùng nhau với các số từ 1 đến n-1,
	
	do đó nó không có ước nào khác ngoài 1 và chính nó.

	- Ngược lại ta phải chứng minh "nếu n là số nguyên tố thì (n-1)!+1 chia hết cho n":
		
		Nếu n là hợp số:
		
			⇒ tồn tại ước của n trong khoảng (2;n)
				
			⇒ gcd((n−1)!,n)>1
				
			⇒ gcd((n−1)! mod n , n)>1
				
			⇒ gcd(n−1,n)>1 (vô lý)
				
		==> n là số nguyên tố.
	
## FIBONACCI NUMBER

**define: n is fibonacci number <=> *E* i: n=F(i)**

F(0) = 1,F(1) = 1,F(2) = 2,...,F(i) = F(i-1) + F(i-2) (i ≥ 2)
	
**1. Dãy fibonacci mở rộng:**
		
**define: Đặt f là dãy số có f(1)=a, f(2)=b,..,f(i)=f(i-1)+f(i-2),... (i>2)**
		
	*Tính giá trị của dãy fibonacci mở rộng (f) dựa vào dãy fibonacci nguyên thủy (F):
			
		f(i) = a.F(i-2) + b.F(i-1) (fibo-dynamic)
		
	*Challenge: let's prove clause: fibo-dynamic
		
**2. Một số hằng đẳng thức vs fibonacci:**
		
	F(a+b) =  F(a)×F(b-1) + F(a+1)×F(b)
		
	∑F(x[i] + t) = ∑F(x[i])×F(t+1) + ∑F(x[i]-1)×F(t)
		
	*Challenge: let's remember these!*
	
## EULER's TOTIENT FUNCTION:

**define: ϕ(n) là số số nguyên tố cùng nhau với n thuộc [1;n]**
	
***ϕ(n)= n×(1−1/p)*** (∏p: is divisor(n) & is prime)
	
``` c++
/// muoii
///O(nlogn)
void sieve_phi(const int &maxn)
{
	for(int i=1;i<maxn;i++) phi[i]=i;
			
	for(int i=2;i<maxn;i++)
		if(phi[i]==i)
			for(int j=i;j<maxn;j+=i)
				phi[j]-=phi[j]/i; /// x*(1- 1/p) = x - x/p
						
}	
```

## FERMAT's little theorem:

**a^p ≡ a (mod p)** *(p is a prime number)*

**a^(p-1) ≡ 1 (mod p)** *(a mod p != 0)*

***hệ quả: a^(p-2) ≡ 1/a (mod p)*** *(a mod p != 0)*


## MODULAR INVERSE:
	
**define: *x* is modular inverse of *a* with modulo *m* if: *x.a ≡ 1* (mod m)**
	
***Find modular inverse *x* of *a* with modulo *m*:***
	
	- With diophantine equationuation:	
		+ gcd(a,m) = 1 ⇒ E x and ax + my = 1
		
		+ Để giải được phương trình ax + my = 1,
		
		các bạn có thể tham khảo bài viết:
		
[Euclid mở rộng - muoii](https://muoii.github.io/2019-07-07-euclid-dynamic/)
	
	- With Euler's theorem:
		
		a>0,n>0 && gcd(a,m)=1  ⇒ a^phi(m) ≡ 1 (mod m) ⇒ x=a^(phi(m)-1)
	
