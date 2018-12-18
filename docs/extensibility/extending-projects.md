---
title: Estendendo projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a914afada4422364db043582be43658cf494b9c0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49864667"
---
# <a name="extend-projects"></a>Estender projetos
Projetos e soluções são as maneiras em que o Visual Studio organiza os arquivos de código e recursos em unidades de compilação e implantação. Você pode encontrar mais informações sobre projetos de [projetos (SDK do Visual Studio)](../extensibility/extending-projects.md).  
  
 Você pode criar seus próprios tipos de projeto com o SDK do Visual Studio e a estrutura de pacote gerenciado para projetos, que pode ser baixado em [estrutura de pacote gerenciado para projetos](https://github.com/tunnelvisionlabs/MPFProj10). Para entender como os projetos personalizados são implementados, consulte [nova geração de projeto: nos bastidores, parte um](../extensibility/internals/new-project-generation-under-the-hood-part-one.md) e [nova geração de projeto: nos bastidores, parte dois](../extensibility/internals/new-project-generation-under-the-hood-part-two.md).  
  
 Os tópicos nesta seção descrevem como criar projetos personalizados e como gerenciar diferentes tipos de solução do Visual Studio.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md)  
 Descreve como criar um sistema de projeto personalizado.  
  
 [Criar um sistema de projeto básico, parte 2](../extensibility/creating-a-basic-project-system-part-2.md)  
 Descreve como criar um sistema de projeto personalizado.  
  
 [Salvar dados em arquivos de projeto](../extensibility/saving-data-in-project-files.md)  
 Explica como adicionar ao projeto (<em>.</em> proj *) os arquivos.  
  
 [Verificar subtipos de um projeto em tempo de execução](../extensibility/verifying-subtypes-of-a-project-at-run-time.md)  
 Explica como verificar o subtipo de um projeto em tempo de execução.  
  
 [Adicionar e remover as páginas de propriedade](../extensibility/adding-and-removing-property-pages.md)  
 Explica como personalizar as páginas de propriedades para o seu projeto personalizado.  
  
 [Adicionar um atributo a um item de projeto](../extensibility/adding-an-attribute-to-a-project-item.md)  
 Explica como adicionar um atributo a um item de projeto personalizado.  
  
 [Manter a propriedade de um item de projeto](../extensibility/persisting-the-property-of-a-project-item.md)  
 Explica como persistir as propriedades de um item de projeto personalizado.  
  
 [Gerenciar projetos universais do Windows](../extensibility/managing-universal-windows-projects.md)  
 Explica como gerenciar projetos universais.  