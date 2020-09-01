# Hola Mundo Serverless

1. [Instalar serverless](#serverless)
2. [Hola mundo](#new)
3. [Endopoint con API Gateway](#apigateway)

<a name="serverless"></a>
## Instalar Serverless y configuración inicial

Para instalar serverless 

~~~
sudo npm install -g serverless  
~~~
 
Creamos unas nuevas credenciales en nuestra cuenta de AWS y copiamos la key y el secret para utilizarlo en la configuración del servicio 
 
~~~
serverless config credentials --provider aws --key <key> --secret <secret> 
~~~
<a name="new"></a>
## Nuevo proyecto

Creamos el proyecto estableciendo el proveedor y el lenguaje en el template y le damos un nombre 

~~~
serverless create --template aws-nodejs --name curso-sls-hola-mundo 
~~~

Esto nos genera dos archivos **handler.js**  con la función que vamos a desarrollar:
 
~~~
module.exports.hello = async event => {
  return { 
    statusCode: 200, 
    body: JSON.stringify(
      {
        message: 'Go Serverless v1.O! Your function executed successfully!,
        input: event, 
      }
      null,
      2
    )
  };
}
~~~

y  **serverless.yml** con los parámetros de configuración.

Para desplegar el proyecto en nuestra cuenta de AWS utilizaremos el siguiente comando: 

~~~
sls deploy 
~~~

Si únicamente queremos desplegar una función en concreto (caso de proyecto con muchas funciones) 
 
~~~
sls deploy –f nombreFuncion –s entorno(dev, pro...) 
~~~
 
Para ejecutar la función en remoto: 

~~~
sls invoke -f nombreFuncion -s entorno(dev, pro...) 
~~~

Si queremos ejecutarla en local añadimos el parámetro *local* después de *invoke*

A esta invocación podemos pasarle parámetros de esta forma 

~~~
sls invoke local -f hello -s dev -d '{"name": "Abel Alonso"}' 
~~~

El parámetro llega a la función en la variable *event*

<a name="apigateway"></a>
## Endpoint con API Gateway

En el archivo **serverless.yaml** añadimos dentro de la función el evento desencadenador: 

~~~
functions:
  hello:
    handler: handler.hello 
    events: 
      - http: 
          path: hols-mundo
          method: get
~~~

   ***Mucho ojo con la tabulación entre http y path***

Volvemos a desplegar y el cambio relizado en serverless.yaml hará que en la lamda se genere un desencadenador de api gateway de forma automática. Podemos comprobar que esto funciona entrando en la URL que se genera al hacer el deploy. 

En la consola de AWS podemos comprobar que efectivamente se ha creado un trigger para el get a esa url 
