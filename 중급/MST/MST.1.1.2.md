#include <iostream>
using namespace std;

int kruskal(vector <pair<int, pair<int, int>>> edge){ //edge 는 {가중치, {노드1, 노드2}} 의 형태로 저장
    sort(edge.begin(),edge.end());
    int count = 0;
    int index= 0;
    int ans = 0;
    while (count!=v-1) {
        int weight = edge[i].first;
        int node1 = find(edge[i].second.first);
        int node2 = find(edge[i].second.second);
        if (node1 == node2) continue;
        ans += curr.w;
        merge(node1, node2);
        index++;
        count++;
    }
    return ans;
}

int main(){
    
    return 0;
}