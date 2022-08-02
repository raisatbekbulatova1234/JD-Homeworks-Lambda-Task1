import java.util.function.*;
import java.util.function.Supplier;

public class Calculator {
    static Supplier<Calculator> instance = Calculator::new;

    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x * y;
    BinaryOperator<Integer> divide = (x, y) -> x / y;

    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;

    Predicate<Integer> isPositive = x -> x > 0;
    Predicate<Integer> isEqualsZero = x -> x == 0;

    Consumer<Integer> println = System.out::println;

}

class Main {

    public static void main(String[] args) {

        Calculator calc = Calculator.instance.get();

        int a = calc.plus.apply(1, 2);
        int b = calc.minus.apply(1, 1);
        int c = calc.divide.apply(a, b);

        calc.println.accept(c);
    }

}
/* Код не работает т.к. в строке 34 b==0, и в строке 35 мы дели на b, соответственно на ноль.
   Решение: проверка на равенство нулю делителя при выполнении метода и вывод на экран предупреждения при y==0;
    BinaryOperator<Integer> divide = (x, y) -> {
        if (y == 0) {
            System.out.println("На ноль делить нельзя");
        }
            return (x / y);
    };
 */