# Как читать график Connections quota utilization


## Описание сценария {#case-description}

Необходимо разобраться, как читать график `Connections quota utilization`.

## Решение {#case-resolution}

`Connections quota utilization` — это процент от лимита (**50 000**) на количество одновременно установленных TCP/UDP-соединений на виртуальной машине. Для каждого соединения мы храним некоторое состояние, которое живет в случаях:

* пока активно сетевое соединение,
* пока не произошло закрытие сессии (`FIN`/`RST`),
* пока не пройдёт три минуты после последнего пакета.

{% note info %}

Некоторое ПО, например, оверлейные сети Docker Swarm, генерируют большое количество незакрытых UDP-соединений. В результате лимит может быть быстро исчерпан. Для обхода этого ограничения можно включить опцию Superflow, которая позволяет увеличить лимит на количество соединений за счёт того, что большие группы соединений учитываются гипервизором как одно.

{% endnote %}

При работе сетевой подсистемы ВМ по умолчанию задействуется определенная часть ресурсов ее vCPU.

Например, несколько сетевых соединений в некоторых случаях могут объединяться гипервизором в одну сессию (flow). 
Этот подход отличается от «программно-ускоренной сети» – другого способа ускорить операции ввода-вывода на ВМ.

Если при создании ВМ для нее была включена **Программно-ускоренная сеть**, то входящие сетевые пакеты будут обработаны на отдельных выделенных ядрах гипервизора. Это позволяет снизить уровень потребления vCPU виртуальной машины, делая работу сервисов, запущенных на ВМ, более стабильной при значительном уровне нагрузки.

Подробнее пишем [здесь](../../../compute/concepts/software-accelerated-network).