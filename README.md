# pydlts
## Краткое описание
### Назначение
Пакет модулей для обработки экспериментальных данных для моей кандидатской диссертации. Набор модулей реализует следующий функционал:
- чтение данных полученных с измерительной установки и их преобразование в единую таблицу (csv-файл);
- поиск оптимальных параметров модели на экспериментальных данных;
- построение графиков с результатами разных этапов обработки;
- автоматическая генерация материалов для отчётов в LaTex;
- пакетная обработка результатов измерений и идентификация моделей.

Чтобы поддерживать идентичность обработки разных комплектров результатов измерений, код оформлен ввиде пакета, который подключается с помощью `pip` и `setuptools`.

**Подробное описание работы модуля и решаемых задач можно найти в [отчёте о работе](https://github.com/AlekseiBogachev/pydlts/blob/main/docs/report/models_main.pdf).**

Документация на GitHub в процессе разработки.

### Типовой рабочий процесс
Обычно, обработка экспериментальных данных происходит в пакетном режиме и состоит из следующих шагов:
1. Пакетная обработка результатов измерений с помощью объекта `BatchDataReaderDLS82E` из модуля `pydlts.misc`:
    - сохранение csv-файлов с результатами измерений в формате, удобном для дальнейшей работы,
    - сохранение графиков, иллюстрирующих полученный результат.
1. Пакетная идентификация моделей с помощью объекта `BatchSingleExp` из модуля `pydlts.misc`:
    - сохранения csv-файлов с оптимальными найденными параметрами моделей,
    - генерация графиков, иллюстрирующих результаты.
1. Создание материалов для отчёта в LaTex на основе сохранённых результатов (пакетная обработка).

Также возможно обрабатывать результаты измерений индивидуально. В таком случае обработка будет состоять из следующих этапов:
1. Обработка результатов измерений (данных непосредственно с измерительной установки) с помощью объекта DataReaderDLS82E из модуля `pydlts.misc`.
1. Сохранение csv-файлов с результатами измерений в формате, удобном для дальнейшей работы, сохранение графиков, иллюстрирующих полученный результат.
Шаги 1 и 2 могут быть пропущены, если такая обработка уже выполнялась.
1. Идентификация параметров необходимой модели. Реализованы слеудющие 2:
    - моноэкспоненциальная модель с показателем нелинейности-неэкспоненциальности объект `SklSingleExpFrequencyScan` из модуля `pydlts.fsmodels`,
    - многоэкспоненциальня модель объект `SklMultiExpFrequencyScan` из модуля `pydlts.fsmodels`.
1. Создание необходимых графиков с помощью необходимых функций из `pydlts.fsplots`.
1. Создание отчёта вручную.

Пример результатов измерений, их обработки, идентификации моделей, графиков и отчёта представлен в репозитории [data-acquisition-and-report](https://github.com/AlekseiBogachev/data-acquisition-and-report).
