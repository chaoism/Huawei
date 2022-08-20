```java
import java.util.Scanner;

public class ClimbMountain {
    // 递归
    public static int climb(int n) {
        if (n < 3) return 1;
        if (n == 3) return 2;
        return climb(n-1) + climb(n-3);
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        int N = in.nextInt();

        // 动态规划
        if (N < 3) {
            System.out.printf("%d", 1);
        }
        if (N == 3) {
            System.out.printf("%d", 2);
        }

        int[] ans = new int[N+1];

        ans[0] = 0;
        ans[1] = 1;
        ans[2] = 1;
        ans[3] = 2;

        for (int i = 4; i <= N; i++) {
            ans[i] = ans[i-1] + ans[i-3];
        }
        System.out.printf("%d", ans[N]);
    }
}
```