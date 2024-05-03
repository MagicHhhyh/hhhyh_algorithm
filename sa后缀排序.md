

```cpp
int a[N], c[N], x[N], y[N];
string s;
void base_sort() {
    for (int i = 0; i < n; i++) c[x[i] = s[i]]++;
    for (int i = 1; i <123; i++)
        c[i] += c[i - 1];
    for (int i = n - 1; ~i; i--)
        a[--c[s[i]]] = i;
    int m = 123;
    for (int k = 1; k < n; k<<=1) {
        int p = 0;
        
        for (int i = n - k; i < n; i++)y[p++] = i;
        for (int i = 0; i < n; i++)if (a[i] >= k)y[p++] = a[i]-k;
        for (int i = 0; i < m; i++)c[i] = 0;
        for (int i = 0; i < n; i++)c[x[i]]++;
        for (int i = 1; i < m; i++)c[i] += c[i - 1];
     
        for (int i = n - 1; ~i; i--)
            a[--c[x[y[i]]]] = y[i];
        swap(x, y);
        x[a[0]] = 0, p = 0;
        for (int i = 1; i < n; i++)
            x[a[i]] = (y[a[i]] == y[a[i - 1]]&&y[a[i]+k]==y[a[i-1]+k]) ? p : ++p;
        m = p+1;
    }
    for (int i = 0; i < n; i++)cout << a[i] + 1 << " ";
}
```