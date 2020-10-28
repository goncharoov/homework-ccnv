# Отчёт о тестировании <Название приложения>

## Краткое описание

28.10.2020 12:00 - 28.10.2020 12:30 было проведено функциональное тестирование приложения Credit Card Number Validator.

На тестирование затрачено: ~0.5 часа. 

В результате тестирования выявлены следующие дефекты:
* Валидацию не проходит карта с номером содержащим более 16 знаков

## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты*:
* [Руководство по установке IntelliJ IDEA](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md)
* Исходный код приложения:
```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```

В качестве тестовых данных использовались данные с сайта https://www.freeformatter.com/credit-card-number-generator-validator.html
* 4929061505732554
* 2221007543895118
* 3539334092296455429

Тестирование производилось в следующем окружении:
* macOS Mojave 10.14.6
* OpenJDK version 11.0.9
* IntelliJ IDEA 2020.2.3 (Community Edition)