```c++
struct node
{
    int mn, pos;
    node operator+(const node& b)
    {
        node c = b;
        if (mn <= c.mn)
            c.mn = mn, c.pos = pos;
        return c;
    }
    void op(int x)
    {
        mn += x;
    }
};
struct
{
    int l, r;
    int tag;
    void op(int x)
    {
        tag += x;
        c.op(x);
    }
    node c;
} tr[N << 2];
void build(int u, int l, int r)
{
    tr[u].l = l;
    tr[u].r = r;
    tr[u].tag = 0;
    tr[u].c.mn = 0, tr[u].c.pos = l;
    if (l == r)
        return;
    int mid = l + r >> 1;
    build(u << 1 | 1, mid + 1, r);
    build(u << 1, l, mid);
}
void push_up(int u)
{
    tr[u].c = tr[u << 1].c + tr[u << 1 | 1].c;
}
void push_down(int u)
{
    tr[u << 1].op(tr[u].tag);
    tr[u << 1 | 1].op(tr[u].tag);
    tr[u].tag = 0;
}
void modify(int u, int l, int r, int d)
{
    if (tr[u].l >= l && tr[u].r <= r)
    {
        tr[u].op(d);
        return;
    }
    else
    {
        int mid = tr[u].l + tr[u].r >> 1;
        push_down(u);
        if (l <= mid)
            modify(u << 1, l, r, d);
        if (r > mid)
            modify(u << 1 | 1, l, r, d);
        push_up(u);
    }
}
node ask(int u, int l, int r)
{
    if (tr[u].l >= l && tr[u].r <= r)
        return tr[u].c;
    int mid = tr[u].l + tr[u].r >> 1;
    push_down(u);
    if (r <= mid)
        return ask(u << 1, l, r);
    if (l > mid)
        return ask(u << 1 | 1, l, r);
    return ask(u << 1, l, r) + ask(u << 1 | 1, l, r);
}
```

