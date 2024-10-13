# Tasks-3

import java.util.ArrayList;
import java.util.List;

public class Main {

    public void main(String[] args) {

        //1 задание
        System.out.println(isStrangePair("ratio", "orator"));
        System.out.println(isStrangePair("bush", "hubris"));

        //2 задание Создание объектов Sale
        Sale laptop = new Sale("Laptop", 124200);
        Sale phone = new Sale("Phone", 51450);
        Sale headphones = new Sale("Headphones", 13800);

        // Вывод информации о товарах
        System.out.println(laptop);
        System.out.println(phone);
        System.out.println(headphones);

        // Вывод цен со скидкой
        System.out.println(laptop.getDiscountedPrice(25));
        System.out.println(phone.getDiscountedPrice(25));
        System.out.println(headphones.getDiscountedPrice(25));

        List<String[]> items = new ArrayList<>();
        items.add(new String[]{"Laptop", "124200"});
        items.add(new String[]{"Phone", "51450"});
        items.add(new String[]{"Headphones", "13800"});

        List<String[]> discountedItems = applyDiscount(items, 25);

        for (String[] item : discountedItems) {
            System.out.println("Товар: " + item[0] + ", Цена: " + item[1]);
        }

        //3
        double x = -2; // Координата x центра мишени
        double y = -3; // Координата y центра мишени
        double r = 4; // Радиус мишени
        double m = 5; // Координата x попадания
        double n = -6; // Координата y попадания

        boolean isHit = TargetHit.isShoot(x, y, r, m, n);
        if (isHit) {
            System.out.println("Попадание в мишень!");
        } else {
            System.out.println("Промах!");
        }

        //4
        int number = 3;
        parityAnalysis analysis = new parityAnalysis(number);

        boolean result = analysis.checkSumParity(); // Вызываем метод
        System.out.println("Сумма цифр " + number + " имеет ту же четность, что и само число: " + result);

        //5
        System.out.println(rps("камень", "ножницы")); // Игрок 1 выигрывает
        System.out.println(rps("бумага", "бумага")); // Ничья
        System.out.println(rps("ножницы", "камень")); // Игрок 2 выигрывает

        //6
        System.out.println(bugger(39));  // 3
        System.out.println(bugger(999)); // 4
        System.out.println(bugger(4));   // 0

        //7

        String object1 = "Скакалка"; // Идентификатор объекта 1
        int price1 = 550; // Цена объекта 1
        int quantity1 = 8; // Количество объекта 1

        String object2 = "Шлем"; // Идентификатор объекта 2
        int price2 = 3750; // Цена объекта 2
        int quantity2 = 4; // Количество объекта 2


        String object3 = "Мяч"; // Идентификатор объекта 2
        int price3 = 2900; // Цена объекта 2
        int quantity3 = 10; // Количество объекта 2


        String mostExpensiveObject = mostExpensive(object1, price1, quantity1,
                object2, price2, quantity2, object3, price3, quantity3);


        System.out.println("Самый дорогой объект: " + mostExpensiveObject);

        //8
        String str = "bbb";
        String longestSubstring = longestUnique(str);
        System.out.println("Самая длинная подстрока с уникальными символами: " + longestSubstring);

        //9
        String word = "arachnophobia";
        String prefix = "arachno";
        String suffix = "phobia";

        System.out.println("isPrefix(" + word + "," + prefix + "):" + isPrefix(word, prefix));
        System.out.println("isSuffix(" + word + "," + suffix + "):" + isSuffix(word, suffix));

        //10
        System.out.println(doesBrickFit(1, 1, 1, 1, 1));
        System.out.println(doesBrickFit(1, 2, 1, 1, 1));

    }


    //1.  Пара строк образует странную пару, если оба из следующих условий истинны:
    //– Первая буква 1-й строки = последняя буква 2-й строки.
    //– Последняя буква 1-й строки = первая буква 2-й строки.
    //– Создайте функцию, которая возвращает true, если пара строк представляет собой странную пару, и false в противном случае.
    public static boolean isStrangePair(String str1, String str2) {
        if (str1.isEmpty() && str2.isEmpty()) {
            return true;
        }
        if (str1.isEmpty() || str2.isEmpty()) {
            return false;
        } else {
            return str1.charAt(0) == str2.charAt(str2.length() - 1) &&
                    str1.charAt(str1.length() - 1) == str2.charAt(0);
        }
    }

