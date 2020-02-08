#include "the3.h"
#define INF 99999 

// You  can define extra functions here
int DFS(int v, bool visited[],int**& edgeList,int n){
    visited[v]=true;
    
    for(int i=0;i<n;i++){
        if(edgeList[v][i]!=0 && !visited[i]) 
            DFS(i,visited,edgeList,n); 
    }
    
}

// INPUT :
//            n         : number of nodes in the graph
//            edgeList  : edges in the graph
//            scores    : importance scores
// return value : 
//                 number of disconnected components
int Important (int n, int**& edgeList, double*& scores)
{ 

    int dist[n][n];
    for(int i=0;i<n;i++){
        
        for(int j=0;j<n;j++){
           
           if(i!=j && edgeList[i][j]==0) dist[i][j]=INF;
            
           else dist[i][j] =edgeList[i][j];
            
        }
    }
    
    for(int i=0;i<n;i++){
        scores[i]=0;
    }
    
    for(int k=0;k<n;k++){
        
        for(int i=0;i<n;i++){
            
            for(int j=0;j<n;j++){
                
                if(dist[i][k] + dist[k][j] < dist[i][j]){
                    dist[i][j] = dist[i][k] + dist[k][j]; 
                     }
            }
        }
    }
    
    for(int k=0;k<n;k++){
        
        for(int i=0;i<n;i++){
            
            for(int j=0;j<n;j++){
                
                 if(i==k || j==k) scores[k]+=0;
                 else if(i==j &&  dist[i][k]!=INF && dist[k][j]!=INF) scores[k]+= (dist[i][k]+dist[k][j]);
                else if(dist[i][j]!=INF && dist[i][k]!=INF && dist[k][j]!=INF) scores[k]+=double(double(dist[i][k]+dist[k][j])/double(dist[i][j])); 
            }
            
        }
        
    }
    
    
    bool* visited = new bool[n];
    int count=0;
    for(int v=0;v<n;v++){
        if(visited[v]==false){
        DFS(v,visited,edgeList,n);
        count+=1;
            
        }
    }
    
    
    
   return count; 
}

