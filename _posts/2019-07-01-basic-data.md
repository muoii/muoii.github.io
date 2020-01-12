---
layout: post
published: true
title: 'Một số cấu trúc dữ liệu cơ bản'
date: '2019-07-07'
tags:
- data
- basic
---

Xin chào!

Có thể nói việc tổ chức dữ liệu là vô cùng cần thiết, nó cho phép ta tối ưu hóa được độ phức tạp cũng như tạo ra code vô cùng *magic* :)

Bài viết này, mình sẽ chỉ *liệt kê* và *chia sẻ liên kết* của một số các trúc dữ liệu cơ bản vì các cấu trúc dữ liệu cơ bản này đã có những bài viết chi tiết và rất hay nên mình sẽ *không* trình bày chi tiết.

# CTDL lưu trữ:

## 1.1 Array & linked list
	
[link tham khảo](http://vnoi.info/wiki/algo/data-structures/array-vs-linked-lists)

## 1.2 Stack, Queue, Deque

- **Stack** là CTDL cho phép thực hiện các thao tác: thêm/xóa phần tử cuối cùng của ctdl trong O(1).

  Vì ta chỉ có thể xóa phần tử ở cuối, nói cách khác là phần tử mà mới được thêm vào gần nhất nên stack còn được gọi là LIFO (Last In First Out).

  Ứng dụng điển hình: khử đệ quy, tìm chu trình Euler, thuật toán tarjan, cầu khớp,... 

- **Queue** là CTDL cho phép thực hiện các thao tác: thêm một phần tử vào cuối và xóa phần tử đầu của ctdl trong O(1).

  Ngược lại vs stack, Queue được gọi là FIFO (First In First Out).
  
  Ứng dụng điển hình: duyệt bfs...
  
- **Deque** là ctdl kết hợp của stack và queue cho phép:

	- Thêm, xóa phần tử đầu của ctdl trong O(1)
	
	- Thêm, xóa phần tử cuối của ctdl trong O(1)

  Ứng dụng nổi bật của deque là tìm min/max trên đoạn tịnh tiến (*bạn có tìm hiểu [tại đây](http://vnoi.info/wiki/algo/data-structures/deque-min-max)*)
  
## 1.3 Heap

- Heap là một cấu trúc dữ liệu cho phép thực hiện các thao tác:

	- Thêm một phần tử, với độ phức tạp O(logN).
	
	- Xóa một phần tử, với độ phức tạp O(logN).
	
	- Tìm max của các phần tử, với độ phức tạp O(1).
  
  Ứng dụng điển hình: dijkstra, prim...
  
  Bạn có thể đọc thêm về heap [tại đây](http://vnoi.info/wiki/translate/wcipeg/Binary-Heap)
 
## 1.4 Cây tìm kiếm

- Có thể kể đến những cây tìm kiếm như Binary Search Tree, Splay tree, Treap 

- Skip list là một ctdl dưới dạng liên kết để thay thế một phần nào đó cho BST, bạn có thể đọc thêm [tại đây](http://vnoi.info/wiki/algo/data-structures/Skip-Lists)

## 1.5 Bảng băm
	
[link tham khảo](https://vnoi.info/wiki/algo/data-structures/hash-table)
	
# CTDL xâu:

## 2.1 Cây tiền tố trie

Mình có viết một bài về nó ở [trie-muoii]()
	
## 2.2 KMP

[link tham khảo](http://vnoi.info/wiki/translate/wcipeg/kmp)
	
## 2.3 Aho Corasick
	
Tham khảo [ở đây](http://www.giaithuatlaptrinh.com/?p=703) hoặc [ở đây](https://www.geeksforgeeks.org/aho-corasick-algorithm-pattern-searching/)

## 2.4 Suffix Tree và ứng dụng

[link tham khảo](https://drive.google.com/file/d/0BwcTB8a10LBwYUwwNVYzbmZiZnM/view)
	
## 2.5 Palindrome Tree

[link tham khảo](http://vnoi.info/wiki/translate/codeforces/palindrome-tree)

# CTDL truy vấn:

## 3.1 Mảng cộng dồn (Prefix Sum)

**a)** 1d array:
	
Cho 1 dãy số A1,A2,...,An và mỗi truy vấn vs cặp số (L,R) yêu cầu tính tổng các giá trị Ai thuộc đoạn (L,R).

question: L R --> anwers = sum(Ai) (L<=i<=R)
	
Ý tưởng: tạo mảng s(i)=sum(A1,A2,..,Ai) vs độ phức tạp O(n), ta có thể trả lời 1 truy vấn trong O(1): anwers(L,R)=s(R)-s(L-1);
	
**b)** 2d array:
	
Cho một bảng số A có kích thước MxN và mỗi truy vấn vs 2 cặp số (x1,y1) và (x2,y2) (x1<=x2,y1<=y2) , tính tổng hình chữ nhật nhận 2 cặp số trên làm tọa độ đỉnh.
	
Tương tự, ta xây dựng s(i,j) là tổng của hình chữ nhật nhận (1,1) và (i,j) là đỉnh:
		
Khi đó, ta có: s(i,j)=s(i−1,j)+s(i,j−1)−s(i−1,j−1)+A(i,j)
		
answers((x1,y1),(x2,y2)) = s(x2,y2) - s(x2,y1-1) - s(x1-1,y2) + s(x1-1,y1-1)
	
**c)** 3d array:
	
Vd: cho khối hình hộp chữ nhật được tạo từ m.n.k ô, mỗi ô lưu một giá trị.
	
Tương tự, ta có thể xây dựng prefix sum như sau:

``` c++
/// build:
for(x,y,z: (1,1,1)-->(m,n,k))
s(x,y,z) =  s(x-1,y,z) + s(x,y-1,z) + s(x,y,z-1)
	  - s(x-1,y-1,z) - s(x-1,y,z-1) - s(x,y-1,z-1)
	  + s(x-1,y-1,z-1) + A(x,y,z)
	  
/// query	
sum((a,b,c)-->(x,y,z)) =  f(x,y,z) 
			- f(a,y,z) - f(x,b,z) - f(x,y,c) 
			+ f(x,b,c) + f(a,y,c) + f(a,b,z)
			- f(a,b,c);

///conditon: a<=x, b<=y, c<=z
```
	
## 3.2 Disjoint Sets

[link tham khảo](http://vnoi.info/wiki/algo/data-structures/disjoint-set)
	
## 3.3 Sparse Table

[link tham khảo](https://www.geeksforgeeks.org/sparse-table/)

## 3.4 Range Tree
	
- là cấu trúc dữ liệu cho phép thực hiện các thao tác cập nhật và truy vấn trên phạm vi nhất định, bạn có thể tiếp cận [tại đây](https://drive.google.com/file/d/0BwcTB8a10LBwbjB2elVmdzg1XzQ/view)
- các cấu trúc quản lí phạm vi điển hình:
		
	+ Segment Tree: [tham khảo](http://vnoi.info/wiki/algo/data-structures/segment-tree-extend)
		
	+ Binary Indexed Tree: [tham khảo](http://vnoi.info/wiki/algo/data-structures/fenwick)
		
## 3.5 Heavy-Light Decomposition
- **HLD** là kĩ thuật phân tách một cây thành nhiều chuỗi đỉnh (chain) rời nhau. Sau đó, ta có thể áp dụng các ctdl *quản lí phạm vi* lên những chuỗi này để có thể cập nhật dữ liệu hoặc trả lời các truy vấn trên một đường đi giữa 2 đỉnh trong cây.
- [tham khảo](http://vnoi.info/wiki/algo/data-structures/heavy-light-decomposition)
	
 **Như vậy mình đã giới thiệu một số cấu trúc dữ liệu cơ bản và liên kết các bài viết chi tiết của nó.**
 
 **Hi vọng bài viết này hữu ích cho bạn!**
 
 *Cảm ơn bạn đọc!*
 
 
 *muoii*
 
