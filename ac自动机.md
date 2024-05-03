```c++
void updata(string a, int id) {
    int u = 0;
    for (int i = 0; i < a.size(); i++) {
        int c = a[i] - 'a';
        if (!tr[u][c])tr[u][c] = ++times;
        u = tr[u][c];
    }
    cnt[u] = id;
}
void getfinal() {
    int u = 0;
    queue<int>q;
    for (int i = 0; i < 26; i++)if (tr[0][i])q.emplace(tr[0][i]);
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        for (int i = 0; i < 26; i++) {
            if (tr[u][i])fail[tr[u][i]] = tr[fail[u]][i], q.emplace(tr[u][i]);
            else tr[u][i] = tr[fail[u]][i];
 }
    }
}
```

第一部分字典树，第二部分final指针

