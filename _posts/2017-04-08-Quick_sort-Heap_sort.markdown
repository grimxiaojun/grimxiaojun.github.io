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

## 题目大意：

```
利用归并排序对数据排序
```

代码如下：

```c++

void merge(vector<int>&v,vector<int>&temp,int start,int end){
	if(start>=end)return;
	int len=end-start;
	int mid=(len>>1)+start;
	int start1=start,end1=mid,start2=mid+1,end2=end;
	merge(v,temp,start1,end1);
	merge(v,temp,start2,end2);
	int k=start;
	while(start1<=end1&&start2<=end2){
		temp[k++]=v[start1]<v[start2]?v[start1++]:v[start2++];
	}
	while(start1<=end1){
		temp[k++]=v[start1++];
	}
	while(start2<=end2){
		temp[k++]=v[start2++];
	}
	for(int i=start;i<=end;++i){
		v[i]=temp[i];
	}
}
void merge_sort(vector<int>&v,int n){
	vector<int>temp(n);
	merge(v,temp,0,n-1);
}

```
## 题目大意：

```
利用选择排序对数据排序
```

代码如下：

```c++
void selection_sort(vector<int>&v,int n){
  int i,j,min;
  for(int i=0;i<n-1;++i){
    min=i;
    for(int j=i+1;j<n;++j){
      if(v[min]>v[j]){
        min=j;
      }
    }
    swap(v[i],v[min]);
  }
}
```

## 题目大意：

```
利用冒泡排序对数据排序
```

代码如下：

```c++
void bubble_sort(vector<int>&v,int n){
  int i,j;
  for(int i=0;i<n-1;++i){
    for(int j=0;j<n-1-i;++j){
      if(v[j]>v[j+1])swap(v[j],v[j+1]);
    }
  }
}
```

## 题目大意：

```
利用插入排序对数据排序
```

代码如下：

```c++
void insertion_sort(vector<int>&v,int n){
  int i,j,temp;
  for(i=1;i<n;++i){
    temp=v[i];
    j=i-1;
    for(;j>=0&&v[j]>temp;--j){
      v[j+1]=v[j];
    }
    v[j+1]=temp;
  }
}
```

