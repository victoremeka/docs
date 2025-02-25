---
title: Configurar la visibilidad y el control de accesos de un paquete
intro: 'Elige quién ha leído, escrito, o administrado el acceso a tu imagen de contenedor y la visibilidad de tus imágenes de contenedor en {% data variables.product.prodname_dotcom %}.'
product: '{% data reusables.gated-features.packages %}'
redirect_from:
  - /packages/managing-container-images-with-github-container-registry/configuring-access-control-and-visibility-for-container-images
  - /packages/guides/configuring-access-control-and-visibility-for-container-images
versions:
  fpt: '*'
  ghec: '*'
  ghes: '*'
shortTitle: Access control & visibility
ms.openlocfilehash: 8ef541f45fd6568db7c8510bc860d81d504494c5
ms.sourcegitcommit: 6185352bc563024d22dee0b257e2775cadd5b797
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2022
ms.locfileid: '148193061'
---
{% data reusables.package_registry.container-registry-ghes-beta %}{% ifversion packages-registries-v2 %}

Los paquetes con permisos granulares tienen un alcance de una cuenta personal o de organización. Puedes cambiar la visibilidad y el control de accesos de un paquete por separado desde el repositorio al cual está conectado (o enlazado).

Algunos registros solo admiten permisos con ámbito de repositorio. Para obtener la lista de estos registros, consulta "[Acerca de los permisos de {% data variables.product.prodname_registry %}](/packages/learn-github-packages/about-permissions-for-github-packages#permissions-for-repository-scoped-packages)".

{% else %}Un paquete hereda los permisos y la visibilidad del repositorio que lo posee.{% endif %} Para obtener más información sobre los permisos para los paquetes, los ámbitos relacionados con los paquetes para PAT o la administración de permisos para los flujos de trabajo de acciones, consulta "[Acerca de los permisos para paquetes de GitHub](/packages/learn-github-packages/about-permissions-for-github-packages)".

{% ifversion packages-registries-v2 %}

## Permisos de visibilidad y acceso para las imágenes de contenedor

{% data reusables.package_registry.visibility-and-access-permissions %}

{% endif %}

## Configurar el acceso a las imágenes de contenedor para tu cuenta personal

Si tienes permisos administrativos en una imagen de contenedor que pertenece a una cuenta personal, puedes asignar roles de lectura, escritura o administrador a otros usuarios. Para obtener más información sobre estos roles de permisos, consulte "[Visibilidad y permisos de acceso para imágenes de contenedor](#visibility-and-access-permissions-for-container-images)".

Si tu paquete es privado o interno y le pertenece a una organización, entonces solo puedes darles acceso a otros miembros o equipos de la misma.

{% data reusables.package_registry.package-settings-option %}
1. En la página de configuración del paquete, haga clic en **Invite teams or people** y escriba el nombre real, el nombre de usuario o la dirección de correo electrónico de la persona a la que quiera conceder acceso. No se puede otorgar acceso a los equipos para aquellas imágenes de contenedor que pertenezcan a una cuenta personal.
  ![Botón de invitación para acceder al contenedor](/assets/images/help/package-registry/container-access-invite.png)
1. Junto al equipo o nombre de usuario, utiliza el menú desplegable de "Rol" para seleccionar un nivel de permisos que desees.
  ![Opciones de acceso al contenedor](/assets/images/help/package-registry/container-access-control-options.png)

Se otorgará acceso automáticamente a los usuarios seleccionados y no necesitarán aceptar una invitación previamente.

## Configurar el acceso a las imágenes de contenedor para una organización

Si tienes permisos administrativos en una imágen de contenedor que pertenezca a una organización, puedes asignar roles de lectura, escritura o administración a otros usuarios y equipos. Para obtener más información sobre estos roles de permisos, consulte "[Visibilidad y permisos de acceso para imágenes de contenedor](#visibility-and-access-permissions-for-container-images)".

Si tu paquete es privado o interno y le pertenece a una organización, entonces solo puedes darles acceso a otros miembros o equipos de la misma.

{% data reusables.package_registry.package-settings-from-org-level %} {% data reusables.package_registry.package-settings-option %}
1. En la página de configuración del paquete, haga clic en **Invite teams or people** y escriba el nombre real, el nombre de usuario o la dirección de correo electrónico de la persona a la que quiera conceder acceso. También puedes ingresar un nombre de equipo desde la organización para otorgar acceso a todos los miembros de éste.
  ![Botón de invitación para acceder al contenedor](/assets/images/help/package-registry/container-access-invite.png)
1. Junto al equipo o nombre de usuario, utiliza el menú desplegable de "Rol" para seleccionar un nivel de permisos que desees.
  ![Opciones de acceso al contenedor](/assets/images/help/package-registry/container-access-control-options.png)

