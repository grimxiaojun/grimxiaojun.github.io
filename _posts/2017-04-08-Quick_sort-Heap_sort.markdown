---
layout: post
title:  "Quick Sort Heap Sort"

---

## 题目大意：

```
利用快速排序对数据排序
```

代码如下：

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
int partition(vector<int>&v,int nLow,int nHigh){
	int nTemp=v[nHigh];
	int i=nLow,j=nLow-1;
	while(i<nHigh){
		if(v[i]<=nTemp){
			++j;
			if(i!=j){
				swap(v[i],v[j]);
			}
		}
		++i;
	}
	swap(v[j+1],v[nHigh]);
	return j+1;
}
void Quick_sort(vector<int>&v,int nLow,int nHigh){	
	if(nLow<nHigh){
		int nIndex=partition(v,nLow,nHigh);
		Quick_sort(v,nLow,nIndex-1);
		Quick_sort(v,nIndex+1,nHigh);
	}
}
int main(){
	int n;
	scanf("%d",&n);
	vector<int>v(n);
	for(int i=0;i<n;++i){
		scanf("%d",&v[i]);
	}
	Quick_sort(v,0,n-1);
	for(int i=0;i<n;++i){
		printf("%d ",v[i]);
	}
	return 0;
}
```



## 题目大意：

```
利用堆排序对数据排序
```

代码如下：

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
void update_tree(vector<int>&v,int root,int n){
	int father=root;
	int child=2*root+1;
	while(child<n){
		if(child!=n-1&&v[child]<v[child+1])++child;
		if(v[father]<v[child])swap(v[father],v[child]);
		else{
			break;
		}
		father=child;
		child=2*father+1;
	}
}
void heap_sort(vector<int>&v,int n){
	for(int i=n/2-1;i>=0;--i){
		update_tree(v,i,n);
	}
	for(int i=n-1;i>=0;--i){
		swap(v[i],v[0]);
		update_tree(v,0,i);
	}
}
int main(){
	int n;
	scanf("%d",&n);
	vector<int>v(n);
	for(int i=0;i<n;++i){
		scanf("%d",&v[i]);
	}
	heap_sort(v,n);
	//Quick_sort(v,0,n-1);
	for(int i=0;i<n;++i){
		printf("%d ",v[i]);
	}
	return 0;
}
```


