# LEETCODE


https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/

class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        // cria a matriz com valores
        vector<vector<int>> Matriz(n,vector<int>(n,INT_MAX/2));
        
		for(auto& x:edges){
			Matriz[x[0]][x[1]]=x[2];
			Matriz[x[1]][x[0]]=x[2];
		}
        
        //algoritmo de Floyd
		for(int i=0;i<n;i++){
            
			for(int j=0;j<n;j++){
                
				for(int k=0;k<n;k++){
                    
					Matriz[j][k]=min(Matriz[j][k],Matriz[j][i]+Matriz[i][k]);
				}
			}
		}   
        
		int city=-1;
		int topo=INT_MAX;
        // i representa a cidades de origem
		for(int i=0;i<n;i++){
            // count numero de caminho <= distancia limite
			int count=0;
			for(int j=0;j<n;j++){
				if(j!=i && Matriz[i][j]<=distanceThreshold){
					count++;
				}
			}
            // cout <= topo, cidade com o menor número de cidades alcançáveis 
			if(count<=topo){
                
				topo=count;
				city=i;
			}
		}
		return city;

    }
};
