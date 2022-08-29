# cameras-verification-OCR
## Описание задачи

На финальном этапе производства каждый прибор должен проходить поверку, суть которой заключается в следующем: прибор устанавливается перед специальным табло, показывающим точное время до миллисекунд. Время, которое прибор видит с помощью видеокамеры на табло должно совпадать с временем, которое прибор видит с помощью интернет-соединения.

Это указывает на то, что прибор регистрирует изображение без задержек, что является критичным.

---

Необходимо создать нейросеть, которая будет распознавать время на табло на каждом кадре с видео, отснятом прибором и далее прибор будет сверять распознанное время с временем, полученным через интернет, сигнализируя об ошибках.

<b>Задача минимум</b>:
Нейросеть игнорирует часы, минуты и секунды и определяет только миллисекунды. Поскольку погрешность измеряется в миллисекундах, этого должно быть достаточно.

<b>Задача максимум</b>:
Нейросеть определяет время на фотографии полностью.

---

## База для обучения

Для создания базы использовалась видеокамера смартфона и сайт, показывающий точное до миллисекунд время. Видео было снято на камеру, затем с помощью библиотеки Open-CV нарезано на черно-белые кадры размером 128х128

---

## Итог

Во время исследования были испытаны три подхода: 

- классификатор; 
- система детектирования объекта; 
- система OCR. 

Несмотря на то, что все три подхода потенциально способны решить поставленную задачу, система OCR справляется заметно лучше.

Классификатор, при всей простоте реализации и высокой скорости, требует большую базу для обучения.

Детектор может обучиться на небольшой базе, тем не менее модель сложно составить и настроить, а inference-модель получается очень медленной.

Система OCR, в свою очередь, не требует очень большой базы для обучения, а inference-модель быстро и качественно работает. Модель не только точно распознает время, но и делает это быстро, даже на CPU.

Кроме того, большим преимуществом данного подхода (в отличие от классификатора) является то, что нет необходимости собирать большой датасет, что дает подходу гибкость и адаптируемость. Можно быстро переобучить модель для поверки на новом табло, другом формате времени или при изменении любых других условий.
