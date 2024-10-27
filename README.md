# UrFU-AD-in-GameDev-Workshop3
Отчет по лабораторной работе #3 выполнил:
- Лукоянов Владислав Александрович
- НМТ - 232202
  
Отметка о выполнении заданий:

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Оценить структуры игры Save RTF. Ознакомиться с прототипом игры Save RTF на движке Unity, проанализировать доступное в игре оружие, предложить собственные варианты оржия.
## Задание 1
### Расширить варианты доступного оружия в игре Save RTF. Визуализировать оружие игры, используя шаблон таблицы.
На основе шаблона, я построил собственную гугл таблицу с данными, характеризующими урон и вероятность попадания: https://docs.google.com/spreadsheets/d/12V0fRsdPyaTffW7ctOaCRHxkH1Bxn4dfSq2ouFk-yuQ/edit?gid=0#gid=0

Взяв за условие, что здоровье первого босса (скриншот ниже) равна 1000 единицам, я опытным путем тестировал оружие, доступное в игре, используя конами-код для начисления денег, бессмертия и генерации боссов.
  
![Скриншот 26-10-2024 165019](https://github.com/user-attachments/assets/2a1dcadd-feac-401e-b960-9f1befd72a90)

Таким образом, я нашел примерный средний урон каждого оружия и колличество выстрелов (ударов для тесака, оборотов цепи для бензопилы) в 1 секунду, используя формулы: 
1. урон: (хп босса)/(кол-во ударов или патронов), 
2. скорострельности: (кол-во патронов)/(время расхода обоймы), 
3. скорость ударов: (кол-во ударов)/(время убиства босса)

Для расчета урона и скорости стрельбы огнестрела было достаточно смотреть сколько патронов пришлось израсходовать и засекать время расхода одной обоймы. Для тесака же пришлось одновременно засекать время убийства босса и считать колличество ударов. Бензопила же сносит хп первого босса примерно за 1 сек, так что для расчета оборотов цепи я, прокачав скорость, подбегал к боссу и в момент нанесения удара отбегал, поэтому данные о количестве оборотов могут быть весьма не точными, но всего удалось насчитать 8 ударов, урон за каждый рассчитывался из учета, что босс покибает всего за секунду.
Также я выяснил, что оружие не имеет никакого отклонения (иначе как объяснить хэдшоты из пистолета-пулемета на расстоянии потери видимости?)

![Скриншот 26-10-2024 164635](https://github.com/user-attachments/assets/b0e1c831-0c1e-4569-8e3e-dfc89ec501ef)

Из этих данных состоит первая таблица "До балансировки", урон стабилен из-за отсутствия какого-либо отклонения, кроме холодного оружия, ведь оно не может попасть дальше вытянутой руки, а урон дисбалансен в пользу бензопилы и АКМ, в итоге получился следующие график и показатели соотношения урона (шкала урона нужна для наглядного соотношения урона оружий, поэтому кол-во штрихов шкалы в 10 раз меньше показателя урона)

![image](https://github.com/user-attachments/assets/5dd425ba-fbac-4c7d-bb71-4c5e660fde36) 
![image](https://github.com/user-attachments/assets/a29cbf55-f6da-4465-bea0-c9f427053a87)

Далее я сбалансировал имеющееся игровое оружие и добавил три варианта нового оружия: метательные ножи, арбалет и, конечно, дробовик, патроны для которого в игре уже имеются. Измененные данные я оформил в таблице "После балансировки", теперь график и показатели соотношения урона имели следущий вид

![image](https://github.com/user-attachments/assets/1fa01dff-951f-487d-8d5e-f0b31c2fd6af)
![image](https://github.com/user-attachments/assets/a41a87cc-06f6-4d42-9ec7-fe19b5f84c1a)

Эффектиность разных видов вооружения теперь зависит от условий дальности стрельбы. Лидировать продолжают бензопила, АКМ и дробовик, но есть несколько дополнительных моментов. Дробовик по настоящему эффективен именно на коротких дистанциях, к тому же его покупка и патроны к нему обойдуться дороже, чем для другого оружия, АКМ и вовсе самое дорогое, покупаемое и обслуживаемое оружие, поэтому его использование игрок не всегда сможет себе позволить, а бензопила продолжает оставаться дорогим оружием ближнего боя, так что большой урон компенсирует риск. Метательные ножи, несмотря на свою, казалось бы, низкуюэффективность покупаются как расходники, дешевле чем некоторые патроны. Для тесака и ибензопилы шанс попадания на расстоянии вытянутой руки 100%, ведь удары этими оружиями не могут отклоняться непроизвольно.

## Задание 2
### Визуализировать параметры оружия в таблице. Построить примеры для: среднеквадратического отклонения (СКО), разброса урона оружия, вариативности времени отклика игрока 

Так как тесак и бензопила - холодное оружие блиского действия, то и попадания из них имеют 0.0 CКО и летят точно в цель, для остального же оружия испольуются программы на python, моделирующие случайность попадания.

Рассмотрим работу этих программ на примере арбалета, коды для моделей попаданий других своих, а также сбалансированных имеющихся в игре оружий можно найти в этом репозитории в заархивированном проекте PyCharm "work3". 

1. Программа для моделирования СКО арбалета и ее рузультаты:

```py
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)  # Фиксируем рандом для воспроизводимости
shots = np.random.normal(loc=0, scale=5, size=(2, 2))  # Отклонения (x, y)

# Вычисляем отклонения (расстояния от центра цели)
distances = np.linalg.norm(shots, axis=1)

# Среднеквадратическое отклонение
std_dev = np.std(distances)

print(f"СКО отклонений: {std_dev:.2f} пикселей")

# Визуализация попаданий
plt.figure(figsize=(6, 6))
plt.scatter(shots[:, 0], shots[:, 1], color='red', label='Попадания')
plt.scatter(0, 0, color='blue', label='Цель', s=100)
plt.xlim(-20, 20)
plt.ylim(-20, 20)
plt.axhline(0, color='black', lw=0.5)
plt.axvline(0, color='black', lw=0.5)
plt.legend()
plt.title("Модель разброса выстрелов")
plt.gca().set_aspect('equal', adjustable='box')
plt.show()
```
СКО: 2,85 пикселей

![image](https://github.com/user-attachments/assets/16deee94-7c0d-4ad9-9713-3edae4fd3b28)

2. Программа для моделирования разброса урона арбалета и ее рузультаты:

```py
import numpy as np
import matplotlib.pyplot as plt

# Генерация случайных значений урона с нормальным распределением
np.random.seed(123)
damage = np.random.normal(loc=25, scale=3, size=100)  # Средний урон = 50, СКО = 10

# Визуализация гистограммы урона
plt.figure(figsize=(8, 6))
plt.hist(damage, bins=10, color='purple', alpha=0.7, edgecolor='black')
plt.axvline(damage.mean(), color='red', linestyle='dashed', linewidth=2, label=f'Среднее: {damage.mean():.2f}')
plt.axvline(damage.mean() + np.std(damage), color='green', linestyle='dotted', label=f'СКО: {np.std(damage):.2f}')
plt.axvline(damage.mean() - np.std(damage), color='green', linestyle='dotted')
plt.legend()
plt.title('Распределение урона оружия')
plt.xlabel('Урон')
plt.ylabel('Частота')
plt.show()
```

![image](https://github.com/user-attachments/assets/e85b69cd-80ea-4e57-8a9f-9abd60235457)

3. Программа вариативности времени отклика игрока и ее рузультаты:

```py
import numpy as np
import matplotlib.pyplot as plt

reaction_times = np.random.normal(loc=500, scale=40, size=20)  # Среднее время = 500 мс

plt.figure(figsize=(8, 6))
plt.plot(reaction_times, 'o-', color='teal')
plt.axhline(reaction_times.mean(), color='red', linestyle='dashed', label=f'Среднее: {reaction_times.mean():.2f} мс')
plt.fill_between(range(20),
                 reaction_times.mean() - np.std(reaction_times),
                 reaction_times.mean() + np.std(reaction_times),
                 color='lightgreen', alpha=0.3, label=f'СКО: ±{np.std(reaction_times):.2f} мс')
plt.legend()
plt.title('Время реакции игрока')
plt.xlabel('Событие')
plt.ylabel('Время (мс)')
plt.show()
```

![image](https://github.com/user-attachments/assets/0fabadc6-ee85-4066-baf8-fb43bb767b23)


## Задание 3
### Визуализировать данные из google-таблицы, и с помощью Python передавать переменные в проект Unity.

## Выводы

В ходе работы работы мне удалось провести анализ арсенала оружия из игры Save RTF и визуализировать характеристики каждого в google таблице. Также я сбалансировал имеющиеся в игре оружия и предложил свои варианты вооружения, построил модели параметров сбалансированного оружия с помощью программ на python. 
