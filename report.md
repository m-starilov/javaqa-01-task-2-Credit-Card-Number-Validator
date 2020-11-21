# Отчёт о тестировании программы Credit Card Number Validator

## Краткое описание

21.11.2020 - 21.11.2020 было проведено функциональное тестирование программы Credit Card Number Validator.

На тестирование затрачено: 1 час

В результате тестирования выявлены следующие дефекты:
1. [Номера карт с количеством цифр отличным от 16 не проходят проверку](https://github.com/m-starilov/javaqa-01-task-2-Credit-Card-Number-Validator/issues/1)

## Описание процесса тестирования

Для тестирования программы Credit Card Number Validator был создан новый java проект в IntelliJ IDEA. Внутри проекта создан новый класс `Main` и туда скопиован код программы. Значение `String number` устанавливалось из тестовых данных и программа запускалась с каждым новым значением.
В ходе тестирования выявлена ошибка проверки карт с количеством цифр не равным 16.


В процессе тестирования использовались следующие артефакты:
* Код программы
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

В качестве тестовых данных использовались данные:
* Сгенерированные валидные номера карт с сайта [freeformatter.com](https://www.freeformatter.com/credit-card-number-generator-validator.html)*
* Произвольные невалидные значения

Тестирование производилось в следующем окружении:
*  ОС WIndows 10 Pro 64bit
*  IntelliJ IDEA

<details>
  <summary>*Пример</summary>

VISA:
* 4556787595108558
* 4539290574315833
* 4716871248372967172

MasterCard:
* 5253296323193463
* 5188542662602055
* 5487929203706651

American Express (AMEX):
* 370050344351439
* 345339756630956
* 349977373372001

Discover:
* 6011541949934738
* 6011548973868849
* 6011231733198524199

JCB:
* 3532167055512139
* 3535634547624795
* 3539412317418485524

Diners Club - North America:
* 5581500036518608
* 5417504782651670
* 5429484198720102

Diners Club - Carte Blanche:
* 30573226590511
* 30453005396549
* 30325346848828

Diners Club - International:
* 36789749107666
* 36947957293475
* 36743725475910

Maestro:
* 5020453930272576
* 0604896535253083
* 6761754815319957

Visa Electron:
* 4844066745177033
* 4844885750480481
* 4844986170867404

InstaPayment:
* 6394481810228729
* 6380804250697028
* 6376700511743716
</details>
