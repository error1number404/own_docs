[1] https://selectel.ru/blog/tcp-vs-udp/
## TCP — протокол транспортного уровня

TCP или Transmission Control Protocol, который используется для транспортировки сообщений между устройствами в сети.

В сети файлы не передаются целиком, а дробятся и передаются в виде относительно небольших сообщений. Далее они передаются другому устройству — получателю, где повторно собираются в файл.

Например, человек хочет скачать картинку. Сервер обрабатывает запрос и высылает в ответ требуемое изображение. Ему, в свою очередь, необходим путь или канал, по которому он будет передавать информацию. Поэтому сервер обращается к сетевому сокету для установки требуемого соединения и отправки картинки. Сервер дробит данные, инкапсулирует их в блоки, которые передаются на уровень TCP получателя при помощи IP-протокола. Далее получатель подтверждает факт передачи.

У протокола TCP есть несколько особенностей:

-   **Система нумерации сегментов.** TCP отслеживает передаваемые и принимаемые сегменты, присваивая номера каждому из них. Байтам данных, которые должны быть переданы, присваивается определенный номер байта, в то время как сегментам присваиваются порядковые номера.
-   **Управление потоком.** Функция ограничивает скорость, с которой отправитель передает данные. Это делается для обеспечения надежности доставки, в том числе чтобы компьютер не генерировал пакетов больше, чем может принять другое устройство. Если говорить простым языком, то получатель постоянно сообщает отправителю о том, какой объем данных может быть получен.
-   **Контроль ошибок.** Функция реализуется для повышения надежности путем проверки байтов на целостность.
-   **Контроль перегрузки сети.** Протокол TCP учитывает уровень перегрузки в сети, определяемый объемом данных, отправленных узлом.
## Примеры применения сетевого протокола TCP

Протокол TCP гарантирует доставку, а также обеспечивает целостность данных, передаваемых в сети. Поэтому он применяется для передачи данных, которые чувствительны к нарушению целостности, — например, текстов, файлов и т.п. Вот несколько протоколов, которые работают по TCP: 

-   SSH, FTP, Telnet: в данных протоколах TCP используется для обмена файлами.
-   SMTP, POP, IMAP: протоколы, где TCP отвечает за передачу сообщений электронной почты.
-   HTTP/HTTPS: протоколы, где TCP отвечает за загрузку страниц из интернета.

Эти примеры работают на уровне приложений стека TCP/IP и передают данные вниз к TCP, на транспортный уровень

## Строение протокола TCP

![[TCP under the hood.png]]

В каждый пакет данных TCP добавляет заголовок общим объемом в 20 байт (или октетов), в котором содержатся 10 обязательных полей:

-   **Порт источника** — порт устройства-отправителя.
-   **Порт назначения** — порт принимающего устройства.
-   **Порядковый номер.** Устройство, инициирующее TCP-соединение, должно выбрать случайный начальный порядковый номер, который затем увеличивается в соответствии с количеством переданных байтов.
-   **Номер подтверждения.** Принимающее устройство увеличивает этот номер с нуля в соответствии с количеством полученных байтов.
-   **Сдвиг данных TCP.** Данный параметр определяет размер заголовка, чтобы система могла понять, где начинаются данные.
-   **Зарезервированные данные** — зарезервированное поле, значение которого всегда равно нулю.
-   **Флаги управления.** TCP использует девять флагов для управления потоком данных в определенных ситуациях — например, при инициировании сброса сессии.
-   **Размер окна** — самая важная часть заголовка TCP. Это поле используется получателем для указания отправителю объема данных, которые он может принять.
-   **Контрольная сумма**. Отправитель генерирует контрольную сумму и передает ее в заголовке каждого пакета. Принимающее устройство может использовать контрольную сумму для проверки ошибок в полученном файле.
-   **Срочный указатель** — это предлагаемая протоколом возможность помечать некоторые байты данных тегом «Срочно» для их пересылки и обработки вне очереди.
-   **Поле опции.** Может использоваться для расширения протокола или его тестирования.