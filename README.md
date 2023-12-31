## Задание
1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.
4. Установить и удалить deb-пакет с помощью dpkg.
5. Выложить историю команд в терминале ubuntu
6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).
7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”
8. Создать таблицы с иерархией из диаграммы в БД
9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения
10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
11.Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
13.Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу на Python, имитирующую работу реестра домашних животных.
В программе должен быть реализован следующий функционал:
14.1 Завести новое животное
14.2 определять животное в правильный класс
14.3 увидеть список команд, которое выполняет животное
14.4 обучить животное новым командам
14.5 Реализовать навигацию по меню

## Решение
1. Создание и объединение файлов в Linux:
```sh
# Creating files
echo "Dogs, cats, hamsters" > "Pet animals"
echo "Horses, camels, donkeys" > "Working animals"

# Combining files
cat "Pet animals" "Working animals" > "Friends of Humans"

# Viewing the contents
cat "Friends of Humans"

# Renaming the file
mv "Friends of Humans" "New File Name"
```

2. Создание директории и перемещение файла:
```sh
# Создание директории
mkdir Новая_директория

# Перемещение файла
mv "Новое имя файла" Новая_директория/
```

3. Подключение репозитория MySQL и установка пакета:
```sql
# Adding MySQL repository
sudo add-apt-repository ppa:mysql/mysql

# Updating the package list
sudo apt-get update

# Installing a package
sudo apt-get install package_name

```

4. Установка и удаление deb-пакета:
```sh
# Установка пакета
sudo dpkg -i имя_пакета.deb

# Удаление пакета
sudo dpkg -r имя_пакета

```

5. История команд в терминале Ubuntu:
```sh
history
```

6. Диаграмма классов:
```
           +-------------------+
           |      Animals      |
           +-------------------+
                   |
           +------------------+
           |                  |
         Pet Animals  Working Animals
           |                  |
           +                  +
           |                  |
 +------------------+    +------------------+
 |                  |    |                  |
Dogs   Cats   Hamsters   Horses   Camels   Donkeys


```

7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”:
```sql
-- Connect to MySQL and create a new database
CREATE DATABASE IF NOT EXISTS `Friends_of_Humans`;

-- Switch to the newly created database
USE `Friends_of_Humans`;

```
8. Создать таблицы с иерархией из диаграммы в БД:
```sql
-- Creating tables based on the class diagram

-- Table for Pet Animals
CREATE TABLE Pet_Animals (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255),
    Category VARCHAR(255)
);

-- Table for Working Animals
CREATE TABLE Working_Animals (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255),
    Category VARCHAR(255)
);

-- Additional columns can be added based on the specific attributes of each class

```

9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения
```sql
-- Inserting data into the Pet Animals table
INSERT INTO Pet_Animals (Name, Category) VALUES
('Dog1', 'Dogs'),
('Cat1', 'Cats'),
('Hamster1', 'Hamsters');

-- Inserting data into the Commands table for Pet Animals
INSERT INTO Commands (AnimalID, Command) VALUES
(1, 'Sit'),
(2, 'Meow'),
(3, 'Run in wheel');

-- Inserting data into the BirthDates table for Pet Animals
INSERT INTO BirthDates (AnimalID, BirthDate) VALUES
(1, '2022-01-15'),
(2, '2021-05-03'),
(3, '2023-02-10');

-- Inserting data into the Working Animals table
INSERT INTO Working_Animals (Name, Category) VALUES
('Horse1', 'Horses'),
('Camel1', 'Camels'),
('Donkey1', 'Donkeys');

-- Inserting data into the Commands table for Working Animals
INSERT INTO Commands (AnimalID, Command) VALUES
(4, 'Gallop'),
(5, 'Grunt'),
(6, 'Bray');

-- Inserting data into the BirthDates table for Working Animals
INSERT INTO BirthDates (AnimalID, BirthDate) VALUES
(4, '2019-07-22'),
(5, '2020-11-05'),
(6, '2018-04-30');
```

10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
```sql
-- Merging tables into a new table
CREATE TABLE All_Animals AS SELECT * FROM Pet_Animals UNION SELECT * FROM Working_Animals;

-- Deleting camels from the merged table
DELETE FROM All_Animals WHERE Category = 'Camels';

```

11. Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице:
```sql
-- Creating a table for Young Animals
CREATE TABLE Young_Animals AS SELECT * FROM All_Animals WHERE Age BETWEEN 1 AND 3;
```

12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
```sql
-- Adding a column for age in months
ALTER TABLE Young_Animals ADD COLUMN Age_in_Months INT;

-- Merging all tables into a final combined table
CREATE TABLE Combined_Table AS SELECT * FROM Pet_Animals
UNION SELECT * FROM Working_Animals
UNION SELECT * FROM Young_Animals;

```

13. Класс с инкапсуляцией и наследованием:
```python
class Animal:
    def __init__(self, name):
        self.name = name

class PetAnimals(Animal):
    def __init__(self, name):
        super().__init__(name)

class WorkingAnimals(Animal):
    def __init__(self, name):
        super().__init__(name)

```

14. Программа на Python:
```python
class Animal:
    def __init__(self, name, animal_class="Default"):
        self.name = name
        self.animal_class = animal_class
        self.commands = []

    def add_command(self, command):
        self.commands.append(command)

    def list_commands(self):
        return self.commands

    def teach_commands(self, new_commands):
        self.commands.extend(new_commands)

# Function to create a new animal
def create_animal():
    name = input("Enter the name of the animal: ")
    animal_class = input("Enter the class of the animal (e.g., Pet or Working): ")
    return Animal(name, animal_class)

# Function to determine the class of an animal
def determine_animal_class(animal):
    print(f"{animal.name} belongs to the {animal.animal_class} class.")

# Function to display the list of commands for an animal
def display_commands(animal):
    commands = animal.list_commands()
    if commands:
        print(f"{animal.name} knows the following commands:")
        for command in commands:
            print(f"- {command}")
    else:
        print(f"{animal.name} has not been taught any commands yet.")

# Function to teach new commands to an animal
def teach_animal(animal):
    new_commands = input("Enter new commands separated by commas: ").split(',')
    animal.teach_commands(new_commands)
    print(f"{animal.name} has learned new commands.")

# Menu navigation function
def navigate_menu(animal):
    while True:
        print("\nMenu:")
        print("1. Create a new animal")
        print("2. Determine the animal class")
        print("3. Display commands")
        print("4. Teach new commands")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            animal = create_animal()
        elif choice == '2':
            determine_animal_class(animal)
        elif choice == '3':
            display_commands(animal)
        elif choice == '4':
            teach_animal(animal)
        elif choice == '5':
            print("Exiting the program. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 5.")

if __name__ == "__main__":
    # Initialize with a default animal
    default_animal = Animal("DefaultAnimal", "DefaultClass")
    
    print("Welcome to the Animal Registry Program!")
    navigate_menu(default_animal)

```
