
# Changelog

Mudanças efetuadas durante o periodo de Beta Test serão documentadas aqui.

## [BETA] - 12/03/2022
### Mudanças com quebra de contrato:
* [[Issue #81](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/81)] - Adicionado o campo `customerName` no endpoint [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
* Alterado o nome do campo `deliveryDetailsURL` para `externalTrackingURL` no endpoint [GET /logistics/delivery/{orderId}](https://abrasel-nacional.github.io/docs/#operation/logisticDetails)
* Alterado o nome do campo `volumes` para `packageQuantity` no endpoint [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
* Alterado o nome de alguns eventos:
  - `PICKUP_STARTED` para `PICKUP_ONGOING`
  - `DELIVERY_STARTED` para `DELIVERY_ONGOING`

### Outras Mudanças
* Adicionado o campo `packageVolume` no endpoint [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
* Adicionado o campo `externalTrackingURL` no endpoint [POST /deliveryUpdate](https://abrasel-nacional.github.io/docs/#operation/newLogisticEvent)
* Adicionado o campo `containerSize` no objeto `Vehicle`.
  Endpoints aftados:
  - [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
  - [POST /logistics/availability](https://abrasel-nacional.github.io/docs/#tag/logisticPrice)
  - [POST /deliveryUpdate](https://abrasel-nacional.github.io/docs/#operation/newLogisticEvent)
  - [GET /logistics/delivery/{orderId}](https://abrasel-nacional.github.io/docs/#operation/logisticDetails)
* Adicionada uma nova seção  nas explicações dos [eventos de logística](https://abrasel-nacional.github.io/docs/#tag/logisticOrder) explicando o funcionamento de novas tentativas de um pedido rejeitado.
  
  
## [BETA] - 21/02/2022

* [[Issue #73](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/73)] - Alterada a descrição dos campos de `latitude` e `longitude` de todos os endpoints que continham estas informações, removendo a descrição `decimal places <= 5` que estava incorreta.
* Retirada a obrigatoriedade de preenchimento dos campos `latitude` e `longitude` nos endpoints :
  - [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
  - [POST /logistics/availability](https://abrasel-nacional.github.io/docs/#tag/logisticPrice)
* Adição do enumerador`INVALID_ADDRESS` como opção de preenchimento do campo `rejectReason` do endpoint [POST /deliveryUpdate](https://abrasel-nacional.github.io/docs/#operation/newLogisticEvent)

* Acrescentados novos [Guidelines](https://abrasel-nacional.github.io/docs/#section/General-Guidelines):
	- Todas as datas devem ser preenchidas considerando o horário em UTC
	- Informações de como prover as {baseURLs} dos endpoints
	- [[Issue #71](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/71)] - Instruções de como enviar parametros de arrays em requests.
	
## [BETA] - 04/02/2022
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
		
### Outras mudanças
* [[Issue #70](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/70)] - Como o formato do campo `MerchantId` possui uma definição bem especifica, o format `UUID` foi removido deixando o campo apenas como `string`. Isso afeta os objetos e parametros que utilizam o Id do merchant. Os lugares afetados são:
  - Parametros do request:
    - Delivery Order Webhook
  - Objetos:
    - Merchant 
    - DeliveryOrder
    - DeliveryOrderEvent
    - DeliveryAvailabilityPrice
    - DeliveryOrderDetails
    
* Adicionada uma nova seção chamada [How to Start](https://abrasel-nacional.github.io/docs/#section/How-to-Start-(Setup-Guide)), para auxiliar as empresas nas implementações e parametrizações.

## [BETA] - 17/01/2022
### Mudanças com quebra de contrato
* Alterada as opções do enum "reason" do campo "rejectedInfo" do endpoint "Delivery Tracking" para inglês.

### Outras alterações
* A descrição dos campos foi revista e melhorada para refletir melhor a finalidade de cada campo.

## [BETA] - 23/12/2021
* [[Issue #58](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/58)] - Adicionado o campo `reference` em todos os objetos relacionados a endereço:
Objetos afetados:
	- `Address`
* [[Issue #61](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/61)] - Corrigido os campos `deliveryPrice` que estavam referenciando um schema incorreto. Endpoints afetados:
	- `Delivery Tracking`
	- `Delivery Availability and Pricing`

## [BETA] - 14/12/2021
### Mudanças com quebra de contrato:
* [[Issue #50](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/50)] - Todos os atributos `latitude` e `longitude` tiveram seu formato alterado para `number` com precisão de 5 casas decimais.
Objetos afetados:
	- `Address`
	- `GeoLocalization`
	
### Outras mudanças
* [[Issue #46](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/46)] - Recomendada a utilização do padrão **ISO 3166-2** nos campos de `state` nos objetos de endereços.


## [BETA] - 22/11/2021

* Release Inicial
