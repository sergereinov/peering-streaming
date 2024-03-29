*(надо же куда-то записать, почему бы и не сюда)*

# Пиринговый стриминг

### Декларируемый мотив
Конкурировать с серверами компаний-гигантов (twitch, youtube, mixer и т.п) может только поставщик услуг с сопоставимыми ресурсами. Или что-то принципиально другое - другая технология, другой подход, другой вид ресурса.

### User feelings
Пользователь выбирает продукт. Факторы выбора разнообразны.
- техническое качество потока, битрейт (8к на телевизор)
- доступность (без сбоев), удобство (включил и работает)
- контент (качество, тематика и т.д.)
- источник (инфлюенсер, группа и ко и т.п.)

Различные реализации идеи пирингового стриминга могут пренебрегать теми или иными факторами.


### Концепт
Стример-источник публикует где-либо "плеер", сгенерированный для трансляции и привязанный к текущему источнику (welcome page, сетевое расположение, доступные методы подключения к нему).

Зритель-потребитель открывает страницу сайта с "плеером" в браузере, подключается к источнику напрямую и начинает выступать в роли прингового узла, раздающего поток от источника дальше по пиринговой сети.

Очередной зритель, подключившись к источнику, получает некую "метрику" сети и несколько адресов работающих "прокси" узлов-ретрансляторов. Зритель, общаясь с "прокси" и перебирая доступные узлы, выбирает подходящие для себя источники. Рассматриваются параметры: состояние и текущая архитектура сети, пинги, достижимое совокупное запаздывание трансляции от "upstream" узлов и т.п.

Алгоритм перебора источников составляется исходя из принципа приоритетов для "онлайн-потока" - никакую часть потока нельзя отложить, нельзя воспроизвести с устаревшей точки, все составляющие пакеты под-потоков (слоев, срезов, каналов и т.п.) должны отражать более-менее один и тот же момент непрерывного потока. (Должны ли? Чат, например, может синхронизироваться менее строго, чем аудио/видео.)

Несмотря на то, что поток нельзя воспроизвести с "устаревшего" времени, "текущий момент" трансляции достигает каждого узла в пиринговой сети не одновременно. У каждого следующего "downstream" узла "текущий момент" запаздывает на время ретрансляции (от источника сквозь сеть) плюс время синхронизации и сборки в непрерывный поток из полученных под-потоков от "соседних" пиринговых узлов.

### Препятствия
- Типичные для p2p: преодоление NAT, граф сети и т.п.
- Нетипичные для p2p: нельзя потом дозагрузить недостающий начальный участок "файла", поскольку поток должен быть непрерывным и актуальным (хотя бы примерно быть похожим на "онлайн").
- Деанонимизация источника: уязвимость к атакам, публичность.
- Для многих узлов сети - больше чем двукратное увеличение объема трафика по сравнению с привычным потоковым вещанием: наборы upstreams + downstreams + резервирование каналов против приема одного upstream + резервирование (техн. деталей).

### ToDo
- Обсуждение
- Знакомство с исследованиями tor-сетей, алгоритмы, нисходящие деревья, графы и т.п.
- Знакомство с достижениями torrent-сетей.
- Знакомство с вариациями javascript резидентных прокси.
- NAT Port Mapping Protocol https://en.wikipedia.org/wiki/NAT_Port_Mapping_Protocol
- Port Control Protocol https://en.wikipedia.org/wiki/Port_Control_Protocol

### Интересные ссылки по теме
 - TCP против UDP https://habr.com/ru/company/oleg-bunin/blog/461829/
 - Обзор некоторых p2p (2006 год) https://www.researchgate.net/publication/3454643_A_Survey_and_Comparison_of_Peer-to-Peer_Overlay_Network_Schemes
 
### Истории по теме
 - Как сделать стриминговый сервис https://habr.com/ru/post/687360/
 - Пиринговый видеохостинг PeerTube https://habr.com/ru/news/776952/
 
