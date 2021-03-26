---
title: Descrição do diretório de modelo (. Arquivos de VSDir) | Microsoft Docs
description: Saiba como um arquivo de descrição de diretório de modelo permite que o IDE do Visual Studio exiba pastas, arquivos. vsz e modelos associados ao seu projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsdir files
- VSDIR files
- template directory description files
ms.assetid: 9df51800-190e-4662-b685-fdaafcff1400
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bdd21dfa9fe5aae11553bb0268017690aba46fe9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080496"
---
# <a name="template-directory-description-vsdir-files"></a>Arquivos de descrição do diretório de modelo (.Vsdir)
Um arquivo de descrição do diretório de modelo (. vsdir) é um arquivo de texto que permite que o IDE (ambiente de desenvolvimento integrado) exiba pastas, arquivos. vsz e arquivos de modelo associados ao seu projeto em caixas de diálogo. O conteúdo inclui um registro por arquivo ou pasta. Todos os arquivos. vsdir em um local referenciado são mesclados, embora apenas um arquivo. vsdir seja geralmente fornecido para descrever várias pastas, assistentes ou arquivos de modelo.

 Pastas (subdiretórios), arquivos que são referenciados no arquivo. vsdir e o próprio arquivo. vsdir estão todos localizados no mesmo diretório. Quando o IDE executa um assistente ou exibe uma pasta ou arquivo nas caixas de diálogo **novo projeto** ou **Adicionar novo item** , o IDE examina o diretório que contém os arquivos executados para determinar se um arquivo. vsdir está presente. Se um arquivo. vsdir for encontrado, o IDE o lerá para determinar se ele contém uma entrada para a pasta ou o arquivo executado ou exibido. Se uma entrada for encontrada, o IDE usará as informações na execução do assistente ou na exibição do conteúdo.

 O exemplo de código a seguir é do arquivo SourceFiles. vsdir na \<EnvSDK> chave do registro \bscprj\bscprj\bscprjprojectitems\ Source_Files:

