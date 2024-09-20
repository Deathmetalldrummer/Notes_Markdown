**Алгоритмы устойчивой сортировки**

**Устойчивая (стабильная) сортировка** — [сортировка](https://ru.wikipedia.org/wiki/Алгоритм_сортировки), которая не меняет относительный порядок сортируемых элементов, имеющих одинаковые ключи, по которым происходит сортировка.

| Алгоритм                                                     | Описание                                                     | **В худшем случае**                                          | **В среднем**                                                | **Затраты памяти** В худшем случае                           | **Примечание**                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Сортировка пузырьком](https://ru.wikipedia.org/wiki/Сортировка_пузырьком) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Bubble sort*) | Проходит по массиву, сравнивает последовательные пары элементов и меняет их местами, если они расположены в неправильном порядке. | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) | В процессе сортировки минимальный элемент "всплывает" вверх массива, напоминая пузырь |
| [Сортировка перемешиванием](https://ru.wikipedia.org/wiki/Сортировка_перемешиванием) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Cocktail sort*) | Двунаправленный, оптимизированный вариант [сортировки пузырьком](https://ru.wikipedia.org/wiki/Сортировка_пузырьком) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) |                                                              |
| [Сортировка вставками](https://ru.wikipedia.org/wiki/Сортировка_вставками) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Insertion sort*) | Элементы входной последовательности просматриваются по одному, и каждый новый поступивший элемент размещается в подходящее место среди ранее упорядоченных элементов | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) |                                                              |
| [Гномья сортировка](https://ru.wikipedia.org/wiki/Гномья_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Gnome sort*) | Гибрид сортировок [вставками](https://ru.wikipedia.org/wiki/Сортировка_вставками) и [пузырьком](https://ru.wikipedia.org/wiki/Сортировка_пузырьком). | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) | Название происходит от предполагаемого поведения [садовых гномов](https://ru.wikipedia.org/wiki/Садовый_гном) при сортировке линии садовых горшков |
| [Сортировка слиянием](https://ru.wikipedia.org/wiki/Сортировка_слиянием) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Merge sort*) | [Рекурсивно](https://ru.wikipedia.org/wiki/Рекурсия) сортирует половины массива, а затем комбинирует их в один | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) |                                                              |
| [Сортировка с помощью двоичного дерева](https://ru.wikipedia.org/wiki/Сортировка_с_помощью_двоичного_дерева) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Tree sort*) | На основе исходных данных строится [двоичное дерево поиска](https://ru.wikipedia.org/wiki/Двоичное_дерево_поиска), в котором последовательно собираются минимальные значения | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) |                                                              |
| Сортировка [Timsort](https://ru.wikipedia.org/wiki/Timsort) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Timsort*) | Гибрид сортировок [вставками](https://ru.wikipedia.org/wiki/Сортировка_вставками) и [слиянием](https://ru.wikipedia.org/wiki/Сортировка_слиянием). Основан на предположении, что при решении практических задач входной массив зачастую состоит из отсортированных подмассивов | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) |                                                              |

**Алгоритмы неустойчивой сортировки**

| Алгоритм                                                     | Описание                                                     | **В худшем случае**                                          | **В среднем**                                                | **Затраты памяти** В худшем случае                           | **Примечание**                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Сортировка выбором](https://ru.wikipedia.org/wiki/Сортировка_выбором) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Selection sort*) | Делит входной массив на упорядоченную и неупорядоченную части. Затем последовательно переносит в первую часть наименьшие элементы из второй | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) |                                                              |
| [Сортировка расчёской](https://ru.wikipedia.org/wiki/Сортировка_расчёской) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Comb sort*) | Модификация [сортировки пузырьком](https://ru.wikipedia.org/wiki/Сортировка_пузырьком), в которой расстояние между сравниваемыми парами значений отлично от 1 | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![{\displaystyle O(n^{2}/2^{p})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd8141798346156ee1d4046908533daca3ff21e9) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) | Несмотря на бóльшую [алгоритмическую сложность](https://ru.wikipedia.org/wiki/Вычислительная_сложность), при не очень больших размерахмассива сортировка расчёской будет более эффективна чем [быстрая сортировка](https://ru.wikipedia.org/wiki/Быстрая_сортировка) |
| [Сортировка Шелла](https://ru.wikipedia.org/wiki/Сортировка_Шелла) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Shell sort*) | Модификация [сортировка вставками](https://ru.wikipedia.org/wiki/Сортировка_вставками), в которой расстояние между сравниваемыми парами значений отлично от 1 | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![{\displaystyle O(n\log ^{2}{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a953c17b6bd6cdf4fcd8daee347cba19b8b2745a) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) |                                                              |
| [Пирамидальная сортировка](https://ru.wikipedia.org/wiki/Пирамидальная_сортировка) (сортировка кучи, Heapsort) | На основе исходных данных строится [двоичное куча](https://ru.wikipedia.org/wiki/Двоичная_куча), в которой последовательно собираются минимальные значения | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) |                                                              |
| [Плавная сортировка](https://ru.wikipedia.org/wiki/Плавная_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Smoothsort*) | Модификация [пирамидальной сортировки](https://ru.wikipedia.org/wiki/Пирамидальная_сортировка), оптимизирущая сортировку частично упорядоченного массива | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) |                                                              |
| [Быстрая сортировка](https://ru.wikipedia.org/wiki/Быстрая_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Quicksort*) | Выбирается опорный элемент p. Все ключи, меньшие, либо равные p перемещаются, влево от него, а все ключи, большие, либо равные p вправо. Далее алгоритм [рекурсивно](https://ru.wikipedia.org/wiki/Рекурсия) применяется к каждой из частей | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) | = O(n*2.7095...)                                             |
| [Интроспективная сортировка](https://ru.wikipedia.org/wiki/Интроспективная_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Introsort*) | Гибрид [быстрой](https://ru.wikipedia.org/wiki/Быстрая_сортировка) и [пирамидальной](https://ru.wikipedia.org/wiki/Пирамидальная_сортировка) сортировок | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![{\displaystyle O(n\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b5ea2d55d8c31feb17ce14f35da4c93f94982b3) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) |                                                              |

**Непрактичные алгоритмы сортировки**

| Алгоритм                                                     | Описание                                                     | **В худшем случае**                                          | **В среднем**                                                | **Затраты памяти** В худшем случае                           | **Примечание**                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------------------------- |
| [Bogosort](https://ru.wikipedia.org/wiki/Bogosort)           | Массив произвольно перемешивается до техпор, пока не окажется отсортированным | Неограниченно                                                | ![{\displaystyle O(n!)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12921c489714d475a454bd39ef644d4334d97113) | ![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) | Используется только в академических целях           |
| [Сортировка перестановкой](https://ru.wikipedia.org/w/index.php?title=Сортировка_перестановкой&action=edit&redlink=1) | Генерируются все возможные последовательности массива, из которых выбирается упорядоченная | ![{\displaystyle O(n!)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12921c489714d475a454bd39ef644d4334d97113) | ![{\displaystyle O(n!)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12921c489714d475a454bd39ef644d4334d97113) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) | Используется только в академических целях           |
| [Гравитационная сортировка](https://ru.wikipedia.org/wiki/Гравитационная_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Bead sort*) | Числа представляются в виде бусинок на штырях, затем сортируются под действием гравитации | ![O(\sqrt{n})](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5526ab1252c0f682bbe07c0ad67c0f29de5522b) | ![O(\sqrt{n})](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5526ab1252c0f682bbe07c0ad67c0f29de5522b) | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | Требуется специализированное аппаратное обеспечение |

**Алгоритмы, не основывающиеся на сравнениях**

| Алгоритм                                                     | Описание                                                     | **В худшем случае**                                          | **В среднем**                                                | **Затраты памяти** В худшем случае                           | **Примечание**                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Блочная сортировка](https://ru.wikipedia.org/wiki/Блочная_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Bucket sort*) | Элементы распределяются по блокам согласно диапазону значений, каждый из которых затем рекурсивно сортируется | ![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) | ![{\displaystyle O(n^{2}+n/k+k)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/73a2e7c522292ff321daf38ff5959a3321d5d211) | ![{\displaystyle O(n+k)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8) | ![k](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) - заранее известное количество корзин |
| [Поразрядная сортировка](https://ru.wikipedia.org/wiki/Поразрядная_сортировка) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Radix sort*) | Массив сортируется согласно с помощью поразрядного сравнения чисел | ![{\displaystyle O(wn)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ad880b817122c4b8f245eb2ef10b3dd2dcbedba8) | ![{\displaystyle O(wn)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ad880b817122c4b8f245eb2ef10b3dd2dcbedba8) | ![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) | ![w](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) — количество бит, требуемых для хранения каждого ключа. |
| [Сортировка подсчётом](https://ru.wikipedia.org/wiki/Сортировка_подсчётом) ([англ.](https://ru.wikipedia.org/wiki/Английский_язык) *Counting sort*) | Подсчитывается количество вхождений каждого целого числа из диапазона ключей в массив. Затем выводится значения всех ненулевых значений | ![{\displaystyle O(n+k)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8) | ![{\displaystyle O(n+k)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8) | ![O(n+k)](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8) | ![k](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) - максимальное значение элементов ключа |
