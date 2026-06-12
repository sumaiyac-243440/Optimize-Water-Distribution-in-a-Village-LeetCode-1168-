#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> parent;

int Find(int x) {

    if(parent[x] == x)
        return x;

    return parent[x] = Find(parent[x]);
}

bool Union(int a, int b) {

    a = Find(a);
    b = Find(b);

    if(a == b)
        return false;

    parent[b] = a;

    return true;
}

int main() {

    int n;
    cin >> n;

    vector<int> wells(n);

    for(int i = 0; i < n; i++)
        cin >> wells[i];

    int m;
    cin >> m;

    vector<vector<int>> edges;

    for(int i = 1; i <= n; i++) {

        edges.push_back({wells[i - 1], 0, i});
    }

    for(int i = 0; i < m; i++) {

        int u, v, cost;
        cin >> u >> v >> cost;

        edges.push_back({cost, u, v});
    }

    sort(edges.begin(), edges.end());

    parent.resize(n + 1);

    for(int i = 0; i <= n; i++)
        parent[i] = i;

    int answer = 0;

    for(auto e : edges) {

        if(Union(e[1], e[2])) {

            answer += e[0];
        }
    }

    cout << answer << endl;

    return 0;
}
