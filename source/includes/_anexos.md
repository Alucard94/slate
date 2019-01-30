# Anexos

## Estados de un Pedido

Estado | Descripción
------ | -----------
NEW | El pedido es recién ingresado al sistema
PRE_OFFERED | Estado previo a que el pedido pase a planeamiento y sea ofertado
OFFERED | El pedido es ofrecido para que un Chazki lo acepte
WAITING | El Chazki va camino a recoger el pedido
ARRIVED | El Chazki llega al punto de recojo del pedido
FAILED_PICK | Falla durante el recojo del pedido
IN_PROGRESS | El Chazki está camino a entregar el pedido
FAILED | Falla ocurrida durante la entrega del pedido
COMPLETED | El pedido es entregado con éxito
REPROGRAMMED | El pedido es reprogramado

## Tipos de Pedido

Tipo | Descripción
---- | -----------
REGULAR | Pedido que puede entregarse al día siguiente de haber sido solicitado
EXPRESS | Pedido que se entrega en un máximo de 3 horas el mismo día que se realiza
PROGRAMADO | Pedido entregado de acuerdo a tres horarios: 9-13, 13-17, 17-21
FOOD | Pedido de comida programado para ser entregado máximo en una hora
FOOD_PROGRAMADO | Pedido de comida programado para ser entregado en una hora específica