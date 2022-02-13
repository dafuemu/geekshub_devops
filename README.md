# Proyecto final

El servicio accounts está desplegado en un cluster de k8s en DigitalOcean. Se puede consultar el estado en:

```
curl 67.207.72.58/actuator/health
```

El objectivo del proyecto era tener un repositorio con el que poder crear un cluster de k8s en AWS, puede hacerlo y el repo es [este](https://github.com/dafuemu/eks-aws-terraform). Finalmente para poder mantener el cluster sin costes opte por DigitalOcena y el repositorio para crear el
cluster es [este](https://github.com/dafuemu/eks-digitalocean-terraform) el cual tiene su propio workflow que basicamente ejecuta los comandos basicos de terraform
para iniciar y aplicar los cambios.

En el cluster hay 3 nodos como minimo 5 como máximo, y en este cluster esta desplegado:

- Account service: Aplicación backend [repo](https://github.com/dafuemu/hexagoanl-java-spring)
- Mysql base de datos: Base de datos a la que se conectaría el servicio, de momento solo es una instancia pero la idea era montar un cluster [repo](https://github.com/dafuemu/mysql_k8_deployment)

Pendiente:
- EFK: Elastic Search, Fluentd y Kibana: El stack para logging, aunque también proporciona monitoring y tracing ()
- Prometheus, Grafana, AlertManager: Stack para Monitoring


Para provisionar el cluster de kubernetes hay otras opciones como **kops** o **helm** por ejemplo, pero he optado por montarlo aplicando los recursos definidos en los diferentes ficheros **yaml**. También me sirve para saber que recursos se necesita desplegar en k8s para cada stack.

## Mejore practicas apara sistemas de almacenamiento
If you are planning to deploy stateful applications, such as Oracle, MySQL, Elasticsearch, and MongoDB, then using StatefulSets is a great option. The following points need to be considered while creating stateful applications:

- Create a separate namespace for databases.
- Place all the needed components for stateful applications, such as ConfigMaps, Secrets, and Services, in the particular namespace.
- Put your custom scripts in the ConfigMaps.
- Use headless service instead of load balancer service while creating Service objects.
- Use the HashiCorp Vault for storing your Secrets.
- Use the persistent volume storage for storing the data. Then your data won’t be deleted even if the Pod dies or crashes.

