# Sensorimotor-rhythm-research
Sensorimotor rhythm (mu-rhythm) is a type of electrical activity of the brain that occurs while moving or observing the movements of other people. Studies show that children with impaired speech development often experience a change in sensorimotor rhythm, which may indicate a violation of the functioning of the brain responsible for speech processes.

The study that uses this repository examines the correlations between the mu-rhythm of normotypic children aged 3-4 years and their speech development (speech development is assessed using the PLS-5 methodology).

Описание процесса обработки данных: 
Процесс обработки и предобработки проводился в интерактивной среде Jupyter Notebook для языка программирования Python с использованием функций библиотеки MNE (https://mne.tools/).
Процесс обработки данных условно делился на 3 этапа: 

Первый этап – понижение частоты дискретизации исходных записей до 500;
Второй этап – стандартный препроцессинг;
Третий этап – подсчет абсолютной плотности спектральной мощности(PSD).

Первый этап
Первый этап включал в себя даунсэмплинг данных до частоты дискретизации 500 и сохранения исходных данных в формате fif. 

Второй этап 
Далее выполнялся стандартный протокол препроцессинга для условий из двух парадигм: Resting State (mu) и Natural Listening (NL). В рамках данного исследования из парадигмы NL были взяты фрагменты: фракталы перед сказкой 30с и фракталы с сказкой (Golden duck) 30 c. Из парадигмы mu были взяты фрагменты пассивного сжатия рук (дважды ведущая рука и один раз противоположная) и 2 фрагмента по 45с с закрытыми глазами. Для каждой парадигмы был создан свой скрипт для препроцессинга: Preprocessing MU и Preprocessing NL. 
Preprocessing NL.
Загружается файл содержащий сказку Golden duck (NL_2/NL_1), происходит фильтрация (фильтр нижних частот: 50 Гц, фильтр верхних частот: 1 Гц), поиск events, и выделение сегментов по меткам s1 – фракталы перед сказкой  и s12 фракталы с сказкой. 
Если метки обнаружены мы выделяем им соответствующий индекс, и обрезаем запись по меткам s1 и s12 на фрагменты по 30 секунд. Далее их сшиваем для последующего препроцессинга. После идет выделение плохих каналов (также есть возможность выделения плохих сегментов по всем отведениям), далее следует интерполяция плохих каналов, после чего следует ICA с интегрированным модулем ALICE, который автоматически выделяет компоненты содержащие глазодвигательные и мышечные артефакты.
Послу удаление плохих компонентов из ICA, происходит ре-референсинг записи относительно общего усредненного референта. Далее выделяем из записи нужные нам фрагменты: выделяем фрагмент видео с фракталами и видео с фракталами с аудио - нагрузкой (сказка Golden duck) и сохраняем их. 
После сохранения каждого фрагмента, как целой записи по 30 секунд, вы делим каждый фрагмент на эпохи длительностью 2 секунды, после чего удаляем автоматически плохие эпохи (threshold = 360e-6) и сохраняем файлы. На этом этапе препроцессинг заканчивается. 
Для парадигмы Resting State (mu) протокол обработки в целом такой же, за исключением того, что там сначала вся запись ЭЭГ проходит стандартный препроцессинг, после которого идет выделение нужных сегментов. 

Процессинг
Процессинг подразумевает собой работу уже с чистыми данными, в ходе которой мы рассчитываем абсолютную плотность спектральной мощности (power spectral density (PSD)) для всех экспериментальных условий в  диапазонах частот 6-13 Гц  и 13-30 Гц по каналам С3 и С4. 

