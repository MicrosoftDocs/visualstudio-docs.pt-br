---
title: Registrando serviços | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- services, registering
ms.assetid: c4ebac40-0374-4dda-948e-06fdda0e9c81
caps.latest.revision: 8
manager: douge
ms.openlocfilehash: e5d8aa9e6652aa41e59d160c5cf25aacd3390572
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49219681"
---
# <a name="registering-services"></a>Registrando serviços
Para dar suporte a carregamento sob demanda, um provedor de serviços deve registrar os seus serviços globais com [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Durante o desenvolvimento, provedores de serviços gerenciados registrar serviços e substituições de serviço, adicionando atributos no código-fonte para pacotes e, em seguida, criando os pacotes no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE. Isso executa o utilitário RegPkg.exe no assembly resultante, o pacote de registro e preparação para implantação. Para obter mais informações, consulte [como: registrar um serviço](../misc/how-to-register-a-service.md).  
  
 Provedores de serviço não gerenciado devem registrar os serviços que eles oferecem [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] nos serviços de seção ou o serviço substituirá a seção do registro do sistema. O fragmento de arquivo. reg a seguir mostra como o serviço, SVsTextManager, pode ser registrado:  
  
```  
[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]  
@="{F5E7E720-1401-11d1-883B-0000F87579D2}"  
"Name"="SVsTextManager"  
```  
  
 No exemplo acima, o número de versão é a versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], tais como 7.1 ou 8.0, a chave {F5E7E71D-1401-11d1-883B-0000F87579D2} é o identificador de serviço (SID) do serviço, SVsTextManager e a {de valor padrão F5E7E720-1401-11D1-883B-0000F87579D2} é o GUID do Gerenciador de texto VSPackage, que fornece o serviço do pacote.  
  
## <a name="remote-services-and-background-threads"></a>Serviços remotos e Threads em segundo plano  
 Serviços que você fornece não estão automaticamente disponíveis remotamente ou threads em segundo plano. Para disponibilizá-las, você deve criar e registrar uma biblioteca de tipos.  
  
 Do código não gerenciado que usa o Visual Studio biblioteca (. VSL), você pode registrar sua biblioteca de tipos dessa maneira:  
  
```  
#define VSL_REGISTER_TYPE_LIB TRUE  
#include <VSLPackageDllEntryPoints.cpp>  
```  
  
 No código gerenciado, você pode adicionar uma etapa de pós-compilação como este:  
  
```  
regasm /tlb MyAssembly.dll  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)