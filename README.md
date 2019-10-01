# git-graph-bfs
#rotten oranges
class Solution {
public:
    int orangesRotting(vector<vector<int>>& v) {
        int r=v.size();
        int c=v[0].size();
        int dist[r][c];
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<c;j++){
                if(v[i][j]==2)
                dist[i][j]=0;
                else if(v[i][j]==0)
                    dist[i][j]=-2;
                else
                    dist[i][j]=-1;
            }
        }
         int flag=1;
          for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
            {
                if(v[i][j]!=0)
                 flag=0; 
            }
        if(flag) return 0;
         queue<pair<int,int>> q;
        for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
            {
                if(v[i][j]==2)
               q.push(make_pair(i,j));  
            }
       if(q.empty())
           return -1;
        while(!q.empty())
        {
            auto node=(q.front());
            q.pop();
            int I=node.first;
            int J=node.second;
            if(J+1<c)
            {
                if(v[I][J+1]==1 && dist[I][J+1]==-1)
                {
                    dist[I][J+1]=dist[I][J]+1;
                    q.push(make_pair(I,J+1));
                }
              
            }
              if(I+1<r)
            {
                if(v[I+1][J]==1 && dist[I+1][J]==-1)
                {
                    dist[I+1][J]=dist[I][J]+1;
                     q.push(make_pair(I+1,J));
                }
              
            }
              if(I-1>=0)
            {
                if(v[I-1][J]==1 && dist[I-1][J]==-1)
                {
                    dist[I-1][J]=dist[I][J]+1;
                     q.push(make_pair(I-1,J));
                }
              
            }
              if(J-1>=0)
            {
                if(v[I][J-1]==1 && dist[I][J-1]==-1)
                {
                    dist[I][J-1]=dist[I][J]+1;
                     q.push(make_pair(I,J-1));
                }
              
            }
                
        }
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<c;j++)
            {
                if(dist[i][j]==-1)
                { return -1;}
            }
        }
        
        int w=0;
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<c;j++)
            {
              w=max(w,dist[i][j]);
            }
            
        }
        return w;
            
        
    }
};
