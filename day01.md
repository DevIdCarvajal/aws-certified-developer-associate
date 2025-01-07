# Tema 1: Introducción a AWS

## Regiones

Una **región** es uno de los centros físicos repartidos por el mundo donde Amazon tiene su infraestructura.

Los principales **criterios de selección de región**, dependiendo de cada caso, son:

1. Latencia
2. Precio
3. Disponibilidad de servicios
4. Regulación

Una región tiene varias **zonas de disponibilidad (Availability Zone, AZ)**, que a su vez tienen uno o más centros de datos.

Se dice **alta disponibilidad (High Availability, HA)** cuando se tienen varias zonas de disponibilidad por región: **HA = AZ<sup>+</sup>**

Las **localizaciones en el borde (edge locations)** permiten replicar servicios, generando una CDN (content delivery network).

Las **herramientas** de trabajo con AWS habituales son:

- **Consola** en navegador web
- **CLI (Command Line Interface)** en consola de comandos
- **SDK (Software Development Kit)** para lenguajes de programación

En términos de seguridad, se dice que **la responsabilidad es compartida** entre Amazon y el cliente que usa sus servicios.

## Administración de Identidades

**Identity and Access Management (IAM)** es un servicio global que permite gestionar los permisos y accesos de una cuenta.

**Características**

- Integrado con otros servicios
- Acceso compartido
- MFA
- Federación de identidad
- Gratis

**Tipos de usuario y buenas prácticas**

1. **Usuario raíz**: Debe tener una contraseña fuerte, autenticación multifactor y no debe usarse para las tareas del día a día, tan solo para crear otros usuarios y asignarles permisos.
2. **Usuario IAM**: Identidades que representan personas o aplicaciones que acceden a los servicios conforme a unas políticas.

**Políticas IAM**

Una **política (policy)** es un documento que otorga o deniega permisos a servicios y recursos:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "service-prefix:action-name",
      "Resource": "*",
      "Condition": {
        "DateGreaterThan": {
          "aws:CurrentTime": "2020-04-01T00:00:00Z"
        },
        "DateLessThan": {
          "aws:CurrentTime": "2020-06-30T23:59:59Z"
        }
      }
    }
  ]
}
```

Como buena práctica, **se debe seguir siempre el principio de menor privilegio**, por el que ante la duda, se otorga la menor cantidad de permisos posible.

**Grupos IAM**

Un **grupo** permite crear un conjunto de políticas de acceso de manera para que varios usuarios asignados a dicho grupo tengan las mismas políticas.

Como buena práctica, se debe crear siempre grupos y asignar usuarios a esos grupos, en lugar de crear usuarios individuales.

**Roles IAM**

Un **rol** es una identidad asumido por una persona o servicio para que tenga **acceso temporal** a otros recursos o servicios.
