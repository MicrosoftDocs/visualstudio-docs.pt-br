---
title: Abrindo e salvando itens de projeto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c406e66b1008f0bb2aad95a427e1329d4269f1f6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158057"
---
# <a name="opening-and-saving-project-items"></a>Abrindo e salvando itens de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Ao adicionar um novo tipo de projeto, você deve gerenciar a abertura e o salvamento de seus arquivos de projetos no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente de desenvolvimento integrado (IDE). Os tópicos a seguir discutem as diferentes abordagens para abrir e salvar arquivos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exibindo arquivos usando o comando Abrir Arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)  
 Fornece uma explicação passo a passo de como o IDE manipula o comando **Open File** e a função de projetos no respondendo a esse comando.  
  
 [Exibindo arquivos usando o comando Abrir Com](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)  
 Fornece uma explicação detalhada e passo a passo de como o IDE trata o comando **Open with** , solicitando a abertura de um arquivo que tem alguma opção de editores padrão.  
  
 [Como abrir editores específicos a um projeto](../../extensibility/how-to-open-project-specific-editors.md)  
 Apresenta instruções passo a passo para especificar que os arquivos de um tipo específico em seu projeto devem ser abertos usando um editor específico do projeto.  
  
 [Como abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)  
 Fornece instruções passo a passo para especificar como habilitar o IDE para abrir um editor padrão para arquivos em seu tipo de projeto.  
  
 [Como abrir editores para documentos abertos](../../extensibility/how-to-open-editors-for-open-documents.md)  
 Fornece instruções detalhadas para abrir um editor específico do projeto para um arquivo aberto.  
  
 [Salvando um documento padrão](../../extensibility/internals/saving-a-standard-document.md)  
 Fornece uma explicação detalhada de como o IDE manipula os comandos **salvar**, **salvar como**e **salvar todos** para um documento aberto em um editor padrão.  
  
 [Salvando um documento personalizado](../../extensibility/internals/saving-a-custom-document.md)  
 Fornece um diagrama e uma explicação detalhada de como o IDE manipula os comandos **salvar**, **salvar como**e **salvar todos os** documentos abertos em um editor personalizado.  
  
 [Determinando qual editor abre um arquivo em um projeto](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)  
 Discute o processo que o IDE segue para selecionar o editor ou designer apropriado para um arquivo.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar designers e editores personalizados](../../extensibility/creating-custom-editors-and-designers.md)  
 Lista os quatro tipos de editores que o IDE pode hospedar e fornece descrições de cada editor.  
  
 [Tipos de Projeto](../../extensibility/internals/project-types.md)  
 Discute como os projetos controlam a maneira como o código é compilado e criado, como os editores são abertos e como os itens de projeto são formatados.
