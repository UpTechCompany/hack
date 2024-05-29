### Пояснительная записка

#### Описание программы

Программа представляет собой игру для нескольких игроков (от 2 до 4) на 5x5 клеточной доске, где игроки поочередно добавляют буквы, чтобы составлять слова. Игра начинается с начального слова, введенного пользователем, которое размещается в центре доски. Цель игры - составлять слова, используя буквы на доске, за что начисляются очки.

#### Основные компоненты

1. **main.cpp**: Основной файл программы, содержащий функцию `main`, которая управляет игровым процессом, взаимодействием с пользователем и инициализацией объекта `Game`.

2. **game.cpp**: Реализация методов класса `Game`, отвечающих за логику игры, обработку ходов игроков, проверку правил, отображение текущего состояния доски и подсчет очков.

3. **game.h**: Заголовочный файл, содержащий объявление класса `Game` и его методов.

#### Класс `Game`

- **Конструктор `Game`**: Инициализирует игровую доску, загружает словарь, устанавливает начальные параметры игры и открывает лог-файл.
- **Деструктор `~Game`**: Закрывает лог-файл.
- **Методы**:
  - `displayBoard()`: Отображает текущее состояние доски.
  - `displayScores()`: Отображает текущие очки игроков.
  - `addLetter(int row, int col, char letter)`: Добавляет букву на доску, проверяя корректность хода и подсчитывая очки.
  - `isValidWord(const std::string& word)`: Проверяет наличие слова в словаре.
  - `isGameOver()`: Проверяет, завершена ли игра.
  - `getScore(int player)`, `getCurrentPlayer()`, `setScore(int player, int score)`, `nextTurn()`, `skipTurn()`: Методы для работы с состоянием игроков и их очками.
  - `isValidPlacement(int row, int col, char letter)`: Проверяет корректность размещения буквы.
  - `isAdjacent(int row, int col)`: Проверяет наличие смежных букв.
  - `findWords()`: Находит все составленные слова на доске.
  - `loadDictionary(const std::string& dictionaryFile)`: Загружает словарь из файла.
  - `initLogFile()`: Инициализирует лог-файл для записи хода игры.

### Блок-схема

```markdown
```mermaid
flowchart TD
    A[Start] --> B[Enter initial 5-letter word]
    B --> C[Enter number of players (2-4)]
    C --> D{Initialize Game}
    D --> E[Load Dictionary]
    E --> F[Set Initial Board State]
    F --> G[Game Loop]
    G --> H{Is Game Over?}
    H -->|No| I[Display Board]
    I --> J[Player's Turn: Enter row, col, and letter]
    J --> K{Skip Turn?}
    K -->|Yes| L[Skip Turn]
    L --> M[Display Scores]
    M --> G
    K -->|No| N{Valid Placement?}
    N -->|No| O[Invalid Move, Retry]
    O --> G
    N -->|Yes| P[Add Letter to Board]
    P --> Q[Find and Validate Words]
    Q --> R[Update Scores]
    R --> M
    H -->|Yes| S[Game Over]
    S --> T[Display Final Scores]
    T --> U[End]

```
