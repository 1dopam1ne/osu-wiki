# Точность

Точность (англ. *accuracy*, жарг. *аккураси*, *акка*) — это оценка того, насколько вовремя игрок нажимает на [ноты](/wiki/Gameplay/Hit_object). Она измеряется в процентах и бывает трёх видов:

1. Точность на конкретной сложности, которая зависит от полученных очков за нажатия.
2. Общая точность, которая складывается из всех рекордов (у каждого из них — свой вес в сумме, чтобы лучшие рекорды сильнее влияли на точность).
3. Точность по [очкам производительности (pp)](/wiki/Performance_points), которая складывается из точности результатов, принёсших больше всего PP.

## Игровые режимы

### ![](/wiki/shared/mode/osu.png) osu!

![Accuracy = (300 \* number of 300s + 100 \* number of 100s + 50 \* number of 50s) / (300 \* (number of 300s + number of 100s + number of 50s + number of misses))](img/accuracy_osu_updated.png "Формула расчёта точности для osu!")

В osu! точность рассчитывается как сумма всех [индивидуальных попаданий](/wiki/Gameplay/Judgement) по нотам, разделённая на максимально возможное количество очков на карте. 

Пример с одной нотой:

```
300 -> 300 / 300 = 1   = 100.00%
100 -> 100 / 300 = 1/3 =  33.33%
50  ->  50 / 300 = 1/6 =  16.67%
0   ->   0 / 300 = 0   =   0.00%
```

### ![](/wiki/shared/mode/taiko.png) osu!taiko

![Accuracy = (number of GREATs + 0.5 \* number of GOODs) / (number of GREATs + number of GOODs + number of misses)](img/accuracy_taiko_updated.png "Формула расчёта точности для osu!taiko")

В osu!taiko точность рассчитывается как сумма точностей нот, делённая на их общее количество. Точность ноты может быть GREAT (良) (cчитается как 100%), GOOD (可) (cчитается как 50%), или MISS/BAD (不可) (считается как 0%, а также сбрасывает комбо). Слайдеры (drum roll) и спиннеры не влияют на точность.

### ![](/wiki/shared/mode/catch.png) osu!catch

![Accuracy = (number of caught fruits + number of caught drops + number of caught droplets) / (number of all fruits + number of all drops + number of all droplets)](img/accuracy_catch_updated.png "Формула расчёта точности для osu!catch")

В osu!catch точность рассчитывается как количество собранных объектов, делённое на их общее количество (бананы при этом нигде не учитываются). Все объекты, кроме бананов, имеют одинаковое значение точности.

*Примечания для пользователей [API](/wiki/osu!api):*

- Количество пойманных дропов названо `count100`.
- Количество пойманных дроплетов названо `count50`.
- Суммарное количество пропущенных фруктов *и* дропов названо `countMiss`.
- Количество пропущенных дроплетов названо `countKatu`.
- `countGeki` — количество пойманных фруктов, завершающих комбо. Оно не участвует в расчёте точности.

### ![](/wiki/shared/mode/mania.png) osu!mania

В osu!mania точность рассчитывается аналогично [osu!](#osu!), а вес радужных 300 (иногда называемых MAX) зависит от наличия мода ScoreV2.

В ScoreV1 радужные и обычные 300 имеют одинаковый вес — 300:

![Accuracy = (300 \* (number of MAXs + number of 300s) + 200 \* number of 200s + 100 \* number of 100s + 50 \* number of 50s) / (300 \* (number of MAXs + number of 300s + number of 200s + number of 100s + number of 50s + number of misses))](img/accuracy_mania_updated_score_v1.png "Формула расчёта точности для osu!mania при ScoreV1")

В ScoreV1 радужные 300 «весят» чуть больше — 305:

![Accuracy = 305 \* number of MAXs + 300 \* number of 300s + 200 \* number of 200s + 100 \* number of 100s + 50 \* number of 50s) / (305 \* (number of MAXs + number of 300s + number of 200s + number of 100s + number of 50s + number of misses))](img/accuracy_mania_updated_score_v2.png "Формула расчёта точности для osu!mania при ScoreV2")

*Примечания для пользователей API:*

- Количество радужных 300 названо `countGeki`.
- Количество 200 названо `countKatu`.

## График производительности

![Performance graph](img/performance_graph.png "График производительности")

График производительности показывает полосу здоровья игрока в течение игры. Если навести на него курсор, будет показана дополнительная информация.

*Примечание: эта информация будет показана только после того, как вы сыграли карту или посмотрели её реплей, и пропадёт, если уйти со [страницы результатов](/wiki/Client/Interface#экран-результатов).*

### Accuracy

При наведении курсора на график всплывает окошко со значениями `Error` (отклонение) и `Unstable Rate` (разброс нажатий).

В связи с тем, как реализованы моды [DT](/wiki/Gameplay/Game_modifier/Double_Time) (Double Time) и [HT](/wiki/Gameplay/Game_modifier/Half_Time) (Half Time), значения `Error` и `Unstable Rate` будут умножены на коэффициент мода. Чтобы получить истинные значения при игре с DT, разделите их на 1.5. Аналогично, при игре с HT умножьте их на 1.33.

#### Error (отклонение)

`Error` показывает два числа: среднее значение всех ранних и всех поздних ударов по нотам. Чем выше [Overall Difficulty](/wiki/Beatmap/Overall_difficulty) карты, тем меньше вы должны отклоняться от идеальных нажатий, чтобы набрать высокую точность.

#### Unstable Rate (разброс нажатий)

`Unstable Rate` отражает то, как стабильно вы нажимаете на ноты, и чем ниже это значение, тем лучше (у игроков высокого ранга оно почти всегда меньше 100). Обратите внимание, что разброс нажатий показывает **не** точность, а насколько размеренно вы нажимаете на ноты. Если вы всегда попадаете по ним очень поздно, но опаздываете примерно на одно и то же время, это число будет таким же низким, как и при стабильных нажатиях вовремя. По сути, разброс нажатий — это их [стандартное отклонение](https://ru.wikipedia.org/wiki/Среднеквадратическое_отклонение) в миллисекундах, умноженное на 10. С тем, как оно считается в стабильной версии osu!, можно ознакомиться с помощью [кода, выложенного peppy](https://gist.github.com/peppy/3a11cb58c856b6af7c1916422f668899).

### Spin

*Примечание: Spin отображается только для [osu!](/wiki/Game_mode/osu!).*

Вместе с информацией о точности можно посмотреть статистику по спиннерам.

#### Speed (скорость вращения)

`Speed` — это средняя скорость вращения, или RPM ([число оборотов в минуту](https://ru.wikipedia.org/wiki/Оборот_в_минуту)) на всех спиннерах карты. Значение с припиской `Max` показывает самую быструю скорость вращения, которой достиг игрок на карте.
