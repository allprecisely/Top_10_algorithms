# Задача Левенштейна (Edit Distance)

https://www.geeksforgeeks.org/edit-distance-dp-5/

Даны две строки `str1` и `str2`, и спосок операций, которые можно применять над строкой str1, чтобы превратить ее в str2. Нужно найти минимальное количество операций, необходимых для конвертации `str1`  -> `str2`.

**Доступные операции:**
 - Вставка одного символа, и замены одного символа на другой
 - Удаление одного символа
 - Замена одного символа на другой
 
Все операции имеют одинаковую стоимость = 1.

**Примеры**

 ```
Дано:   str1 = "geek", str2 = "gesek"
Результат:  1
Результат достигается вставкой символа 's' в str1.

Дано:   str1 = "cat", str2 = "cut"
Результат:  1
Результат достигается заменой символа 'a' на 'u'.

Дано:   str1 = "sunday", str2 = "saturday"
Результат:  3
Последние первые буквы одинаковы.  Все, что нам нужно, это
преобразовать "un" в "atur". Для этого нужно 3 операции. 
Замена 'n' на 'r', вставка t, вставка a
```

**Выделяем подпроблему**

Идея состоит в том, чтобы обрабатывать все символы один за другим, начиная с левой или правой стороны обеих строк.
Мы пройдем через правый угол, есть две возможности для каждой пары пройденных строк.

m: длина str1 (первая строка)
n: длина str2 (вторая строка)

Если последние символы двух строк одинаковы, делать нечего. Проигнорируем последние символы и получим количество оставшихся строк. Далее мы повторяем алгоритм для длин m-1 и n-1.
Иначе (если последние символы не совпадают), мы рассмотрим все операции над «str1», рассмотрим все три операции над последним символом первой строки, рекурсивно вычисляем минимальную стоимость для всех трех операций и принимаем минимум от трех значений.
 - Вставить: повтор для m и n-1
 - Удалить: повтор для m-1 и n
 - Заменить: повтор для m-1 и n-1
 
Ниже приведена реализация Python вышеупомянутого рекурсивного решения.

```
# Решение полным перебором, m - длина первой строки, n - длина второй строки
def editDistance(str1, str2, m , n): 
  
    # Если первая строка пустая, нужно добавить в нее все символы из второй строки
    if m==0: 
         return n 
  
    # Если вторая строка пустая, нужно удалить из первой все символы
    if n==0: 
        return m 
  
    # Если последние символы одинаковые, ничего не делаем
    # Просто запускаем алгоритм работать без учета последних букв. 
    if str1[m-1]==str2[n-1]: 
        return editDistance(str1,str2,m-1,n-1) 
  
    # Если они не одинаковы, считаем все три операции для последнего символа 
    # рекурсивно вычисляя все стоимости и выбирая наименьшее из них
    return 1 + min(editDistance(str1, str2, m, n-1),    # Вставка 
                   editDistance(str1, str2, m-1, n),    # Удаление 
                   editDistance(str1, str2, m-1, n-1)    # Замена 
                   ) 
```

Временная сложность вышеуказанного решения является экспоненциальной. В худшем случае мы можем выполнить O (3<sup>m</sup>) операций. Худший случай случается, когда ни один из символов двух строк не совпадает. Ниже приведена рекурсивная диаграмма вызовов для наихудшего случая.

![иллюстрация иллюстрация](https://www.geeksforgeeks.org/wp-content/uploads/EditDistance.png)

Мы видим, что многие подзадачи решаются снова и снова, например, `eD (2,2)` вызывается три раза. Поскольку те же самые подзадачи вызываются снова, эта проблема имеет свойство Перекрывающиеся подзадачи. Таким образом, проблема редактирования расстояния имеет оба свойства задачи динамического программирования. Как и другие типичные проблемы динамического программирования (DP), повторных вычислений с одинаковыми подзадачами можно избежать, создав временный массив, в котором хранятся результаты подзадач.

**Сложность времени:** O (m x n)
**Вспомогательная память:** O (m x n)

**Приложения:** Есть много практических применений алгоритма Левенштейна. Один из примеров: отобразить все слова в словаре, которые находятся рядом с заданным неправильно написанным словом.
