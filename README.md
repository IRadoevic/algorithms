# graph


#BFS and DFS
#include <bits/stdc++.h>

using namespace std;

class Graph{

    int v;
    list <int> *adj;
    bool *visited = new bool[v];

    public:Graph(int v)
    {
        this->v = v;
        adj = new list <int> [v];
    }
    public: void addEdge(int v, int w)
    {
        adj[v].push_back(w);
    }
    public: void BFS(int s)
    {
        bool *visited = new bool[v];
        for(int i = 0; i < v; i++)
        {
            visited[i] = false;
        }
        list<int> queue;
        visited[s] = true;
        queue.push_back(s);

        list<int>::iterator i;

        while(!queue.empty())
        {
            s = queue.front();
            cout << s << " ";
            queue.pop_front();

            for (i = adj[s].begin(); i != adj[s].end(); i++)
            {
                if (!visited[*i])
                {
                    visited[*i] = true;
                    queue.push_back(*i);
                }
            }
        }
    }
    public: void DFS(int v)
    {
        visited[v] = true;
        cout << v << " ";

        list<int>::iterator i;
        for (i = adj[v].begin(); i != adj[v].end(); ++i)
        {
            if (!visited[*i])
            {
                DFS(*i);
            }
        }
    }
};
int main()
{
    int v, w, s;
    cin >> v >> w >> s;
    Graph g(v);
    for(int i = 0; i < w; i++)
    {
        int a, b;
        cin >> a >> b;
        g.addEdge(a, b);
    }
    g.BFS(s);
    cout << endl;
    g.DFS(s);
}
