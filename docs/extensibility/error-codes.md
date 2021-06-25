---
title: Códigos de erro | Microsoft Docs
description: Este artigo contém uma lista de códigos de erro, valores e descrições para funções de API de plug-in de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eedc9311bcafdd4241e065b40079abed3977dcef
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898299"
---
# <a name="error-codes"></a>Códigos do Erro
Quando uma função de API de Plug-in de Controle do Código-Fonte retorna um erro, espera-se que seja um dos códigos de erro a seguir. Todos os erros são negativos, avisos ou códigos de erro informacionais são positivos e o sucesso é 0.

|Código do Erro|Valor|Descrição|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|O plug-in dá suporte à adição de arquivos do controle do código-fonte em duas etapas. Para obter mais informações, consulte [SccSetOption](../extensibility/sccsetoption-function.md).|
|`SCC_I_FILEDIFFERS`|6|O arquivo local é diferente do arquivo no banco de dados de controle do código-fonte (por exemplo, [SccDiff](../extensibility/sccdiff-function.md) pode retornar esse valor).|
|`SCC_I_RELOADFILE`|5|O arquivo local foi alterado durante a operação de controle do código-fonte; O IDE deve recarregar o arquivo, se possível.|
|`SCC_I_FILENOTAFFECTED`|4|O arquivo não é afetado.|
|`SCC_I_PROJECTCREATED`|3|O Projeto foi criado durante a operação de controle do código-fonte (por exemplo, durante uma chamada para [SccOpenProject](../extensibility/sccopenproject-function.md) quando `SCC_OP_CREATEIFNEW` o sinalizador é especificado).|
|`SCC_I_OPERATIONCANCELED`|2|A operação foi cancelada.|
|`SCC_I_ADV_SUPPORT`|1|O plug-in dá suporte a opções avançadas para o comando especificado. Para obter mais informações, [consulte SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md).|
|`SCC_OK`|0|Sucesso.|
|`SCC_E_INITIALIZEFAILED`|-1|Erro: falha na inicialização.|
|`SCC_E_UNKNOWNPROJECT`|-2|Erro: o projeto é desconhecido.|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|Erro: não foi possível criar o projeto.|
|`SCC_E_NOTCHECKEDOUT`|-4|Erro: o arquivo não está marcado.|
|`SCC_E_ALREADYCHECKEDOUT`|-5|Erro: o arquivo já foi verificado.|
|`SCC_E_FILEISLOCKED`|-6|Erro: o arquivo está bloqueado.|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|Erro: o arquivo é verificado exclusivamente.|
|`SCC_E_ACCESSFAILURE`|-8|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|`SCC_E_CHECKINCONFLICT`|-9|Erro: houve um conflito durante o check-in.|
|`SCC_E_FILEALREADYEXISTS`|-10|Erro: o arquivo já existe.|
|`SCC_E_FILENOTCONTROLLED`|-11|Erro: o arquivo não está sob controle do código-fonte.|
|`SCC_E_FILEISCHECKEDOUT`|-12|Erro: o arquivo é verificado.|
|`SCC_E_NOSPECIFIEDVERSION`|-13|Erro: não há nenhuma versão especificada.|
|`SCC_E_OPNOTSUPPORTED`|-14|Erro: não há suporte para a operação.|
|`SCC_E_NONSPECIFICERROR`|-15|Erro não específico.|
|`SCC_E_OPNOTPERFORMED`|-16|Erro, a operação não foi executada.|
|`SCC_E_TYPENOTSUPPORTED`|-17|Erro: o tipo do arquivo, por exemplo, binário, não é suportado pelo sistema de controle do código-fonte.|
|`SCC_E_VERIFYMERGE`|-18|O arquivo foi mesclado automaticamente, mas não foi verificado porque está pendente na verificação do usuário.|
|`SCC_E_FIXMERGE`|-19|O arquivo foi mesclado automaticamente, mas não foi verificado devido a um conflito de mesclagem que deve ser resolvido manualmente.|
|`SCC_E_SHELLFAILURE`|-20|Erro devido a uma falha de shell.|
|`SCC_E_INVALIDUSER`|-21|Erro: o usuário é inválido.|
|`SCC_E_PROJECTALREADYOPEN`|-22|Erro: o projeto já está aberto.|
|`SCC_E_PROJSYNTAXERR`|-23|Erro de sintaxe do projeto.|
|`SCC_E_INVALIDFILEPATH`|-24|Erro: o caminho do arquivo é inválido.|
|`SCC_E_PROJNOTOPEN`|-25|Erro: o projeto não está aberto.|
|`SCC_E_NOTAUTHORIZED`|-26|Erro: o usuário não está autorizado a executar essa operação.|
|`SCC_E_FILESYNTAXERR`|-27|Erro de sintaxe de arquivo.|
|`SCC_E_FILENOTEXIST`|-28|Erro, o arquivo local não existe.|
|`SCC_E_CONNECTIONFAILURE`|-29|Erro: houve uma falha de conexão.|
|`SCC_E_UNKNOWNERROR`|-30|Erro desconhecido.|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|A operação de get em segundo plano está em andamento no momento.|

## <a name="macros-provided-for-quick-checking"></a>Macros fornecidas para verificação rápida

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>Comentários
 Todas as funções de API de plug-in de controle do código-fonte (exceto [SccAdd,](../extensibility/sccadd-function.md) [SccCheckin](../extensibility/scccheckin-function.md)e [SccDiff](../extensibility/sccdiff-function.md)) devem ter êxito quando os arquivos locais passados como argumentos não existirem na pasta de trabalho. Por exemplo, o IDE pode emitir uma chamada para [SccCheckout](../extensibility/scccheckout-function.md) ou [SccUncheckout](../extensibility/sccuncheckout-function.md) em um arquivo que não existe na pasta de trabalho, mas existe no sistema de controle do código-fonte. Essa chamada seria bem-sucedida. Somente quando não houver nenhum arquivo na pasta de trabalho ou no sistema de controle do código-fonte, a função deverá falhar.

 Determinadas funções, como `SccAdd` e , devem retornar especificamente quando o arquivo na pasta de trabalho não `SccCheckin` `SCC_E_FILENOTEXIST` existir. Espera-se que outras funções sejam bem-sucedidas quando o arquivo de trabalho não existir, se as funções operarem em um nome de arquivo válido no sistema de controle do código-fonte.

 O plug-in de controle do código-fonte não deve fazer suposições sobre privilégios em um arquivo na pasta de trabalho, mesmo que o plug-in tenha marcado o arquivo somente leitura durante alguma operação. Um arquivo na pasta de trabalho pode ser movido, excluído e alterado fora do controle do plug-in.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
