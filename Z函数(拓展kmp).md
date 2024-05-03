```c++
vector<int> Z(string s)
{
    int n = s.size();
    vector<int> z(n);
    for (int i = 1, l = 0, r = 0; i < n; i++)
    {
        if (r > i)
            z[i] = min(r - i, z[i - l]);
        while (i + z[i] < n && s[i + z[i]] == s[z[i]])
            z[i]++;
        if (i + z[i] > r)
            l = i, r = i + z[i];
    }
    return z;
}
```

