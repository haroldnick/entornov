# Servicio WebApi

El protocolo HTTP no sirve sólo para proveer páginas web sino también es una potente plataforma para la construcción de APIs que exponen servicios y datos. HTTP es simple, flexible y ubicuo. Casi cualquier plataforma actualmente tiene o utiliza el protocolo HTTP, por lo que los servicios HTTP pueden llegar a una amplia gama de clientes, incluyendo los navegadores, dispositivos móviles y aplicaciones de escritorio tradicionales. 
Microsoft ASP.NET WebAPI es un marco para la construcción de las API web en la parte superior del marco .NET de Microsoft que permite aprovechar todo el conjunto de características presente sobre el protocolo HTTP.
El servicio WebAPI de LegisOffice utiliza esta herramienta de Microsoft WebAPI para exponer servicios a sus clientes mediante peticiones HTTP (GET, POST, PUT, DELETE) en formato JSON.

El servicio WebAPI de LegisOffice se encarga de exponer métodos generales de recepción de información de vigilancia judicial a partir de un mecanismo de autenticación basado en Usuario / Clave / Proveedor. 

Para poder acceder a algún un recurso – excepto Test y ValidarCredenciales – es requerido que el cliente incluya el Token de acceso - obtenido al validar sus credenciales - en el encabezado de autorización de la petición HTTP.

A continuación, se describen a detalla los contratos expuestos en el servicio WebAPI.

URL del servicio en producción: (https://vj.legisoffice.com/LOServiceVJ/.) Todos los recursos están agrupados sobre el controlador llamado: VJ, la URL de consumo quedaría así: (https://vj.legisoffice.com/LOServiceVJ/VJ/) + EL RECURSO SOLICITADO

**Test**
*Método HTTP: GET*
Verifica si el servicio de vigilancia judicial está disponible.
**INFORMACIÓN SOLICITUD**
Parámetros URL: Ninguno

Parámetros cuerpo solicitud: Ninguno

**Información respuesta**

| Tipo      | Descripción                     | Mensaje                                                              |  
|-----------|---------------------------------|--------------------------------------------------------------------- |
| String    | Mensaje conexión establecida    | Conexión establecida con LegisOffice Servicio de vigilancia judicial | 

## ValidarCredenciales	

Método HTTP: POST
Valida las credenciales de autenticación para un proveedor y genera un identificador único de sesión.
INFORMACIÓN SOLICITUD
Parámetros URL: Ninguno

Parámetros cuerpo solicitud:

| Objeto    | Autenticación                                                                                          |  
|-----------|---------------------------------|--------------------------------------------------------------------- |
| String    | Mensaje conexión establecida    | Conexión establecida con LegisOffice Servicio de vigilancia judicial | 



## RegistrarActuacion

Método HTTP: POST
Registra la información de una actuación y retorna el identificador único de la actuación.
INFORMACIÓN SOLICITUD
Cabecera de autenticación: Authentication = Token – Espacio – Guid obtenido como respuesta al consumir el método ValidarCredenciales codificado en base64 (ISO-8859-1)

Parámetros URL: Ninguno

Parámetros cuerpo solicitud:


## RegistrarDocumentoActuacion

Método HTTP: POST
Registra un documento sobre una actuación y retorna si se pudo registrar o no.
INFORMACIÓN SOLICITUD
Cabecera de autenticación: Authentication = Token – Espacio – Guid obtenido como respuesta al consumir el método ValidarCredenciales codificado en base64 (ISO-8859-1)

Parámetros URL: Ninguno

Parámetros cuerpo solicitud:


| Tipo      | Descripción                     | Mensaje                                                              | 
|-----------|---------------------------------|--------------------------------------------------------------------- |
| String    | Mensaje conexión establecida    | Conexión establecida con LegisOffice Servicio de vigilancia judicial | 
|-----------|---------------------------------|--------------------------------------------------------------------- |
| String    | Mensaje conexión establecida    | Conexión establecida con LegisOffice Servicio de vigilancia judicial | 
|-----------|---------------------------------|--------------------------------------------------------------------- |
| String    | Mensaje conexión establecida    | Conexión establecida con LegisOffice Servicio de vigilancia judicial | 

## ActualizarActuacion

Método HTTP: PUT
Actualiza la información de una actuación y retorna si se pudo actualizar o no.
INFORMACIÓN SOLICITUD
Cabecera de autenticación: Authentication = Token – Espacio – Guid obtenido como respuesta al consumir el método ValidarCredenciales codificado en base64 (ISO-8859-1)

Parámetros URL: Ninguno

Parámetros cuerpo solicitud:

## EliminarActuacion	

Método HTTP: POST
Elimina una actuación y los documentos asociados a la misma. Retorna si se pudo realizar la eliminación o no.
INFORMACIÓN SOLICITUD
Cabecera de autenticación: Authentication = Token – Espacio – Guid obtenido como respuesta al consumir el método ValidarCredenciales codificado en base64 (ISO-8859-1)

Parámetros URL: Ninguno

Parámetros cuerpo solicitud:

```javascript
using (HttpClient client = new HttpClient())
{
    client.BaseAddress = new Uri("https://VJ.legisoffice.com/LoServiceVJ/");
    // token = AF4E27DB-1DCE-4FE2-9B13-AF7255C542EE
    // El valor del token se envía codificado en base64 Encoding ISO-8859-1.
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Token", token.ToString().ToBase64());
    
    var model = new RegistrarActuacionModel() 
    { 
        Oficina = "general",
        Caso = "532ADE8F-895B-4C34-A7DA-4D07FEAAAE06",
        Titulo = "Actuación 1",
        Descripcion = "Descripción para la actuación 1",
        Fecha = DateTime.Now,
        Radicado = "742756423189720013165000",
        Juzgado = "Nombre Completo del juzgado "
        CodigoExterno = "Codigo o ID del caso que maneja el proveedor "
    };

    var content = new StringContent(JsonConvert.SerializeObject(model), Encoding.UTF8, "application/json");
    var response = client.PostAsync("vj/RegistrarActuacion", content).Result;

    if (response.IsSuccessStatusCode)
    {
        string result = response.Content.ReadAsStringAsync().Result;
        var idActuacion = JsonConvert.DeserializeObject<int?>(result);
    }}
```