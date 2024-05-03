```cpp

struct {
	int l, r;
	int sum;
	int add;
}tr[N << 2];
void push_up(int u) {
	tr[u].sum = tr[u << 1].sum + tr[u << 1 | 1].sum;
}
void build(int u, int l, int r)
{
	tr[u].l = l; tr[u].r = r;
	if (l == r)return;
	int mid = l + r >> 1;
	build(u << 1 | 1, mid + 1, r);
	build(u << 1, l, mid);
}
void push_down(int u)
{
	auto& root = tr[u], &left = tr[u << 1], &right = tr[u << 1 | 1];
	if (root.add) {
		left.add += root.add, left.sum += (left.r - left.l + 1) * root.add;
		right.add += root.add, right.sum += (right.r - right.l + 1) * root.add;
		root.add = 0;
	}
}
void modify(int u, int l, int r, int d)
{
	if (tr[u].l >= l && tr[u].r <= r) {
		tr[u].sum += (tr[u].r - tr[u].l + 1) * d;
		tr[u].add += d;
	}
	else {
		push_down(u);
		int mid = tr[u].l + tr[u].r >> 1;
		if (l <= mid)modify(u << 1, l, r, d);
		if (r > mid)modify(u << 1 | 1, l, r, d);
		push_up(u);
	}
}
int query(int u, int l, int r) {
	if (tr[u].l >= l && tr[u].r <= r)return tr[u].sum;
	push_down(u);
	int mid = tr[u].l + tr[u].r >> 1;
	int sum = 0;
	if (l <= mid)sum += query(u << 1, l, r);
	if (r > mid)sum += query(u << 1 | 1, l, r);
	return sum;
}


```