---
title: Utilitário CreateExpInstance | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a0f7f52f45023106d3e504258a538823c1c8fbb4
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500651"
---
# <a name="createexpinstance-utility"></a>Utilitário CreateExpInstance
Use o **CreateExpInstance** utilitário para criar, redefinir ou excluir uma instância experimental do Visual Studio. Você pode usar a instância experimental para depurar e testar as extensões do Visual Studio sem alterar o produto subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix  
```  
  
## <a name="parameters"></a>Parâmetros  
 **/ Criar** cria a instância experimental.  
  
 **/ Redefinição**  
 Exclui a instância experimental e, em seguida, cria um novo.  
  
 **/Clean**  
 Exclui a instância experimental.  
  
 **/ VSInstance**  
 O nome do diretório que contém a instância do Visual Studio base para copiar.  
  
 **/ RootSuffix**  
 O sufixo a ser acrescentado ao nome do diretório de instância experimental.  
  
## <a name="remarks"></a>Comentários  
 Quando você estiver trabalhando em uma extensão do Visual Studio, você pode pressionar F5 para abrir a instância experimental do padrão e instalar a extensão atual. Se nenhuma instância experimental estiver disponível, o Visual Studio cria um que tenha as configurações padrão.  
  
 O local padrão da instância experimental depende do número de versão do Visual Studio. Por exemplo, para o Visual Studio 2015, o local é *%localappdata%\Microsoft\VisualStudio\14.0Exp\\*. Todos os arquivos no local de diretório são considerados parte dessa instância. Qualquer instância experimental adicional não será carregada pelo Visual Studio, a menos que o nome do diretório é alterado para o local padrão.  
  
 Visual Studio não acessar o registro do sistema quando ele é aberto na instância experimental. Isso é diferente de versões anteriores do Visual Studio, que usavam uma versão experimental da seção do registro.  
  
 O **CreateExpInstance** substitui o utilitário do **VsRegEx** utilitário.  
  
 O exemplo a seguir redefine a instância experimental do padrão do Visual Studio:  
  
 **CreateExpInstance.exe /Reset /VSInstance = 14.0 /RootSuffix = Exp**  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../../extensibility/internals/vspackages.md)