    //2.  Создайте метод, принимающий на вход список товаров, где каждый элемент списка – массив,
    // содержащий название товара и его цену, и значение скидки, применяемой ко всем товарам.
    // Верните список с товарами и новыми ценами на них. Цена товара должна быть округлена до ближайшего
    // целого числа, если после применения скидки цена товара становится меньше 1, то ее следует округлить до 1.
    public static List<String[]> applyDiscount(List<String[]> items, double discount) {
        List<String[]> discountedItems = new ArrayList<>();

        for (String[] item : items) {
            String name = item[0];
            double originalPrice = Double.parseDouble(item[1]);
            double discountedPrice = originalPrice - (originalPrice * discount / 100);
            discountedPrice = Math.round(discountedPrice);
            discountedPrice = Math.max(discountedPrice, 1);
            discountedItems.add(new String[]{name, String.valueOf(discountedPrice)});
        }
        return discountedItems;
    }


    static class Sale {

        private String name;
        private double price;

        public Sale(String name, double price) {
            this.name = name;
            this.price = price;
        }

        public double getDiscountedPrice(double discount) {
            double discountedPrice = price - (price * discount / 100);
            discountedPrice = Math.round(discountedPrice);
            discountedPrice = Math.max(discountedPrice, 1);
            return discountedPrice;
        }

        @Override
        public String toString() {
            return "Товар: " + name + ", Цена: " + price;
        }

    }

    //3.  Создайте метод, определяющий факт попадания в круглую мишень на координатной плоскости.
    // В качестве входных данных выступают координаты центра круглой мишени (первые два входных параметра x, y),
    // радиус мишени (третий входной параметр r) и координаты попадания (четвертый и пятый входные параметры m, n).
    // Чтобы узнать, принадлежит ли точка кругу, необходимо узнать превышает ли расстояние до центра величину радиуса.

    class TargetHit {
        public static boolean isShoot(double x, double y, double r, double m, double n) {
            // Рассчитываем расстояние между точкой попадания и центром мишени
            double distance = Math.sqrt(Math.pow(m - x, 2) + Math.pow(n - y, 2));

            // Проверяем, превышает ли расстояние радиус мишени
            return distance <= r;
        }
    }

    //4.	Создайте функцию, которая принимает число в качестве входных данных и возвращает true, если сумма его цифр имеет ту же четность,
    // что и все число. В противном случае верните false.

    class parityAnalysis {
        private int number;

        // Конструктор класса
        public parityAnalysis(int number) {
            this.number = number;
        }

        // Метод для проверки четности
        public boolean checkSumParity() {
            int sumDigits = 0;
            int temp = number;

            // Суммируем цифры числа
            while (temp > 0) {
                sumDigits += temp % 10;
                temp /= 10;
            }

            // Проверяем четность числа и суммы цифр
            return (number % 2 == 0) == (sumDigits % 2 == 0);
        }
    }

    //5.	Создайте функцию, имитирующую игру "камень, ножницы, бумага". Функция принимает входные данные обоих игроков (камень, ножницы или бумага),
    // первый параметр от первого игрока, второй от второго игрока. Функция возвращает результат в следующем формате:
    // "Игрок 1 выигрывает", "Игрок 2 выигрывает", "Ничья" (если оба входа одинаковы)

    public static String rps(String player1, String player2) {
        if (player1.equals(player2)) {
            return "Ничья";
        } else if ((player1.equals("камень") && player2.equals("ножницы")) ||
                (player1.equals("ножницы") && player2.equals("бумага")) ||
                (player1.equals("бумага") && player2.equals("камень"))) {
            return "Игрок 1 выигрывает";
        } else {
            return "Игрок 2 выигрывает";
        }
    }
//6.	Создайте метод, который принимает число и возвращает его мультипликативное постоянство,
// которое представляет собой количество раз, которое вы должны умножать цифры введенного аргументаы,
// пока не достигнете одной цифры.


