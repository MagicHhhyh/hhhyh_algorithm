```c++
template <typename T>
class KMP {
public:
    vector<int> nx;
    T a;
    KMP(T input) {
        a = input;
        int n = a.size();
        nx.resize(n);
        int j = 0;
        for (int i = 1; i < n; i++) {
            while (j > 0 && a[i] != a[j]) j = nx[j - 1];
            if (a[i] == a[j]) j++;
            nx[i] = j;
        }
    }
    vector<int> find_times(T b) {
        int n = b.size();
        int j = 0;
        vector<int> pos;
        for (int i = 0; i < n; i++) {
            while (j > 0 && b[i] != a[j]) j = nx[j - 1];
            if (b[i] == a[j]) j++;
            if (j == a.size()) {
                j = nx[j - 1];
                pos.push_back(i - a.size() + 1);
            }
        }
        return pos;
    }
    int get_bord(int x) {
        return nx[x];
    }
};
```

