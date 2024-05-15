# Исследование Алгоритмов Сортировки
В данной работе будет разобрано несколько популярных алгоритмов сортировки массивов целых чисел и произведено сравнение скорости сортировки различных алгоритмов в зависимости от размера сортируемого массива.

## Содержание
- [Вступление](#вступление)
- [Гипотеза](#гипотеза)
- [Bubble Sort](#bubble-sort)
- [Merge Sort](#merge-sort)
- [Insertion sort](#insertion-sort)
- [Timsort](#timsort)
- [Gnome Sort](#gnome-sort)
- [Counting Sort](#counting-sort)
- [Radix Sort LSD](#radix-sort-lsd)
- [Heap Sort](#heap-sort)
- [Selection Sort](#selection-sort)
- [Cycle Sort](#cycle-sort)
- [Shell Sort](#shell-sort)
- [Эксперимент cравнение эффективности алгоритмов на разных компиляторах](#эксперимент-сравнение-эффективности-алгоритмов-на-разных-компиляторах)
- [Источники](#источники)


## <a id ="вступление">Вступление</a>
Сортировочные алгоритмы занимают особое место в истории и развитии информатики. Их цель заключается в упорядочении элементов массива или списка в определённой последовательности, например, по возрастанию или убыванию.  

В настоящее время существует множество различных сортировочных алгоритмов, каждый из которых имеет свои преимущества и недостатки в зависимости от конкретной задачи. Выбор подходящего алгоритма зависит от многих факторов, таких как объём данных, требуемая вычислительная сложность, доступность памяти и другие особенности конкретной задачи.

Вычислительная сложность — понятие в информатике и теории ал-горитмов, обозначающее  функцию зависимости  времени работы алго-ритма от размера входных данных. Для описания такой функции исполь-зуют заглавную букву «О». Сама функция может быть, например, линей-ной O(N), квадратичной O(N2), логарифмической O(log N), где N размер массива. Следует отметить, что оценка вычислительной сложности явля-ется асимптотическим показателем и используется при устремлении раз-мера сортируемого массива к бесконечности. Она позволяет предсказать время  выполнения  и  сравнивать эффективность  различных  алгоритмов друг с другом. При реальных объемах данных, эта оценка не может слу-жить для точных расчетов.  Многие алгоритмы предлагают выбор между объёмом памяти и ско-ростью. Задачу можно решить быстро, используя большой объём памяти, или медленнее, занимая меньший. При сравнении различных алгоритмов важно знать, как зависит объем затраченных ресурсов (объем  памяти  и время выполнения) от количества входных данных. Допустим,  при сор-тировке одним  методом  обработка десяти  тысячи  чисел занимает  1  секунду, а обработка миллиона чисел – 10 секунд, при использовании дру-гого алгоритма  может потребоваться две и пять секунд соответственно. В таких условиях нельзя однозначно сказать, какой алгоритм лучше, так как каждое  вычислительное  устройство  имеет  свои  особенности,  кото-рые могут влиять на длительность вычисления. Обычно при разработке алгоритма не берутся во внимание некоторые технические детали, такие как размер кэша процессора, тип многозадачности, реализуемый опера-ционной системой и др.

Анализ алгоритмов проводят на абстрактной модели, называемой ма-шиной  с  произвольным  доступом  к  памяти  (RAM). Модель  состоит из памяти и процессора, которые работают следующим образом: 
1. Память состоит из ячеек, каждая из которых имеет адрес и может хранить один элемент данных.
2. Каждое  обращение  к  памяти  занимает  одну  единицу  времени, независимо от номера адресуемой ячейки.
3. Количество  памяти  достаточно  для  выполнения  любого  алгоритма.
4. Процессор выполняет любую элементарную операцию (например, основные логические и арифметические операции, чтение из памяти, запись в память, вызов подпрограммы и т.п.) за один временной шаг.
5. Циклы и функции не считаются элементарными операциями. Такая модель  далека от реального компьютера, но она  замечательно подходит для анализа временной сложности алгоритмов.

Основные классы алгоритмов повышения на алгоритмах повторения и рекурсивные алгоритмы. В основе алгоритмов повторения операторов цикла и условных операторов. Анализ алгоритмов такого класса требует подсчета всех циклов и операций внутри них.

Рекурсивные алгоритмы строятся на основе математической рекурсивной функции. В языках программирования рекурсивной понижения называется программа-функция, которая обращается сама к себе. Рекурсивная программа не может продолжать себя бесконечно, поэтому второй важный момент обеспечивает рекурсивную программу - условия доступности, позволяющие выполнить программу остановки себя. Анализ рекурсивного алгоритма, как правило, сложнее. Он требует подсчета операций вызова рекурсивной функции, чтобы условия выполнения содержали рекурсию и подсчет операций внутри каждой вызванной рекурсивной функции.


В дальнейшем работе мы рассмотрим наиболее популярные и эффективные сортировочные алгоритмы, изучим их принципы работы, а также сравним их производительность и скорость работы.

---
# Гипотеза

Скорость выполнения алгоритмов сортировки может значительно варьироваться в зависимости от используемого компилятора, поскольку различные компиляторы могут оптимизировать код по-разному. Это связано с тем, что компиляторы используют различные стратегии для преобразования исходного кода программы в машинный код, включая оптимизацию производительности, минимизацию использования памяти и другие аспекты. В результате, один и тот же алгоритм сортировки может выполняться быстрее или медленнее на разных компиляторах из-за различий в их способах генерации машинного кода. Кроме того, некоторые компиляторы могут предлагать специализированные инструкции процессора или использовать более эффективные структуры данных, что также влияет на скорость выполнения алгоритма. Таким образом, выбор компилятора может оказывать значительное влияние на производительность алгоритмов сортировки.

## Bubble Sort
Bubble sort (также известен как сортировка пузырьком или сортировка с понижением) — это простой алгоритм сортировки, который работает путём повторяющихся проходов по массиву. На каждом проходе алгоритм сравнивает пары соседних элементов и меняет их местами, если они находятся в неправильном порядке. В результате каждого прохождения самое большое не отсортированное число будет становится на свое место так как при каждом сравнении алгоритм будет менять его местами со всеми остальными элементами неотсортировннаой части массива. Этот процесс продолжается до тех пор, пока массив не будет отсортирован. Алгоритм сортировки сравнения назван в честь того, как более крупные элементы «всплывают» вверх списка.

### Реализация на языке с++
```c++
 void bubbleSort(vector<int>& array){ 
  for (int i = 0; i < array.size(); i++){
    bool swapped = false;
    for ( int j = 0; j < array.size() — i — 1; j++){
      if (array[j] > array[j + 1] ){
        swap(array[j], array[j + 1]);
        swapped = true;
      }
    }
    if(!swapped){break;}
  }
}
```
Функция работает следующим образом: так как в конце каждого прохода как минимум один элемент(наибольший из неотсортированных) встает на свое место, нам может потребоваться максимум n прохождений(первый цикл) по неотсортированной части массива(второй цикл, где -i отсортированная к этому моменту часть). При этом переменная swapped отвечает за проверку отсортированности массива. Если прохождение по массиву обошлось без перестановок - значит массив уже отсортирован и продолжать обход не имеет смысла. Оставшееся условие - это то самое сравнение двух соседних элементов и их перестановка в случае не соответствия порядка(в нашем случае порядка возрастания)

### Анализ сложности и памяти
Дополнительная память не требуется, наибольшая ее затрата - это выделение буфера для перестановки двух элементов. 

Расстояние и направление, в котором элементы должны двигаться во время сортировки, определяют производительность пузырьковой сортировки, поскольку элементы движутся в разных направлениях с разной скоростью. Элемент, который должен переместиться в конец списка, может перемещаться быстро, поскольку он может участвовать в последовательных заменах. Например, самый большой элемент в списке выиграет каждую замену, поэтому он переместится на отсортированную позицию при первом проходе, даже если он начинается ближе к началу. С другой стороны, элемент, который должен двигаться к началу списка, не может двигаться быстрее, чем на один шаг за проход, поэтому элементы движутся к началу очень медленно. Если наименьший элемент находится в конце списка, потребуется n - 1 шагов, чтобы переместить его в начало.

Исходя из этого худший случай - это убывающий массив. Тогда сложность: O((n-1) + (n-2) + ... + 1) = O(n^2). Лучший - возрастающий массив. В этом случае осознания бессмысленности происходящего придет ровно через n шагов и сложность соответственно будет О(n).

В среднем мы имеем (n-1) + (n-2) + ... + ... = n(n-1)/2. Отсюда средняя сложность также О(n)

![sorting bobble](https://github.com/GorshkovIoann/sorting_algorithms/blob/main/Figurebubblesort.png)

---

## Merge Sort

Merge sort (Сортировка слиянием)  — алгоритм сортировки, который упорядочивает списки (или другие структуры данных, доступ к элементам которых можно получать только последовательно, например — потоки) в определённом порядке.

При сортировке сначала массив разбивается на несколько подмассивов меньшего размера. Затем эти подмассивы сортируются с помощью рекурсивного вызова или непосредственно, если их размер достаточно мал(обычно размер будет равен единице). Наконец, их решения комбинируются, и получается решение исходной задачи.
### Реализация на языке с++
```c++
using namespace std;

//функция слияния двух подмассивов в массив.
// первый подмассив arr[begin..mid]
// второй подмассив arr[mid+1..end]
void merge(int array[], int const left, int const mid, int const right)
{
    int const subArrayOne = mid - left + 1;
    int const subArrayTwo = right - mid;

    // создание временных массивов
    auto *leftArray = new int[subArrayOne],
         *rightArray = new int[subArrayTwo];

    // заполняем первой половиной исходного массива первый временный массив
    // второй половиной второй временный массив
    for (auto i = 0; i < subArrayOne; i++)
        leftArray[i] = array[left + i];
    for (auto j = 0; j < subArrayTwo; j++)
        rightArray[j] = array[mid + 1 + j];

    auto indexOfSubArrayOne = 0, indexOfSubArrayTwo = 0;
    int indexOfMergedArray = left;

    // сливаем два массива обратно в array[left..right]
    // с помощьюдвух указателей бегущих от начала временных массивов
    // и заполняющих array наимаеньшим из двух элементов
    // при этом передвигая указатель на этот элемент на +1
    while (indexOfSubArrayOne < subArrayOne
           && indexOfSubArrayTwo < subArrayTwo) {
        if (leftArray[indexOfSubArrayOne]
            <= rightArray[indexOfSubArrayTwo]) {
            array[indexOfMergedArray]
                = leftArray[indexOfSubArrayOne];
            indexOfSubArrayOne++;
        }
        else {
            array[indexOfMergedArray]
                = rightArray[indexOfSubArrayTwo];
            indexOfSubArrayTwo++;
        }
        indexOfMergedArray++;
    }

    // Копируем оставшиеся элементы 
    // leftArray[], ecли они есть
    while (indexOfSubArrayOne < subArrayOne) {
        array[indexOfMergedArray]
            = leftArray[indexOfSubArrayOne];
        indexOfSubArrayOne++;
        indexOfMergedArray++;
    }

    // Копируем оставшиеся элементы 
    // rightArray[], ecли они есть
    while (indexOfSubArrayTwo < subArrayTwo) {
        array[indexOfMergedArray]
            = rightArray[indexOfSubArrayTwo];
        indexOfSubArrayTwo++;
        indexOfMergedArray++;
    }
    delete[] leftArray;
    delete[] rightArray;
}

// begin - индекс первого элемента, end - индекс последнего
void mergeSort(int array[], int const begin, int const end)
{
    if (begin >= end)
        return;

    int mid = begin + (end - begin) / 2;
    mergeSort(array, begin, mid);
    mergeSort(array, mid + 1, end);
    merge(array, begin, mid, end);
}
```


1. Массив рекурсивно разбивается пополам, и каждая из половин делится пополам до тех пор, пока размер подмассива не станет равным единице.
2. Выполняется операция алгоритма, называемая слиянием. Два подмассива сливаются в общий результирующий массив, при этом  из  каждого выбирается меньший элемент (сортировка по возрастанию) и записывается  в  свободную  левую  ячейку результирующего  массива(Действительно, таким образом можно превратить два отсортированных массива в 1 отсортированный, так как на каждом шаге в результирующий массив будет записываться наименьший из еще не записанных элементов). В случае если один из массивов закончится, элементы другого записываются в массив, где они собираются.
3. Элементы  перезаписываются  из результирующего  массива  в  исходный. 

### Анализ сложности и памяти
Память: для создания двух временных подмассивов длинной n/2 на каждом шаге нам потребуется ровно n ячеек памяти и так как сортировка происходит не на месте нам также нужна дополнительная память на копию массива или другими словами merge sort требует O(n) памяти.

Оценим сложность: Пусть Т(n) - время сортировки массива длины n. Тогда Т(n) = 2T(n/2) + время выполнения п.2. Время выполнения п.2 равно времени за которое два указателя пройдут массивы длинной n/2 = O(n). Тогда T(n) = 2T(n/2) + O(n) = logn * T(1) + logn * O(n) = O(nlogn). 
То есть вне зависимости от изначального состояния массива его сортировка занимает O(nlogn) времени.

![](https://github.com/GorshkovIoann/sorting_algorithms/blob/main/merge_sort.png)

---

## Insertion Sort

Insertion sort(сортировка вставками) - один из первых устойчивых видов сортировки. Идея заключается в следующем: есть часть массива, которая уже отсортирована, и требуется вставить остальные элементы массива в отсортированную часть, сохранив при этом упорядоченность. Для этого на каждом шаге алгоритма мы выбираем один из элементов входных данных и вставляем его на нужную позицию в уже отсортированной части массива, до тех пор пока весь набор входных данных не будет отсортирован. Метод выбора очередного элемента из исходного массива произволен, однако обычно (и с целью получения устойчивого алгоритма сортировки), элементы вставляются по порядку их появления во входном массиве.

### Реализация на языке с++

```c++
using namespace std;

//функция сортировки вставками
void insertionSort(int arr[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        // двигаем элементы arr[0..i-1],
        // которые больше чем key, 
        // на одну позицию вперед
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        //вставляем key позади больших его элементов
        arr[j + 1] = key;
    }
}

```

- Нам нужно начать со второго элемента массива, поскольку предполагается, что первый элемент массива отсортирован.
- Сравните второй элемент с первым элементом и проверьте, меньше ли второй элемент, а затем поменяйте их местами.
- Перейдите к третьему элементу и сравните его со вторым элементом, затем с первым элементом и поменяйте местами, если необходимо, чтобы поместить его в правильное положение среди первых трех элементов.
- Продолжайте этот процесс, сравнивая каждый элемент с предыдущими и меняя их местами по мере необходимости, чтобы разместить его в правильном положении среди отсортированных элементов.
- Повторяйте, пока весь массив не будет отсортирован.

### Анализ сложности и памяти

Память: необходимо создать лишь 3 буферные переменные => паямть = О(1).

Оценим сложность: Так как в процессе работы алгоритма могут меняться местами только соседние элементы, каждый обмен уменьшает число инверсий на единицу. Следовательно, количество обменов равно количеству инверсий в исходном массиве вне зависимости от реализации сортировки. Максимальное количество инверсий содержится в массиве, элементы которого отсортированы по невозрастанию. Число инверсий в таком массиве = n(n-1)/2
Получается алгоритм работает за О(n + k),  где k - число инверсий, то есть за 
О(n+n^2) = O(n^2), так как число инверсий можно ограничить n^2.

---


## Timsort

Timsort — гибридный алгоритм сортировки, сочетающий различные подходы.

Данный алгоритм является относительно новым и был придуман Тимом Петерсом в 2002 году. На массивах данных, которые содержат упорядоченные подмассивы, алгоритм Тима Петерса показывает себя намного лучше других сортировок. В настоящее время Timsort является стандартной сортировкой в Python и GNU Octave.

Основная идея Tim Sort — использовать существующий порядок данных для минимизации количества сравнений и замен. Это достигается путем разделения массива на небольшие подмассивы, называемые сериями, которые уже отсортированы, а затем объединения этих серий с использованием модифицированного алгоритма сортировки слиянием.

### Реализация на языке с++

```c++
//Tim Sort. 
using namespace std; 
const int RUN = 32; 
  
// Эта функция сортирует вставкой 
//массив 
//начиная с левого индекса до правого
//находящегося на расстоянии не больше //RUN
void insertionSort(int arr[], int left, int right) 
{ 
    for (int i = left + 1; i <= right; i++) { 
        int temp = arr[i]; 
        int j = i - 1; 
        while (j >= left && arr[j] > temp) { 
            arr[j + 1] = arr[j]; 
            j--; 
        } 
        arr[j + 1] = temp; 
    } 
} 
  
// Merge функция сортирует подмассивы RUN 
void merge(int arr[], int l, int m, int r) 
{ 
  
    // изначальный массив разделяется      //на два 
    //левый и правый 
    int len1 = m - l + 1, len2 = r - m; 
    int left[len1], right[len2]; 
    for (int i = 0; i < len1; i++) 
        left[i] = arr[l + i]; 
    for (int i = 0; i < len2; i++) 
        right[i] = arr[m + 1 + i]; 
  
    int i = 0; 
    int j = 0; 
    int k = l; 
  
    // после сравнения мы  
    // сливаем их обратно
    // точно как в merge sort
    while (i < len1 && j < len2) { 
        if (left[i] <= right[j]) { 
            arr[k] = left[i]; 
            i++; 
        } 
        else { 
            arr[k] = right[j]; 
            j++; 
        } 
        k++; 
    } 
  
    // аналогично merge sort 
    while (i < len1) { 
        arr[k] = left[i]; 
        k++; 
        i++; 
    } 
  
    // аналогично merge sort
    while (j < len2) { 
        arr[k] = right[j]; 
        k++; 
        j++; 
    } 
} 
  
// тимсорт для сортировки массива 
// array[0...n-1] (похоже на merge sort) 
void timSort(int arr[], int n) 
{ 
  
    // cортировка подмассивов длинны RUN вставками 
    for (int i = 0; i < n; i += RUN) 
        insertionSort(arr, i, min((i + RUN - 1), (n - 1))); 
  
    // начинаем слияние массивов размера RUN (в нашем случае 32). 
    // то есть сначала массивы длины 64 
    // затем 128, 256 
    // и т.д. .... 
    for (int size = RUN; size < n; size = 2 * size) { 
  
        // выбираем стартовую точку 
        // девого подмассива. Мы 
        // Будем сливать массивы вида
        // arr[left..left+size-1] 
        // и arr[left+size, left+2*size-1] 
        // после слияния всех таких массивов 
        // увеличим left на 2*size 
        for (int left = 0; left < n; left += 2 * size) { 
  
            // Находим конечную точку
            // левого подмассива
            // mid+1 — начальная точка
            // правого подмассива
            int mid = left + size - 1; 
            int right = min((left + 2 * size - 1), (n - 1)); 
  
            //обьединяем подмассив arr[left.....mid] & 
            // arr[mid+1....right] 
            if (mid < right) 
                merge(arr, left, mid, right); 
        } 
    } 
} 
``` 
Замечу что число run определяется на основе n, исходя из следующих принципов:
- Не должно быть слишком большим, поскольку к подмассиву размера minrun
 будет в дальнейшем применена сортировка вставками (эффективна только на небольших массивах).
- Оно не должно быть слишком маленьким, так как чем меньше подмассив, тем больше итераций слияния подмассивов придётся выполнить на последнем шаге алгоритма. Оптимальная величина для n/run — степень двойки. Это требование обусловлено тем, что алгоритм слияния подмассивов наиболее эффективно работает на подмассивах примерно равного размера.
- Автором алгоритма было выбрано оптимальное значение, которое принадлежит диапазону [32;65).
- если n<64, тогда n=minrun и Timsort превращается в сортировку вставками.

Как итог, мы просто сначала сортируем небольшие подмасссивы с помощью Вставок, а затем сливаем получившиеся отсортированные массивы как в merge sort.

### Анализ сложности и памяти
Память:  так как мы используем merge sort и вставки наши затраты на память в любом случае = O(n)+O(1) = O(n)

Aнализ сложности: Не сложно заметить, что чем меньше массивов, тем меньше произойдёт операций слияния, но чем их длины больше, тем дольше эти слияния будут происходить.
Тогда пусть k — число кусков, на которые разбился наш исходный массив, очевидно k
 = n/RUN. Заметим также, что подмассивы, на которые делится исходный массив обладают одинаковой длинной(за исключением быть может последнего).
Мы выяснили, что при слиянии, длинна образовавшегося слитого массива увеличивается в ≈2 раза. Таким образом получаем, что каждый подмассив RUN может участвовать в не более O(logn) операций слияния, а значит и каждый элемент будет задействован в сравниниях не более O(logn) раз. Элементов n, откуда получаем оценку в O(nlogn).

Также нужно сказать про сортировку вставками, которая используется для сортировки подмассивов RUN: в нашем случае, алгоритм работает за O(RUN+inv), где inv
 — число обменов элементов входного массива, равное числу инверсий. C учетом значения k получим, что сортировка всех блоков может занять O(RUN+inv)⋅k=O(RUN+inv)⋅n/RUN . Что в худшем случае (inv=RUN(RUN−1)/2)
может занимать O(n⋅RUN) времени. Откуда видно, что константа RUN играет немалое значение: при большом RUN слияний будет меньше, а сортировки вставками будут выполняться долго. Причём эти функции растут с разной скоростью, поэтому и ещё после экспериментов на различных значениях и был выбран оптимальный диапазон — от 32 до 64.

![](https://github.com/GorshkovIoann/sorting_algorithms/blob/main/timsort.png)

---

## Gnome Sort
Сортировка гномов, также называемая глупой сортировкой, основана на концепции садового гнома, сортирующего свои цветочные горшки. Садовый гном сортирует цветочные горшки следующим методом:  

- Он смотрит на цветочный горшок рядом с ним и на предыдущий; если они расположены в правильном порядке, он делает шаг на один горшок вперед, в противном случае он меняет их местами и делает шаг назад на один горшок.
- Если предыдущего горшка нет (он находится в начале линии горшка), он делает шаг вперед; если рядом с ним нет горшка (он находится в конце линии горшков), он готов.

### Реализация на языке с++
```c++
//Gnome sort
#include <iostream> 
using namespace std; 
  
// функция гномьей сортировки 
void gnomeSort(vector<int> &vec)
{
    int index = 0;
    //гном делает шаги пока сзади не больше
    //тогда он меняет местами текущий(n) и  n-1 горшок
    while (index < vec.size())
    {
        if (index == 0 || vec[index] >= vec[index - 1])
        {
            index++;
        }
        else
        {
            swap(vec[index], vec[index - 1]);
            index--;
        }
    }
}
```
### Анализ сложности и памяти
Память: Алгоритм сортирует на месте и не требует доп памяти=> O(1)

Анализ сложности: лучший случай О(n) - отсортированный массив. Худший - O(n^2) - убывающий массив.(в этом случае гном будет для каждого элемента совершать 2к движений, где к - индекс элемента)

---

## Counting Sort
Сортировка подсчётом (англ. counting sort) — алгоритм сортировки целых чисел в диапазоне от 0 до некоторой константы k.
Исходная последовательность чисел длины n хранится в массиве A. Также используется вспомогательный массив C с индексами от 0 до k−1, изначально заполняемый нулями.
Алгоритм сортировки:
- Последовательно пройдём по массиву Aи запишем в C[i]количество чисел, равных i.
- Теперь достаточно пройти по массиву Cи для каждого number∈{0,...,k−1} в массив A
 последовательно записать число number C[number] раз.

### Реализация на языке с++
```c++
#include <algorithm>
using namespace std;

void countSort(int inputArray[], int n)
{

    // находим наибольший элемент inputArray[].
    int M = 0;

    for (int i = 0; i < n; i++)
        M = max(M, inputArray[i]);

    // инициализируем вектор countArray[] нулями
    int *countArray = new int[M + 1];
    std::fill_n(countArray, 10, 0);

    // Сопоставим каждый элемент inputArray[] как индекс
    // массива countArray[]

    for (int i = 0; i < n; i++)
        countArray[inputArray[i]]++;
    // записываем в массив числа от меньшего к большему
    // столько раз сколько они встречались в изначальном массиве
    int pos = 0;
    for (int number = 0; number <= 9; number++)
    {
        for (int i = 0; i < countArray[number] - 1; i++)
        {
            inputArray[pos] = number;
            pos = pos + 1;
        }
    }
}
```
### Анализ сложности и памяти

Память: нам нужен массив длинны к(макс число) - скорее всего в силу использования этого алгоритма это число не велико и может считаться константой. То есть О(к).

Анализ сложности: поиск наибольшего числа - n операций. Распределение чисел по массиву подсчета - еще n операций. заполнение итогового массива максимум за n*k операций => O(n).

---

## Radix Sort LSD

Цифровая сортировка (англ. radix sort) — один из алгоритмов сортировки, использующих внутреннюю структуру сортируемых объектов( в данном случае отношения линейного порядка). Алгоритм состоит в последовательной сортировке объектов какой-либо устойчивой сортировкой по каждому разряду, в порядке от младшего разряда к старшему, после чего последовательности будут расположены в требуемом порядке.(для чисел чаще всего сортировкой подсчетом)
LSD-сортировкой (Least Significant Digit radix sort)- начинает сортировку с правых разрядов.

## Корректность алгоритма LSD-сортировки:
Докажем, что данный алгоритм работает верно, используя метод математической индукции по номеру разряда. 
- Пусть n — количество разрядов в сортируемых объектах.
- База: n=1. Очевидно, что алгоритм работает верно, потому что в таком случае мы просто сортируем младшие разряды какой-то заранее выбранной устойчивой сортировкой.
- Переход: Пусть для n=k алгоритм правильно отсортировал последовательности по k младшим разрядам. Покажем, что в таком случае, при сортировке по (k+1) разряду, последовательности также будут отсортированы в правильном порядке.
- Вспомогательная сортировка разобьет все объекты на группы, в которых (k+1) разряд объектов одинаковый.
- Рассмотрим такие группы. Для сортировки по отдельным разрядам мы используем устойчивую сортировку, следовательно порядок объектов с одинаковым (k+1) разрядом не изменился. Но по предположению индукции по предыдущим k разрядам последовательности были отсортированы правильно, и поэтому в каждой такой группе они будут отсортированы верно. Также верно, что сами группы находятся в правильном относительно друг друга порядке, а, следовательно, и все объекты отсортированы правильно по (k+1) младшим разрядам.
- что и требовалось доказать.

### Реализация на языке с++
```c++
//вспомогательная функция находит заданный разряд числа
int digit(int number, int position) {
    int count = 0;
    //сдвигаем число вправо на количество разрядов
    while (number != 0) {
        if (count == position) {
            //возвращаем нужный разряд обрезая все слева
            return number % 10;
        }
        number /= 10;
        count++;
    }
    return 0; // если разряда нет
}
//radix sort функция, m - мах колво разрядов числа в массиве А
// n - длинна массива
void radixSort(int A[], int m, int n){
     //вспомогательный массив B который будет заполняться как в counting sort
     int* B = new int[n];
     //для каждого разряда начиная с правого
     for(int i = 1; i < m; i++){
          //создаем вспомогательный массив для хранения количества тех или иных разрядов
          int C[10] = {0,0,0,0,0,0,0,0,0,0};
         //реализуем counting sort для i разряда чисел                               
         for(int j = 0; j < n - 1; j++){
             int d = digit(A[j], i);
             C[d]++;
         }
         //заполняем В аналогично counting sort
         int count = 0;
         for(int j = 0 ; j <= 9;j++){
             int tmp = C[j];
             C[j] = count;
             count += tmp;
         }
         for(int j = 0; j < n - 1; j++){
            int  d = digit(A[j], i);                             
             B[C[d]] = A[j];            
             C[d]++;
         }
         A = B;
     }
}
```
### Анализ сложности и памяти
Аналогично сортировке вставками имеем О(1) памяти

Анализ сложности: мы m раз вызываем сортировку подсчетом(О(n)). Если колличество разрядов числа мало m-сonst. Имеем общую сложность О(n)

![](https://github.com/GorshkovIoann/sorting_algorithms/blob/main/lsd.png)

---

## Heap Sort

Сортировка пирамидой — это метод сортировки на основе сравнения, основанный на структуре данных двоичной кучи . Это похоже на сортировку выбором , при которой мы сначала находим минимальный элемент и помещаем минимальный элемент в начало. Повторите тот же процесс для остальных элементов.
Алгоритм работы: пусть необходимо отсортировать массив A, размером n. 
- Построим на базе этого массива за O(n) кучу для максимума.
- Так как максимальный элемент находится в корне, то если поменять его местами с A[n−1], он встанет на своё место.
- Далее вызовем процедуру siftDown(0), предварительно уменьшив heapSizeна 1. Она за O(logn) просеет A[0] на нужное место и сформирует новую кучу (так как мы уменьшили её размер, то куча располагается с A[0]по A[n−2], а элемент A[n−1]
находится на своём месте).
- Повторим эту процедуру для новой кучи, только корень будет менять местами не с A[n−1], а с A[n−2].
- Делая аналогичные действия, пока heapSize не станет равен 1, мы будем ставить наибольшее из оставшихся чисел в конец не отсортированной части. Очевидно, что таким образом, мы получим отсортированный массив.

Двоичная куча — это законченное двоичное дерево, в котором элементы хранятся в особом порядке: значение в родительском узле больше (или меньше) значений в его двух дочерних узлах. Первый вариант называется max-heap, а второй — min-heap. Куча может быть представлена двоичным деревом или массивом.

Законченное двоичное дерево — это двоичное дерево, в котором каждый уровень, за исключением, возможно, последнего, имеет полный набор узлов, и все листья расположены как можно левее.


### Реализация на языке с++
```c++

// Реализация пирамидальной сортировки на C++
#include <iostream>

using namespace std;

// Процедура для преобразования в двоичную кучу поддерева с корневым узлом i, что является
// индексом в arr[]. n - размер кучи

void heapify(int arr[], int n, int i)
{
    int largest = i;   
// Инициализируем наибольший элемент как корень
    int l = 2*i + 1; // левый = 2*i + 1
    int r = 2*i + 2; // правый = 2*i + 2

 // Если левый дочерний элемент больше корня
    if (l < n && arr[l] > arr[largest])
        largest = l;

   // Если правый дочерний элемент больше, чем самый большой элемент на данный момент
    if (r < n && arr[r] > arr[largest])
        largest = r;

    // Если самый большой элемент не корень
    if (largest != i)
    {
        swap(arr[i], arr[largest]);

// Рекурсивно преобразуем в двоичную кучу затронутое поддерево
        heapify(arr, n, largest);
    }
}

// Основная функция, выполняющая пирамидальную сортировку
void heapSort(int arr[], int n)
{
  // Построение кучи (перегруппируем массив)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

   // Один за другим извлекаем элементы из кучи
    for (int i=n-1; i>=0; i--)
    {
        // Перемещаем текущий корень в конец
        swap(arr[0], arr[i]);

        // вызываем процедуру heapify на уменьшенной куче
        heapify(arr, i, 0);
    }
}
```

Поскольку двоичная куча — это законченное двоичное дерево, ее можно легко представить в виде массива, а представление на основе массива является эффективным с точки зрения расхода памяти. Если родительский узел хранится в индексе I, левый дочерний элемент может быть вычислен как 2 I + 1, а правый дочерний элемент — как 2 I + 2 (при условии, что индексирование начинается с 0)


### Анализ сложности и памяти

Память: сортировка происходит на месте с изменением данных в самом массиве и пямять нужна лишь на несколько локальных переменных => О(1).

Анализ сложности: heapify - просеивания элемента вниз каждое действие отсеивает половину элементов => работает за О(logn). swap происходит за О(1), а сам цикл выполняется всегда n-1 раз(по очереди переставляя наибольшие элементы кучи в отсартированный конец массива). Сама куча строится также линейно за n/2 вызовов в цикле. Следовательно вся сортировка O(n)+O(n*logn)=O(nlogn).

![](https://github.com/GorshkovIoann/sorting_algorithms/blob/main/heapsort.png)
---

## Selection Sort
- Это простой алгоритм сортировки, который вращается вокруг сравнения
- На каждой итерации помещается один элемент
- Мы выбираем минимальный элемент в массиве и помещаем его в начало массива, меняя местами с начальным элементом
- Мы также можем сделать это, выбрав максимальный элемент и поместив его в конце
- Сортировка по выбору в основном выбирает элемент на каждой итерации и помещает его в соответствующую позицию
### Реализация на языке c++
```c++
#include <iostream>
using namespace std;

void swap(int *a, int *b) {
  int temp = *a;
  *a = *b;
  *b = temp;
}

//selection sort function
void selectionSort(int arr[], int n) {
  for (int j = 0; j < n - 1; j++) {
    int min = j;
    for (int i = j + 1; i < n; i++) {

      if (arr[i] < arr[min])
        min = i;
    }

    swap(&arr[min], &arr[j]);
  }
}
```
### Анализ сложности и памяти

В худшем случае на каждой итерации нам приходится обходить весь массив для поиска минимальных элементов, и это будет продолжаться для всех n элементов. Следовательно, всего будет выполнено n ^ 2 операции.Наилучшая временная сложность: O (n). Средняя временная сложность: O (n ^ 2)

Из плюсов данной сортировки можно выделить то , что В реализации сортировки по выбору не требуется дополнительного пространства, то есть мы не используем никаких массивов, связанных списков, стеков, очередей и т.д. Для хранения наших элементов. Следовательно, сложность пространства равна: O (1)

---

## Cycle Sort

Циклическая сортировка начинается с первой позиции i=0 и находит конечное назначение элемента по адресу i. Затем она меняется местами  i с пунктом назначения элемента, затем находит пункт назначения нового элемента по адресу i и повторяется. Если в какой-либо точке находится пункт назначения i, циклическая сортировка увеличивается i вместо замены. Эти процессы повторяются до тех пор, пока не будет достигнут конец списка.

### Реализация на языке с++
```c++
public static void cycle_sort(int[] array) {
    int n = array.length;
    
	for(int i = 0; i < n-1; i++) {
		int temp = array[i];
		int dest = i;
		
		for(int j = i+1; j < n; j++) //find destination by counting lesser
		    if(array[j] < temp) dest++;
		
		if(dest != i) {
			do {
				while(array[dest] == temp) dest++; //handle equal elements
				
				int temp1 = array[dest];
				array[dest] = temp;
				temp = temp1;
				
				dest = i;
		
        		for(int j = i+1; j < n; j++) //find destination by counting lesser
        		    if(array[j] < temp) dest++;
			}
			while(dest != i);
			
			array[i] = temp;
		}
	}
}
```
### Анализ сложности и памяти
Поскольку каждый элемент перемещается в конечный пункт назначения, они меняются местами не более одного раза и больше никогда не перемещаются, поэтому циклическая сортировка совершает O(n) перемещения. В простейшей версии циклическая сортировка обычно реализуется в O(n^2) сравнениях и  O(1) пространстве. Чтобы найти пункт назначения элемента, циклическая сортировка выполняет итерации по списку, подсчитывая количество элементов, меньшее, чем элемент. Для этого требуются O(n) сравнения для O(n) элементов, поэтому используется циклическая сортировка O(n^2).


---

## Shell Sort
Shell sort а в основном является разновидностью Insertion sort. При сортировке по вставке мы перемещаем элементы только на одну позицию вперед. Когда элемент нужно переместить далеко вперед, задействовано много движений. Идея ShellSort в том, чтобы разрешить обмен удаленными элементами. В Shell sort мы сортируем массив h по большому значению h . Мы продолжаем уменьшать значение h, пока оно не станет равным 1. Массив называется h-отсортированным, если отсортированы все подсписки каждого h-го элемента.

Алгоритм:

− Запуск
− Инициализируйте значение размера промежутка, скажем h.
− Разделите список на меньшие части. В каждом должны быть равные интервалы до h.
− Отсортируйте эти вложенные списки с помощью сортировки по вставке.
– Повторяйте этот шаг 2, пока список не будет отсортирован.
– Распечатайте отсортированный список.
– Остановка.

### Реализация на языке с++
``c++
void ShellSort(std::vector<int> &arr)
{
    int n = arr.size();
    for (int interval = n / 2; interval > 0; interval /= 2)
    {
        for (int i = interval; i < n; i += 1)
        {
            int temp = arr[i];
            int j;
            for (j = i; j >= interval && arr[j - interval] > temp; j -= interval)
            {
                arr[j] = arr[j - interval];
            }
            arr[j] = temp;
        }
    }
}
```

### Анализ сложности и памяти

Временная сложность: Временная сложность вышеупомянутой реализации Shellsort равна O(n2). В приведенной выше реализации разрыв сокращается вдвое на каждой итерации. Существует множество других способов сокращения пробелов, что приводит к увеличению временных затрат. Смотрите это для получения более подробной информации.
Наихудшая сложность сортировки оболочки равна O (n^2)
Когда данный список массивов уже отсортирован, общее количество сравнений каждого интервала равно размеру данного массива.
Итак, в лучшем случае сложность равна Ω(n log (n))
Средняя сложность: O (n* log n) ~ O(n1.25)

Пространственная сложность: O (1).
---

# Эксперимент cравнение эффективности алгоритмов на разных компиляторах


---
## Источники

(https://sortingalgos.miraheze.org/wiki)
(https://www.geeksforgeeks.org)