    public static int bugger(int number) {
        if (number < 10) {
            return 0; // Однозначное число, уже достигнуто
        }

        int count = 0;
        while (number >= 10) {
            count++; // Увеличиваем счетчик
            number = multiplyDigits(number); // Пересчитываем число
        }
        return count;
    }

    private static int multiplyDigits(int number) {
        int product = 1;
        while (number > 0) {
            product *= number % 10; // Умножаем на последнюю цифру
            number /= 10; // Удаляем последнюю цифру
        }
        return product;
    }
//7.	Создайте метод, принимающий массив объектов, представляющих инвентарь,
// где каждый предмет инвентаря представлен в виде массива строк и чисел (предмет, цена, количество),
// и вычисляющий предмет инвентаря с наибольшей общей стоимостью (цена × количество).


    public static String mostExpensive(String object1, int price1, int quantity1,
                                       String object2, int price2, int quantity2,
                                       String object3, int price3, int quantity3) {
        int totalCost1 = price1 * quantity1;
        int totalCost2 = price2 * quantity2;
        int totalCost3 = price3 * quantity3;

        if (totalCost1 > totalCost2 && totalCost1 > totalCost3) {
            return object1;
        } else if (totalCost2 > totalCost1 && totalCost2 > totalCost3) {
            return object2;
        } else if (totalCost3 > totalCost1 && totalCost3 > totalCost2) {
            return object3;
        } else {
            return ("Цены одинаковые");
        }
    }

//8.	Напишите метод, находящий в строке подстроку из уникальных символов наибольшей длины.

    public static String longestUnique(String str) {
        if (str.isEmpty()) {
            return "";// Пустая строка, если входная строка пуста
        }
        String longestSubstring = "";
        for (int i = 0; i < str.length(); i++) {
            for (int j = i + 1; j <= str.length(); j++) {
                String substring = str.substring(i, j);
                if (isUnique(substring) && substring.length() > longestSubstring.length()) {
                    longestSubstring = substring;
                }
            }
        }
        return longestSubstring;
    }

    private static boolean isUnique(String str) {
        for (int i = 0; i < str.length(); i++) {
            for (int j = i + 1; j < str.length(); j++) {
                if (str.charAt(i) == str.charAt(j)) {
                    return false; // Символ повторяется
                }
            }
        }
        return true; // Все символы уникальны
    }
//9.Создайте две функции: isPrefix(word, prefix-) и isSuffix (word, -suffix).
// – isPrefix должен возвращать true, если он начинается с префиксного аргумента.
// – isSuffix должен возвращать true, если он заканчивается аргументом суффикса.
// – В противном случае верните false.

    public static boolean isPrefix(String word, String prefix) {
        if (word.length() < prefix.length()) {
            return false;
        }
        return word.substring(0, prefix.length()).equals(prefix); // Сравниваем начальную часть слова с префиксом
    }

    public static boolean isSuffix(String word, String Suffix) {
        if (word.length() < Suffix.length()) {
            return false;
        }
        return word.substring(0, Suffix.length()).equals(Suffix); // Сравниваем начальную часть слова с суффиксом
    }



    /*10.	Напишите метод, который принимает следующие параметры (a, b, c, w, h):
    три измерения кирпича: высоту (a), ширину (b) и глубину (c) и возвращает true,
    если этот кирпич может поместиться в отверстие с шириной (w) и высотой (h).
    Пример:
    doesBrickFit(1, 1, 1, 1, 1) ➞ true

    doesBrickFit(1, 2, 1, 1, 1) ➞ true

    doesBrickFit(1, 2, 2, 1, 1) ➞ false

    Примечание:
            - Вы можете повернуть кирпич любой стороной к отверстию.
            - Если размеры кирпича равны размерам отверстия, то он поместится в отверстие.
            - Можно помещать кирпич только под ортогональным углом.*/

    public static boolean doesBrickFit (int a, int b,int c, int w, int h) { // Проверяем все возможные ориентации кирпича
        return (a <= w && b <= h) || (a <= h && b <= w) || (a <= w && c <= h) ||
                (a <= h && c <= w) || (b <= w && c <= h) || (b <= h && c <= w);
    }
}