Se otorgará acceso automáticamente a los usuarios o equipos seleccionados y no necesitarán aceptar una invitación previamente.

## Heredar el acceso a una imagen de contenedor desde un repositorio

Para simplificar la administración de paquetes a través de los flujos de trabajo de {% data variables.product.prodname_actions %}, puedes habilitar a una imagen de contenedor para que herede los permisos de acceso de un repositorio predeterminadamente.

Si heredas los permisos de acceso del repositorio en donde se almacenan los flujos de trabajo de tu paquete, entonces puedes ajustar el acceso al mismo a través de los permisos del repositorio.

Una vez que el repositorio se sincronice, no podrás acceder a la configuración de acceso granular del paquete. Para personalizar los permisos de paquete a través de la configuración de acceso granular del paquete, primero debes sincronizar el repositorio.

{% data reusables.package_registry.package-settings-from-org-level %} {% data reusables.package_registry.package-settings-option %}
2. En "Repository source", seleccione **Inherit access from repository (recommended)** .
  ![Casilla de verificación para heredar el acceso al repositorio](/assets/images/help/package-registry/inherit-repo-access-for-package.png)

## Garantizar el acceso al flujo de trabajo para tu paquete

Para garantizar que el flujo de trabajo de {% data variables.product.prodname_actions %} tiene acceso a tu paquete, debes otorgar acceso explícito al repositorio en donde se almacena el flujo de trabajo.

El repositorio especificado no necesita ser aquél en donde se mantiene el código fuente del paquete. Puedes dar acceso de flujo de trabajo a un paquete para varios repositorios.

{% note %}

**Nota:** La sincronización de la imagen de contenedor con un repositorio mediante la opción de menú **Action access** no es lo mismo que conectar el contenedor a un repositorio. Para obtener más información sobre cómo vincular un repositorio al contenedor, consulte "[Conexión de un repositorio a un paquete](/packages/learn-github-packages/connecting-a-repository-to-a-package)".

{% endnote %}

### Acceso de {% data variables.product.prodname_actions %} para las imágenes de contenedor que pertenecen a cuentas de usuario 

{% data reusables.package_registry.package-settings-option %}
1. En la barra lateral de la izquierda, haga clic en **Actions access**.
  ![Opción "Actions access" en el menú de la izquierda](/assets/images/help/package-registry/organization-repo-access-for-a-package.png)
2. Para garantizar que tu flujo de trabajo tiene acceso a tu paquete de contenedor, debes agregar el repositorio en donde se almacena el flujo de trabajo. Haga clic en **Add repository** y busque el repositorio que quiera agregar.
   ![Botón "Add repository"](/assets/images/help/package-registry/add-repository-button.png)
3. Utilizando el menú desplegable de "rol", selecciona el nivel de acceso predeterminado que te gustaría que tuviera el repositorio en tu imagen de contenedor.
  ![Niveles de acceso de permisos para otorgar a los repositorios](/assets/images/help/package-registry/repository-permission-options-for-package-access-through-actions.png)

Para personalizar aún más el acceso a la imagen de contenedor, consulte "[Configuración del acceso a imágenes de contenedor para su cuenta personal](#configuring-access-to-container-images-for-your-personal-account)".

### Acceso a las {% data variables.product.prodname_actions %} para las imágenes de contenedor que pertenezcan a organizaciones 

{% data reusables.package_registry.package-settings-from-org-level %} {% data reusables.package_registry.package-settings-option %}
1. En la barra lateral de la izquierda, haga clic en **Actions access**.
  ![Opción "Actions access" en el menú de la izquierda](/assets/images/help/package-registry/organization-repo-access-for-a-package.png)
2. Haga clic en **Add repository** y busque el repositorio que quiera agregar.
   ![Botón "Add repository"](/assets/images/help/package-registry/add-repository-button.png)
3. Selecciona el nivel de acceso predeterminado que te gustaría que tuvieran los miembros del repositorio en tu imagen de contenedor utilizando el menú desplegable de "rol". No se incluirá a los colaboradores externos.
  ![Niveles de acceso de permisos para otorgar a los repositorios](/assets/images/help/package-registry/repository-permission-options-for-package-access-through-actions.png)

Para personalizar aún más el acceso a la imagen de contenedor, consulte "[Configuración del acceso a imágenes de contenedor para una organización](#configuring-access-to-container-images-for-an-organization)".

{% ifversion fpt or ghec %}
## Garantizar el acceso de {% data variables.product.prodname_github_codespaces %} al paquete

De manera predeterminada, un codespace puede acceder sin problemas a determinados paquetes que admiten permisos detallados, tales como los paquetes que se publican en el mismo repositorio con la opción de **Heredar acceso** seleccionada. Para obtener una lista de los registros de {% data variables.product.prodname_registry %} que admiten permisos detallados y un acceso sin problemas a {% data variables.product.prodname_github_codespaces %}, consulta "[Acerca de los permisos de {% data variables.product.prodname_registry %}](/packages/learn-github-packages/about-permissions-for-github-packages#granular-permissions-for-userorganization-scoped-packages)".

