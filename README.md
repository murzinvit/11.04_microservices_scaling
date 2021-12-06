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
- Обеспечивать возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных таких как пароли, ключи доступа, ключи шифрования и т.п.

Обоснуйте свой выбор.

В качестве решения подойдёт k8s. </br>
1)Поддержка контейнеров: k8s поддерживает разные системы контейнеризации, к напримеру Docker, containerd </br>
2) Обеспечивать обнаружение сервисов и маршрутизацию запросов </br>
3) Обеспечивать возможность автоматического масштабирования </br>
В k8s есть функция autoscaling </br>
4) Обеспечивать явное разделение ресурсов доступных извне и внутри системы </br>
В k8s есть возможноть разграничить доступ к ресурсам при помощи NetworkPolicy и GlobalNetworkPolicy, namespaces, ingress-controller - маршрутизация </br>
трафика строго на определённый сервис </br>
5) Обеспечивать возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных</br>
таких как пароли, ключи доступа, ключи шифрования и т.п </br>
В k8s есть объект - secret для хранения чевствительных данных. Также есть vault для множества функционала по хранению секретов.</br>
Есть оператор - env для установки переменных среды в контейнеры. </br>


### Задача 2: Распределенный кэш * (необязательная)

Разработчикам вашей компании понадобился распределенный кэш для организации хранения временной информации по сессиям пользователей.
Вам необходимо построить Redis Cluster состоящий из трех шард с тремя репликами.
