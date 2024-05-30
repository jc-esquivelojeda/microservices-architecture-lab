# Laboratorio de diseño e implementacion de arquitectura de microservicios

## Documentación de la arquitectura y ruta de migracion: 

  La ruta de migracion propuesta contiene los siguientes procesos:

  - Para disminuir la probabilidad de downtime y agilizar el proceso de migracion se sugiere utilizar el patron de la enredadera o strangler fig, el cual sugiere la creacion de servicios que funcionen a la par con la solucion monolitica,
  se empezaria realizando los servicios menos criticos para ir reduciendo carga al monolito hasta que finalmente se separen en microservicios la totalidad de las funciones
  - Para la comunicacion entre microservicios se  utilizara comunicacion asincrona mediante mensajeria basada en eventos con una cola de mensajes como activeMQ o kafka para la comunicacion entre los servicios
  - Para el manejo de informacion  cada servicio debera tener su propia base de datos con el fin de cumplir con el aislamiento de datos, dicha informacion solo podrá ser consultada desde su respectivo microservicio
  -  Para el registro de las peticiones se creara un logging centralizado para registrar la interaccion con los servicios y validar en caso de que se presente algun incidente
  -  Para el  manejo el enrutamiento entre las peticiones del monolito y de los microservicios se creara un api gateway 
  -  Para iniciar el proceso de migracion de microservicios implicara separar las funcionalidades por dominios como a continuacion se describe:
      - <strong>usuarios:</strong> aqui se manejaran las operaciones de login, logout, registro del usuario, actualizacion del perfil y cancelacion de cuenta como ejemplos
      - <strong>Productos:</strong> este microservicio se encargara de las funcionalidades de busqueda de productos en sus multiples combinaciones como busqueda paginada, por termino de busqueda, por id de producto y detalle de producto, asi como las acciones crud para los productos
      - <strong>Pedidos:</strong> en este servicio se manejaran las operaciones relacionadas con el pedido como creacion actualizacion y cancelacion de pedidos asi como la actualizacion y consulta de estatus
      - <strong>soporte:</strong> aqui se manejara el manejo de tickets de aclaracion, consulta del estado de una aclaracion y reportes de algun incidente con los pedidos 
  - Realizar la Migración de los microservicios desde los mas basicos hasta los mas complejos como sigue:
      1. <strong>Primera etapa:</strong> Soporte, la funcionalidad de tickes de soporte no representan una funcionalidad critica del sistema por lo que como piloto de pruebas seria ideal para no afectar la funcionalidad principal que es vender
      2. <strong>Segunda etapa:</strong> Usuarios, si bien el correcto ingreso a la aplicacion representa un mayor impacto que el punto anterior, al no estar fuertemente acoplada con  otras funcionalidades, se pueden empezar a  migrar los microservicios de las funcionalidades que involucren incios y cierres de de sesion hasta cumplir con todas las acciones para este dominio  
      3. <strong>Tercera etapa:</strong> Productos, para el caso de este dominio la consulta de productos pudiera presentar el que mas impacto al performance presente por lo que se pudiera dejar al ultimo sin embargo creo que el pedido es el mas critico de todos ya que representa la operacion que genera ingresos   
      4. <strong>Cuarta etapa:</strong> Pedidos, al ser el core del sistema ecommerce se le debe de dar mayor peso, ademas de que requiere que los demas servicios ya se encuentren funcionando completamente por lo que seria este el ultimo en implementarse
                
A continuacion se presenta el diagrama a nivel general de la arquitectura de microservicios, adicionalmente incluye donde quedaria acoplado el monolito en el inter en lo que se migra la todalidad de los microservicios:

![microservicios drawio](https://github.com/jc-esquivelojeda/microservices-architecture-lab/assets/123103329/625fa197-14aa-4bbe-b5b0-121f2918ed28)


