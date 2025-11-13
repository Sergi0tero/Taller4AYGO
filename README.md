
# Reporte del Desafío AWS CDK

## 1. Introducción
Este reporte presenta los resultados del desafío de AWS CDK, cuyo objetivo fue introducir el uso del **Cloud Development Kit (CDK)** de AWS como un marco de **Infraestructura como Código (IaC)**.  
El CDK permite definir infraestructura en la nube utilizando lenguajes de programación comunes, facilitando la automatización, escalabilidad y mantenimiento del entorno en AWS.

---

## 2. Configuración del Entorno y Bootstrap de CDK
Se instaló la **CDK CLI** siguiendo la documentación oficial de AWS.  
Dado que en el entorno de **AWS Academy Learner Lab** no se permite la creación de roles de IAM, fue necesario crear manualmente el archivo `bootstrap-template.yaml` de forma local.  

### Ajustes realizados en `bootstrap-template.yaml`
- Se **eliminaron** o **comentaron** las secciones del template que intentaban crear roles de IAM (ya que la plataforma no permite crear IAM roles nuevos).  
- Se **reemplazaron** las referencias a roles recién creados por el **rol proporcionado por el laboratorio**: **LabRole**. En mi caso utilicé el ARN que proporciona el entorno del lab: `arn:aws:iam::779616496726:role/LabRole`.  
- Con este cambio, los recursos del bootstrap usan el rol existente (`LabRole`) en lugar de esperar la creación de nuevos roles por parte del template.

<img width="921" height="501" alt="image" src="https://github.com/user-attachments/assets/3a37cf92-e9a7-482d-9380-c1cf7e731117" />
<img width="921" height="437" alt="image" src="https://github.com/user-attachments/assets/c7ce4d93-a983-4e18-99b3-a5de397d9f5d" />


---

## 3. Implementación y Despliegue de la Función Lambda con CDK
Se desarrolló una aplicación web sencilla basada en **AWS Lambda**, siguiendo el tutorial oficial de AWS.  
La función Lambda fue configurada para ejecutarse con el runtime **Node.js 20.x**, respondiendo con el mensaje `"Hello World!"`.  
Posteriormente, se desplegó el stack con éxito mediante **AWS CDK**, verificándose su correcta creación en el servicio **CloudFormation**.

<img width="921" height="577" alt="image" src="https://github.com/user-attachments/assets/c8bdada3-f822-4743-ab85-e4b80f693e93" />
<img width="921" height="402" alt="image" src="https://github.com/user-attachments/assets/c701e210-4399-4adc-b1a5-15f7c673555d" />

---

## 4. Prueba de la Función Lambda
Una vez desplegada la infraestructura, se probó el enlace público generado por el CDK para la función Lambda.  
La ejecución devolvió correctamente la respuesta `"Hello World!"`, confirmando el éxito del despliegue y funcionamiento de la aplicación.

<img width="921" height="201" alt="image" src="https://github.com/user-attachments/assets/93df5b6c-a875-49e4-b5d6-9025a1096773" />

---

## 5. Notas técnicas adicionales
- En el código del stack (implementado en Java), la función Lambda fue creada utilizando `Role.fromRoleArn(..., "arn:aws:iam::779616496726:role/LabRole")` para enlazar explícitamente el `LabRole` provisto por el entorno.  
- Si en un futuro se va a ejecutar el mismo CDK stack en una cuenta propia con permisos completos, se puede restaurar el `bootstrap-template.yaml` original (o generar uno nuevo) que cree los roles necesarios automáticamente, y eliminar la referencia fija al `LabRole` en el código.

---

## 6. Conclusiones
El laboratorio permitió comprender el proceso completo de creación, configuración y despliegue de una función Lambda mediante **AWS CDK**, incluyendo cómo adaptar el flujo cuando el entorno tiene restricciones de IAM.  
Al documentar y versionar el `bootstrap-template.yaml` modificado y explicar el uso de `LabRole`, se facilita la reproducibilidad del ejercicio y la comprensión de las adaptaciones realizadas para AWS Academy.
