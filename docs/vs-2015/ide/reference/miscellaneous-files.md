---
title: Arquivos diversos | Microsoft Docs
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
- VS.newfile
- VS.OpenWith
- MiscellaneousFilesProject
helpviewer_keywords:
- solutions, miscellaneous files
- builds [Visual Studio], miscellaneous files
- standalone files
- Solution Explorer, miscellaneous files
- Miscellaneous Files folder
- files [Visual Studio], outside of containers
- files [Visual Studio], Miscellaneous Files folder
ms.assetid: 5b96640b-8efe-48a4-8d0a-1ae3f9587e44
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: cb9c7fb46517ff2d6dffdeb0cedfc4982c1f3366
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49258459"
---
# <a name="miscellaneous-files"></a>Arquivos diversos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Talvez você queira usar os editores [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para trabalhar de forma independente nos arquivos de um projeto ou de uma solução. Enquanto você tiver uma solução aberta, pode abrir e modificar arquivos sem adicioná-los a uma solução ou um projeto. Os arquivos com os quais você deseja trabalhar independentemente dos contêineres são chamados de arquivos diversos. Os arquivos diversos são externos às soluções e projetos, não estão incluídos em builds e não podem ser incluídos com uma solução sob controle do código-fonte.  
  
 Abrir arquivos independentemente de um contêiner é útil para uma variedade de razões. Você pode ter um arquivo que deseja exibir enquanto desenvolve uma solução baseada em projeto, mas que não é parte integrante do desenvolvimento da solução. Exemplos comuns incluem instruções ou anotações de desenvolvimento, esquema de banco de dados e fragmentos de código. Além disso, você talvez queira criar um arquivo autônomo.  
  
 ![Projetos de soluções](../../ide/reference/media/projects-solutions-misc.gif "Projects_Solutions_Misc")  
  
 O Gerenciador de Soluções poderá exibir uma pasta Arquivos Diversos para os arquivos se as opções para a pasta estiverem habilitadas. As opções podem ser definidas em [Caixa de diálogo Documentos, Ambiente, Opções](../../ide/reference/documents-environment-options-dialog-box.md). Depois de fechar um arquivo diverso, ele não é associado a nenhuma solução ou projeto específico, a menos que uma opção seja habilitada para isso também.  
  
 A pasta Arquivos Diversos representa os arquivos como links. Embora essa pasta não seja parte de uma solução, quando você abre uma solução, alguns ou todos os arquivos diversos que estavam abertos quando a solução foi fechada pela última vez são reabertos, dependendo das configurações da pasta.  
  
> [!NOTE]
>  Alguns dos arquivos que não aparecem na pasta Arquivos Diversos são arquivos que você não pode modificar dentro do IDE, como arquivos .zip e arquivos .doc. O IDE não rastreará arquivos que podem ser modificados apenas por um editor externo.  
  
## <a name="commands-available-in-the-ide"></a>Comandos disponíveis no IDE  
 Os menus, barras de ferramentas e os comandos que eles contêm mudam com base no formato do arquivo aberto. Quando você abre um arquivo de texto, por exemplo, a barra de ferramentas Editor de Texto aparece e seus comandos estão disponíveis. Se você abrir um arquivo de Esquema XML, a barra de ferramentas Esquema XML será exibida. Ao editar o Esquema XML, os comandos da barra de ferramentas Editor de Texto (ou a barra de ferramentas em si) estão indisponíveis. O Esquema XML é a janela ativa e como tal, tem contexto de seleção atual. Quando você muda entre um arquivo de projeto e um arquivo diverso, todos os comandos relacionados ao projeto desaparecem e somente aqueles que estão diretamente relacionados aos arquivos diversos são exibidos.  
  
## <a name="folder-display-options"></a>Opções de exibição de pasta  
 Você pode definir opções de exibição para a Pasta de Diversos para que ela seja exibida mesmo que você não tenha aberto nenhum Arquivo Diverso. O arquivo de solução não gerencia permanentemente uma lista de arquivos diversos. Ele usa um recurso opcional que permite que ele se lembre uma lista de arquivos MRU (recentemente usados) por usuário.  
  
## <a name="see-also"></a>Consulte também  
 [Soluções e projetos](../../ide/solutions-and-projects-in-visual-studio.md)   
 [Caixa de diálogo Documentos, Ambiente, Opções](../../ide/reference/documents-environment-options-dialog-box.md)



