# Paso 2: Configurar API Gateway

## En la carpeta /gateway:

1. **Crear un Proyecto NestJS**
   - Asegúrate de estar en la carpeta `gateway`:
     ```bash
     cd Control-Machinery/gateway
     ```
   - Ejecuta el siguiente comando para crear un nuevo proyecto NestJS en la carpeta actual:
     ```bash
     nest new .
     ```
   - Selecciona las opciones deseadas durante la creación del proyecto.

2. **Instalar Dependencias Necesarias**
   - Asegúrate de tener las dependencias necesarias para el API Gateway. Puedes necesitar `@nestjs/microservices` y `@nestjs/axios`:
     ```bash
     npm install @nestjs/microservices @nestjs/axios
     ```

3. **Configurar el API Gateway**
   - Abre el archivo `main.ts` y configúralo para que actúe como el punto de entrada para todos los microservicios. Aquí tienes un ejemplo básico de configuración:

     ```typescript
     import { NestFactory } from '@nestjs/core';
     import { AppModule } from './app.module';
     import { MicroserviceOptions, Transport } from '@nestjs/microservices';

     async function bootstrap() {
       const app = await NestFactory.create(AppModule);
       const microservice = app.connectMicroservice<MicroserviceOptions>({
         transport: Transport.TCP,
         options: {
           host: 'localhost',
           port: 3001,
         },
       });

       await app.startAllMicroservices();
       await app.listen(3000);
       console.log('API Gateway is running on: http://localhost:3000');
     }
     bootstrap();
     ```

4. **Probar la Comunicación Básica entre Microservicios**
   - Para probar la comunicación básica, puedes crear un microservicio simple. Asegúrate de que tu microservicio esté configurado para escuchar en el puerto que especificaste (en este caso, 3001).
   - Puedes usar un cliente como Postman o Insomnia para enviar solicitudes al API Gateway y verificar que la configuración sea correcta.

5. **Estructura de Directorios Final en /gateway**
   Después de completar el Paso 2, tu estructura de directorios debería verse así:

