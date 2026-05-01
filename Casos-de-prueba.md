Casos de Prueba: Flujo de Recuperación de Contraseña
​Módulo: Gestión de Usuarios / Autenticación
Ambiente: Aplicación Móvil (Android/iOS)
Documentación de Referencia: Especificaciones de Login v2.0
​ID: TC-001 | Título: Recuperación de contraseña exitosa (Happy Path)
​Precondiciones: El usuario tiene una cuenta activa y el correo electrónico está registrado en la base de datos.
​Pasos:
​Abrir la aplicación.
​Tocar en "Olvidé mi contraseña".
​Ingresar el correo electrónico válido: usuario_test@streaming.com.
​Tocar el botón "Enviar instrucciones".
​Abrir la bandeja de entrada del correo y hacer clic en el enlace de recuperación.
​Ingresar una nueva contraseña válida y confirmar.
​Resultado Esperado: El sistema debe mostrar un mensaje de éxito y permitir el login con la nueva contraseña.
​Datos de Prueba: Correo: usuario_test@streaming.com | Nueva Clave: Password2026!.
​ID: TC-002 | Título: Validación de límite de caracteres en campo Email (Edge Case)
​Precondiciones: La pantalla de recuperación de contraseña está abierta.
​Pasos:
​Ingresar un correo electrónico con una longitud superior a 50 caracteres.
​Intentar presionar el botón "Enviar instrucciones".
​Resultado Esperado: El sistema debe manejar correctamente la cadena larga, ya sea permitiendo el envío si es un formato válido o mostrando un error de validación de longitud antes de procesar. No debe ocurrir un cierre inesperado (crash).
​Datos de Prueba: usuario_con_un_nombre_extremadamente_largo_para_test_de_limites@streaming.com.
​ID: TC-003 | Título: Intento de SQL Injection en campo de recuperación (Negative Test)
​Precondiciones: El sistema está en la pantalla de "Olvidé mi contraseña".
​Pasos:
​Ingresar la siguiente cadena en el campo de correo: ' OR 1=1 --.
​Tocar el botón "Enviar instrucciones".
​Resultado Esperado: El sistema debe sanitizar la entrada y mostrar el mensaje de error estándar: "Correo electrónico no válido o no encontrado". Bajo ninguna circunstancia debe devolver información de la base de datos o saltar la validación.
​Datos de Prueba: ' OR 1=1 --.
​ID: TC-004 | Título: Uso de token de recuperación expirado (Negative Test)
​Precondiciones: El usuario ha solicitado un correo de recuperación, pero el token ha superado su tiempo de vida (ej. 24 horas).
​Pasos:
​Abrir el correo de recuperación recibido anteriormente (expirado).
​Hacer clic en el enlace de recuperación de contraseña.
​Resultado Esperado: La aplicación o el sitio web de destino deben mostrar el mensaje: "El enlace de recuperación ha expirado. Por favor, solicite uno nuevo". No debe permitir el cambio de clave.
​Datos de Prueba: Token generado hace >24 hs.
​ID: TC-005 | Título: Formato de correo electrónico inválido (Negative Test)
​Precondiciones: El usuario está en la pantalla de recuperación de contraseña.
​Pasos:
​Ingresar un texto que no cumpla con la estructura de correo: usuario#streaming.com.
​Intentar enviar la solicitud.
​Resultado Esperado: El botón "Enviar" debe permanecer deshabilitado o debe aparecer un mensaje de error en tiempo real: "Por favor, ingrese un formato de correo electrónico válido".
​Datos de Prueba: usuario#streaming.com | test@com | sin_arroba.com
