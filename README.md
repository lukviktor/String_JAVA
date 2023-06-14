# String_JAVA
## Класс String
Строка – это последовательность символов.
В Java строки реализованы с помощью трех основных классов модуля [java.base ](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/module-summary.html), пакета [java.lang](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/package-summary.html), таких как: `String`, `StringBuilder`, `StringBuffer`.
Больше информации о методах класса String вы сможете найти в [официальной документации](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).
Пакет java.lang подключается автоматически.
Все три класса объявлены как `final`.
Это означает, что нет возможности создать собственную реализацию классов-наследников со свойствами строк.
Для форматирования и обработки строк применяются классы _**Formatter**_, _**Pattern**_, _**Matcher**_.

### При этом следует отметить ряд особенностей класса String:
* является общедоступным (нет необходимости в импорте пакета)
* является финализированным, то есть не может иметь потомков
* реализует интерфейсы _Serializable_, _Comparable<String>_, _CharSequence_
* объект класса String представляет собой строку, а также является неизменяемым или немодифицируемым (_immutable_).

### Со строками можно выполнять различные операции. Для этого класс String имеет ряд методов:
Прототип метода Назначение метода
* `char charAt(int pos)`	Получение символа по указанной позиции pos
* `String concat(String s)` или «`+`»	Соединение (конкатенация) двух строк
* `boolean endsWith(String suffix)`	Проверка, заканчивается ли эта строка указанным суффиксом
* `boolean equals(Object ob)`	Сравнение двух строк с учетом регистра
* `boolean equalsIgnoreCase(String s)`	Сравнение двух строк без учета регистра
* `static String format(String format, Object... args)`	Получение строки согласно формату, указанному первым аргументом, включив в нее все перечисленные данные во втором аргументе
* `void getChars(<параметры>)`	Получение символов строки в виде массива двухбайтных значений
* `int indexOf(int ch)`	Определение позиции первого вхождения указанного символа в строке
* `String intern()`	Добавление строки в пул строк
* `int lastIndexOf(char c)`	Определение позиции последнего вхождения указанного символа в строке
* `int length()`	Определение длины строки
* `boolean matches(String regex)`	Определение соответствия строки указанному регулярному выражению
* `String repeat(int count)`	Возвращение строки, которая представляет собой конкатенацию этой строки, повторяющееся указанное количество раз
* `String replace(char c1, char c2)`	Замена в строке всех вхождений первого символа вторым символом
* `String replaceAll(String regex, String replacement)`	Заменяет каждую подстроку этой строки, которая соответствует указанному регулярному выражению, на указанную вторым аргументом строку
* `String split(String regex)`	Получение массива строк на основе разделителя в виде регулярного выражения
* `boolean startsWith(String prefix)`	Проверка, начинается ли эта строка с указанного префикса
* `String substring(int n)`	Извлечение из строки подстроки, начиная с позиции n
* `String substring(int n, int m)`	Извлечение из строки подстроки длиной (m-n), начиная с позиции n
* `String toLowerCase()`	Преобразование всех символов строки в нижний регистр
* `String toUpperCase()`	Преобразование всех символов строки в верхний регистр
* `String trim()`	Удаление всех пробелов в начале и в конце строки
* `static String valueOf(<значение>)`	Преобразование переменной базового типа к строке

### Объединение или конкатенация – операция объединения строк, в результате которой возвращается одна строка, полученная вследствие объединения второй строки с окончанием первой.
Результат объединения необходимо помещать в переменную, чтобы его можно было в дальнейшем использовать.

В Java существует два способа объединения строк: метод `concat()` и перегруженные операторы "`+`" и "`+=`". `Метод String concat(String str)` не вносит изменения в строку.
Он создает новую строку (новый объект String), которая является результатом слияния текущей строки и переданной в метод как параметр.
Необходимо отметить, что "`+`" – это один из немногих перегруженных операторов в языке Java. Перегрузка операторов для объектов пользовательских классов невозможна.

#### Когда нужно извлечь одновременно массив символов, необходимо использовать метод getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin), где:

* srcBegin – первый индекс в строке, необходим для начала извлечения символов
* srcEnd – последний индекс в строке, до которого будут извлекаться символы
* dst – массив, в который будут помещены извлеченные символы
* dstBegin – индекс в массиве dst, начиная с которого нужно добавить извлеченные из строки символы.
```
    String str = "Software And Hardware!";
    int start = 9;
    int end = 12;
    char[] dst = new char[end - start];
    str.getChars(start, end, dst, 0);
    System.out.println(dst);

      Вывод в консоли:
      And
```

`regionMatches()` - данный метод выполняет сравнение определенных подстрок в пределах двух строк.

Этот метод имеет две формы:

Форма 1: boolean regionMatches(int toffset, String other, int oofset, int len)

Форма 2: boolean regionMatches(boolean ignoreCase, int toffset, String other, int oofset, int len), где

* `ignoreCase`: флаг, указывающий, что можно не учитывать регистр символов при сравнении (если флаг имеет значениеtrue, то регистр не учитывается)
* `toffset`: индекс, с которого начинается сравнение в строке, из которой мы вызываем этот метод
* `other`: строка, с которой сравнивается вызывающая строка
* `oofset`: индекс, с которого начинается сравнение в строке, с которой сравниваем
* `len`: количество символов, которые будут сравниваться в двух строках.

