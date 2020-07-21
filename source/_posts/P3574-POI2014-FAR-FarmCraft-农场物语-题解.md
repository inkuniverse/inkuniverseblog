---
title: 'P3574 [POI2014]FAR-FarmCraft 农场物语 题解'
date: 2020-07-21 22:02:07
tags: 题解
---

 [P3574 [POI2014]FAR-FarmCraft](https://www.luogu.com.cn/problem/P3574)

 <!--more-->

 ![https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200721220526.png](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200721220526.png)

# 状态设计
设 f(i) 表示遍历 i 的子树所需时间。
g(i) 表示遍历 i 的子树，且所有人都装好软件所需的最少时间。
贪心按照 g(i) − f(i) 从大到小的顺序遍历儿子即可。
需要注意的是转移的方程。应该这样写：
# 方程的注意点

`for(int i=0;i<cnt;i++) f[u]=max(f[u],f[v]+g[u]+1),g[u]+=g[v]+2;`
+1 是因为自己也要算进去.

# 参考代码

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N=500010;
int f[N],g[N],son[N],n,cnt,tot,ver[N],nxt[N],h[N],a[N];
inline void add(int x,int y){ver[++tot]=y,nxt[tot]=h[x],h[x]=tot;}
inline bool cmp(int x,int y){return f[x]-g[x]>f[y]-g[y];}
inline void dfs(int u,int fa)
{
	if(u!=1) f[u]=a[u];
	for(int i=h[u];i;i=nxt[i]) if(ver[i]!=fa) dfs(ver[i],u);
	cnt=0;
	for(int i=h[u];i;i=nxt[i]) if(ver[i]!=fa) son[cnt++]=ver[i];
	sort(son,son+cnt,cmp);
	for(int i=0;i<cnt;i++) f[u]=max(f[u],f[son[i]]+g[u]+1),g[u]+=g[son[i]]+2;
}

int main()
{
	scanf("%d",&n);
	for(int i=1;i<=n;i++) scanf("%d",&a[i]);
	for(int i=1;i<n;i++)
	{
		int x,y;
		scanf("%d%d",&x,&y);
		add(x,y),add(y,x);
	}
	dfs(1,0);
	printf("%d",max(f[1],g[1]+a[1]));
	return 0;
}
```

