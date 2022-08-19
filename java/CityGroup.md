```java
public class CityGroup {
    public class UF {
        int N;
        int count;
        
        int[] id;
        int[] size;

        UF (int n) {
            N = n;
            count = n;

            id = new int[n+1];
            size = new int[n+1];

            for (int i = 1; i <= n; i++) {
                id[i] = i;
                size[i] = 1;
            }
        }

        private int find(int p) {
            if (p == id[p]) {
                return p;
            }

            id[p] = find(id[p]);
            return id[p];
        }

        public void union(int p, int q) {
            int pRoot = find(p);
            int qRoot = find(q);

            if (pRoot != qRoot) {
                if (size[pRoot] > size[qRoot]) {
                    id[qRoot] = id[pRoot];
                    size[pRoot] += size[qRoot];
                } else {
                    id[pRoot] = id[qRoot];
                    size[qRoot] += size[pRoot];
                }
                count--;
            }
        }

        public int getMax () {  // 统计并查集的最大值
            int max = 0;
            for (int i = 1; i < size.length; i++) {
                max = Math.max(max, size[i]);
            }
            return max;
        }
    }

     public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();

        int[][] arr = new int[n][2];
        for (int i = 0; i < n - 1; i++) {
            arr[i][0] = in.nextInt();
            arr[i][1] = in.nextInt();
        }

        // 并查集
        int res = Integer.MAX_VALUE;  // 统计最小聚集度
        int[] maxArray = new int[n + 1];  // 统计每个城市的聚集度
        for (int i = 1; i <= n; i++) {  // 对于每一个城市
            UF uf = new UF(n);
            for (int j = 0; j < n - 1; j++) {  // 判断每一条路径
                if (arr[j][0] == i || arr[j][1] == i)  {
                    continue;
                } else {
                    uf.union(arr[j][0], arr[j][1]);
                }
            }
            maxArray[i] = uf.getMax();  // 每个城市对应的聚集度
            res = Math.min(res, maxArray[i]);  // 切掉路径后的最小聚集度
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 1; i < maxArray.length; i++) {
            if (maxArray[i] == res) {
                sb.append(i).append(" ");
            }
        }
        sb.setLength(sb.length() - 1);
        System.out.format("%s", sb);
}
```