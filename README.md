Документація з виправлення програми обробки анкет

Виявлені проблеми та їх вирішення

1. Клас Form.java

Проблеми:
- Конструктор не призначав значення полям класу
- Потрібно додати метод toString() для правильного відображення об'єктів у списках

Виправлення:
- Додано присвоєння значень у конструкторі через ключове слово `this`
- Додано метод toString(), щоб при виведенні списку одружених осіб відображались імена

```java
public Form(String name, int birthday, String hobby, int duration, String level, boolean marriage, double salary) {
    this.name = name;
    this.birthday = birthday;
    this.hobby = hobby;
    this.duration = duration;
    this.level = level;
    this.marriage = marriage;
    this.salary = salary;
}

@Override
public String toString() {
    return name;
}
```

2. Клас FormAnalytics.java

**Проблеми:**
- Невідповідність типів у методі middleSalary (використання += з double)
- Відсутність методу для сортування за віком
- Відсутність методу для додавання вже створених об'єктів Form

Виправлення:
- Змінено тип змінної middleSalary з int на double, щоб правильно працювати з числами з плаваючою точкою
- Додано розрахунок середнього значення (ділення на кількість осіб)
- Додано метод add(Form person) для додавання існуючих об'єктів Form
- Реалізовано метод sortByAge() для сортування за роком народження

```java
public void middleSalary(){
    double middleSalary = 0;

    for (Form middle : persons){
        middleSalary += middle.salary;
    }
    
    if (!persons.isEmpty()) {
        middleSalary = middleSalary / persons.size();
    }

    System.out.println("Середня зарплата: " + middleSalary);
}

public void add(Form person) {
    persons.add(person);
}

public void sortByAge() {
    Collections.sort(persons, new Comparator<Form>() {
        @Override
        public int compare(Form person1, Form person2) {
            return person1.birthday.compareTo(person2.birthday);
        }
    });
    
    System.out.println("Відсортовано за роком народження:");
    show();
}
```

3. Клас Main.java

Проблеми:
- Об'єкти Form створювались, але не додавались до колекції FormAnalytics
- Не було викликів методів для демонстрації функціональності

Виправлення:
- Створено об'єкт FormAnalytics
- Додано всі створені анкети до цього об'єкту
- Додано виклики методів для демонстрації всіх функцій програми

```java
// Створюємо об'єкт для роботи з анкетами
FormAnalytics analytics = new FormAnalytics();

// Додаємо анкети до аналітичного інструменту
analytics.add(person1);
analytics.add(person2);
// ... додавання інших об'єктів

// Виконуємо операції аналізу
System.out.println("Список всіх анкет:");
analytics.show();

System.out.println("\n--------------------------\n");
analytics.middleSalary();

System.out.println("\n--------------------------\n");
analytics.marriaages();

System.out.println("\n--------------------------\n");
analytics.sortByAge();
```

Виправлення помилок запуску

Виправлено наступні помилки під час запуску програми:

1. "Class 'Main' not found in module 'OOP-PR5_6'":
   - Перевірено структуру проекту та розміщення файлів
   - Налаштовано конфігурацію запуску в IntelliJ IDEA

2. "Main method not found in class Main":
   - Перевірено наявність та правильність сигнатури методу main
   - Перебудовано проект для оновлення скомпільованих файлів

Висновки

Після внесення всіх виправлень програма має коректно:
- Зберігати інформацію про анкети
- Відображати список всіх анкет
- Обчислювати середню зарплату
- Показувати список одружених осіб
- Сортувати анкети за віком (роком народження)
