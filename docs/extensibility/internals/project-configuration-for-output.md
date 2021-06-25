---
title: Configuração do projeto para saída | Microsoft Docs
description: Saiba mais sobre os processos de build aos quais cada configuração pode dar suporte e as interfaces e métodos pelos quais os itens de saída podem ser disponibilizados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b718e70bac0d9e09936daf743420acc04a1c4ad
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899869"
---
# <a name="project-configuration-for-output"></a>Configuração de projeto para saída
Cada configuração pode dar suporte a um conjunto de processos de build que produzem itens de saída, como arquivos executáveis ou de recurso. Esses itens de saída são privados para o usuário e podem ser colocados em grupos que vinculam tipos de saída relacionados, como arquivos executáveis (arquivos .exe, .dll, .lib) e arquivos de origem (arquivos .idl, .h).

 Os itens de saída podem ser disponibilizados por <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> meio dos métodos e enumerados com os métodos <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> . Quando você deseja agrupar itens de saída, seu projeto também deve implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> interface .

 O constructo desenvolvido pela implementação `IVsOutputGroup` permite que os projetos a agrupam saídas de acordo com o uso. Por exemplo, uma DLL pode ser agrupada com seu banco de dados de programa (PDB).

> [!NOTE]
> Um arquivo PDB contém informações de depuração e é criado quando a opção 'Gerar Informações de Depuração' é especificada ao criar o .dll ou .exe. O arquivo .pdb geralmente é gerado apenas para a configuração do projeto de depuração.

 O projeto deve retornar o mesmo número de grupos para cada configuração compatível, embora o número de saídas contidos em um grupo possa variar de configuração para configuração. Por exemplo, a DLL de Matt do projeto pode incluir mattd.dll e mattd.pdb na configuração de Depuração, mas incluir apenas matt.dll configuração de Varejo.

 Os grupos também têm as mesmas informações de identificador, como nome canônico, nome de exibição e informações de grupo, da configuração à configuração em um projeto. Essa consistência permite que a implantação e o empacotamento continuem funcionando mesmo se as configurações mudarem.

 Os grupos também podem ter uma saída de chave que permite que os atalhos de empacotamento apontem para algo significativo. Qualquer grupo pode estar vazio em uma determinada configuração, portanto, nenhuma suposição deve ser feita sobre o tamanho de um grupo. O tamanho (número de saídas) de cada grupo em qualquer configuração pode ser diferente do tamanho de outro grupo na mesma configuração. Ele também pode ser diferente do tamanho do mesmo grupo em outra configuração.

 ![Gráfico de Grupos de Saída](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups") Grupos de saída

 O principal uso da interface é fornecer acesso para criar, implantar e depurar objetos de gerenciamento e permitir aos projetos a liberdade de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> agrupar saídas. Para obter mais informações sobre o uso dessa interface, consulte [Project Configuration Object](../../extensibility/internals/project-configuration-object.md).

 No diagrama anterior, o Grupo Criado tem uma saída de chave entre configurações (bD.exe ou b.exe) para que o usuário possa criar um atalho para Criado e saber que o atalho funcionará independentemente da configuração implantada. A Origem do Grupo não tem uma saída de chave, portanto, o usuário não pode criar um atalho para ela. Se o Grupo de Depuração Criado tiver uma saída de chave, mas o Grupo de Varejo Criado não tiver, isso seria uma implementação incorreta. Segue-se, então, que se qualquer configuração tiver um grupo que não contenha saídas e, como resultado, nenhum arquivo de chave, outras configurações com esse grupo que contenham saídas não poderão ter arquivos de chave. Os editores do instalador supõem que nomes canônicos e nomes de exibição de grupos, além da existência de um arquivo de chave, não mudam com base em configurações.

 Observe que, se um projeto tiver um que não deseja empacotar ou implantar, será suficiente não colocar `IVsOutputGroup` essa saída em um grupo. A saída ainda pode ser enumerada normalmente implementando o método que retorna todas as saídas de uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> configuração, independentemente do agrupamento.

 Para obter mais informações, consulte a implementação de `IVsOutputGroup` no exemplo projeto personalizado em [MPF for Projects](https://github.com/tunnelvisionlabs/MPFProj10).

## <a name="see-also"></a>Confira também
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Configuração de projeto para compilar](../../extensibility/internals/project-configuration-for-building.md)
- [Objeto de configuração de projeto](../../extensibility/internals/project-configuration-object.md)
- [Configuração da solução](../../extensibility/internals/solution-configuration.md)
