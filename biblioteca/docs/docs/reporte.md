# Reportes

Se proporcionará un acceso a una página con la información exclusiva por proveedor de las transacciones realizadas a través del servicio WebAPI la cual mostrará los consumos satisfactorios y errados de actuaciones y documentos, evidenciando los motivos por los cuales se presentaron fallas en la transmisión de la información, además de la posibilidad de exportar dicha información a Excel y opciones de filtro. También los reportes de los casos marcados con vigilancia en LegisOffice y el reporte de los casos cerrados en los últimos 180 días.

Esta página contará con los siguientes reportes:

## Casos marcados para vigilancia

 1. Fecha solicitud Vigilancia
 2. Fecha inicia vigilancia
 3. Identificador de la oficina
 4. Nombre de la oficina
 5. Radicado
 6. Parte activa
 7. Parte pasiva
 8. Jurisdicción
 9. Código caso
 10. Consecutivo    


## Casos retirados de vigilancia (se evalúan los últimos 180 días)

1. Fecha solicitud vigilancia
2. Fecha Inicia vigilancia
3. Fecha termina vigilancia
4. Identificador de la oficina
5. Nombre de la oficina
6. Radicado
7. Parte Activa
8. Parte Pasiva
9. Jurisdicción
10. Código caso
11. consecutivo

## Actuación

1. Caso
2. Título
3. Descripción
4. Fecha
5. Radicado
6. Juzgado
7. Oficina 
8. Código externo 
9. Respuesta de consumo
10. Mensaje de entrada (json) solo se ven las exportaciones de excel.

## Prototipo

## Restricciones

* La plataforma de LegisOffice, está diseñada para soportar 100.000 mil casos por oficina, cuando se identifique que una oficina va a superar este límite se debe contactar el área comercial de LEGIS.

* El máximo peso de documento por actuación es de 100 MB.

* El formato establecido para los documentos de las actuaciones de PDF.

* El tamaño y tipo de campo de los diferentes métodos del servicio, son los establecidos en el ítem de las especificaciones de los servicios web.





