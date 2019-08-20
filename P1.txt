// Problem 1: Print paths are given source-destination using (normal path/ shortest path).(Easy)
//This can be solved by my given BFS code. 
//Take input from user source and destination vertex. Just run the BFS for the user given source vertex. 
//Then print path using the printpath function feeding it with source vertex, destination vertex, and parent array . 


#include <iostream>
#include<fstream>
#include <queue>


using namespace std;

void printPath(int sourceVertex, int queryVertex, int parent[]) {
 
        if (sourceVertex == queryVertex) {
           cout<< queryVertex << "->";
        } else if (parent[queryVertex] == -1) {
            cout << "no path";
        } else {
            printPath(sourceVertex, parent[queryVertex],parent);
            cout<< queryVertex << "->";
        }
    }


int main()
{
    // take the graph from file as input
    ifstream reader;
    reader.open("input.txt");
    int vertex, edges;
    reader >> vertex >> edges;
    
    int ** graph;
    graph=new int *[vertex];
    
    for(int i=0; i< vertex; i++){
        
        graph[i]=new int[vertex];
    }
    for(int i=0;i<vertex;i++)
		for(int j=0;j<vertex;j++)
			reader >> graph[i][j];



    // taking user query
    int source, destination;
    cout << "Please Give Source and Destination Vertex ( 0 ~"<< vertex-1<<" )" << endl;
    cin >> source >> destination;

    //-----  implement BFS---------
    int *visited=new int[vertex];
    // 0 means not explored;
    // 1 means explored;
    int * parent=new int[vertex];
    // -1 means the starting source node;
    // other values means other nodes under the source node;
    
    // taking the source verted from user
        queue<int> bfsQueue; 
        visited[source] = 1;
        parent[source] = -1;
 
        bfsQueue.push(source);
        while (!bfsQueue.empty()) {
            int dequededElement = bfsQueue.front();// take the first element
            bfsQueue.pop();// delete it from the queue
            for (int i = 0; i <vertex; i++) {
                if (graph[dequededElement][i] == 1) {
                    if (visited[i] == 0) {
                        bfsQueue.push(i);
                        visited[i] = 1;
                        parent[i] = dequededElement;
                    }
                }
            }
            visited[dequededElement] = 2;//fully explored
        }
        
    // now pass the user given source vertex and destination vertex into this method.
    cout<< "The shortest path is as follows: "<< endl;
    printPath(source,destination,parent);


    return 0;
}