Методы `int compareTo(String anotherString)` и `int compareToIgnoreCase(String str)` позволяют сравнить две строки. Также результаты этих методов могут ответить на вопрос, какая из двух строк больше в лексикографическом порядке, а какая меньше:

* если метод возвращает значение больше 0, то исходная строка больше
* если метод возвращает значение меньше 0, то наоборот, полученная строка больше.
Лексикографический порядок означает, например, что строка "A" меньше, чем строка "B", так как символ 'A' в алфавите стоит перед символом 'B'. Если первые символы строк равны, то в расчет берутся следующие символы.

### `String format(String format, Object... args).` создания форматированных строк.
```
String formatString = "We are printing double variable (%f), string (\"%s\") and integer variable (%d).";
System.out.println(String.format(formatString, 0.7, "Java", 10));
```

Ниже представлены наиболее часто используемые варианты управляющих последовательностей.

* `%d` – целое число (int, long, …)
* `%f` – вещественное число (float, double)
* `%s` – строка
* `%c` – символ
* `%%` – символ %
* `%t` – дата/время
* `%b` – булево значение


### StringBuffer и StringBuilder
Для решения проблемы неэффективного использования памяти в Java были добавлены классы `StringBuffer` и `StringBuilder`. По сути, это расширяемая строка, в которую можно вносить изменения без ущерба для производительности.

Классы `StringBuffer` и `StringBuilder` очень похожи. Они имеют одинаковые конструкторы, одни и те же методы, которые одинаково используются. Их основное различие состоит в том, что `StringBuffer` – потокобезопасный и синхронизированный. Это значит, что его лучше использовать в многопоточных приложениях, где к объекту могут иметь доступ несколько потоков. Если же разрабатывается однопоточное приложение, то лучше воспользоваться классом `StringBuilder`. Он не потокобезопасный, но работает быстрее, чем `StringBuffer`.

Во время создания нового объекта `StringBuffer` вызывается конструктор по умолчанию. Он автоматически резервирует память объёмом 16 символов (емкость буфера). Это в дальнейшем позволяет быстро вносить изменения в содержимое объекта, оставаясь в пределах выделенной под объект памяти. Размер необходимой памяти можно указывать в конструкторе. В случае, когда длина строки `StringBuffer` после изменения превышает размер выделенной памяти, объём объекта автоматически увеличивается на столько, чтобы еще оставался небольшой резерв для возможных изменений.

При необходимости объекты классов StringBuffer, StringBuilder и String можно преобразовывать друг в друга. Для этого существует ряд методов. Также можно использовать и конструкторы:

Конструктор класса `StringBuffer`/`StringBuilder` может принимать в качестве параметра объект `String`.
Объекты класса `StringBuffer`/`StringBuilder` можно преобразовать в объект класса `String` методом `toString()` или с помощью конструктора класса `String`.
Обратите внимание на некоторые методы класса `StringBuilder`. У класса `StringBuffer` – методы аналогичны.

* `int capacity()`	Возвращает количество символов, для которых зарезервирована память – емкость буфера объекта.
* `void ensureCapacity(int minimumCapacity)`	Изменяет минимальную емкость буфера объекта.
* `void setLength(int newLength)`	`Изменяет размер содержимого в большую/меньшую сторону:
 если новый размер больше хранящейся строки – строка будет дополнена пробелами в конце
если новый размер меньше – строка будет усечена.`
* `StringBuilder append(….)`	Добавляет подстроку (символы, значения базовых типов, массивы и строки) в конец StringBuffer/StringBuilder.
* `StringBuilder insert(….)`	Вставляет подстроку (символы, значения базовых типов, массивы и строки) в указанную позицию.
* `char charAt(int index)`	Возвращает символ с указанным индексом.
* `StringBuilder delete(int start, int end)`	Удаляет подстроку, указанную позициями.
* `StringBuilder deleteCharAt(int index)`	Удаляет символ по указанному индексу.
* `StringBuilder replace(int start, int end, String str)`	Заменяет подстроку между определенными позициями в StringBuffer на другую подстроку.
* `String substring(int start)`
* `String substring(int start, int end)`	Обрезает строку с определенного индекса до конца либо до определенного индекса, и возвращает в виде новой строки.
* `StringBuilder reverse()`	Переворачивает строку символов.

Также следует отметить, что в Java 8 был добавлен класс StringJoiner. Основное его назначение – объединение нескольких строк в одну с заданием разделителя, префикса и суффикса. У класса два конструктора:
* StringJoiner(CharSequence delimiter, CharSequence prefix, CharSequence suffix)
* StringJoiner(CharSequence delimiter).

```
StringJoiner joiner = new StringJoiner(":", "<<", ">>");
String result = joiner.add("blanc").add("rouge").add("blanc").toString();
System.out.println(result);

Вывод в консоли:
<<blanc:rouge:blanc>>
```

[java.util.regex](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/package-summary.html)  – пакет стандартной библиотеки Java, содержащий основные классы для работы с регулярными выражениями
