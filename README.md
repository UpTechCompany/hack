### Пояснительная записка

#### Описание программы

Программа реализует игру, в которой участвуют от 2 до 4 игроков. Игровая доска размером 5x5 начинается с начального слова, вводимого пользователем, размещенного по центру. Игроки поочередно добавляют буквы на доску, стараясь составлять новые слова. Игра продолжается до тех пор, пока не будут выполнены условия завершения (заполнение доски или определенное количество пропусков).

#### Основные компоненты программы

1. **main.cpp**: Содержит основную функцию `main`, управляющую игровым процессом и взаимодействием с пользователем.

2. **game.cpp**: Реализация методов класса `Game`, отвечающих за игровую логику, обработку ходов игроков и отображение состояния игры.

3. **game.h**: Заголовочный файл, содержащий объявление класса `Game` и его методов.

### Детализация методов класса `Game`

#### Конструктор `Game(const std::string& initialWord, const std::string& dictionaryFile, int numPlayers)`

Инициализирует игру:
- Создает пустую игровую доску 5x5.
- Размещает начальное слово в середине доски.
- Загружает словарь из файла.
- Инициализирует лог-файл для записи хода игры.
- Устанавливает начальные параметры игры: текущего игрока, количество пропусков подряд и начальные очки.

#### Деструктор `~Game()`

Закрывает лог-файл, если он открыт.

#### Методы

- **`void displayBoard() const`**:
  Отображает текущее состояние доски в консоли и записывает его в лог-файл.

- **`void displayScores() const`**:
  Отображает текущие очки всех игроков в консоли и записывает их в лог-файл.

- **`bool addLetter(int row, int col, char letter)`**:
  Добавляет букву на указанную позицию на доске, проверяя корректность хода. Если ход корректный:
  - Буква добавляется на доску.
  - Логируются действия игрока.
  - Проверяются и обновляются составленные слова.
  - Обновляются очки текущего игрока.
  - Сбрасывается счетчик пропусков.
  - Переходит к следующему игроку.

- **`bool isValidWord(const std::string& word) const`**:
  Проверяет, является ли слово допустимым (есть ли оно в загруженном словаре).

- **`bool isGameOver() const`**:
  Проверяет, завершена ли игра (заполнена ли доска или количество пропусков подряд достигло числа игроков).

- **`int getScore(int player) const`**:
  Возвращает текущий счет указанного игрока.

- **`int getCurrentPlayer() const`**:
  Возвращает индекс текущего игрока.

- **`void setScore(int player, int score)`**:
  Устанавливает счет для указанного игрока.

- **`void nextTurn()`**:
  Переходит к следующему игроку.

- **`void skipTurn()`**:
  Пропускает ход текущего игрока, увеличивая счетчик пропусков и переходя к следующему игроку.

- **`bool isValidPlacement(int row, int col, char letter) const`**:
  Проверяет, является ли размещение буквы допустимым:
  - Клетка должна быть в пределах доски и пустой.
  - Клетка должна быть смежной с другой занятой клеткой.

- **`bool isAdjacent(int row, int col) const`**:
  Проверяет, есть ли занятые клетки рядом с указанной позицией.

- **`std::vector<std::string> findWords() const`**:
  Находит все допустимые слова на доске (горизонтальные и вертикальные).

- **`void loadDictionary(const std::string& dictionaryFile)`**:
  Загружает словарь из указанного файла.

- **`void initLogFile()`**:
  Инициализирует лог-файл для записи хода игры.

### Блок-схема

```mermaid
graph TD;
    A[Начало] --> B[Введите начальное 5-буквенное слово];
    B --> C{Введите количество игроков 2-4?};
    C --> D[Инициализировать игру];
    D --> E[Загрузить словарь];
    E --> F[Установить начальное состояние доски];
    F --> G[Игровой цикл];
    G --> H{Игра завершена?};
    H -->|Нет| I[Отобразить доску];
    I --> J[Ход игрока: Введите строку, столбец и букву];
    J --> K{Пропустить ход?};
    K -->|Да| L[Пропустить ход];
    L --> M[Отобразить счет];
    M --> G;
    K -->|Нет| N{Корректное размещение?};
    N -->|Нет| O[Некорректный ход, Повторить];
    O --> G;
    N -->|Да| P[Добавить букву на доску];
    P --> Q[Найти и проверить слова];
    Q --> R{Найдены допустимые слова?};
    R -->|Да| S[Обновить счет];
    S --> M;
    R -->|Нет| T[Продолжить];
    T --> M;
    H -->|Да| U[Игра завершена];
    U --> V[Отобразить финальные очки];
    V --> W[Конец];



```
