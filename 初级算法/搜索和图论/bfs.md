对于边权为1的最短路,可以用bfs解决.而像某些图形一次变换1个字符什么,变成另一种字符,一般可以用bfs解决.将每1个图看成1个点,最后图形的样子为终点.

示例:八数码

```java
import java.util.*;
import java.io.*;
class Main{
    static int N = 9;
    static int[] dirx = {-1,0,1,0},diry = {0,1,0,-1};
    // static streamTokenizer in = new streamTokenizer(new BufferedReader(new InputStreamReader(System.in)));
    static PrintWriter out = new PrintWriter(System.out);
    public static void main(String[] a) throws Exception{
        // Scanner in = new Scanner(System.in);
        FastReader in = new FastReader();
        StringBuilder bd = new StringBuilder();
        for(int i = 0; i < 9; i++){
            // in.nextToken();
            bd.append(in.next());
        }
        out.println(bfs(bd.toString().toCharArray()));
        out.flush();
    } 
    
    static int bfs(char[] s){
        Queue<String> q = new ArrayDeque<>();
        HashMap<String,Integer> dict = new HashMap<>();//字符串->操作次数
        String ori = String.valueOf(s,0,N);
        dict.put(ori,0);
        q.add(ori);
        String end = "12345678x";
        while(!q.isEmpty()){
            String t = q.poll();//弹出队首元素
            // out.println(t);
            if(t.equals(end)) return dict.get(end);
            int d = dict.get(t);
            int k = t.indexOf("x");
            int x = k/3,y = k%3; //对应的行和列坐标
            char[] tarr = t.toCharArray();//注意是对t数组修改,不是对s数组修改
            for(int i = 0,row,col; i < 4; i++){
                row = x + dirx[i];col = y + diry[i];
                if(row >= 0 && row < 3 && col >= 0 && col < 3){
                    swap(tarr,row*3 + col,k);
                    // String tt = t.replace('x',t.charAt(row*3+col)).replace();
                    String tt = new String(tarr,0,N);
                    if(!dict.containsKey(tt)){
                        dict.put(tt,d+1);
                        q.add(tt);
                    }
                    swap(tarr,row*3 + col,k);
                }
            }
        }
        return -1;
    }
    
    static void swap(char[] s,int i,int j){
        char c = s[i];
        s[i] = s[j];
        s[j] = c;
    }
}

//快读模板
class FastReader{
    StringTokenizer st;
    BufferedReader br;
    public FastReader(){
        br = new BufferedReader(new InputStreamReader(System.in));
    }
    
    String next(){
        // String str = "";
        
            while(st == null || !st.hasMoreElements()){
            try{
                // str = br.readLine();
                st = new StringTokenizer(br.readLine());
                }catch(Exception e){
            throw new RuntimeException(e);
        }
        // st = new StringTokenizer(str);
            }
            return st.nextToken();
        
    }
}

```

