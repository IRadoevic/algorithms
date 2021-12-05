# graph


#BFS and DFS        /// 
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



Dijkstra   /// Shortest path in a weighted graph
#include <bits/stdc++.h>

using namespace std;

#include <limits.h>
 
#define V 9

int minDistance(int dist[], bool sptSet[])
{
    int min = INT_MAX, min_index;
 
    for (int v = 0; v < V; v++)
    {
        if (sptSet[v] == false && dist[v] <= min)
        {
            min = dist[v];
            min_index = v;
        }
            
    }
    return min_index;
}

void printSolution(int dist[])
{
    cout <<"Vertex \t Distance from Source" << endl;
    for (int i = 0; i < V; i++)
    {
        cout  << i << " \t\t"<<dist[i]<< endl;
    } 
}

void dijkstra(int graph[V][V], int src)
{
    int dist[V];
    bool sptSet[V];
    for (int i = 0; i < V; i++)
    {
        dist[i] = INT_MAX;
        sptSet[i] = false;
    }
    dist[src] = 0;
    for (int count = 0; count < V - 1; count++) {
        int u = minDistance(dist, sptSet);
        sptSet[u] = true;
        for (int v = 0; v < V; v++)
        {
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v])
            {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }
    printSolution(dist);
}

int main()
{
    int graph[V][V] = { { 0, 4, 0, 0, 0, 0, 0, 8, 0 },
                        { 4, 0, 8, 0, 0, 0, 0, 11, 0 },
                        { 0, 8, 0, 7, 0, 4, 0, 0, 2 },
                        { 0, 0, 7, 0, 9, 14, 0, 0, 0 },
                        { 0, 0, 0, 9, 0, 10, 0, 0, 0 },
                        { 0, 0, 4, 14, 10, 0, 2, 0, 0 },
                        { 0, 0, 0, 0, 0, 2, 0, 1, 6 },
                        { 8, 11, 0, 0, 0, 0, 1, 0, 7 },
                        { 0, 0, 2, 0, 0, 0, 6, 7, 0 } };
 
    dijkstra(graph, 0);
 
    return 0;
}
