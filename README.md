
import java.util.Scanner;
import java.util.List;
import java.util.ArrayList;

public class Main {

    public static void generateSub(int i, List<Integer> v, int n, List<Boolean> temp, int sum, int[] cntways) {
        if (i == n) {
            int sumsplit = 0;
            for (int j = 0; j < n; j++) {
                if (temp.get(j)) {
                    sumsplit += v.get(j);
                }
            }
            if (sumsplit == sum) {
                for (int j = 0; j < n; j++) {
                    if (temp.get(j)) {
                        System.out.print(v.get(j) + " ");
                    }
                }
                System.out.print("and ");
                for (int x = 0; x < n; x++) {
                    if (!temp.get(x)) {
                        System.out.print(v.get(x) + " ");
                    }
                }
                System.out.println();
                cntways[0]++;
            }
            return;
        }

        temp.set(i, true);
        generateSub(i + 1, v, n, temp, sum, cntways);
        temp.set(i, false);
        generateSub(i + 1, v, n, temp, sum, cntways);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<Integer> v = new ArrayList<>();
        int sum = 0;
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt();
            v.add(val);
            sum += val;
        }
        List<Boolean> temp = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            temp.add(false);
        }
        if (sum % 2 != 0) {
            System.out.println("0");
            return;
        }
        sum = sum / 2;
        int[] cntways = {0};
        generateSub(0, v, n, temp, sum, cntways);
        System.out.println(cntways[0]);
    }
}
