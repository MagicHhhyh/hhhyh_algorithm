```c++
   vector<vector<int>> fa(n, vector<int>(21, -1));
    vector<int>dep(n);
    function<void(int x, int fa)> dfs = [&](int x, int f)
    {
        fa[x][0]=f;
        for(int i=1;i<=20;i++){
            if(fa[x][i-1]==-1)fa[x][i]=-1;
            else fa[x][i]=fa[fa[x][i-1]][i-1];
        }
        for (auto y : e[x])
        {
            if(y==f)continue;
            dep[y]=dep[x]+1;
            dfs(y,x);
        }
    };
    function<int(int x,int y)>getfa=[&](int x,int y){
        if(dep[x]<dep[y])swap(x,y);
        for(int i=20;~i;i--)if(fa[x][i]!=-1&&dep[fa[x][i]]<=dep[y])x=fa[x][i];
        if(x==y)return x;
        for(int i=20;~i;i--)if(fa[x][i]!=fa[y][i])x=fa[x][i],y=fa[y][i];
        return fa[x][0];
    };
    
```



