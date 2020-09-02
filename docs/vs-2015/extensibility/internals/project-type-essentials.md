---
title: Tipo de projeto Essentials | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e45d5f252deaf1788ae5093048ef8afb900fbe4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704071"
---
# <a name="project-type-essentials"></a>Conceitos básicos do tipo de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] inclui vários tipos de projeto para linguagens como [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ou [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] também permite que você crie seus próprios tipos de projeto.  
  
 Se você quiser apenas adicionar comandos personalizados, editores ou janelas de ferramentas ao [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , poderá fazer isso sem criar um novo tipo de projeto. Para obter mais informações, consulte estes tópicos:  
  
- [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)  
  
- [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md)  
  
- [Ampliar e personalizar janelas de ferramentas](../../extensibility/extending-and-customizing-tool-windows.md)  
  
  Da mesma forma, se você quiser personalizar o comportamento dos [!INCLUDE[csprcs](../../includes/csprcs-md.md)] tipos de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] projeto e fornecidos, poderá fazer isso usando subtipos de projeto. Para obter mais informações, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).  
  
  Você deve criar um novo tipo de projeto para projetos baseados em um idioma diferente de [!INCLUDE[csprcs](../../includes/csprcs-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] se desejar oferecer suporte a um ou mais dos seguintes:  
  
- Build  
  
- Implantação  
  
- Várias configurações  
  
- Controle do código-fonte  
  
- Depuração  
  
- Itens de projeto no Gerenciador de Soluções  
  
- As caixas de diálogo **Abrir projeto** ou **novo projeto**  
  
- Aninhamento de projetos  
  
- Para obter mais informações sobre os recursos de tipos de projeto, consulte o seguinte:  
  
- Os tipos de projeto são objetos em um VSPackage que implementam o conjunto de interfaces [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] esperados. Se você estiver usando C# para desenvolver um tipo de projeto, as classes de projeto de estrutura de pacote gerenciado implementarão as interfaces necessárias para você e permitirá que você herde essa implementação. Para obter mais informações, consulte [usando a estrutura de pacote gerenciado para implementar um tipo de projeto (C#)](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md).  
  
- Para desenvolvedores de C++, as classes na biblioteca HierUtil funcionam de maneira semelhante. Para obter mais informações, consulte [não está no Build: usando classes de projeto HierUtil7 para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/a5c16a09-94a2-46ef-87b5-35b815e2f346).  
  
- Os tipos de projeto podem dar suporte a dados diferentes de arquivos de código-fonte típicos que se baseiam em um assembly. exe ou. dll. Por exemplo, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] os projetos de banco de dados contêm referências a arquivos de script e de consulta armazenados no disco e adicionam comandos a **Gerenciador de soluções** para executar os scripts e consultas em um banco de dados, mas os projetos não dão suporte ao comportamento de compilação. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).  
  
- Um tipo de projeto não precisa usar arquivos. Por exemplo, um tipo de projeto pode armazenar todos os seus dados em um banco de dado. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] fornece ao tipo de projeto controle completo sobre como eles mantêm dados para projetos e itens de projeto. Para obter mais informações, consulte [Project Type design decisions](../../extensibility/internals/project-type-design-decisions.md).  
  
- Os tipos de projeto devem fornecer uma *fábrica de projetos*, que é um objeto que cria uma instância do tipo de projeto sempre que [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é instruído a abrir ou criar um projeto baseado nesse tipo de projeto. Para obter mais informações, consulte [criando instâncias de projeto usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).  
  
- Os tipos de projeto devem fornecer modelos para projetos e itens de projeto. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] usa os modelos quando os usuários criam novos projetos e adicionam novos itens a projetos existentes. Para obter mais informações, consulte [adicionando projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
- Os tipos de projeto podem dar suporte a várias configurações, como Debug e Release. Os usuários podem alterar as diferentes configurações de um projeto usando as páginas de propriedades fornecidas por você. Para obter mais informações, consulte [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de projeto de implantação](../../extensibility/internals/deploying-project-types.md)
