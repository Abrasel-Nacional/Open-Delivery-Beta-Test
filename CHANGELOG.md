# Changelog

Mudanças efetuadas durante o periodo de Beta Test serão documentadas aqui.
## [1.00 rc4]
* [[Issue #21](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/21)] - Inclusão de atributo **`X-App-MerchanId`** como parametro de **header** no request do webhook de notificação de pedido (/orderEvent) com o intuito de identificar qual merchant está recebendo o pedido.
* [[Issue #22](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/22)] - Alterado o endpoint de autenticação /oauth/token para **POST** . Estava incorretamente descrito como GET.
* Alterada as opções no atributo `type` no objeto `payments` do endpoint `/orders/{orderId}` de `ONLINE` e `OFFLINE` para `PREPAID` e `PENDING` para melhor refletir a intenção do campo.
* Corrigida a opção do atributo `grantType` do endpoint `oauth/token` de `clientCredentials` para `client_credentials`.

* Incluído em todos os endpoints qual é o HOST e a DIREÇÃO do endpoint.

* O webhook de /merchantUpdate e o endpoint /merchantStatus foram movidos para uma nova seção chamada 'Merchant Status and Update' para separar os endpoints relacionados a merchant que são responsabilidade do Software Service e os que são do Ordering Application.



## [1.00 rc3]
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

## [1.00 rc2]
* [[Issue #3](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/3)] Inclusão dos atributos `entityType` e `updatedObject` no request do webhook de notificação de atualizações do cardápio com o intuitio de já notificar a plataforma de pedidos sobre atualizações menores de uma determinada entidade (como mudança de status).

## [1.00 rc1]
* Inclusão do atributo `moreInfo` no response do endpoint `GET /merchantStatus` com o intuitio de fornecer mais informações para os Software Services.
* [[Isuue #5](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/5)] Inclusão de exemplos dos formatos de data (date-time, date e time) na seção `General Guidelines`

## [1.00 rc0]
* Versão inicial da documentação do Open Delivery disponibilizada para testes.
