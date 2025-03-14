# Описание данной библиотеки FSM
Она не для запуска. Тут просто анализ. Потому что тут много интересного в этом коде

- Тут имеется вызов `` import pwd `` - которая обеспечивает доступ к Базе Данных 
пользователей и паролей. Он доступен во всех версиях Unix. Может использоваться для сбора информации о паролях   
- Имеется обработчик сигналов операционной системы
- ``class Transition``  - это класс представляющий переходы FSM
- Тут имеется цепочка переходов и имеются ссылки на предыдущие и последующие переходы в виде ссылок переменных.
Паттерн ``Цепочка``. Имеется ссылка на `after`, `before`. Когда выбирается  `on` вызывается то что происходит при переходе 
на данное звено из цепочки
 


Как использовать библиотеку
```python
from statelogic import StateLogic

# Основной инстанс
state_logic = StateLogic()
```

## Использование. ``start`` нажимаем и происходит переход
```
from statelogic import FSM

class MyFSM(FSM):
    def __init__(self):
        super().__init__(self)
        self.state("INITIAL")
        self.transition("start", "INITIAL", "RUNNING")
    
    def onSTART(self):
        print("Transitioning to RUNNING state")

fsm_instance = MyFSM()
fsm_instance.start() # Когда дергаем start происходит переход
```

## Получение информации о собственном приложении
```
from statelogic import AppData

app_data = AppData()
app_data.appName("My Application")
app_data.author("Your Name")

print(app_data.appName())  # Output: My Application
print(app_data.author())    # Output: Your Name
```

Addition methods in AppData


```
app_data.majorVersion(1)
app_data.minorVersion(0)

print(app_data.version())  # Output: 1.0
```


## Использование класса `Attr`. Автоматическое рефлективное определение свойств новому классу

```
from statelogic import Attr

class MyClass:
    def __init__(self):
        self.name = Attr(self, attrName="name", value="Default Name") # Назначаем свойство

my_instance = MyClass()
print(my_instance.name())  # Используем свойство

# Обновляем имя
my_instance.name("New Name")
print(my_instance.name())  # Output: New Name
```

## Using Transition Class
```
from statelogic import Transition
transition = Transition(name="Start to End", fromState="START", toState="END")
print(transition.name)        # Output: Start to End
print(transition.fromState)   # Output: START
print(transition.toState)     # Output: END
```


##  Вывод сообщений
```
state_logic.criticalMsg("This is a critical message", tag="ERROR")
```