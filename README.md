#     Tekton-OpenShift-HelloWorld
_Este repositorio contiene los archivos necesarios para generar un "Hola mundo" usando pipelines de Tekton en un cluster de Red Hat Openshift_





## Prerrequisitos
1. Tener una cuenta en [IBM Cloud](https://cloud.ibm.com/) con un grupo de recursos disponible (puede ser el _Default_).
2. Una api key para la cuenta de IBM Cloud.
3. Un cluster de de Kubernetes en la cuenta de IBM Cloud.
4. Tener una cuenta de [GitHub](https://github.com).





## Procedimiento
### Crear servicio de _Continuous Delivery_ en IBM Cloud
En IBM Cloud entre al apartado **Catalog** > **Developer tools** > **Continuous Delivery**.

INGRESAR GIF 1

Llene los siguientes campos:
 - **Select a location**: Selecione la locación donde está su cluster.
 - **Select a pricing plan**: Selecciona la opción _Lite_.
 - **Service name**: Ingrese un nombre para el servicio.
 - **Select a resource group**: Seleccione el grupo de recursos donde está su cluster.
Acepte términos y condiciones y dé click en **Create**

### Clonar/Descargar repositorio de Github
En su cuenta de Github copie el contenido de este repositorio.

### Crear servicio de _Toolchain_ en IBM Cloud
En IBM Cloud entre al apartado **Catalog** > **Developer tools** > **Toolchain** > **Build your own**. 

INGRESAR GIF 2

Llene los siguientes campos:
  - **Toolchain name**: Ingrese un nombre para el _toolchain_.
  - **Select region**: Selecione la locación donde está su cluster.
  - **Select a resource group**: Seleccione el grupo de recursos donde está su cluster.
Dé click en **Create**.

### Agregar Github y Delivery Pipeline
Se encontrará en la pestaña **Overview**, dé click en **Add** > **Github**, llené los siguientes campos:
 - **GitHub Server**: Seleccione _Github_.
 - **Auth type**: Seleccione _OAtuh_.
 - **Repository type**: Seleccione _Existing_.
 - **Repository URL**: Ingrese el enlace del repositorio donde copió los archivos de este repositorio.
 - **Git Integration Owner**: Seleccione su nombre de usuario de Github.
 - Deje los demás campos por defecto.
 - Dé click en **Create Integration**.
Ya queda configurado el repositorio, ahora se debe agregar el _Delivery Pipeline_, nuevamente dé click en **Add** > **Delivery Pipeline**, llené los siguientes campos:
  - **Pipeline name**: Un nombre para su _Pipeline_.
  - **Pipeline type**: Seleccione _Tekton_.
 - Dé click en **Create Integration**.
Si no hemos creado el _Continuous Delivery_ o lo creamos en un grupo de recursos distinto, se obtiene un mensaje de advertencia donde nos pedirá crearlo _Continuous Delivery service required_.

## Configuración Delivery Pipeline
En la vista **Overview** obtendremos los nombres de las integraciones creadas. Dé click sobre la integración del _Delivery Pipeline_. Llene los apartados de la siguiente manera:
 - **Definitions**: Dé click en **Add** y seleccione su repositorio agregado anteriormente y dé click en **Add** > **Save**.
 - **Worker**: Seleccione el _Worker_ público de su locación y dé click en **Save**.
 - **Environment properties**: Dando click en **Add**, agregue las siguientes propiedades de entorno:
   - **


INGRESAR IMAGEN 1


















Autores: IBM Cloud Tech Sales - Juan Diego Tovar Cárdenas.






Use a Tekton pipeline to build and deploy a simple hello world node application with IBM Cloud Devops ( https://cloud.ibm.com/devops).

The `.tekton` folder contains Tekton Resource definitions that create a Tekton PipelineRun. This "runs" a pipeline that builds a simple node application into an image, scans the image for vulnerabilities, and then deploys the application with IBM Cloud Kubernetes Service.

In order to build and deploy to your own cluster this sample requires parameterization of the following:
- `apikey` an IBM Cloud API Key
- `cluster` the name of your IKS cluster where you will be deploying the sample app
- `clusterNamespace` the namespace in your cluster where the app will be deployed (default: `prod`) (**\<su-nombre>-ns**)
- `clusterRegion` the region where your IKS cluster is located (default: `us-south`)
- `registryNamespace` the IBM Cloud Container Registry namespace where the app image will be built and stored. (**tekton-handson**)
- `registryRegion` the region where your  IBM Cloud Container Registry is located (default: `us-south`)
- `repository` the source git repository where your resources are cloned (default: `https://github.com/open-toolchain/hello-tekton`). Change this if you are forking this repo
- `revision` the branch of the source git repository where your resources are cloned (default: `master`).
