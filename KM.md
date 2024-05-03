```c++
  vector<i64> ex1(n+1), ex2(n+1);
    vector<int> left(n+1);
    
        auto bfs = [&](int u)
        {
            int dy = 0;
            vector<int> vis(n + 1);
            vector<int> pre(n + 1);
            vector<i64> slock(n + 1, 1e18);
            left[0] = u;
            do
            {
                int i = left[dy];
                int d = 1e18;
                int nx = 0;
                vis[dy] = 1;
                for (int j = 1; j <= n; j++)
                {
                    if (vis[j])
                        continue;
                    if (slock[j] > ex1[i] + ex2[j] - g[i][j])
                        slock[j] = ex1[i] + ex2[j] - g[i][j], pre[j] = dy;
                    if (slock[j] < d)
                        d = slock[j], nx = j;
                }
                for (int j = 0; j <= n; j++)
                {
                    if (vis[j])
                        ex1[left[j]] -= d, ex2[j] += d;
                    else
                        slock[j] -= d;
                }
                dy = nx;
            } while (left[dy]);
            while (dy)
                left[dy] = left[pre[dy]], dy = pre[dy];
        };
        for (int i = 1; i <= n; i++)
        {
            bfs(i);
        }
        i64 ans=0;
        for(int i=1;i<=n;i++){
            ans+=g[left[i]][i];
        }
```

