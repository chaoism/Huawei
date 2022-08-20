```java
import java.util.ArrayList;
import java.util.Scanner;

public class FootPrint {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        String res = in.nextLine();
        char[] str = res.toCharArray();
        String ans = "(0,0)";  // 默认值，非法时的结果

        int MAX = Integer.MIN_VALUE;
        int i = 0, j = 1;
        while (j < str.length) {
            while (str[i] == '(') {
                if (str[j] == ')') {
                    String[] s = res.substring(i+1, j).split(",");
                    System.out.printf("%s, %s\n", s[0], s[1]);

                    if (s[0].charAt(0) != '0' && s[1].charAt(0) != '0') {

                        int num1 = Integer.parseInt(s[0]);
                        int num2 = Integer.parseInt(s[1]);
                        if (num1 < 1000 && num2 < 1000 && num1 * num1 + num2 * num2 > MAX) {

                            MAX = num1 * num1 + num2 * num2;
                            ans = "(" + s[0] + "," + s[1] + ")";
                        }
                    }

                    break;
                }
                j++;
            }
            i = j;
            j = i+1;
        }

        System.out.println(ans);
    }
}

```