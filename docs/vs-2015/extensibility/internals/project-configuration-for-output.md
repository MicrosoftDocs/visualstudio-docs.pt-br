---
title: Configuração para a saída de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1c23f9210175b848bfdf3ddab56776092e39212c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51740897"
---
# <a name="project-configuration-for-output"></a>Configuração de projeto para saída
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Cada configuração pode dar suporte a um conjunto de processos de compilação que produzir saída itens como arquivos de recurso ou executável. Esses itens de saída são particulares para o usuário e podem ser colocados em grupos que vinculam os tipos relacionados de saída, como arquivos executáveis (.exe,. dll,. lib) e arquivos de origem (. idl, arquivos. h).  
  
 Itens de saída podem ser disponibilizados por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> métodos e enumeradas com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> métodos. Quando você deseja agrupar itens de saída, seu projeto também deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> interface.  
  
 A construção desenvolvidos com a implementação de `IVsOutputGroup` permite que os projetos para saídas de grupo de acordo com o uso. Por exemplo, uma DLL pode ser agrupada com seu banco de dados do programa (PDB).  
  
> [!NOTE]
>  Um arquivo PDB contiver informações de depuração e ele é criado quando a opção 'Gerar informações de depuração' é especificada ao criar o arquivo. dll ou .exe. Geralmente, o arquivo. PDB é gerado para configuração de projeto de depuração somente.  
  
 O projeto deve retornar o mesmo número de grupos para cada configuração com suporte, mesmo que o número de saídas contido dentro de um grupo pode variar de uma configuração para a configuração. Por exemplo, Matt do projeto DLL pode incluir mattd.dll e mattd.pdb na configuração de depuração, mas apenas incluir matt.dll na configuração de varejo.  
  
 Os grupos também têm as mesmas informações de identificador, como o nome canônico, nome de exibição e informações de grupo de configuração para a configuração dentro de um projeto. Essa consistência permite que a implantação e empacotamento para continuar a operar mesmo se alterar as configurações.  
  
 Grupos também podem ter uma saída de chave que permite que os atalhos de empacotamento apontar para algo significativo. Qualquer grupo pode ser vazio em uma determinada configuração, portanto, nenhuma suposição deve ser feita sobre o tamanho de um grupo. O tamanho (número de saídas) de cada grupo em qualquer configuração pode ser diferente do tamanho de outro grupo na mesma configuração. Ele também pode ser diferente do tamanho do mesmo grupo em outra configuração.  
  
 ![Gráfico de grupos de saída](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups")  
Grupos de saída  
  
 O principal uso do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> interface é fornecer acesso para compilar, implantar e depurar objetos de gerenciamento e permitir que os projetos a liberdade de saídas de grupo. Para obter mais informações sobre o uso dessa interface, consulte [objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md).  
  
 No diagrama anterior, o grupo criado tem uma chave de saída em configurações (bD.exe ou b.exe), portanto, o usuário pode criar um atalho para desenvolvido e saber que o atalho funcionarão independentemente da configuração implantada. Origem do grupo não tem uma chave de saída, portanto, o usuário não é possível criar um atalho para ele. Se a depuração grupo criado tem uma chave de saída, mas o grupo de varejo criado não, isso seria uma implementação incorreta. Ele apresenta, em seguida, em seguida, se qualquer configuração tiver um grupo que não contenha nenhuma saída, e, como resultado, nenhum arquivo de chave, em seguida, outras configurações que contêm as saídas com esse grupo não podem ter arquivos de chave. Os editores de instalador pressupõem a nomes canônicos e nomes de exibição de grupos, além da existência de um arquivo de chave, não são alterados com base em configurações.  
  
 Observe que, se um projeto tem um `IVsOutputGroup` que ele deseja empacotar ou implantar, é suficiente para não colocar essa saída em um grupo. A saída ainda pode ser enumerada normalmente Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> método que retorna todas as saídas de uma configuração independentemente do agrupamento.  
  
 Para obter mais informações, consulte a implementação de `IVsOutputGroup` no exemplo personalizados de projeto no [MPF de projetos](http://mpfproj12.codeplex.com).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para criação](../../extensibility/internals/project-configuration-for-building.md)   
 [Objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md)   
 [Configuração da solução](../../extensibility/internals/solution-configuration.md)

