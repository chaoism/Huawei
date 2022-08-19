```java
import java.util.Scanner;

public class ShoutSeven {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        String[] lines = in.nextLine().split(" ");
        int N = lines.length;

        int K = 0;
        for (String s : lines) {
            K += Integer.parseInt(s);
        }

        int[] ans = new int[N];
        int sum = 0;
        int i = 0;
        int shout = 1;

        while (sum != K) {
            int idx = i % N;
            if (shout % 7 == 0) {   // 7的倍数
                ans[idx] += 1;
                sum ++;
            } else {
                String tmp = Integer.toString(shout);
                if (tmp.contains("7")) {
                    ans[idx] += 1;
                    sum ++;
                }
            }
            shout++;
            i++;
        }

        for (int j = 0; j < N; j++) {
            System.out.format("%d ", ans[j]);
        }
    }
}
```