---
title: Utilitário CreateExpInstance | Microsoft Docs
description: Saiba mais sobre o utilitário CreateExpInstance que permite criar, redefinir ou excluir uma instância experimental do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cce9bc25cb2ed820d3291ab65d94a868bb401ec9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898130"
---
# <a name="createexpinstance-utility"></a>Utilitário CreateExpInstance
Use o **utilitário CreateExpInstance** para criar, redefinir ou excluir uma instância experimental do Visual Studio. Você pode usar a instância experimental para depurar e testar Visual Studio extensões sem alterar o produto subjacente.

## <a name="syntax"></a>Sintaxe

```
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix
```

## <a name="parameters"></a>Parâmetros
 **/Create** Cria a instância experimental.

 **/Reset** Exclui a instância experimental e, em seguida, cria uma nova.

 **/Clean** Exclui a instância experimental.

 **/VSInstance** O nome do diretório que contém a instância Visual Studio base a ser copiada.

 **/RootSuffix** O sufixo a ser anexado ao nome do diretório de instância experimental.

## <a name="remarks"></a>Comentários
 Ao trabalhar em uma extensão Visual Studio, você pode pressionar F5 para abrir a instância experimental padrão e instalar a extensão atual. Se nenhuma instância experimental estiver disponível, Visual Studio criará uma que tenha as configurações padrão.

 O local padrão da instância experimental depende do número Visual Studio versão. Por exemplo, por Visual Studio 2015, o local é *%localappdata%\Microsoft\VisualStudio\14.0Exp. \\* Todos os arquivos no local do diretório são considerados parte dessa instância. Quaisquer instâncias experimentais adicionais não serão carregadas por Visual Studio a menos que o nome do diretório seja alterado para o local padrão.

 Visual Studio não acessa o registro do sistema quando abre a instância experimental. Isso difere das versões anteriores do Visual Studio, que usavam uma versão experimental do hive do Registro.

 O **utilitário CreateExpInstance** substitui o **utilitário VsRegEx.**

 O exemplo a seguir redefine a instância experimental padrão do Visual Studio:

 **CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp**

## <a name="see-also"></a>Confira também
- [VSPackages](../../extensibility/internals/vspackages.md)
