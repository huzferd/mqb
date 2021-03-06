disqus: https-mqb-readthedocs-io
# Управление климатической системой

### Отображение скорости вращения вентилятора Климатроника в автоматическом режиме

```
Блок 08 → Кодирование
> Индикация режима вентилятора в автоматическом режиме → активировать 
> 11 байт - вместо значения 00001110 поставить значение 01001110 (6 бит → включить)
→ Применить (с перезагрузкой блока)
	
(в длинном кодированим и изменить третий байт с С0 на 40, то есть изменить седьмой бит с 1 на 0)
```
```
ODIS E: AC Automat -> MAS06416 -> Включ.
```

??? note "Кодирование в VCDS"    
    08 - Климат-контроль  
    Кодирование - 07 → Длинное кодирование  
    Байт 11 → Бит 6 → ставим галочку  
    Если нет 6 бита, можно изменить только сам код - вместо значения 00001110 поставить значение 01001110  
    Выход  
    Сохранить  
    ![Screenshot](../images/climate.jpg)    
    
??? note "Кодирование в OBD11"   
    08 Электроника отопителя и климатической установки → Длинное кодирование  
    > Индикация режима вентилятора в автоматическом режиме:  
    Старое значение: не активир.  
    Новое значение: активир.   

### Сохранение последней стадии нагрева передних сидений

!!! tip ""
    Описание/Цель активации: Навсегда запоминает последнюю выбранную интенсивность обогрева сидения водителя. Просто удобная штука для более тонкой настройки автомобиля под себя.

```
Блок 08 → Адаптация 
> Speicherung der Sitzheizungsstufe Fahrer (Retention of driver’s seat heater level) → активировать 
→ Применить
> Speicherung der Sitzheizungsstufe Beifahrer активировать (Retention of passenger’s seat heater level) → активировать
→ Применить
```
	
??? note "Кодирование в OBD11"	
    08 Электроника отопителя и климатической установки → Адаптация  
    > Сохранение уровня нагрева сиденья водителя  
    Старое значение: акт. на 10 мин.  
    Новое значение: акт.  
    > Сохранение уровня нагрева сиденья переднего пассажира  
    Старое значение: не акт.  
    Новое значение: акт.  
	
### Автоматический Подогрев рулевого колеса в зависимости от наружной температуры воздуха

!!! tip ""
     Существует 2 режима:  
     Lenkradtemperatur - по датчику в руле
     Aussentemperatur - по датчику наружней температуры
     
     Lenkradtemperatur - включается при зажигании, если рулевое колесо имеет низкую температуру. Актуально при движении на трассе
     Aussentemperatur - работает всегда

```
Блок 8 → Кодирование
> Электроника отопителя и климатической установки / Heated_steering_wheel_automatic_mode
> Подогрев рулевого колеса, автоматический режим: «не установл» на нужное значение
→ Применить
```
    
??? note "Кодирование в OBD11"
    08 Электроника отопителя и климатической установки → Длинное кодирование  
    > Подогрев рулевого колеса, автоматический режим:  
    
??? note "Кодирование в VCDS"
    08 - Климат-контроль  
    Кодирование - 07 → Длинное кодирование  
    Байт 13 →   
    > Бит 2 - по датчику в руле  
    > Бит 3 - по наружней температуре  
    Одновременно оба бита включать нельзя!
    Если выбора битов нет, то можно поменять значение самого байта: 14 (по датчику в руле) или 18 (по наружней температуре)  
    Выход    
    Сохранить    
    ![Screenshot](../images/wheel.PNG)    

### Подогрев зеркал вместе с задним стеклом

!!! note ""
     Данная кодировка не работает для автомобилей Tiguan

```
Блок 09 -> Кодирование
> Подогрев зеркал включен, пока включен обогрев заднего стекла
выбираем «Вкл»
→ Применить (с перезагрузкой блока)
```
		
??? note "Кодирование в VCDS"    
    09 - Электроника бортовой сети  
    Кодирование - 07 → Длинное кодирование   
    Байт 15 → Бит 3: Mirror Heating ON while Rear Window Heater ON  
    Выход  
    Сохранить  
    ![Screenshot](../images/rear.jpg)  

### Увеличение времени обогрева заднего стекла

*Особенности
	Вводимое значение измеряется в секундах, например 1200 / 60 = 20 (минут)
	
	Блок 09 → Адаптация
	> (03)-Window heater → вводим нужное значение 
	→ Применить
	> Обогрев стекла - Abschalttemperatur fuer Heckscheibenheizung
	Старое значение: 35.0 °C
	Новое значение: 38.0 °C
	→ Применить

> логин-пароль 31347

### Увеличение температуры и времени обогрева переднего и заднего стекла

*Особенности
	Вводимое значение измеряется в секундах, например 1200 / 60 = 20 (минут)

	Блок 09 → Адаптация
	> (03)-Window heater → вводим нужное значение
	→ Применить

	Изменение температуры и времени обогрева заднего стекла
	Aдаптация — Обогрев стекла
		— Heckscheibenheizung Zeitwert: с «320 с» на «640 с»
		— Abschalttemperatur fuer Heckscheibenheizung: с «35.0 °C» на «38.0 °C»
	
	Изменение температуры и времени обогрева лобового стекла
	Aдаптация — Обогрев стекла
		— Frontscheibenheizung Zeitwert: «320 с» на «640 с»
		— Abschalttemperatur fuer Frontscheibenheizung: «35.0 °C» на «38.0 °C»

> логин-пароль 31347

### Активация Air Care Climatronic

!!! note ""
    Когда AirCare активен, система Climatronic начинает пропускать воздух через салонный фильтр в режиме рециркуляции совместно с подачей свежего воздуха снаружи. В результате этого воздух в салоне Вашего автомобиля очищается наиболее эффективно и его качество улучшается благодаря интенсивному отсеиванию мелких частиц.  
    Для функционирования этой опции рекомендуется использовать гипоаллергенный салонный фильтр. Он служит для эффективного отделения твердых частиц пыли и пыльцы, которые являются серьезной проблемой в городских условиях, особенно в весенне-осенний сезоны.

!!! warning ""
    Для активации данного функционала потребуется:  
    - Блок Climatronic с ПО не ниже 1403;  
    - Блок Gateway с ПО не ниже 1244/2244;  
    - Блок Infotainment MIB (STD2/HIGH2) от 2016 г.в. (от 2017 м.г.);  

```
Блок 08 → кодирование
> [LN]_filtering_interior_air
выбираем [VN]_installed
→ Применить (с перезагрузкой блока)
```

??? note "Кодирование в VCDS"    
    08 - Климат-контроль  
    Кодирование - 07 → Длинное кодирование  
    Байт 15 → Бит 5-6 → 20 Фильтрация воздуха салона, установл.  
    Выход  
    Сохранить  