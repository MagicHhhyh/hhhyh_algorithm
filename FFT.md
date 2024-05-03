

```c++
#include<bits/stdc++.h>
#include<complex>
using namespace std;
const int N = 1e7;
int r[N];

#define PI acos(-1)
complex<double>a[N],b[N];
void FFT(std::complex<double>*a,int len,int type) {
	for (int i = 0; i < len; i++) {
		if (i<r[i]) {
			swap(a[i], a[r[i]]);
		}
	}
	for (int slen = 2; slen <= len; slen <<= 1) {
		for (int j = 0; j < len; j += slen) {
			std::complex<double> w(1, 0);
			std::complex<double> exp(cos(PI * 2 / slen), sin(type*PI * 2 / slen));
			for (int k = 0; k < slen/2; k++) {
				auto x = a[j + k]; auto y = a[j + k+slen/2] *w;
				a[j + k] = x + y;
				a[j + k + slen / 2] = x - y;
				w *= exp;
			}
		}
	}
}

int main() {
	int n, m;
	cin >> n >> m;
    for (int i = 0; i <= n; i++) { 
	double x;
	cin >> x;
	a[i].real(x);
}
for (int i = 0; i <= m; i++) { 
	double x;
	cin >> x;
	b[i].real(x);
}
int len = 1;
int l=0;
while (len <= n + m) {
	len <<= 1; l++;
}
for (int i = 0; i < len; i++) {
	r[i] = (r[i >> 1] >> 1) | ((i & 1) << (l - 1));
}
FFT(a,len, 1);
FFT(b,len, 1);
for (int i = 0; i <=len; i++) {
	a[i] *= b[i];
}
FFT(a, len, -1);
for (int i = 0; i <= n + m; i++)cout << (int)(a[i].real()/len+0.5) << " ";
}
```
