# Вводная часть

В качестве темы диплома выступает поведенческая аналитика, а именно детекция аномальных событий в видеонаблюдении([ссылка на paperswithcode](https://paperswithcode.com/paper/real-world-anomaly-detection-in-surveillance)).

# Используемые данные
Для обучения модели и проверки результатов в качестве основного набора данных будет использоваться [UCF-CRIME](https://paperswithcode.com/dataset/ucf-crime). Этот датасет можно скачать в [DROPBOX](https://www.dropbox.com/sh/75v5ehq4cdg5g5g/AABvnJSwZI7zXb8_myBA0CLHa?dl=0), почти каждый из архивов весит меньше 5 Гб, кроме Training-Normal-Videos(~ 35 Гб), поэтому полностью хранить их в гугл драйве не предоставляется возможным.

Краткое описание:
  [Ссылка на статью]( https://arxiv.org/pdf/1801.04264v3.pdf )

Введение: 
    Поднимается тема использования видеокамер для отслеживания "аномальных" событий.
Очевидно, что дать конкретное определение аномального события не предоставляется возможным,
потому их очень много и всё зависит от конкретных ситуаций. И встает вопрос, 
как создать систему, способную автоматически сигнализировать о дивиантном поведении.
Вариант с определением нормального поведения, когда отклонение от нормы ведет к предсказанию
аномального поведения, не подходит, посколюку отпять поднимается вопрос, что такое "нормально".
В данной статье презентуется MIL подход для решения поставленной задачи с использованием 
weakly labeled data  (i.e. video-level labels – normal or abnormal, 
		which are much easier to obtain than temporal annotations).

Предложенный подход: 
	Сначала экземпляр видео делится на некоторое количество сегментов; 
группа сегментов исходного видео образуют экземпляр мешка(bag). 
Далее используя аномальные и нормальные мешки, обучаем модель на MIL с помощью ranking loss + l2.
Во время обучения всё видео маркируется соответствующим классом: Ba - positive bag(содержится аномалия) и
Bn - negative bag(без аномалий). Затем предлагается, что целевая функция у аномальних сегментов будет больше,
чем нормальных, что поможет обучить модель точнее определять класс. Конечная формула лосса на стр. 4 уравнение (7).

Далее идут детали реализации и подготовки данных.
