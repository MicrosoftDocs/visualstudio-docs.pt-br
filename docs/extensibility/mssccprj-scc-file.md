---
title: MSSCCPRJ. Arquivo SCC | Microsoft Docs
description: Saiba mais sobre o MSSCCPRJ. O arquivo SCC, que é um arquivo local do lado do cliente usado pelo plug-in de controle do código-fonte, que funciona com o SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e006e4462522f4c464f40e0656dcef4d32c85fb7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899245"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ. Arquivo SCC
Quando você coloca uma solução ou projeto do Visual Studio no controle do código-fonte usando o IDE, o IDE recebe duas partes principais de informações. As informações são provenientes do plug-in de controle do código-fonte na forma de cadeias de caracteres. Essas cadeias de caracteres, "AuxPath" e "ProjName", são opacas para o IDE, mas elas são usadas pelo plug-in para localizar a solução ou o projeto no controle de versão. Normalmente, o IDE obtém essas cadeias de caracteres pela primeira vez chamando [SccGetProjPath](../extensibility/sccgetprojpath-function.md)e, em seguida, salva-as no arquivo da solução ou do projeto para chamadas futuras para o [SccOpenProject](../extensibility/sccopenproject-function.md). Quando inseridos na solução e nos arquivos de projeto, as cadeias de caracteres "AuxPath" e "ProjName" não são atualizadas automaticamente quando um usuário ramifica, bifurca ou copia arquivos de solução e de projeto que estão no controle de versão. Para garantir que os arquivos de solução e de projeto apontem para o local correto no controle de versão, os usuários devem atualizar manualmente as cadeias de caracteres. Como as cadeias de caracteres são destinadas a serem opacas, talvez nem sempre fique claro como elas devem ser atualizadas.

 O plug-in de controle do código-fonte pode evitar esse problema armazenando as cadeias de caracteres "AuxPath" e "ProjName" em um arquivo especial chamado arquivo *MSSCCPRJ. SCC* . É um arquivo local do lado do cliente que é de propriedade e mantido pelo plug-in do. Esse arquivo nunca é colocado sob o controle do código-fonte, mas é gerado pelo plug-in para cada diretório que contém arquivos de origem controlada. Para determinar quais arquivos são arquivos de solução e projeto do Visual Studio, um plug-in de controle do código-fonte pode comparar as extensões de arquivo com uma lista padrão ou fornecida pelo usuário. Depois que o IDE detecta que um plug-in dá suporte ao arquivo *MSSCCPRJ. SCC* , ele deixa de incorporar as cadeias de caracteres "AuxPath" e "ProjName" em arquivos de solução e de projeto e lê essas cadeias de caracteres do arquivo *MSSCCPRJ. SCC* em vez disso.

 Um plug-in de controle do código-fonte que dá suporte ao arquivo *MSSCCPRJ. SCC* deve aderir às seguintes diretrizes:

- Só pode haver um arquivo *MSSCCPRJ. SCC* por diretório.

- Um arquivo *MSSCCPRJ. SCC* pode conter "AuxPath" e "ProjName" para vários arquivos que estão sob o controle do código-fonte dentro de um determinado diretório.

- A cadeia de caracteres "AuxPath" não deve ter aspas dentro dela. É permitido ter aspas ao seu respeito como delimitadores (por exemplo, um par de aspas duplas pode ser usado para indicar uma cadeia de caracteres vazia). O IDE removerá todas as aspas da cadeia de caracteres "AuxPath" quando ela for lida no arquivo *MSSCCPRJ. SCC* .

- A cadeia de caracteres "ProjName" no *MSSCCPRJ. O arquivo SCC* deve corresponder exatamente à cadeia de caracteres retornada da `SccGetProjPath` função. Se a cadeia de caracteres retornada pela função tiver aspas em torno dela, a cadeia de caracteres no arquivo *MSSCCPRJ. SCC* deverá ter aspas em torno dele e vice-versa.

- Um arquivo *MSSCCPRJ. SCC* é criado ou atualizado sempre que um arquivo é colocado no controle do código-fonte.

- Se um arquivo *MSSCCPRJ. SCC* for excluído, um provedor deverá gerá-lo novamente na próxima vez que executar uma operação de controle do código-fonte relacionada a esse diretório.

- Um arquivo *MSSCCPRJ. SCC* deve seguir estritamente o formato definido.

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>Uma ilustração do MSSCCPRJ. Formato de arquivo SCC
 Veja a seguir um exemplo do formato de arquivo *MSSCCPRJ. SCC* (os números de linha são fornecidos apenas como um guia e não devem ser incluídos no corpo do arquivo):

- [Linha 1] `SCC = This is a Source Code Control file`

- [Linha 2]

- [Linha 3] `[TestApp.sln]`

- [Linha 4] `SCC_Aux_Path = "\\server\vss\"`

- [Linha 5] `SCC_Project_Name = "$/TestApp"`

- [Linha 6]

- [Linha 7] `[TestApp.csproj]`

- [Linha 8] `SCC_Aux_Path = "\\server\vss\"`

- [Linha 9] `SCC_Project_Name = "$/TestApp"`

 A primeira linha declara a finalidade do arquivo e serve como a assinatura para todos os arquivos desse tipo. Essa linha deve aparecer exatamente como esta em todos os arquivos *MSSCCPRJ. SCC* :

 `SCC = This is a Source Code Control file`

 A seção a seguir detalha as configurações para cada arquivo, marcado pelo nome do arquivo entre colchetes. Esta seção é repetida para cada arquivo que está sendo acompanhado. Essa linha é uma amostra de um nome de arquivo, ou seja, `[TestApp.csproj]` . O IDE espera as duas linhas a seguir. No entanto, ele não define o estilo dos valores definidos. As variáveis são `SCC_Aux_Path` e `SCC_Project_Name` .

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 Não há nenhum delimitador final para esta seção. O nome do arquivo, bem como todos os literais que aparecem no arquivo, são definidos no arquivo de cabeçalho SCC. h. Para obter mais informações, consulte [cadeias de caracteres usadas como chaves para localizar um plug-in de controle do código-fonte](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md).

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [Cadeias de caracteres usadas como chaves para localizar um plug-in de controle do código-fonte](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
