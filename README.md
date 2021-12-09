## Домашнее задание к занятию "11.04 Микросервисы: масштабирование" </br>
### Задача 1: Кластеризация </br>
Предложите решение для обеспечения развертывания, запуска и управления приложениями. </br>
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия. </br>
Решение должно соответствовать следующим требованиям: </br>
- Поддержка контейнеров;
- Обеспечивать обнаружение сервисов и маршрутизацию запросов;
- Обеспечивать возможность горизонтального масштабирования;
- Обеспечивать возможность автоматического масштабирования;
- Обеспечивать явное разделение ресурсов доступных извне и внутри системы;
- Обеспечивать возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных таких как пароли, ключи доступа, ключи шифрования и т.п. Обоснуйте свой выбор.

#### В качестве закрытия всех перечисленных запрсов подойдёт Kubernetes. </br>

1) Поддержка контейнеров: </br>
`Kubernetes поддерживает только Container Runtime, которые работают с Container Runtime Interface (CRI).
Kubernetes поддерживает разные системы контейнеризации, например: Docker(containerd через dockershim), cri-o(RedHat), rkt` </br>

2) Обеспечивать обнаружение сервисов и маршрутизацию запросов </br>
`Kubernetes DNS: каждому сервису, созданному с помощью объекта Service, присваивается доменное имя, совпадающее с именем самого сервиса. Маршрутизация происходт
через kube-proxy и virtual ip` </br>

3) Обеспечивать возможность автоматического масштабирования </br>
`В Kubernetes есть функция autoscaling: в зависимости от нагрузки Kubernetes сам будет потдерживать min либо max к-во запущенных экземпляров сервиса` </br>

4) Обеспечивать возможность горизонтального масштабирования </br>
`Горизонтальное масштабирование в  Kubernetes это увеличение количества Pod с запущенными контейнерами, разумно распределенными по всему кластеру` </br>

6) Обеспечивать явное разделение ресурсов доступных извне и внутри системы </br>
`namespaces: это способ разделить кластер на индивидуальные зоны, где возможно использовать одни и те же имена объектов Kubernetes, что-то вроде пакетов в Java или пространств имен в С#.` </br>
`NetworkPolicy и GlobalNetworkPolicy: разграничение доступа внутри кластера, контроль исходящего и входящего трафика` </br>
`ingress-controller: маршрутизация трафика определённый сервис` </br>

7) Обеспечивать возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных
таких как пароли, ключи доступа, ключи шифрования и т.п </br>
`В k8s есть объект - secret для хранения чевствительных данных. Также есть vault для множества функционала по хранению секретов.
Есть оператор - env для установки переменных среды в контейнеры` </br>

### Задача 2: Распределенный кэш * (необязательная)

Разработчикам вашей компании понадобился распределенный кэш для организации хранения временной информации по сессиям пользователей.
Вам необходимо построить Redis Cluster состоящий из трех шард с тремя репликами.


---
work notes: </br>
https://www.devmind.ru/k8s/razvorachivaem-ha-cluster-redis-in-kubernetes </br>
https://andreyex.ru/ubuntu/chto-takoe-obnaruzhenie-servisov-v-kubernetes/amp/?q= </br>
https://habr.com/ru/company/true_engineering/blog/426821/ </br>
https://habr.com/ru/company/flant/blog/491320/ </br>
https://mcs.mail.ru/blog/10-populyarnyh-instrumentov-dlya-ci-cd </br>
https://ipsoftware.ru/posts-cloud/k8s-3-services/ </br>
