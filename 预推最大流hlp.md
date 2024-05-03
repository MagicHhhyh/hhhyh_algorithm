```c++
bool bfs(int t) {
	queue<int>q;
	for (int i = 1; i <= n; i++)ht[i] = INF;
	ht[t] = 0;
	q.push(t);
	while (!q.empty()) {
		int x = q.front();
		q.pop();
		for (int i = h[x]; ~i; i = ne[i]) {
			if (w[i^1]>0&&ht[v[i]] > ht[x] + 1) {
				ht[v[i]] = ht[x] + 1;
				q.push(v[i]);
			}
		}
	}
	return ht[t] != INF;
}
void add(int u, int vv, int ww) {
	ne[cnt] = h[u]; h[u] = cnt; v[cnt] = vv; w[cnt] = ww; cnt++;
}
bool getmxh() {
	while (st[mxh].empty() && mxh >= 0)mxh--;
	return mxh >= 0;
}
bool push(int u) {
	bool f = u != s;
	for (int i = h[u]; ~i; i=ne[i]) {
		if (f && ht[v[i]]+1 != ht[u]  || !w[i])continue;
		int k = min(mxflow[u], w[i]);
		if (v[i] != s && v[i] != t && !mxflow[v[i]])mxh = max(mxh, ht[v[i]]),st[ht[v[i]]].push_back(v[i]);
		mxflow[u] -= k;
		mxflow[v[i]] += k;
		w[i] -= k;
		w[i ^ 1] += k;
		if (mxflow[u] == 0)return 0;
	}
	return true;
}
void re(int u) {
	ht[u] = INF;
	for (int i = h[u]; ~i; i = ne[i]) {
		if (w[i])ht[u] = min(ht[u], ht[v[i]]);
	}
	if (++ht[u] < n) {
		push(u);
		mxh = max(ht[u], mxh);
		st[ht[u]].push_back(u);
		++gap[ht[u]];
	}
}
int hlpp() {
	if(!bfs(t))return 0;
	for (int i = 1; i <= n; i++) {
		if (ht[i] != INF)gap[ht[i]]++;
	}
	mxflow[s] = 1e18;
	ht[s] = n;
	push(s);
	while (getmxh()) {
		int u = st[mxh].back();
		st[mxh].pop_back();
		if (push(u)) {
			if(--gap[ht[u]]==0)
			for (int i = 1; i <= n; i++) {
				if (ht[i] > ht[u])ht[i] = n + 1;
			}
			re(u);
		}
	}
	return mxflow[t];
}
```

