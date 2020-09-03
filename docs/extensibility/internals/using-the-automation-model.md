---
title: Usando o modelo de automação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b9d7bd789a41f7a5e801552ca07f9f228921867
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704227"
---
# <a name="using-the-automation-model"></a>Usando o modelo de automação
Depois de conectar o VSPackage à automação, você pode obter as propriedades e os métodos chamando o <xref:EnvDTE.DTEClass.GetObject%2A> método no <xref:EnvDTE._DTE> objeto, passando uma cadeia de caracteres que representa o objeto que você deseja recuperar.

## <a name="obtaining-project-objects"></a>Obtendo objetos do projeto
 A seguir estão dois exemplos de código que mostram como um consumidor de automação Obtém os objetos de automação do projeto. Para obter informações sobre como obter o objeto DTE, consulte [como: obter referências aos objetos DTE e DTE2](https://msdn.microsoft.com/Library/c92e3c8e-82e6-4a67-85da-e43c50ffd8e4).

```vb
Sub DoAutomation()
    Dim MyProjects As Projects
    MyProjects = DTE.GetObject("AcmeProject")
End Sub
```

```cpp
void DoAutomation(void)
{
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.
    pMyPkg = pDTE->GetObject("AcmeProjects");

   // The '=' performs a Query Interface.
   // Assumes pDTE is already available as a global.
   // Use pMyPkg to access your projects object's properties and methods.
}

```

 Neste ponto, você pode usar os objetos de projeto padrão que fazem parte de um VSPackage específico para mover para baixo o modelo de hierarquia.

 O exemplo de código a seguir mostra como obter um objeto personalizado que é uma propriedade de um tipo de projeto personalizado.:

```vb
Dim MyPrj As Project
Dim MyPrjItem As ProjectItem
Dim objMyObject as MyExtendedObject

MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project
objMyObject = MyPrj.Object 'You call .Object to get to special Project
                           'implementation
objMyObject.MySpecialMethodOrProperty
```

 O código a seguir lista os nomes de todas as propriedades na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] opção ambiente **geral** no menu **ferramentas** :

```vb
dim objDTE
dim objEnv
set objDTE = CreateObject("VisualStudio.DTE")
set objEnv = objDTE.Properties("Environment", "General")
for each obj in ObjEnv
MsgBox obj.Name
Next

```

## <a name="see-also"></a>Confira também
- <xref:EnvDTE.DTEClass.GetObject%2A>
