## 7.6.  Написание собственных провайдеров для Terraform

> Бывает, что
> общедоступная документация по терраформ ресурсам не всегда достоверна,
> в документации не хватает каких-нибудь правил валидации или неточно описаны параметры,
> понадобиться использовать провайдер без официальной документации,
> может возникнуть необходимость написать свой провайдер для системы используемой в ваших проектах
>	
> Давайте потренируемся читать исходный код AWS провайдера, который можно склонировать от сюда: https://github.com/hashicorp/terraform-provider-aws.git. 
> Просто найдите нужные ресурсы в исходном коде и ответы на вопросы станут понятны.
>
> Найдите, где перечислены все доступные resource и data_source, приложите ссылку на эти строки в коде на гитхабе.
> Для создания очереди сообщений SQS используется ресурс aws_sqs_queue у которого есть параметр name.
> С каким другим параметром конфликтует name? Приложите строчку кода, в которой это указано.
> Какая максимальная длина имени?
> Какому регулярному выражению должно подчиняться имя?
### *Найдите, где перечислены все доступные resource и data_source, приложите ссылку на эти строки в коде на гитхабе.*

Из презентации к лекции сказано, что в provider.go можно задать доступные ресурсы (блок resources)и источники данных (блок data), также если перейти в `terraform-provider-aws/main.go`, то тело провайдера находится `terraform-provider-aws/internal/provider/provider.go`

#### Переходим в provider.go: 
* Ссылка на(DataSourcesMap) коллекцию доступных источников данных - 
https://github.com/hashicorp/terraform-provider-aws/blob/7230993c7834dd03e898efc959bbf1dc831d0d42/internal/provider/provider.go#L413
* Ссылка на (ResourcesMap) список доступных ресурсов этого поставщика -
https://github.com/hashicorp/terraform-provider-aws/blob/7230993c7834dd03e898efc959bbf1dc831d0d42/internal/provider/provider.go#L916
				
### *Для создания очереди сообщений SQS используется ресурс aws_sqs_queue у которого есть параметр name.* *С каким другим параметром конфликтует name? Приложите строчку кода, в которой это указано.* 

* Ссылка на строчку кода: https://github.com/hashicorp/terraform-provider-aws/blob/8a04c06a6cc5eeb7ad478f2451d8e07a31550100/internal/service/sqs/queue.go#L87

### *Какая максимальная длина имени?*

* К сожалению не удалось найти явного указания на проверку максимальной длины и общим поиском нашла..

Ссылка на строчку кода: https://github.com/hashicorp/terraform-provider-aws/blob/8a04c06a6cc5eeb7ad478f2451d8e07a31550100/internal/service/sqs/queue.go#L407

###  *Какому регулярному выражению должно подчиняться имя?*
Ссылка на строчку кода: https://github.com/hashicorp/terraform-provider-aws/blob/8a04c06a6cc5eeb7ad478f2451d8e07a31550100/internal/service/sqs/queue.go#L422



