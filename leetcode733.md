~~~
class Solution {
public:
    void dfs(vector<vector<int>>& image, int i, int j, int orgColor,int newcolor){
        if(i<0 || j<0 || i>=image.size() || j>=image[0].size() || image[i][j] == newcolor || image[i][j] != orgColor){
            return;
        }
        image[i][j] = newcolor;
        dfs(image,i-1,j,orgColor,newcolor);
        dfs(image,i+1,j,orgColor,newcolor);
        dfs(image,i,j-1,orgColor,newcolor);
        dfs(image,i,j+1,orgColor,newcolor);
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        dfs(image,sr,sc,image[sr][sc],color);
        return image;
    }
};
~~~