De otra manera, para asegurarte de que un codespace tiene acceso a tu paquete, debes otorgar acceso al repositorio en donde se esté lanzando dicho codespace.

El repositorio especificado no necesita ser aquél en donde se mantiene el código fuente del paquete. Puedes otorgar acceso a un paquete para los codespaces en diversos repositorios.

Una vez que hayas seleccionado el paquete que quieres compartir con un codespace de un repositorio, puedes otorgar este acceso de repositorio.

1. En la barra lateral derecha, haga clic en **Package settings**.

   ![Opción "Package settings" en el menú de la derecha](/assets/images/help/package-registry/package-settings.png)
   
2. En "Manage Codespaces access", haga clic en **Add repository**.

   ![Botón "Add repository"](/assets/images/help/package-registry/manage-codespaces-access-blank.png)

3. Busca el repositorio que quieras agregar.

   ![Botón "Add repository"](/assets/images/help/package-registry/manage-codespaces-access-search.png)
   
4. Repite los pasos para cualquier repositorio adicional al que quieras otorgarle acceso.

5. Si el codespace para un repositorio ya no necesita acceso a una imagen, puedes eliminar el acceso.

   ![Botón "Remove repository"](/assets/images/help/package-registry/manage-codespaces-access-item.png)

{% endif %}
## Configurar la visibilidad de las imágenes de contenedor para tu cuenta personal

Cuando publicas un paquete por primera vez, la visibilidad predeterminada es privada y solo tú puedes verlo. Puedes modificar el acceso a las imágenes de contenedor públicas si cambias la configuración de acceso.

Se puede acceder anónimamente a un paquete público sin autenticación. Una vez que hagas tu paquete público, no puedes hacerlo privado nuevamente.

{% data reusables.package_registry.package-settings-option %}
5. Debajo de "Zona de peligro", elige una configuración de visibilidad:
    - Para que cualquier usuario pueda ver la imagen de contenedor, haga clic en **Make public**.
    {% warning %}

    **Advertencia:** Una vez que haga público un paquete, no podrá volver a hacerlo privado.

    {% endwarning %}
    - Para que la imagen de contenedor sea visible para una selección personalizada de usuarios, haga clic en **Make private**.
  ![Opciones de visibilidad del contenedor](/assets/images/help/package-registry/container-visibility-option.png)

## Visibilidad de creación de un contenedor para los miembros de una organización

Puedes elegir la visibilidad de los contenedores que los miembros de las organizaciones pueden publicar predeterminadamente.

{% data reusables.profile.access_org %} {% data reusables.profile.org_settings %}
4. En la izquierda, haga clic en **Packages**.
6. Debajo de "Creación de contenedores", elige si quieres habilitar la creación de imágenes de contenedor públicas, privadas o internas.
    - Para permitir que los miembros de la organización creen imágenes de contenedor públicas, haga clic en **Public**.
    - Para permitir a los miembros de la organización crear imágenes de contenedor privadas que solo sean visibles para otros miembros de la organización, haga clic en **Private**. Puedes personalizar aún más la visibilidad de las imagenes de contenedor privadas.
    - Para permitir a los miembros de la organización crear imágenes de contenedor internas que sean visibles para todos los miembros de la organización, haga clic en **Internal**. Si la organización pertenece a una empresa, las imágenes de contenedor serán visibles para todos los miembros de la empresa.
    ![Opciones de visibilidad para las imágenes de contenedor que publican los miembros de la organización](/assets/images/help/package-registry/container-creation-org-settings.png)

## Configurar la visibilidad de las imágenes de contenedor para una organización

Cuando publicas un paquete por primera vez, la visibilidad predeterminada es privada y solo tú puedes verlo. Puedes otorgar roles de acceso diferentes a los usuarios o equipos para tu imagen de contenedor a través de la configuración de acceso.

Se puede acceder anónimamente a un paquete público sin autenticación. Una vez que hagas tu paquete público, no puedes hacerlo privado nuevamente.

{% data reusables.package_registry.package-settings-from-org-level %} {% data reusables.package_registry.package-settings-option %}
5. Debajo de "Zona de peligro", elige una configuración de visibilidad:
    - Para que cualquier usuario pueda ver la imagen de contenedor, haga clic en **Make public**.
    {% warning %}

    **Advertencia:** Una vez que haga público un paquete, no podrá volver a hacerlo privado.

    {% endwarning %}
    - Para que la imagen de contenedor sea visible para una selección personalizada de usuarios, haga clic en **Make private**.
  ![Opciones de visibilidad del contenedor](/assets/images/help/package-registry/container-visibility-option.png)
