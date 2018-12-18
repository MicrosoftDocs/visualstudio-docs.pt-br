---
title: 'Extensão de amostra do Excel: Classe ExtensionPackage | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e45410a-1819-4d54-ac21-7280152f7e3a
caps.latest.revision: 11
ms.author: gewarren
manager: douge
ms.openlocfilehash: 64e6d838172325bb00cdd8a28ef6adb6d1a345b5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49286007"
---
# <a name="sample-excel-extension-extensionpackage-class"></a>Extensão de exemplo do Excel: classe ExtensionPackage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa classe estende a classe <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> e fornece o ponto de entrada para a extensão de teste de IU codificado que está testando uma Planilha do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)].  
  
## <a name="assembly-attribute"></a>Atributos do Assembly  
 O arquivo começa com um atributo de assembly que identifica o assembly como uma extensão de teste de interface do usuário.  
  
```  
[assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(  
    "ExcelExtensionPackage",  
    typeof(  
     Microsoft.VisualStudio.Test.Sample.UI.ExtensionPackage))]  
```  
  
 Esse atributo declara o nome de classe base, o nome da classe de pacote e o nome de classe totalmente qualificado da classe de pacote de extensão personalizada.  
  
## <a name="simple-properties"></a>Propriedades Simples  
 Essa classe tem propriedades que fornecem valores que são usados pela estrutura de teste da interface do usuário codificada para identificar e descrever a extensão e o assembly. Consulte os comentários do código para obter mais informações.  
  
## <a name="getservice-method"></a>Método GetService  
 O método <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> é o único ponto de entrada usado pela estrutura de teste de IU codificado para obter acesso ao gerente de tecnologia, ao provedor de propriedade e ao filtro de ação, conforme identificado pela classe base de cada objeto.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>   
 [Estendendo testes de IU codificados e gravações da ação para dar suporte ao Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)



