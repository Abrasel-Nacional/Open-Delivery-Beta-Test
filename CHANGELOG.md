# Changelog

Mudanças efetuadas durante o periodo de Beta Test serão documentadas aqui.

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
  * Webhook de recebimento de eventos de pedido: `/events`
* [[Issue #11](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/13)] - Incluída a opção `LOGISTIC_SERVICES` no atributo `receivedBy` no objeto `otherFees` do endpoint `/orders/{orderId}`

* Foram ajustadas as descrições e exemplos de diversos atributos para refletir melhor a informação a ser preenchida.

## [1.00 rc2]
* [[Issue #3](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/3)] Inclusão dos atributos `entityType` e `updatedObject` no request do webhook de notificação de atualizações do cardápio com o intuitio de já notificar a plataforma de pedidos sobre atualizações menores de uma determinada entidade (como mudança de status).

## [1.00 rc1]
* Inclusão do atributo `moreInfo` no response do endpoint `GET /merchantStatus` com o intuitio de fornecer mais informações para os Software Services.
* [[Isuue #5](https://github.com/Abrasel-Nacional/Open-Delivery-Beta-Test/issues/5)] Inclusão de exemplos dos formatos de data (date-time, date e time) na seção `General Guidelines`

## [1.00 rc0]
* Versão inicial da documentação do Open Delivery disponibilizada para testes.