```
HeaderFile.h|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#125|130|#126|0|0|0|#127
SourceFile.cpp|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#122|110|#123|0|0|0|#124
```

 Nesse caso, dois registros estão em um arquivo. Uma nova linha (caractere de retorno de carro) separa cada registro. Cada linha representa um tipo de arquivo diferente. Um caractere de pipe (&#124;) separa os campos em cada registro. Um único diretório pode conter vários arquivos. vsdir que têm nomes de arquivo diferentes, ou você pode ter um arquivo. vsdir para cada tipo de arquivo.

## <a name="fields"></a>Campos
 A tabela a seguir lista os campos especificados para cada registro.

| Campo | Descrição |
| - | - |
| Nome do caminho relativo (RelPathName) | O nome da pasta, modelo ou arquivo. vsz, como HeaderFile. h ou MyWizard. vsz. Esse campo também pode ser um nome usado para representar uma pasta. |
| {clsidPackage} | O GUID do VSPackage que permite o acesso a cadeias de caracteres localizadas, como localizador, descrição, IconResourceId e SuggestedBaseName, nos recursos da DLL (biblioteca de vínculo dinâmico) de satélite do VSPackage. IconResourceId se aplica se DLLPath não for fornecido. **Observação:**  Esse campo é opcional, a menos que um ou mais dos campos anteriores seja um identificador de recurso. Normalmente, esse campo é deixado em branco para arquivos. vsdir que correspondem a assistentes de terceiros que não localizam seu texto. |
| Localizador | O nome localizado do arquivo de modelo ou assistente. Esse campo pode ser uma cadeia de caracteres ou um identificador de recurso do formato "#ResID". Esse nome é exibido na caixa de diálogo **Adicionar novo item** . **Observação:**  Se o localizador for um identificador de recurso, {clsidPackage} será necessário. |
| SortPriority | Um inteiro que representa a prioridade relativa deste arquivo de modelo ou assistente. Por exemplo, se esse item tiver um valor de 1, esse item será exibido ao lado de outros itens com um valor de 1 e à frente de todos os itens com um valor de classificação 2 ou maior.<br /><br /> A prioridade de classificação é relativa aos itens no mesmo diretório. Pode haver mais de um arquivo. vsdir no mesmo diretório. Nesse caso, os itens de todos <em>.</em> os arquivos VSDir nesse diretório são mesclados. Os itens com a mesma prioridade são listados em ordem lexicográfica não diferencia maiúsculas de minúsculas do nome exibido. A `_wcsicmp` função é usada para ordenar os itens.<br /><br /> Os itens não descritos nos arquivos. vsdir incluem um número de prioridade maior que o número de prioridade mais alto listado nos arquivos. VSDir. O resultado é que esses itens estão no final da lista exibida, independentemente de seu nome. |
| Descrição | A descrição localizada do arquivo de modelo ou do assistente. Esse campo pode ser uma cadeia de caracteres ou um identificador de recurso do formato "#ResID". Essa cadeia de caracteres aparece na caixa de diálogo **novo projeto** ou **Adicionar novo item** quando o item é selecionado. |
| DLLPath ou {clsidPackage} | Usado para carregar um ícone para o arquivo de modelo ou assistente. O ícone é carregado como um recurso de um arquivo. dll ou. exe usando o IconResourceId. Esse arquivo. dll ou. exe pode ser identificado usando um caminho completo ou usando um GUID de um VSPackage. A DLL de implementação do VSPackage é usada para carregar o ícone (não a DLL satélite). |
| IconResourceId | O identificador de recurso na DLL de implementação DLL ou VSPackage que determina o ícone a ser exibido. |
| Sinalizadores ( <xref:Microsoft.VisualStudio.Shell.Interop.__VSDIRFLAGS> ) | Usado para desabilitar ou habilitar os campos de **nome** e **local** na caixa de diálogo **Adicionar novo item** . O valor do campo **flags** é o equivalente Decimal da combinação de sinalizadores de bits necessários.<br /><br /> Quando um usuário seleciona um item na **nova** guia, o projeto determina se o campo nome e o campo local são mostrados quando a caixa de diálogo **Adicionar novo item** é exibida pela primeira vez. Um item, por meio de um arquivo. vsdir, pode controlar apenas se os campos estão habilitados versus desabilitados quando o item é selecionado. |
| SuggestedBaseName | Representa o nome padrão do arquivo, do assistente ou do modelo. Este campo é uma cadeia de caracteres ou um identificador de recurso do formato "#ResID". O IDE usa esse valor para fornecer um nome padrão para o item. Esse valor base é acrescentado com um valor inteiro para tornar o nome exclusivo, como MyFile21. ASP.<br /><br /> Na lista anterior, descrição, DLLPath, IconResourceId, sinalizadores e SuggestedBaseNumber se aplicam somente a arquivos de modelo e de assistente. Esses campos não se aplicam a pastas. Esse fato é ilustrado no código do arquivo BscPrjProjectItems na \<EnvSDK> chave do registro \BscPrj\BscPrj\BscPrjProjectItems. Esse arquivo contém três registros (um para cada pasta) com quatro campos para cada registro: RelPathName, {clsidPackage}, Localizadaname e SortPriority.<br /><br /> `General&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#110&#124;100`<br /><br /> `Source_Files&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#111&#124;110`<br /><br /> `Env&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#112&#124;120` |

 Ao criar um arquivo do assistente, você também deve considerar os seguintes problemas.

- Qualquer campo não obrigatório para o qual não haja dados significativos deve conter um 0 (zero) como um espaço reservado.

- Se nenhum nome localizado for fornecido, o nome do caminho relativo será usado no arquivo do assistente.

- DLLPath substitui clsidPackage para o local do ícone.

- Se nenhum ícone for definido, o IDE substituirá o ícone padrão por um arquivo que tenha essa extensão.

- Se nenhum nome base sugerido for fornecido, ' Project ' será usado.

- Se você excluir os arquivos. vsz, pastas ou arquivos de modelo, também deverá remover seus registros associados do arquivo. VSDir.

## <a name="see-also"></a>Confira também
- [Assistentes](../../extensibility/internals/wizards.md)
- [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
