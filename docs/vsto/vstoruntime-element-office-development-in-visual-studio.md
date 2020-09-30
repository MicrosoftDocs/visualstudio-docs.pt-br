---
title: '&lt;&gt;elemento vstoRuntime (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <vstoRuntime> element
- <vstoRuntime> element
- vstoRuntime element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ffebff9e5cee8666d1b178fca09262ecd45c99b1
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584354"
---
# <a name="ltvstoruntimegt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento vstoRuntime (desenvolvimento do Office no Visual Studio)
  O `vstoRuntime` elemento do `vstav3` namespace contém uma versão com suporte do ferramentas do Visual Studio para o tempo de execução do Office para uma solução específica do Office.

## <a name="syntax"></a>Sintaxe

```xml
<vstoRuntime
    release
    version
    supportUrl />
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `vstoRuntime` elemento é obrigatório e está no `vstav3` namespace. Se uma solução do Office oferecer suporte a duas versões do Ferramentas do Visual Studio para o tempo de execução do Office, haverá dois `vstoRuntime` elementos no manifesto do aplicativo.

 O `vstoRuntime` elemento tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`release`|Obrigatórios. A versão de lançamento do Ferramentas do Visual Studio para o tempo de execução do Office.|
|`version`|Obrigatório. Número de versão do Ferramentas do Visual Studio para o tempo de execução do Office.|
|`supportUrl`|Opcional. Link para o local de instalação do Ferramentas do Visual Studio para o tempo de execução do Office.|

 `vstoRuntime` Não tem elementos.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir ilustra o `vstoRuntime` elemento em um manifesto de aplicativo para uma solução do Office implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

```xml
<vstav3:vstoRuntime
    release="VSTOR40Beta1"
    version="10.0.20303"
    supportUrl="http://www.microsoft.com" />
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
