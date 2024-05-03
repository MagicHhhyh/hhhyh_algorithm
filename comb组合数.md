```c++
const i64 P=998244353;
template <i64 mod= P>
struct Comb
{
	template <typename T>
	T qp(T a, T b, T P = mod)
	{
		T res = 1;
		while (b)
		{
			if (b & 1)
				res = res * a % P;
			a = a * a % P;
			b >>= 1;
		}
		return res;
	}
	vector<i64> suf, fac;
	Comb(int n = 1e6)
	{
		suf.resize(n + 1);
		fac.resize(n + 1);
		fac[0] = suf[0] = 1;
		for (int i = 1; i <= n; i++)
			fac[i] = fac[i - 1] * i % mod;
        suf[n]=qp(fac[n],mod-2);
        for(int i=n-1;i;i--)
        	suf[i] = suf[i + 1] * (i+1) % mod;
	}
	i64 C(int n, int m)
	{
		return fac[n] * suf[n - m] % mod * suf[m] % mod;
	}
};
```

