---
title: Evaluación de las opciones para migrar datos de las series 5000-7000 de StorSimple | Microsoft Docs
description: Proporciona información general de las opciones para migrar datos desde las series 5000-7000 de StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: twooley
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/31/2019
ms.author: alkohli
ms.openlocfilehash: e3412e31ae976efc8164076b30ad61360a030db4
ms.sourcegitcommit: fea5a47f2fee25f35612ddd583e955c3e8430a95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2019
ms.locfileid: "55511945"
---
# <a name="options-to-migrate-data-from-storsimple-5000-7000-series"></a>Opciones para migrar datos desde la serie 5000-7000 de StorSimple 

> [!IMPORTANT]
> El 31 de julio de 2019, finalizará el estado de compatibilidad de la serie StorSimple 5000/7000. Se recomienda que los clientes de la serie StorSimple 5000/7000 migren a una de las alternativas descritas en el documento.

La serie 5000-7000 de StorSimple alcanzará el [fin del soporte técnico](https://support.microsoft.com/lifecycle/search?alpha=StorSimple%205000%2F7000%20Series) en julio de 2019. Los clientes que ejecutan la serie 5000-7000 de StorSimple tienen una opción para actualizar a otros servicios híbridos de primera entidad de Azure. En este artículo se describen las opciones híbridas de Azure disponibles para migrar datos. 

## <a name="migration-options"></a>Opciones de migración

Los clientes que usan la serie 5000-7000 de StorSimple pueden utilizar las opciones de Azure o de terceros.

### <a name="azure-options"></a>Opciones de Azure

#### <a name="upgrade-to-storsimple-8000-series"></a>Actualización a la serie 8000 de StorSimple

No cambie de plataforma y actualice a la serie 8000 de StorSimple.  Esta ruta de actualización requiere que los clientes reemplacen los dispositivos de la serie 5000-7000 a una serie 8000. Los datos se migran desde el dispositivo de la serie 5000-7000 mediante la herramienta de migración. Una vez que la migración se haya completado correctamente, los dispositivos de la serie 8000 de StorSimple seguirán colocando datos en capas en Azure Blob Storage. 

Para obtener más información sobre cómo migrar datos mediante la serie 8000 de StorSimple, vaya a [Migración de datos del dispositivo de la serie 5000-7000 de StorSimple a la serie 8000](storsimple-8000-migrate-from-5000-7000.md).

#### <a name="migrate-to-azure-file-sync"></a>Migración a Azure File Sync

Esta nueva opción de migración permite a los clientes almacenar los recursos compartidos de archivos de su organización en Azure Files. Estos recursos compartidos de archivos se pueden centralizar luego para acceder a ellos de forma local mediante Azure File Sync (AFS). AFS puede implementarse en un host de Windows Server. La migración de datos real se realiza entonces como una copia de host o mediante la herramienta de migración.

Para obtener más información sobre cómo migrar datos a Azure File Sync, vaya a [Migrate data from StorSimple 5000-7000 series to Azure File Sync](https://aka.ms/StorSimpleMigrationAFS) (Migración de datos desde la serie 5000-7000 de StorSimple a Azure File Sync).

### <a name="third-party-options"></a>Opciones de terceros

#### <a name="migrate-to-panzura-freedom-nas"></a>Migración a Panzura Freedom NAS

Los clientes de StorSimple 5000-7000 pueden elegir Panzura Freedom NAS como opción de migración para mantener sus datos en Azure. La solución Panzura Freedom proporciona una solución NAS que abarca centros de datos, oficinas, y nubes públicas y privadas. La solución permite flujos de trabajo de locales, híbridos y en la nube para clientes móviles, SMB y NFS. Esta migración es compatible con Panzura y los clientes pueden comenzar solicitando soporte técnico para la migración desde el [sitio web de Panzura](https://panzura.com/storsimple-migration/).

#### <a name="migrate-to-cohesity"></a>Migración a Cohesity

Cohesity le permite migrar los datos desde las series 5000–7000 actuales de StorSimple a la plataforma de datos de Cohesity en Azure. La plataforma de datos de Cohesity es una solución de escala de web definida por software que consolida los archivos, las copias de seguridad, los objetos y las VM en una única solución nativa en la nube. Tras la migración a la plataforma de datos, puede administrar, proteger y aprovisionar datos y aplicaciones de la nube al núcleo a través de un único panel de vidrio. Con Cohesity, inicie con tan solo tres nodos. Obtenga más información acerca de [Migration to the Cohesity DataPlatform](https://info.cohesity.com/migrate-from-storsimple-to-cohesity.html) (Migración a la plataforma de datos de Cohesity).

## <a name="migration---frequently-asked-questions"></a>Migración: preguntas frecuentes

### <a name="q-when-do-the-storsimple-5000-and-7000-series-devices-reach-end-of-service"></a>P: ¿Cuándo llega la serie 5000 y 7000 de StorSimple al final del servicio? 

A. La serie 5000-7000 de StorSimple llega al [final del servicio](https://support.microsoft.com/lifecycle/search?alpha=StorSimple%205000%2F7000%20Series) en julio de 2019. El final del servicio implica que Microsoft ya no podrá proporcionar soporte técnico para hardware y software de estos dispositivos después de julio de 2019. Se recomienda encarecidamente que empiece a formular ya un plan para migrar los datos de sus dispositivos.

### <a name="q-what-happens-to-the-data-i-have-stored-in-azure"></a>P: ¿Qué ocurre con los datos que he almacenado en Azure?  

A. Podrá seguir usando los datos en Azure cuando haya migrado a un servicio más reciente. 


### <a name="q-what-happens-to-the-data-i-have-stored-locally-on-my-storsimple-device"></a>P: ¿Qué ocurre con los datos que he almacenado localmente en el dispositivo de StorSimple? 

A. Los datos que se encuentran en el dispositivo local se pueden copiar en el servicio más reciente, como se describe en los documentos de migración.

### <a name="q-what-happens-if-i-want-to-keep-my-storsimple-50007000-series-appliance"></a>P: ¿Qué ocurre si quiero mantener mi dispositivo de la serie 5000/7000 de StorSimple? 

A. Si bien los servicios podrían seguir funcionando, Microsoft ya no podrá proporcionar soporte técnico de hardware y software. Se recomienda totalmente la migración para la continuidad empresarial.

### <a name="q-what-options-are-available-to-migrate-data-from-storsimple-5000-7000-series-devices"></a>P: ¿Qué opciones están disponibles para migrar datos de los dispositivos de la serie 5000-7000 de StorSimple? 

A. Dependiendo de su escenario, los usuarios de la serie 5000-7000 de StorSimple tienen las siguientes opciones de migración. 

 - **Actualización a la serie 8000**: use esta opción si quiere permanecer en la plataforma de StorSimple. 
 - **Migración a Azure File Sync**: use esta opción si quiere cambiar al formato nativo de Azure. Puede usar Azure File Sync para la administración centralizada de recursos compartidos de archivos. 

Puede ponerse en contacto con el soporte técnico de Microsoft para analizar las opciones de migración que no aparecen aquí.

### <a name="q-is-migration-to-other-storage-solutions-supported"></a>P: ¿Se admite la migración a otras soluciones de almacenamiento?

A. Sí. Se admite la migración a otras soluciones de almacenamiento mediante la copia de host de los datos.

### <a name="q-is-migration-supported-by-microsoft"></a>P: ¿Microsoft admite la migración? 

A. La migración desde la serie 5000 o 7000 es una operación completamente admitida. De hecho, Microsoft recomienda ponerse en contacto con el soporte técnico antes de iniciar la migración. La migración es actualmente una operación asistida. Si va a migrar datos desde un dispositivo de la serie 5000-7000 de StorSimple, [abra una incidencia de soporte técnico](storsimple-8000-contact-microsoft-support.md).

### <a name="q-what-is-the-pricing-model-for-both-the-migration-options"></a>P: ¿Cuál es el modelo de precios para ambas opciones de migración?

A. El costo de migración varía según la opción que elija. Mientras la migración propiamente dicha es gratis, si decide actualizar a la serie 8000 de StorSimple el costo será el del dispositivo de hardware. 

De forma similar, cuando se usa Azure File Sync, pueden aplicarse tarifas de suscripción para el servicio. En cada caso, los clientes también tendrán que pagar los costos de almacenamiento en curso. Consulte la siguiente información para obtener una estimación: 
- [Precios de StorSimple](https://azure.microsoft.com/pricing/details/storsimple/)  
- [Precios de AFS]( https://azure.microsoft.com/pricing/details/storage/files/)

### <a name="q--how-long-does-it-take-to-complete-a-migration"></a>P:  ¿Cuánto tiempo se tarda en completar una migración?

A. El tiempo para migrar los datos depende de la cantidad de los datos y la opción de actualización seleccionada. 

### <a name="q-what-is-the-end-of-support-date-for-storsimple-8000-series"></a>P: ¿Cuál es la fecha final del soporte técnico para la serie 8000 de StorSimple?

A. La fecha final del soporte técnico para la serie 8000 de StorSimple está publicada [aquí](https://support.microsoft.com/lifecycle/search?alpha=Azure%20StorSimple%208000%20Series).


## <a name="next-steps"></a>Pasos siguientes
 - [Migración de datos del dispositivo de la serie 5000-7000 de StorSimple a la serie 8000](storsimple-8000-migrate-from-5000-7000.md)
 - [Migrate data from a StorSimple 5000-7000 series to Azure File Sync](storsimple-5000-7000-afs-migration.md) (Migración de datos de la serie 5000-7000 de StorSimple a Azure File Sync)
