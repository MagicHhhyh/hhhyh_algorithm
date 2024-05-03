

```c++
int h[N], ne[N], w[N], v[N],s,t,d[N],cur[N]; 
void add(int u, int vv, int wi) { 
    ne[cnt] = h[u]; h[u] = cnt; w[cnt] = wi; v[cnt] = vv; cnt++;
}
bool bfs() {
    memset(d, 0, sizeof d);
    queue<int>q; d[s] = 1;
    q.emplace(s);
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        for (int i = h[u]; i; i = ne[i]) {
            int vv = v[i];
            if (d[vv] == 0&&w[i]>0) {
                d[vv] = d[u] + 1;
                if (vv == t)return true;
                q.emplace(vv);     
          
            }
        }
    }
    return false;
}
int dfs(int u, int flow) {
    if (u == t)return flow;
    int sum = 0;
    for (int i = cur[u]; i; i = ne[i]) {
        cur[u] = i;
        int vv = v[i];
        if (d[vv] == d[u] + 1 && w[i]>0) {
            int f= dfs(vv, min(flow, w[i]));
            w[i] -= f;
            w[i ^ 1] += f;
            sum += f;
            flow -= f;
            if (flow == 0)break;
        }
    }
    if (sum == 0)d[u] = 0;
    return sum;
}
void dinic() {
    while (bfs()) {
        //  memccpy()
        memcpy(cur, h, sizeof h);
        int d = dfs(s, 1e18);
        ans += d;
    }
}
```

