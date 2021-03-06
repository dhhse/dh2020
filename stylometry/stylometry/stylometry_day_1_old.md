# Попрактикуемся в стилометрии

(на всякий случай: инструкция по установке stylo [тут](https://docs.google.com/document/d/1WyUeY6Qi7rlNRg73Bmo0FSPH3dwGjSxzS1SAi0D3uqw/edit?usp=sharing), по началу работы со stylo — [тут](https://docs.google.com/document/d/19vcol7KV80U4LnzpUVgi8DiTOmEUg6BOqp-vSddCUOo/edit?usp=sharing))

[Презентация Stylo in a nutshell](https://computationalstylistics.github.io/stylo_nutshell/)

[Документ STYLO_HOWTO (очень полезный)](https://drive.google.com/file/d/1duyYsHYKnkmKQe28xv4t8wB202vtZCEI/view?usp=sharing)

[Оф.сайт разработчиков Stylo](https://computationalstylistics.github.io/)

[Гитхаб репозиторий Stylo](https://github.com/computationalstylistics/stylo)

# Попрактикуемся!

## 0. Лукьяненко versus Донцова (тестируем Stylo)

[Тексты](stylometry_texts/0_Лукьяненко%20Донцова.zip)

Получите такое (на настройках по умолчанию)

![lukdon](pics/lukdon_ca.png)

## 1. Пушкин, Лермонтов, Гоголь (тестируем Stylo)

[Тексты](stylometry_texts/1_pushkin_lermontov_gogol.zip)

### Получите такое (на настройках по умолчанию)

![pgl100](pics/pgl_100.png)

### Теперь попробуйте 200 MFW

Надо в интерфейсе Stylo пойти во вкладку FEATURES и выставить там минимум и максимум на 200.

![set200](pics/set200mfw.png)

Получите такое:

![pgl_200](pics/pgl_200.png)

### Теперь попробуйте 300 MFW

![pgl_300](pics/pgl_300.png)

Авторский сигнал устойчив!  

## 2. Достоевский, Толстой, Тургенев, Гончаров (тестируем Stylo)

[Тексты](stylometry_texts/2_fourteen_russian_novels.zip)

### Получите такое (на настройках по умолчанию) 

![14_clust](pics/14_clust.png)

### Посмотрим на цифры, стоящие за визуализацией

Надо в интерфейсе Stylo пойти во вкладку OUTPUT и кликнуть там Save distance table.
Когда stylo отработает, в рабочей папке появится файл с названием вида "distance_table_[...]txt" 
По сути это CSV-таблица (вернее, DSV, потому что разделитель тут не запятая, а вовсе даже пробел.) 
Эту табличку можно открыть в любом табличном редакторе (в LibreOffice для этого достаточно поменять расширение файла на .csv; в Excel проще ничего не менять, а пойти в "Get data"/ "get external data"/ "получить данные" и там нажать From Text / из текста, а потом выбрать файл). 
Для наглядности табличку здорово раскрасить:

![pic](pics/distances_14.png)

###  Изменится ли что-то при 300 MFW?

![pic](pics/14_clust_300.png)

Авторский сигнал снова устойчив!

###  А можно ли объединить в одном эксперименте — сразу несколько прогонов на разных настройках (100? 200? 300 слов)? Да!Для этого есть Bootstrap Consensus Tree!

Надо в интерфейсе Stylo пойти во вкладку STATISTICS:

![pic](pics/switch2bootstrap.png)

А потом выставить диапазон и шаг (Increment) во вкладкe FEATURES:

![pic](pics/increment4boot.png)

#### Результат

![pic](pics/bootstrap14.png)

### Как в качестве признаков использовать не целые слова, а цепочки символов (символьные n-gram'ы)? 

Вкладка FEATURES, поменять words на chars:

![pic](pics/words2chars.png)


Так мы будем измерять частотности не слов. 

![pic](pics/14_clust_100_chars.png)

Авторский сигнал ВСЕ ЕЩЕ устойчив! 

Загляните в файл wordlist.txt и убедитесь, что теперь признаками для нас выступают не слова. 

### В этом месте хочется попытаться осмыслить: ЧТО же мы все-таки измеряем таким образом? И почему оно так устойчиво работает.

"I think we should lock linguists and philologists in a room and not let them leave it until they explain what is happening" (Ян Рыбицкий на одном из стилометрических докладов во время конференции DH 2019 в Утрехте)


### Задание: сломайте этот тест!

Выставить такие Features, чтобы авторы кластеризовались с ошибкой (изменение языка с Other на English не считается, это слишком тупо).



# Окей, Даня, хватит тестов! Давай что-нибудь настоящее постилометрим!



## 3. Сурков и Дубовицкий (боевое применение  Stylo)

[Тексты -- по 2](stylometry_texts/3_surkov.zip)

![surkov small](pics/surkov_2_each.png)

[Тексты, расширенный набор](stylometry_texts/4_surkov_extended.zip)

![surkov big](pics/surkov_big.png)

## Знакомые с Gephi могут попытаться получить еще такую визуализацию стилометрической близости:

![surkov](pics/surkov_network.png)

Менее знакомые, но чувствующие в себе силы могут воспользоваться [моей общей инструкцией](https://docs.google.com/document/d/1w3hWna5_BF60jxLf7Tn_sv6GyOCkYJ9ad4kQFU9mWLg/edit?usp=sharing) по визуализации CSV-таблицы с ребрами при помощи Gephi (вам будет не очень релевантна часть про размеры узлов). 

Но вообще построение стилометрических сетей мы пройдем отдельно. 


### Задание для энтузиастов: улучшить эксперимент с Сурковым

Это пока плохое доказательство, т.к. может вносить искажение разность жанров. Хорошо бы добавить еще парочку документов типа "сборник статей" (как Surkov_Statyi.txt), но принадлежащие НЕ суркову, а кому-то еще. Сделать пару таких и подмешать в корпус



## 4. Шолохов и компания (боевое применение  Stylo)

[Тексты: Шолохов, Крюков, Краснушкин](stylometry_texts/sholokhov.zip)

### Попробуйте 100 MFW

![pic](pics/sholokhov_small_100.png)


### Попробуйте 200 MFW

![lukdon](pics/sholokhov_small_200.png)

### Попробуйте 300 MFW

![lukdon](pics/sholokhov_small_300.png)

### Попробуйте Bootstrap Consensus Tree 100 -- 300 с шагом 10
![pic](pics/sholokhov_small_bootstrap.png)

Сетевая визуализация тех же стилометрических близостей:

![pic](pics/sholokhov_small_network.png)

[Тексты: Шолохов, Крюков, Краснушкин + Серафимович, Платонов](stylometry_texts/sholokhov_extended.zip)

## Расширенный эксперимент Шолохов++ — добавим Серафимовича и Платонова 

### пробуйте сами :)

...

А вот и полноценная научная статья о том, что думает Delta про авторство Шолохова: 
[Н.П. Великанова, Б.В. Орехов. Цифровая текстология: атрибуция текста на примере романа М.А. Шолохова «Тихий Дон»](http://nevmenandr.net/personalia/QuietDon.pdf)


## [Все тексты для практики, использованные выше (ссылка на папку)](stylometry_texts)
