         ___        ______     ____ _                 _  ___  
        / \ \      / / ___|   / ___| | ___  _   _  __| |/ _ \ 
       / _ \ \ /\ / /\___ \  | |   | |/ _ \| | | |/ _` | (_) |
      / ___ \ V  V /  ___) | | |___| | (_) | |_| | (_| |\__, |
     /_/   \_\_/\_/  |____/   \____|_|\___/ \__,_|\__,_|  /_/ 
 ----------------------------------------------------------------- 
### Multi-website Practice with AWS CloudFront

#### Step 1:
- **Create 2 S3 Buckets:**
  - Disable public access blocking.
  - Enable static website hosting in the Properties tab, with the index.html document.
  - Add the following policy in the Permissions tab:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": [
            "s3:GetObject"
          ],
          "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
      ]
    }
    ```
  - Create a folder named "shop" in bucket 1.

#### Step 2:
- **Create a Cloud9 environment with t2.small:**
  - Run the following commands:
    ```bash
    wget https://www.free-css.com/assets/files/free-css-templates/download/page287/eflyer.zip
    unzip eflyer.zip
    aws s3 cp html/ s3://web-corporativa-ed/shop/ --recursive
    git clone https://github.com/mdyeates/my-portfolio.git
    cd my-portfolio/
    npm install
    npm run build
    aws s3 cp build/ s3://web-corporativa-ed2/ --recursive
    ```

#### Step 3:
- **Create a CloudFront Distribution:**
  - Choose the S3 bucket (nombre-bucket-2) where the portfolio is hosted as the origin.
  - Once CloudFront is created, go to Settings to change the document root to index.html.
  - Create a new origin in Origins and choose bucket 1.
  - Go to the Behaviors tab, and add a behavior with the path "/shop/*" and choose the S3 bucket (nombre-bucket-1) where the ecommerce template is hosted.

---
Feel free to adjust the placeholders ("YOUR_BUCKET_NAME", "nombre-bucket-1", "nombre-bucket-2") with your actual bucket names.

### Español:
### Práctica de Multi-sitio con AWS CloudFront

#### Paso 1:
- **Crear 2 Buckets de S3:**
  - Deshabilitar el bloqueo de acceso público.
  - Habilitar el hospedaje de sitio web estático en la pestaña Propiedades, con el documento index.html.
  - Agregar la siguiente política en la pestaña Permisos:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": [
            "s3:GetObject"
          ],
          "Resource": "arn:aws:s3:::NOMBRE_DE_TU_BUCKET/*"
        }
      ]
    }
    ```
  - Crear una carpeta llamada "shop" en el bucket 1.

#### Paso 2:
- **Crear un entorno Cloud9 con t2.small:**
  - Ejecutar los siguientes comandos:
    ```bash
    wget https://www.free-css.com/assets/files/free-css-templates/download/page287/eflyer.zip
    unzip eflyer.zip
    aws s3 cp html/ s3://web-corporativa-ed/shop/ --recursive
    git clone https://github.com/mdyeates/my-portfolio.git
    cd my-portfolio/
    npm install
    npm run build
    aws s3 cp build/ s3://web-corporativa-ed2/ --recursive
    ```

#### Paso 3:
- **Crear una Distribución de CloudFront:**
  - Elegir el bucket de S3 (nombre-bucket-2) donde se aloja el portafolio como origen.
  - Una vez creada la distribución de CloudFront, ir a Configuración para cambiar la raíz del documento por index.html.
  - Crear un nuevo origen en Orígenes y elegir el bucket 1.
  - Ir a la pestaña de Comportamientos, y agregar un comportamiento con la ruta "/shop/*" y elegir el bucket de S3 (nombre-bucket-1) donde se aloja la plantilla del comercio electrónico.

---
Siéntete libre de ajustar los marcadores de posición ("NOMBRE_DE_TU_BUCKET", "nombre-bucket-1", "nombre-bucket-2") con los nombres reales de tus buckets.

