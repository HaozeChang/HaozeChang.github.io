---
title: 'prime number filtering'
date: 2024-01-14
permalink: /posts/2024/04/blog-post-4/
tags:
  - cool posts
  - prime number
---
## 筛选质数/合数：
### 1.朴素想法：循环看找不找的一个非1/非本身数字能整除该数字

```cpp
bool isPrime(int n){
	for(int i = 1;i<n;i++){
		if(i!=1&&i!=n&&n%i==0){
			return false;
		}
	}
	return true;
}
	
```

### 2.简单优化：缩小范围
假设x*y = n, 如果n%x为0，那么x%y肯定也是0,因此只要找到sqrt（n）即可

```cpp
bool isPrime2(int n){
	for(int i = 1;i<sqrt(n)+1;i++){
		if(i!=1&&i!=n&&n%i==0){
			return false;
		}
	}
	return true;
}
```

### 3.埃氏筛法
先初始化一个数组，我们认为全部是质数，从2开始，已知2是质数，但是2的倍数肯定是合数，所以标记他的全部倍数。然后检查3，检查到4时发现其已经标记为合数，跳过。
```cpp
bool isPrime3(int n){
	vector<bool>primes(n,0);
	int primeNum = 0;
	for(int i = 2;i<n;i++){
		if(primes[i]){
			primeNum++;
			for(int h = i*i;h<n;h+=i){
				primes[h] = false;
			}
		}
	}
	return true;
}
```

