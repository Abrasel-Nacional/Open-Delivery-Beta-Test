# Changelog

Mudanças efetuadas durante o periodo de Beta Test serão documentadas aqui.

## [1.0.0-rc.11] - 21/02/2022

* [[Issue #76](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/76)] - Adição da entidade `ITEM` como opção do campo  `entityType`  no endpoint [POST /merchantUpdate](https://abrasel-nacional.github.io/docs/#operation/menuUpdated)  .
* [[Issue #75](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/75)] - Arrumada as descrições dos campos `preparationStartTime` e `takeoutDatetime` do endpoint [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/paths/~1orders~1{orderId}/get) para deixar mais clara a função dos campos. 
* [[Issue #73](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/73)] - Alterada a descrição dos campos de `latitude` e `longitude` de todos os endpoints que continham estas informações, removendo a descrição `decimal places <= 5` que estava incorreta.
* Retirada a obrigatoriedade de preenchimento dos campos `latitude` e `longitude` nos endpoints :
  - [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
  - [POST /logistics/availability](https://abrasel-nacional.github.io/docs/#tag/logisticPrice)
* Adição do enumerador`INVALID_ADDRESS` como opção de preenchimento do campo `rejectReason` do endpoint [POST /deliveryUpdate](https://abrasel-nacional.github.io/docs/#operation/newLogisticEvent)

* Acrescentados novos [Guidelines](https://abrasel-nacional.github.io/docs/#section/General-Guidelines):
	- Todas as datas devem ser preenchidas considerando o horário em UTC
	- Informações de como prover as {baseURLs} dos endpoints
	- [[Issue #71](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/71)] - Instruções de como enviar parametros de arrays em requests.
	
## [1.0.0-rc.10] - 04/02/2022
### Mudanças com quebra de contrato:
* Os nomes dos campos do endpoint [/oauth/token](https://abrasel-nacional.github.io/docs/#operation/getToken) foram alterados para atender o padrão proposto pelo oAuth, seguindo as regras descritas nas páginas do padrão:

  - Request: (https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)
    -   `clientId` para `client_id`
    - 	`clientSecret` para `client_secret`
    -	`grantType` para `grant_type`

  - Response: (https://www.oauth.com/oauth2-servers/access-tokens/access-token-response/)
    -   `accessToken` para `access_token`
    - 	`tokenType` para `token_type`
    -	`expiresIn` para `expires_in`
		
* Foram efetuadas duas alterações no endpoint [/events:polling](https://abrasel-nacional.github.io/docs/#operation/pollingEvents)
  - Foi retirada a obrigatoriedade do campo `eventType` no request. Ao não informar este campo, a ORDERING APPLICATION deverá retornar todos os eventos que ainda não foram ack do merchant efetuando o polling, independente do `eventType`.

  - [[Issue #69](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/69)] - A resposta HTTP 200 do endpoint estava incorretamente retornado um objeto simples. A resposta foi corrigida para retornar um array de objetos.  
  de:  
  `{ "eventId": "string", "eventType": "CREATED", "orderId": "string", "orderURL": "http://example.com", "createdAt": "2019-08-24T14:15:22Z" }`  
  para:  
  `[ { "eventId": "string", "eventType": "CREATED", "orderId": "string", "orderURL": "http://example.com", "createdAt": "2019-08-24T14:15:22Z" } ]`

### Outras mudanças
* Foi adicionado um novo campo nos endpoint [/events:polling](http://localhost:9093/-307623811#operation/pollingEvents) e [/orders/{orderId}](http://localhost:9093/-307623811#tag/ordersDetails/paths/~1orders~1{orderId}/get)  chamado `sourceAppId` para ser utilizado pelas empresas que efetuam o papel de Hub.
* [[Issue #67](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/67)] - Retirada a obrigatoriedade do campo `clientId` do metadata do objeto Event do pedido para os eventType = `CONFIRMED`. 
* [[Issue #70](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/70)] - Como o formato do campo `MerchantId` possui uma definição bem especifica, o format `UUID` foi removido deixando o campo apenas como `string`. Isso afeta os objetos e parametros que utilizam o Id do merchant. Os lugares afetados são:
  - Parametros do request:
    - /merchantStatus
    - /events:polling
    - Order Webhook
    - Delivery Order Webhook
  - Objetos:
    - Merchant 
    - Order
    - DeliveryOrder
    - DeliveryOrderEvent
    - DeliveryAvailabilityPrice
    - DeliveryOrderDetails
    
* Adicionada uma nova seção chamada [How to Start](https://abrasel-nacional.github.io/docs/#section/How-to-Start-(Setup-Guide)), para auxiliar as empresas nas implementações e parametrizações.

## [1.0.0-rc.9] - 23/12/2021
* [[Issue #58](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/58)] - Adicionado o campo `reference` em todos os objetos relacionados a endereço:
Objetos afetados:
	- `Address`
	- `Order`
* [[Issue #61](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/61)] - Corrigido os campos `deliveryPrice` que estavam referenciando um schema incorreto. Endpoints afetados:
	- `Delivery Tracking`
	- `Delivery Availability and Pricing`
* [[Issue #62](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/62)] - Adicionado o HTTP code **204** no endpoint `GET /events:pooling` a ser utilizado para os casos de não existir novos eventos.
* [[Issue #63](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/63)] 
	- Removido o texto descritivo do schema do endpoint `POST /orders/{orderId}/requestCancellation`. 
	- Corrigida a opção `INTERNAL_DIFFICULTIES_OF_THE_RESTAURANT` que estava formatada de maneira incorreta do mesmo endpoint acima. 

## [1.0.0-rc.8] - 14/12/2021
### Mudanças com quebra de contrato:
* [[Issue #50](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/50)] - Todos os atributos `latitude` e `longitude` tiveram seu formato alterado para `number` com precisão de 5 casas decimais.
Objetos afetados:
	- `Address`
	- `Polygon`
	- `GeoRadius`
	- `Order`
	- `GeoLocalization`
	
### Outras mudanças
* [[Issue #52](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/52)] - Retirada a obrigatoriedade de preenchimento do  campo `image` nos objetos `Item` e `Category`.
* [[Issue #46](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/46)] - Recomendada a utilização do padrão **ISO 3166-2** nos campos de `state` nos objetos de endereços.


## [1.0.0-rc.7] - 26/11/2021
### Mudanças com quebra de contrato:
* [[Issue #43](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/43)] - Alterado os atributos `out_of_stock_items` e `invalid_items` do endpoint `/orders/{orderId}/requestCancellation` para `outOfStockItems` e `invalidItems` corrigindo-os para o padrão camelCase utilizado no restante da documentação.

### Outras mudanças
* Reestruturação do menu lateral, separando melhor as seções:
  * Adicionado uma seção 'Table of Contents';
  * Separação da documentação por versões (1.0.0-rc.X e 1.1.0-rc.X);
* Removido o `format` do atributo `description` do `nutricionalInfo` do objeto `item` do Merchant que estava incorretamente marcado como "UUID";
* Corrigida a grafia da opção `BURGUER` para `BURGER` no atributo  `merchantCategories` do objeto `BasicInfo` do Merchant.

Correções nos exemplos 
* [[Issue #48](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/48)] - Corrigido todos os campos `country` para representar a sua descrição de forma correta;
* [[Issue #49](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/49)] - Corrigido todos os campos  `currency` para representar a sua descrição de forma correta;
* [[Issue #51](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/51)] - Corrigido todos os campos de "image" para melhor representar o schema do objeto `Image`;
* [[Issue #53](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/53)] - Corrigida a ortografia de todos os campos `itemId` no exemplo do `/merchant` (`itemid` para `itemId`);
* [[Issue #54](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/54)] - Corrigido alguns campos `id` no exemplo do `/merchant` que tinham uma aspas adicional 
* [[Issue #55](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/55)] - Corrigido o campo `contactPhone` no exemplo do `/merchant`
* [[Issue #56](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/56)] - Corrigido o objeto `services` no exemplo do `/merchant`
* [[Issue #57](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/57)] - Corrigido o objeto `weekHours` no exemplo do `/merchant`
* Corrigido o campo `contactEmails` no exemplo de `/merchant`
* Corrigido o objeto `availability` no exemplo do `/merchant`  

## [1.0.0-rc.6] - 18/10/2021
### Mudanças com quebra de contrato:
* [[Issue #32](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/32)] 
  - Removido todos os `@` da frente dos atributos `@id`. Agora todos os atributos estão padronizados como `id`.  
  - Removido todos os campos `@type` das entidades do `/merchant`.
  - Removido o `@` do atributo `@type` do objeto `orders` que foi renomeado para `type` (sem o @).
![image](https://user-images.githubusercontent.com/80956588/137760918-3f3185b8-0696-4060-ab86-87b6ba05eb39.png)

* [[Issue #35](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/35)] - Corrigido o nome do atributo **`X-App-MerchanId`** do parametro de **header** no request do webhook de notificação de pedido para **`X-App-MerchantId`**.
* [[Issue #39](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/39)] - Alterado os retornos dos seguintes endpoints de `HTTP 200` para `HTTP 202`:
  - `/orders/{orderId}/confirm`
  - `/orders/{orderId}/requestCancellation`
  - `/orders/{orderId}/readyForPickup`
  - `/orders/{orderId}/dispatch`
 
 ### Outras mudanças
* Reestruturação do menu lateral, separando melhor as seções.
* Corrigido alguns campos dos exemplos, para refletir corretamente a descrição dos campos.

## [1.0.0-rc.5] - 11/10/2021
### Mudanças com quebra de contrato:
* [[Issues #19](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/19) | [#20](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/20) | [ #27](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/27) | [ #33](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/33)] - Reformulação de toda a estrutura da entidade `SERVICE_AREA`. Os campos da entidade receberam uma nova estrutura facilitando o cadastro, bem como integrando a parte de taxas e distancia de entrega. Com isso a entidade `SERVICE_AREA_FEE` foi excluída da documentação pois sua função foi incorporada na 'SERVICE_AREA`.

	A nova estrutura pode ser conferida na documentação: https://abrasel-nacional.github.io/docs/#section/Service  

* [[Issue #30](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/30)] - Alterado o atributo `availability` do endpoint `/merchant` para **`availabilities`** seguindo o padrão de grafia no plural dos demais campos. 
* [[Issue #29](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/29)] - Alterada o tipo do atributo `isAlcoholic` na propriedade `nutritionalInfo` do objeto `items` do endpoint `/merchant` de `string` para `boolean`.

## [1.0.0-rc.4] - 04/10/2021
* [[Issue #21](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/21)] - Inclusão de atributo **`X-App-MerchanId`** como parametro de **header** no request do webhook de notificação de pedido (/orderEvent) com o intuito de identificar qual merchant está recebendo o pedido.
* [[Issue #22](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/22)] - Corrigido o endpoint de autenticação `/oauth/token` para **`POST`** . Estava incorretamente descrito como `GET`.
* [[Issue #22](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/22)] - Corrigida a opção do atributo `grantType` do endpoint `oauth/token` de `clientCredentials` para `client_credentials`.
* Alterada as opções no atributo `type` no objeto `payments` do endpoint `/orders/{orderId}` de `ONLINE` e `OFFLINE` para `PREPAID` e `PENDING` para melhor refletir a intenção do campo.

* Incluído em todos os endpoints qual é o HOST e a DIREÇÃO do endpoint.

* O webhook de /merchantUpdate e o endpoint /merchantStatus foram movidos para uma nova seção chamada 'Merchant Status and Update' para separar os endpoints relacionados a merchant que são responsabilidade do Software Service e os que são do Ordering Application.



## [1.0.0-rc.3] - 13/09/2021
### Mudanças com quebra de contrato:
* [[Issue #8](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/8)] - Alterada a autenticação do endpoint `/merchant` para `apiKey` ao invés de `oauth2`. A autenticação também passa a ser opcional. Ver issue para maiores detalhes.
* [[Issue #13](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/13)] e [[Issue #15](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/15)]  - Alterado o nome de alguns atributos nos seguintes objetos:
  * `availabilityIds` no objeto `itemOffer` do endpoint `/merchant` para `availabilityId`
  * `optionGroupsIds` no objeto `itemOffer` do endpoint `/merchant` para `optionGroupsId`
  * `price` no objeto `options` do endpoint `/orders/{orderId}` para `totalPrice`
* [[Issue #12](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/12)] - Alterado os atributos de imagens para um objeto do tipo `image` composto por duas propriedades: `URL` e `CRC`  
	As propriedades alteradas foram:
  * `logoURL` no objeto `basicInfo` do endpoint `/merchant` para `logoImage`
  * `bannerURL` no objeto `basicInfo` do endpoint `/merchant` para `bannerImage`
  * `imageURL` no objeto `category` do endpoint `/merchant` para `image`
  * `imageURL` no objeto `item` do endpoint `/merchant` para `image`
* [[Issue #16](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/16)] - Alterado alguns atributos que correspondem à valores para utilizar o objeto `Price` ao invés de um `number` diretamente.  
Atributos alterados:
  * `value` no objeto `discounts` do endpoint `/oders/orderid` para `amount`
  * todos os atributos da propriedade `total` do endpoint `/orders/{orderid}`
	  * além disso o nome do atributo `items` foi alterado para `itemsPrice`
* [[Issue #7](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/7)] - Removido o campo `expectedPreparationStartTime` do atributo `metadata` do objeto `Event`. Ver issue para maiores detalhes.
### Mudanças sem quebra de contrato:
* [[Issue #13](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/13)] - Alterada a grafia das seguintes propriedades:
	* `merchantUrl` no endpoint `/merchantList` para `merchantURL`
	* `orderUrl` no objeto `Event` utilizado no webhook e no pooling de pedidos para `orderURL`
* Identificação do path para os webhooks:
  * Webhook de atualização de cardápio: `/merchantUpdate`
  * Webhook de recebimento de eventos de pedido: `/newEvent`
* [[Issue #11](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/11)] - Incluída a opção `LOGISTIC_SERVICES` no atributo `receivedBy` no objeto `otherFees` do endpoint `/orders/{orderId}`
* [[Issue #9](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/9)] - Acrescentado e corrigido os status codes dos seguintes endpoints:
  * /merchantStatus
    * 400 - Bad Request - Adicionado
  * /merchantUpdate (webhook)
    * 400 - Bad Request - Adicionado

  * /events:polling
    * 400 - Bad Request - Adicionado
  * /events/acknowledgment:
    * 400 - Bad Request - Adicionado
    * 404 - Not Found - Adicionado
  * /newEvent (webhook)
    * 400 - Bad Request - Adicionado  
    
  * /orders/{orderId}:
    * 400 - Bad Request - Corrigido
    * 403 - Forbidden - Adicionado
    * 404 - Not Found - Corrigido
    * 503 - Service Unavailable - Corrigido 
  * /orders/{orderId}/confirm:
    * 400 - Bad Request - Adicionado
    * 404 - Not Found - Adicionado
  * /orders/{orderId}/readyForPickup:
    * 400 - Bad Request - Adicionado
    * 404 - Not Found - Adicionado
  * /orders/{orderId}/dispatch:
    * 400 - Bad Request - Adicionado
    * 404 - Not Found - Adicionado
  * /orders/{orderId}/requestCancellation:
    * 400 - Bad Request - Adicionado
    * 403 - Forbidden - Adicionado
    * 404 - Not Found - Adicionado
    * 503 - Service Unavailable - Corrigido 
  * /orders/{orderId}/acceptCancellation:
    * 400 - Bad Request - Adicionado
    * 403 - Forbidden - Adicionado
    * 404 - Not Found - Adicionado
    * 503 - Service Unavailable - Corrigido 
  * /orders/{orderId}/denyCancellation:
    * 400 - Bad Request - Adicionado
    * 403 - Forbidden - Adicionado
    * 404 - Not Found - Adicionado
    * 503 - Service Unavailable - Corrigido 
    
  * /salesReport:
    * 400 - Bad Request - Adicionado

  * /merchantList:
    * 400 - Bad Request - Corrigido
    * 404 - Not Found - Corrigido
    * 503 - Service Unavailable - Corrigido 

* Foram ajustadas as descrições e exemplos de diversos atributos para refletir melhor a informação a ser preenchida.

## [1.0.0-rc.2] - 18/08/2021
* [[Issue #3](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/3)] Inclusão dos atributos `entityType` e `updatedObject` no request do webhook de notificação de atualizações do cardápio com o intuitio de já notificar a plataforma de pedidos sobre atualizações menores de uma determinada entidade (como mudança de status).

## [1.0.0-rc.1] - 18/08/2021
* Inclusão do atributo `moreInfo` no response do endpoint `GET /merchantStatus` com o intuitio de fornecer mais informações para os Software Services.
* [[Isuue #5](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/5)] Inclusão de exemplos dos formatos de data (date-time, date e time) na seção `General Guidelines`

## [1.0.0-rc.0] - 18/08/2021
* Versão inicial da documentação do Open Delivery disponibilizada para testes.
