#include <iostream>
#include <vector>
using namespace std;

vector<vector<int>> adj; // graph represented as an adjacency list
int n; // number of vertices
int s; // start
vector<bool> visited;

void dfs(int v) {
    visited[v] = true;
    for (int u : adj[v]) {
        if (!visited[u])
            dfs(u);
    }
}

int main(){
    dfs(s);
    return 0;
}