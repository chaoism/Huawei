# 【计算礼品发放的最小分组数目】

又到了一年的末尾，项目组让小明负责新年晚会的小礼品发放工作。

为使得参加晚会的同时所获得的小礼品价值相对平衡，需要把小礼品根据价格进行分组，但每组最多只能包括两件小礼品，并且每个分组的价格总和不能超过一个价格上限。

为了保证发放小礼品的效率，小明需要找到分组数目最少的方案。

你的任务是写一个程序，找出分组数最少的分组方案，并输出最少的分组数目。

### 输入

第一行数据为分组礼品价格之和的上限

第二行数据为每个小礼品的价格，按照空格隔开，每个礼品价格不超过分组价格和的上限

### 输出

输出最小分组数量


### 样例

输入

```
5
1 2 5
```

输出

```
2
```

## 详解

简单的贪心算法。先组大，再组小。

```java
public class GiftGroup {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int MAX = Integer.parseInt(in.nextLine());

        String[] lines = in.nextLine().split(" ");
        int size = lines.length;
        int[] giftPrices = new int[size];
        Arrays.sort(giftPrices);

        for (int i = 0; i < size; i++) {
            giftPrices[i] = Integer.parseInt(lines[i]);
        }

        int ans = 0;
        int i = 0;
        int j = size - 1;
        while (j >= i){
            if(Integer.valueOf(i).equals(Integer.valueOf(j))){
                ans++;
                break;
            }
            if(giftPrices[j] + giftPrices[i] <= MAX){
                ans++;
                i++;
                j--;
            }else{
                j--;
                ans++;
            }
        }

        System.out.format("%d", ans);
    }
}
```
