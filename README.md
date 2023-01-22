# Домашнее задание к занятию "Система сборки Maven, управление зависимостями, автотесты на JUnit5"

## Задание 1. Дописываем тесты
Нашей целью будет переделать проект с приложением про бонус с покупки на мавен и хорошо его протестировать.

1. Создайте проект на базе Maven.

1. Добавьте в проект JUnit Jupiter & Surefire Plugin

1. Создайте сервисный класс со следующим исходным кодом:

```java
public class BonusService {
  public long calculate(long amount, boolean registered) {
    int percent = registered ? 3 : 1;
    long bonus = amount * percent / 100;
    long limit = 500;
    if (bonus > limit) {
      bonus = limit;
    }
    return bonus;
  }
}
```

4. Создайте тестовый класс со следующим исходным кодом:

```java
import static org.junit.jupiter.api.Assertions.*;

public class BonusServiceTest {

  @org.junit.jupiter.api.Test
  void shouldCalculateForRegisteredAndUnderLimit() {
    BonusService service = new BonusService();

    // подготавливаем данные:
    long amount = 1000;
    boolean registered = true;
    long expected = 30;

    // вызываем целевой метод:
    long actual = service.calculate(amount, registered);

    // производим проверку (сравниваем ожидаемый и фактический):
    assertEquals(expected, actual);
  }

  @org.junit.jupiter.api.Test
  void shouldCalculateForRegisteredAndOverLimit() {
    BonusService service = new BonusService();

    // подготавливаем данные:
    long amount = 1_000_000;
    boolean registered = true;
    long expected = 500;

    // вызываем целевой метод:
    long actual = service.calculate(amount, registered);

    // производим проверку (сравниваем ожидаемый и фактический):
    assertEquals(expected, actual);
  }
}
```

5. Запустите тесты через `mvn clean test`, убедитесь что они запускаются и проходят.

6. Проведите тест-дизайн сервисного класса (очень глубоко его можно не проводить), допишите недостающие тесты.

7. Убедитесь, что тесты запускаются и проходят.

**Результат:** отправьте на проверку ссылку на гитхаб-репозиторий с вашим проектом.
