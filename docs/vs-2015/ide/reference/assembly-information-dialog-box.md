---
title: Caixa de diálogo Informações do Assembly | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vb.ProjectPropertiesAssemblyInfo
helpviewer_keywords:
- Assembly Information dialog box
ms.assetid: 8f1f6449-e03d-4a5b-9076-d3b1f84ada48
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8526dfbe970c43e1ab55534c13a1e6708b2b4693
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248021"
---
# <a name="assembly-information-dialog-box"></a>Caixa de diálogo Informações do Assembly
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
A caixa de diálogo **Informações do Assembly** é usada para especificar os valores dos atributos de assembly global [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], que são armazenados no arquivo AssemblyInfo criado automaticamente com o projeto. No **Gerenciador de Soluções**, o arquivo está localizado no nó **Meu Projeto** em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] (clique em **Mostrar Todos os Arquivos** para exibi-lo); ele está localizado em **Propriedades** em [!INCLUDE[csprcs](../../includes/csprcs-md.md)]. Para obter mais informações sobre atributos de assembly, consulte [Atributos](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205).  
  
 Para acessar essa caixa de diálogo, selecione um nó do projeto no **Gerenciador de Soluções** e, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Aplicativo**. Na página **Aplicativo**, clique no botão **Informações do Assembly**.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Título**  
 Especifica um título para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyTitleAttribute>.  
  
 **Descrição**  
 Especifica uma descrição opcional para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyDescriptionAttribute>.  
  
 **Empresa**  
 Especifica um nome de empresa para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyCompanyAttribute>.  
  
 **Produto**  
 Especifica um nome de produto para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyProductAttribute>.  
  
 **Direitos Autorais**  
 Especifica uma notificação de direitos autorais para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyCopyrightAttribute>.  
  
 **Marca Registrada**  
 Especifica uma marca registrada para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyTrademarkAttribute>.  
  
 **Versão do Assembly**  
 Especifica a versão do assembly. Corresponde ao <xref:System.Reflection.AssemblyVersionAttribute>.  
  
 **Versão do Arquivo**  
 Especifica um número de versão que instrui o compilador a usar uma versão específica do recurso de versão de arquivo do Win32. Corresponde ao <xref:System.Reflection.AssemblyFileVersionAttribute>.  
  
 **GUID**  
 Um GUID exclusivo que identifica o assembly. Ao criar um projeto, o Visual Studio gera um GUID para o assembly. Corresponde ao <xref:System.Guid>.  
  
 **Linguagem Neutra**  
 Especifica a qual cultura o assembly dá suporte. Corresponde ao <xref:System.Resources.NeutralResourcesLanguageAttribute>. O padrão é **(Nenhum)**.  
  
 **Tornar um assembly visível para o COM**  
 Especifica se os tipos no assembly estarão disponíveis para o COM. Corresponde ao <xref:System.Runtime.InteropServices.ComVisibleAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Página de Aplicativo, Designer de Projeto (Visual Basic)](../../ide/reference/application-page-project-designer-visual-basic.md)   
 [Atributos](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)



