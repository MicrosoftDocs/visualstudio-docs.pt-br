---
title: Práticas recomendadas para segurança em VSPackages | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 940644cd3950c38c6383371c1844b54b328acd0c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697274"
---
# <a name="best-practices-for-security-in-vspackages"></a>Práticas de segurança recomendadas em VSPackages
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para instalar o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] no seu computador, você deve estar executando em um contexto com credenciais administrativas. A unidade básica de segurança e a implantação de um [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] aplicativo é o [VSPackages](../../extensibility/internals/vspackages.md). Um VSPackage deverá ser registrado usando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], que também requer credenciais administrativas.  
  
 Os administradores têm permissões completas para escrever no registro e sistema de arquivos e executar qualquer código. Você deve ter essas permissões para desenvolver, implantar ou instalar um VSPackage.  
  
 Assim que ele é instalado, um VSPackage é totalmente confiável. Devido a esse nível alto de permissão associada a um VSPackage, é possível instalar inadvertidamente um VSPackage que tenha más intenções.  
  
 Os usuários devem garantir que eles instalar VSPackages somente de fontes confiáveis. As empresas desenvolvendo os VSPackages fortemente devem nomear e assiná-las garantir que o usuário dessa violação é impedido. As empresas desenvolvendo os VSPackages devem examinar suas dependências externas, como serviços da web e de instalação remota, para avaliar e corrigir quaisquer problemas de segurança.  
  
 Para obter mais informações, consulte as diretrizes de codificação segura para o .NET Framework ([https://msdn.microsoft.com/library/d55zzx87.aspx](https://msdn.microsoft.com/library/d55zzx87.aspx)).  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de suplemento](https://msdn.microsoft.com/library/44a5c651-6246-4310-b371-65378917c799)   
 [Segurança DDEX](https://msdn.microsoft.com/44a52a70-5c98-450e-993d-4a3b32f69ba8)
