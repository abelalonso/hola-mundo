# Hola Mundo Serverless

## Instalar Serverless y configuración inicial

Para instalar serverless 

~~~
sudo npm install -g serverless  
~~~
 
Creamos unas nuevas credenciales en nuestra cuenta de AWS y copiamos la key y el secret para utilizarlo en la configuración del servicio 
 
~~~
serverless config credentials --provider aws --key <key> --secret <secret> 
~~~

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

 

sls invoke local -f hello -s dev -d '{"name": "Abel Alonso"}' 

 

El parámetro llega a la función en la variable event 

 
