---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - anexos

search: true
---

# Introduction

Para poder realizar los pedidos de los servicios de Chazki se habilitaron endpoints para el registro del delivery y la consulta del estado de los pedidos.

Estos servicios se encuentran registrados en el dominio propiedad de chazki y se detallan en el apartado a continuación.

Encuentra más acerca de Chazki [aquí](https://www.chazki.com/#/). Vea también nuestros [Términos y condiciones](https://pe.chazki.com/tyc.html).

# Authentication

> Usar el siguiente código para la autenticación:

```shell
# Se puede enviar el encabeza en cada petición
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> Reemplazar `YOUR_CHAZKI_API_KEY` por su API key.

Empleamos un Key para brindar acceso a nuestro API. Puede solicitar su Chazki API Key en nuestro [developer portal](http://example.com/developers).

Nuestro API espera que el Chazki API Key sea incluído en el header de cada petición al servidor, como se muestra a continuación:

`chazki-api-key: YOUR_CHAZKI_API_KEY`

<aside class="notice">
Se debe reemplazar <code>YOUR_CHAZKI_API_KEY</code> por el Key que se le asignó.
</aside>

# Services

## Registro de un Delivery

```shell
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> Estructura JSON de envío para el registro de un delivery:

```json
[
    {
        "storeId": "23434j3808e4b04d9cfec50112",
        "branchId": "234kj2l3k4j34e4b04d9cfec50115",
        "deliveryTrackCode": "0000001061015",
        "proofPayment": "Boleta",
        "deliveryCost": 0,
        "mode": "Regular",
        "time": "",
        "paymentMethod": "Pagado",
        "country": "PE",
        "listItemSold": [
            {
                "name": "Asus - Tablet Memo Pad ME70CX-1A022A 7 Android 4.3 1GB 8GB - Negro",
                "currency": "PEN",
                "price": 255,
                "weight": 0.9,
                "volumen": 0.9,
                "quantity": 1,
                "unity": "Paquete",
                "size": "S"
            }
        ],
        "notes": "El paquete lo deja en la recepción del edificio",
        "documentNumber": "12345678987",
        "name_tmp": "",
        "lastName": "",
        "companyName": "Zapateria CCE",
        "email": "cce@gmail.com",
        "phone": "989555879",
        "documentType": "RUC",
        "addressClient": [
            {
                "nivel_2": "LIMA",
                "nivel_3": "LIMA",
                "nivel_4": "SAN BORJA",
                "name": "Calle Bronzino 501",
                "reference": "Alt. Cavallini",
                "alias": "Oficina central",
                "position": {
                    "latitude": 0,
                    "longitude": 0
                }
            }
        ]
    }
]
```
> Estructura JSON de los datos de salida de nuestro API:

```json
{
    "response": "",
    "descriptionResponse": "",
    "codeDelivery": ""
}
```

Este endpoint permite registrar un delivery o ruta. Dado que en el envío es un arreglo, se pueden registrar varios puntos a donde se desea que llegue el Chazki, por lo tanto, se forma una ruta; caso contrario, se puede registrar solo un punto de llegada.

### HTTP Request

`POST https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService`

### Estructura de envío

Attribute | Type | Description | Provider | Required
--------- | ---- | ----------- | -------- | --------
storeId | String | Campo referido a la tienda | Chazki | SI
branchId | String | Lugar o Sucursal desde donde se origina el pedido | Chazki | SI
deliveryTrackCode | String | Código que identifica el pedido, este código debe ser único | Cliente | SI
proofPayment | String | Evidencia física que tendrá el empaque y será entregada al cliente final. BOLETA O FACTURA | Cliente | SI
deliveryCost | Float | Es 0, salvo que el cliente cobre un monto adicional por la entrega | Cliente | SI
mode | String | Puede ser "Regular", "Express" o "Programado", dependiendo del tipo de servicio deseado | Cliente | SI
time | String | Ventana horaria si el servicio es "Programado". Ejemplo: 9-13 | Cliente | SI
paymentMethod | String | Puede ser "Pagado" o "Efectivo" | Cliente | SI
country | String | País donde se genera el delivery (PE: Perú, MX: México, AR: Argentina) | Cliente | SI
<b>listItemSold</b> | Collection | Lista de ítems enviados como parte del delivery | | 
name | String | Descripción del producto | Cliente | SI
currency | String | Moneda. Por defecto "PEN" | Cliente | SI
price | Double | Precio. En caso sea efectivo debe ser el precio real, o referencial en caso de ser pagado. | Cliente | NO (colocar 0)
weight | Double | Peso referencial del paquete | Cliente | NO (colocar 0)
volumen | Double | Peso referencial del paquete, dato para el cálculo de factuación | Cliente | NO (colocar 0)
quantity | Integer | Cantidad de ítems | Cliente | SI
unity | String | Unidad de outer pack | Cliente | SI
size | String | Unidad de medida del pedido (XS, S, M, L) | Cliente | SI
 | | | | 
notes | String | Datos adicionales, que facilitan la entrega. Puede ser vacío | Cliente | NO (colocar "")
documentNumber | String | Documento del cliente | Cliente | SI
name_tmp | String | Nombre del que recibe el pedido/Persona Natural | Cliente | SI
lastName | String | Apellido del que recibe el pedido/Persona Natural | Cliente | SI
companyName | String | En caso el envío es realizado a una empresa | Cliente | SI
email | String | Correo electrónico del cliente | Cliente | SI
phone | String | Teléfono del cliente | Cliente | SI
documentType | String | Tipo de documento del cliente DNI, RUC y CDE (Carnet de extranjería) | Cliente | SI
<b>AddressClient</b> | Collection | Información del cliente | | 
name | String | Dirección del cliente | Cliente | SI
nivel_2 | String | Departamento de la dirección del cliente | Cliente | SI
nivel_3 | String | Provincia de la dirección del cliente | Cliente | SI
nivel_4 | String | Distrito de la dirección del cliente | Cliente | SI
reference | String | Referencia a la dirección del cliente | Cliente | SI
alias | String | Alias del punto de envío | Cliente | SI
<b>Position</b> | | | | 
latitude | Double | Latitud, en caso de ser desconocida colocar 0 | Cliente | SI
longitude | Double | Longitud, en caso de ser desconocida colocar 0 | Cliente | SI

### Estructura de respuesta del API

Attribute | Type | Description | Provider 
--------- | ---- | ----------- | -------- 
response | Integer | Código de respuesta (0: no se pudo efectuar, 1: se registró correctamente)<br><ul><li><b>0:</b> Error a nivel funcional, ejemplo: "Datos incorrectos en la trama"</li><li><b>1: </b> Éxito</li><li><b>99: </b> Error técnico, puede ser considerado como caída del servidor</li></ul> | Chazki
descriptionResponse | String | Descripción de la respuesta<br><ul><li><b>0:</b> "FAILED"</li><li><b>1: </b> "SUCCESS"</li><li><b>99: </b> "ERROR: faltan parámetros, NullpointerException"</li></ul> | Chazki
codeDelivery | String | Código Track del delivery. Si es un conjunto de deliveries retornará separado por coma (",") | Chazki

## Consulta de Estado y Posición del Chazki

```shell
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/track/select/deliveryCode?code=XXXX&store=XXXX"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> El comando anterior retorna una estructura JSON como la siguiente:

```json
{
    "position": {
        "latitude": 0,
        "longitude": 0
    },
    "status": "",
    "timestamp": "",
    "rd": "",
    "cel": "",
    "motivo": ""
}
```

Esta API nos permite ver el movimiento del Chazki y el estado en que se encuentra el delivery.

### HTTP Request

`GET https://sandboxintegracion.chazki.com:8443/chazkiServices/track/select/deliveryCode?code=XXXX&store=XXXX`

### URL Parameters

Parameter | Description | Type | Provider | Required
--------- | ----------- | ---- | -------- | --------
code | Código track del delivery | String | Cliente | SI
store | Código de la empresa | String | Cliente | SI

### Resultado

Attribute | Description | Type | Provider
--------- | ----------- | ---- | --------
position | Retorna los puntos de latitud y longitu | String | Chazki
status | Estado en que se encuentra el delivery | String | Chazki
timestamp | Fecha de la última actualización de la posición del Chazki | String | Chazki
rd | Nombre y apellido del Chazki | String | Chazki
motivo | El motivo se visualiza si es que ocurrió alguna falla | String | Chazki

## Historial de Estados

```shell
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/status/record?code=XXXX&store=XXXX"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> El comando anterior retorna una estructura JSON como la siguiente:

```json
{
    "response": 1,
    "descriptionResponse": "SUCCESS",
    "messages": "",
    "service_1": [
        {
            "status": "Nuevo",
            "date": "26/04/2018 09:26:03"
        },
        {
            "status": "Aceptado",
            "date": "26/04/2018 10:26:03"
        },
        {
            "status": "Recogido",
            "date": "26/04/2018 11:26:03"
        },
        {
            "status": "Fallo Entrega",
            "date": "26/04/2018 12:26:03",
            "reason": "NE - No se encuentra el cliente"
        }
    ],
    "service_2": [
        {
            "status": "Aceptado",
            "date": "26/04/2018 10:26:03"
        },
        {
            "status": "Recogido",
            "date": "26/04/2018 11:26:03"
        },
        {
            "status": "Entregado",
            "date": "26/04/2018 12:26:03"
        }
    ]
}
```

Esta API nos permite ver los estados por los que paso el delivery agrupados por servicios. La agrupación de servicios hace referencia a los intentos que se realizó para la entrega del delivery.

### HTTP Request

`GET https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/status/record?code=XXXX&store=XXXX`

### URL Parameters

Parameter | Description | Type | Provider | Required
--------- | ----------- | ---- | -------- | --------
code | Código track del delivery | String | Cliente | SI
store | Código de la empresa | String | Cliente | SI

### Resultado

Attribute | Description | Type | Provider
--------- | ----------- | ---- | --------
response | Respuesta de la petición (0: Error, 1: OK, 99: ERROR) | Integer | Chazki
descriptionResponse | Descripción breve del código de error | String | Chazki
message | Mensaje de respuesta si es que el valor de "response" es 0 o 99 | String | Chazki
<b>Service</b> | Servicios por el cual pasó el delivery | String | Chazki
status | Estado del delivery | String | Chazki
date | Fecha de estado | String | Chazki
reason | Motivo si el estado fue "Fallo Recojo" o "Fallo Entrega" | String | Chazki

## Logística Inversa

```shell
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> Estructura JSON de envío para el registro de un delivery:

```json
[
    {
        "storeId": "23434j3808e4b04d9cfec50112",
        "branchId": "234kj2l3k4j34e4b04d9cfec50115",
        "deliveryTrackCode": "0000001061015",
        "proofPayment": "Boleta",
        "deliveryCost": 0,
        "mode": "Regular",
        "time": "",
        "paymentMethod": "Pagado",
        "country": "PE",
        "listItemSold": [
            {
                "name": "Asus - Tablet Memo Pad ME70CX-1A022A 7 Android 4.3 1GB 8GB - Negro",
                "currency": "PEN",
                "price": 255,
                "weight": 0.9,
                "volumen": 0.9,
                "quantity": 1,
                "unity": "Paquete",
                "size": "S"
            }
        ],
        "notes": "El paquete lo deja en la recepción del edificio",
        "documentNumber": "12345678987",
        "name_tmp": "",
        "lastName": "",
        "companyName": "Zapateria CCE",
        "email": "cce@gmail.com",
        "phone": "989555879",
        "documentType": "RUC",
        "addressClient": [
            {
                "nivel_2": "LIMA",
                "nivel_3": "LIMA",
                "nivel_4": "SAN BORJA",
                "name": "Calle Bronzino 501",
                "reference": "Alt. Cavallini",
                "alias": "Oficina central",
                "position": {
                    "latitude": 0,
                    "longitude": 0
                }
            }
        ],
        "depotRequestData": {
            "nameDepot": "C Cívico",
            "contactName": "",
            "contactMovil": "(01) 433 8318",
            "address": {
                "name": "Av. Garcilazo de la Vega Nro 1337 Int. 2011 C.C. Real Plaza Centro Cívico",
                "department": "LIMA",
                "province": "LIMA",
                "district": "LIMA",
                "reference": "",
                "position": {
                    "latitude": -12.056538775523,
                    "longitude": -77.037388086319
                }
            }
        }
    }
]
```
> Estructura JSON de los datos de salida de nuestro API:

```json
{
    "response": "",
    "descriptionResponse": "",
    "codeDelivery": ""
}
```

Esta API nos permite poder realizar logística inversa en caso se necesite recoger pedidos devueltos por el cliente. Para este caso, se ha agregado en la estructura el objeto <b>depotRequestData</b>, en el que se enviarán los datos correspondientes a la ubicación de recojo del pedido devuelto.

### HTTP Request

`POST https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService`

### Estructura de envío

Attribute | Type | Description | Provider | Required
--------- | ---- | ----------- | -------- | --------
storeId | String | Campo referido a la tienda | Chazki | SI
branchId | String | Lugar o Sucursal desde donde se origina el pedido | Chazki | SI
deliveryTrackCode | String | Código que identifica el pedido, este código debe ser único | Cliente | SI
proofPayment | String | Evidencia física que tendrá el empaque y será entregada al cliente final. BOLETA O FACTURA | Cliente | SI
deliveryCost | Float | Es 0, salvo que el cliente cobre un monto adicional por la entrega | Cliente | SI
mode | String | Puede ser "Regular", "Express" o "Programado", dependiendo del tipo de servicio deseado | Cliente | SI
time | String | Ventana horaria si el servicio es "Programado". Ejemplo: 9-13 | Cliente | SI
paymentMethod | String | Puede ser "Pagado" o "Efectivo" | Cliente | SI
country | String | País donde se genera el delivery (PE: Perú, MX: México, AR: Argentina) | Cliente | SI
<b>listItemSold</b> | Collection | Lista de ítems enviados como parte del delivery | | 
name | String | Descripción del producto | Cliente | SI
currency | String | Moneda. Por defecto "PEN" | Cliente | SI
price | Double | Precio. En caso sea efectivo debe ser el precio real, o referencial en caso de ser pagado. | Cliente | NO (colocar 0)
weight | Double | Peso referencial del paquete | Cliente | NO (colocar 0)
volumen | Double | Peso referencial del paquete, dato para el cálculo de factuación | Cliente | NO (colocar 0)
quantity | Integer | Cantidad de ítems | Cliente | SI
unity | String | Unidad de outer pack | Cliente | SI
size | String | Unidad de medida del pedido (XS, S, M, L) | Cliente | SI
 | | | | 
notes | String | Datos adicionales, que facilitan la entrega. Puede ser vacío | Cliente | NO (colocar "")
documentNumber | String | Documento del cliente | Cliente | SI
name_tmp | String | Nombre del que recibe el pedido/Persona Natural | Cliente | SI
lastName | String | Apellido del que recibe el pedido/Persona Natural | Cliente | SI
companyName | String | En caso el envío es realizado a una empresa | Cliente | SI
email | String | Correo electrónico del cliente | Cliente | SI
phone | String | Teléfono del cliente | Cliente | SI
documentType | String | Tipo de documento del cliente DNI, RUC y CDE (Carnet de extranjería) | Cliente | SI
<b>AddressClient</b> | Collection | Información del cliente | | 
name | String | Dirección del cliente | Cliente | SI
nivel_2 | String | Departamento de la dirección del cliente | Cliente | SI
nivel_3 | String | Provincia de la dirección del cliente | Cliente | SI
nivel_4 | String | Distrito de la dirección del cliente | Cliente | SI
reference | String | Referencia a la dirección del cliente | Cliente | SI
alias | String | Alias del punto de envío | Cliente | SI
<b>Position</b> | | | | 
latitude | Double | Latitud, en caso de ser desconocida colocar 0 | Cliente | SI
longitude | Double | Longitud, en caso de ser desconocida colocar 0 | Cliente | SI
<b>depotRequestData</b> | | | | 
nameDepot | String | Alias del lugar de recojo | Cliente | SI
contactName | String | Nombre del contacto | Cliente | SI
contactMovil | String | Número de teléfono de contacto | Cliente | SI
<b>address</b> | | | | 
name | String | Dirección de recojo | Cliente | SI
department | String | Departamento de la dirección de recojo | Cliente | SI
province | String | Provincia de la dirección de recojo | Cliente | SI
district | String | Distrito de la dirección de recojo | Cliente | SI
reference | String | Referencia a la dirección de recojo | Cliente | SI
<b>Position</b> | | | | 
latitude | Double | Latitud, en caso de ser desconocida colocar 0 | Cliente | SI
longitude | Double | Longitud, en caso de ser desconocida colocar 0 | Cliente | SI

### Estructura de respuesta del API

Attribute | Type | Description | Provider 
--------- | ---- | ----------- | -------- 
response | Integer | Código de respuesta (0: no se pudo efectuar, 1: se registró correctamente)<br><ul><li><b>0:</b> Error a nivel funcional, ejemplo: "Datos incorrectos en la trama"</li><li><b>1: </b> Éxito</li><li><b>99: </b> Error técnico, puede ser considerado como caída del servidor</li></ul> | Chazki
descriptionResponse | String | Descripción de la respuesta<br><ul><li><b>0:</b> "FAILED"</li><li><b>1: </b> "SUCCESS"</li><li><b>99: </b> "ERROR: faltan parámetros, NullpointerException"</li></ul> | Chazki
codeDelivery | String | Código Track del delivery. Si es un conjunto de deliveries retornará separado por coma (",") | Chazki

## Registro de un Delivery con días de anticipación (OPCIONAL)

```shell
curl "https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService"
  -H "chazki-api-key: YOUR_CHAZKI_API_KEY"
```

> Estructura JSON de envío para el registro de un delivery:

```json
[
    {
        "storeId": "23434j3808e4b04d9cfec50112",
        "branchId": "234kj2l3k4j34e4b04d9cfec50115",
        "deliveryTrackCode": "0000001061015",
        "proofPayment": "Boleta",
        "deliveryCost": 0,
        "mode": "Programado",
        "time": "13/11/18 9-13",
        "paymentMethod": "Pagado",
        "country": "PE",
        "listItemSold": [
            {
                "name": "Asus - Tablet Memo Pad ME70CX-1A022A 7 Android 4.3 1GB 8GB - Negro",
                "currency": "PEN",
                "price": 255,
                "weight": 0.9,
                "volumen": 0.9,
                "quantity": 1,
                "unity": "Paquete",
                "size": "S"
            }
        ],
        "notes": "El paquete lo deja en la recepción del edificio",
        "documentNumber": "12345678987",
        "name_tmp": "",
        "lastName": "",
        "companyName": "Zapateria CCE",
        "email": "cce@gmail.com",
        "phone": "989555879",
        "documentType": "RUC",
        "addressClient": [
            {
                "nivel_2": "LIMA",
                "nivel_3": "LIMA",
                "nivel_4": "SAN BORJA",
                "name": "Calle Bronzino 501",
                "reference": "Alt. Cavallini",
                "alias": "Oficina central",
                "position": {
                    "latitude": 0,
                    "longitude": 0
                }
            }
        ]
    }
]
```
> Estructura JSON de los datos de salida de nuestro API:

```json
{
    "response": "",
    "descriptionResponse": "",
    "codeDelivery": ""
}
```

Esta API nos permite poder registrar un delivery o una ruta. Es decir, dado que el envío es un arreglo, se pueden registrar varios puntos a donde se desea que llegue el Chazki por lo tanto se estaría formando una ruta, caso contrario, también se le puede registrar solo un punto de llegada.

En este caso, el formato del campo <b>time</b> es de la forma "<b>dd/MM/YY NN-NN</b>" donde <b>NN-NN</b> indica el rango horario de envío del delivery, y, el campo <b>mode</b> debe ser <b>Programado</b>.

### HTTP Request

`POST https://sandboxintegracion.chazki.com:8443/chazkiServices/delivery/create/deliveryService`

### Estructura de envío

Attribute | Type | Description | Provider | Required
--------- | ---- | ----------- | -------- | --------
storeId | String | Campo referido a la tienda | Chazki | SI
branchId | String | Lugar o Sucursal desde donde se origina el pedido | Chazki | SI
deliveryTrackCode | String | Código que identifica el pedido, este código debe ser único | Cliente | SI
proofPayment | String | Evidencia física que tendrá el empaque y será entregada al cliente final. BOLETA O FACTURA | Cliente | SI
deliveryCost | Float | Es 0, salvo que el cliente cobre un monto adicional por la entrega | Cliente | SI
mode | String | Puede ser "Regular", "Express" o "Programado", dependiendo del tipo de servicio deseado | Cliente | SI
time | String | Ventana horaria si el servicio es "Programado" con días de anticipación. Ejemplo: 15/12/18 13-17 | Cliente | SI
paymentMethod | String | Puede ser "Pagado" o "Efectivo" | Cliente | SI
country | String | País donde se genera el delivery (PE: Perú, MX: México, AR: Argentina) | Cliente | SI
<b>listItemSold</b> | Collection | Lista de ítems enviados como parte del delivery | | 
name | String | Descripción del producto | Cliente | SI
currency | String | Moneda. Por defecto "PEN" | Cliente | SI
price | Double | Precio. En caso sea efectivo debe ser el precio real, o referencial en caso de ser pagado. | Cliente | NO (colocar 0)
weight | Double | Peso referencial del paquete | Cliente | NO (colocar 0)
volumen | Double | Peso referencial del paquete, dato para el cálculo de factuación | Cliente | NO (colocar 0)
quantity | Integer | Cantidad de ítems | Cliente | SI
unity | String | Unidad de outer pack | Cliente | SI
size | String | Unidad de medida del pedido (XS, S, M, L) | Cliente | SI
 | | | | 
notes | String | Datos adicionales, que facilitan la entrega. Puede ser vacío | Cliente | NO (colocar "")
documentNumber | String | Documento del cliente | Cliente | SI
name_tmp | String | Nombre del que recibe el pedido/Persona Natural | Cliente | SI
lastName | String | Apellido del que recibe el pedido/Persona Natural | Cliente | SI
companyName | String | En caso el envío es realizado a una empresa | Cliente | SI
email | String | Correo electrónico del cliente | Cliente | SI
phone | String | Teléfono del cliente | Cliente | SI
documentType | String | Tipo de documento del cliente DNI, RUC y CDE (Carnet de extranjería) | Cliente | SI
<b>AddressClient</b> | Collection | Información del cliente | | 
name | String | Dirección del cliente | Cliente | SI
nivel_2 | String | Departamento de la dirección del cliente | Cliente | SI
nivel_3 | String | Provincia de la dirección del cliente | Cliente | SI
nivel_4 | String | Distrito de la dirección del cliente | Cliente | SI
reference | String | Referencia a la dirección del cliente | Cliente | SI
alias | String | Alias del punto de envío | Cliente | SI
<b>Position</b> | | | | 
latitude | Double | Latitud, en caso de ser desconocida colocar 0 | Cliente | SI
longitude | Double | Longitud, en caso de ser desconocida colocar 0 | Cliente | SI

### Estructura de respuesta del API

Attribute | Type | Description | Provider 
--------- | ---- | ----------- | -------- 
response | Integer | Código de respuesta (0: no se pudo efectuar, 1: se registró correctamente)<br><ul><li><b>0:</b> Error a nivel funcional, ejemplo: "Datos incorrectos en la trama"</li><li><b>1: </b> Éxito</li><li><b>99: </b> Error técnico, puede ser considerado como caída del servidor</li></ul> | Chazki
descriptionResponse | String | Descripción de la respuesta<br><ul><li><b>0:</b> "FAILED"</li><li><b>1: </b> "SUCCESS"</li><li><b>99: </b> "ERROR: faltan parámetros, NullpointerException"</li></ul> | Chazki
codeDelivery | String | Código Track del delivery. Si es un conjunto de deliveries retornará separado por coma (",") | Chazki