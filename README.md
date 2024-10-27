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

Исходя из этих данных состоит первая таблица "До балансировки", урон стабилен из-за отсутствия какого-либо отклонения, кроме холодного оружия, ведь оно не может попасть дальше вытянутой руки, а урон дисбалансен в пользу бензопилы и АКМ, в итоге получился следующий график 

![image](https://github.com/user-attachments/assets/5dd425ba-fbac-4c7d-bb71-4c5e660fde36)

Далее я сбалансировал имеющееся игровое оружие и добавил три варианта нового оружия: метательные ножи, арбалет и, конечно, дробовик, патроны для которого уже имеется 

## Задание 2
### Визуализировать параметры оружия в таблице. Построить примеры для: среднеквадратического отклонения (СКО), разброса урона оружия, вариативности времени отклика игрока 


## Задание 3
### Визуализировать данные из google-таблицы, и с помощью Python передавать переменные в проект Unity.

## Выводы


