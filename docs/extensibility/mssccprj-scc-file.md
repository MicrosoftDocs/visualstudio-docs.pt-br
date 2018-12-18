---
title: MSSCCPRJ. Arquivos SCC | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: cc754437433124e033b0f0fb0feac79487664b51
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636065"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ. Arquivos SCC
Quando você coloca uma solução do Visual Studio ou o projeto sob controle do código-fonte usando o IDE, o IDE recebe duas informações cruciais. A informação vem de controle de fonte de plug-in na forma de cadeias de caracteres. Essas cadeias de caracteres "AuxPath" e "Nomedoprojeto" são opacas para o IDE, mas eles são usados pelo plug-in para localizar a solução ou projeto no controle de versão. O IDE normalmente obtém essas cadeias de caracteres na primeira vez chamando o [SccGetProjPath](../extensibility/sccgetprojpath-function.md), e ele, em seguida, salva-os no arquivo de projeto ou solução para futuras chamadas para o [SccOpenProject](../extensibility/sccopenproject-function.md). Quando inseridos nos arquivos de solução e projeto, as cadeias de caracteres "AuxPath" e "Nomedoprojeto" não são atualizadas automaticamente quando um usuário de branches, bifurcações, ou copia os arquivos de solução e projeto que estão no controle de versão. Para certificar-se de que os arquivos de solução e projeto apontam para sua localização correta no controle de versão, os usuários devem atualizar manualmente as cadeias de caracteres. Porque as cadeias de caracteres devem ser opaco, pode não sempre ser claro como eles devem ser atualizados.  
  
 O plug-in de controle do código-fonte pode evitar esse problema ao armazenar as cadeias de caracteres "AuxPath" e "Nomedoprojeto" em um arquivo especial chamado de *Mssccprj* arquivo. É um arquivo local e o lado do cliente que é de propriedade e mantido pelo plug-in. Esse arquivo nunca é colocado sob controle do código-fonte, mas é gerado pelo plug-in para cada diretório que contém arquivos de controle do código-fonte. Para determinar quais arquivos são arquivos de solução e projeto do Visual Studio, um plug-in de controle do código-fonte pode comparar as extensões de arquivo em relação a uma lista padrão ou fornecido pelo usuário. Depois que o IDE detecta que um oferece suporte a plug-in a *Mssccprj* arquivo, ele deixa de inserir as cadeias de caracteres "AuxPath" e "Nomedoprojeto" em arquivos de solução e projeto, e ele lê essas cadeias de caracteres da *Mssccprj*do arquivo em vez disso.  
  
 Um plug-in de controle de fonte que ofereça suporte a *Mssccprj* arquivo deve seguir as diretrizes a seguir:  
  
-   Pode haver somente um *Mssccprj* arquivo por diretório.  
  
-   Uma *Mssccprj* arquivo pode conter a "AuxPath" e "Nomedoprojeto" para vários arquivos que estão sob controle do código-fonte dentro de um determinado diretório.  
  
-   A cadeia de caracteres "AuxPath" não deve ter aspas dentro dele. Ele tem permissão para ter aspas ao redor dele como delimitadores (por exemplo, um par de aspas duplas pode ser usado para indicar uma cadeia de caracteres vazia). O IDE removeremos todas as aspas da cadeia de caracteres "AuxPath" quando são lidos a partir de *Mssccprj* arquivo.  
  
-   Cadeia de caracteres "Nomedoprojeto" no *MSSCCPRJ. Arquivos SCC* deve corresponder exatamente a cadeia de caracteres retornada do `SccGetProjPath` função. Se a cadeia de caracteres retornada pela função tem aspas ao redor dela, a cadeia de caracteres na *Mssccprj* arquivo deve ter aspas ao redor dele e vice-versa.  
  
-   Uma *Mssccprj* arquivo é criado ou atualizado sempre que um arquivo é colocado sob controle do código-fonte.  
  
-   Se um *Mssccprj* arquivo é excluído, um provedor deverá gerá-la novamente na próxima vez que ele executa uma operação de controle do código-fonte relativas a esse diretório.  
  
-   Uma *Mssccprj* arquivo estritamente deve seguir o formato definido.  
  
## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>Uma ilustração de MSSCCPRJ. Formato de arquivo do SCC  
 A seguir está um exemplo do *Mssccprj* formato de arquivo (os números de linha são fornecidos apenas como um guia e não devem ser incluídos no corpo do arquivo):  
  
 [Linha 1] `SCC = This is a Source Code Control file`  
  
 [Linha 2]  
  
 [Linha 3] `[TestApp.sln]`  
  
 [Linha 4] `SCC_Aux_Path = "\\server\vss\"`  
  
 [Linha 5] `SCC_Project_Name = "$/TestApp"`  
  
 [Linha 6]  
  
 [Linha 7] `[TestApp.csproj]`  
  
 [Linha 8] `SCC_Aux_Path = "\\server\vss\"`  
  
 [Linha 9] `SCC_Project_Name = "$/TestApp"`  
  
 A primeira linha declara a finalidade do arquivo e serve como a assinatura para todos os arquivos desse tipo. Essa linha deve aparecer exatamente como isso em todos os *Mssccprj* arquivos:  
  
 `SCC = This is a Source Code Control file`  
  
 A seção a seguir fornece detalhes sobre as configurações para cada arquivo, marcada pelo nome do arquivo entre colchetes. Esta seção é repetida para cada arquivo que estão sendo rastreado. Essa linha é um exemplo de um nome de arquivo, ou seja, `[TestApp.csproj]`. O IDE espera que as duas linhas a seguir. No entanto, ele não define o estilo dos valores definidos. As variáveis são `SCC_Aux_Path` e `SCC_Project_Name`.  
  
 `SCC_Aux_Path = "\\server\vss\"`  
  
 `SCC_Project_Name = "$/TestApp"`  
  
 Não há nenhum delimitador final para essa seção. O nome do arquivo, bem como todos os literais que aparecem no arquivo, são definidos no arquivo de cabeçalho scc.h. Para obter mais informações, consulte [cadeias de caracteres usadas como chaves para localizar um controle de fonte plug-in](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md).  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [Cadeias de caracteres usadas como chaves para localizar um controle de fonte plug-in](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)