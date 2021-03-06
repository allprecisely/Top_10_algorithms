# Бинарный поиск
*Двоичный поиск / Метод дихотомии / Метод деления пополам (binary search)*
*https://www.geeksforgeeks.org/binary-search/*

Задача: написать функцию, принимающую на вход отсортированный массив и элемент, который необходимо найти.
На выходе ожидается получить индекс первого совпадения с искомым элементом в данном массиве или -1 в случае его отсутствия.

Алгоритм:
1. Определение значения элемента в середине структуры данных. Полученное значение сравнивается с ключом.
2. Если ключ меньше значения середины, то поиск осуществляется в первой половине элементов, иначе — во второй.
3. Поиск сводится к тому, что вновь определяется значение серединного элемента в выбранной половине и сравнивается с ключом.
4. Процесс продолжается до тех пор, пока не будет найден элемент со значением ключа или не станет пустым интервал для поиска.

![alt text](https://www.geeksforgeeks.org/wp-content/uploads/Binary-Search.png)

Преимущества данного алгоритма: сложность О(log n), в то время как сложность линейного поиска О(n).
