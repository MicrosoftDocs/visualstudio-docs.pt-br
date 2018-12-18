---
title: Função SccGet | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 78c766e52278c8bae29e57cad6f1c0255de4ea43
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51761722"
---
# <a name="sccget-function"></a>Função SccGet
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função recupera uma cópia de um ou mais arquivos para exibir e compilar, mas não para edição. Na maioria dos sistemas, os arquivos são marcados como somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccGet(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle do código-fonte.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 nFiles  
 [in] Número de arquivos especificados no `lpFileNames` matriz.  
  
 lpFileNames  
 [in] Matriz de nomes totalmente qualificados dos arquivos a serem recuperados.  
  
 fOptions  
 [in] Sinalizadores de comando (`SCC_GET_ALL`, `SCC_GET_RECURSIVE`).  
  
 pvOptions  
 [in] Opções de plug-in específico de controle de origem.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Sucesso da operação de obtenção.|  
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle de origem.|  
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não suporta esta operação.|  
|SCC_E_FILEISCHECKEDOUT|Não é possível obter o arquivo que o usuário atualmente tem check-out.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NOSPECIFIEDVERSION|Uma versão inválida ou data/hora especificado.|  
|SCC_E_NONSPECIFICERROR|Falha não específica; arquivo não foi sincronizado.|  
|SCC_I_OPERATIONCANCELED|Operação cancelada antes da conclusão.|  
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado para executar esta operação.|  
  
## <a name="remarks"></a>Comentários  
 Essa função é chamada com uma contagem e uma matriz de nomes dos arquivos a serem recuperados. Se o IDE passa o sinalizador `SCC_GET_ALL`, isso significa que os itens na `lpFileNames` não são arquivos, diretórios, mas e se todos os arquivos sob controle do código-fonte nos diretórios de determinado devem ser recuperadas.  
  
 O `SCC_GET_ALL` sinalizador pode ser combinado com o `SCC_GET_RECURSIVE` sinalizador para recuperar todos os arquivos nos diretórios de determinado e todos os subdiretórios também.  
  
> [!NOTE]
>  `SCC_GET_RECURSIVE` nunca deve ser passado sem `SCC_GET_ALL`. Além disso, observe que se diretórios C:\A e C:\A\B são ambos repassadas recursiva obtém, C:\A\B e todos os seus subdiretórios serão realmente recuperados duas vezes. É responsabilidade do IDE — e não o controle de fonte do plug-in — para certificar-se de que as duplicatas como esse são mantidas fora da matriz.  
  
 Por fim, mesmo se o controle de fonte de uma plug-in especificado o `SCC_CAP_GET_NOUI` sinalizador na inicialização, indicando que ele não tem uma interface do usuário para um comando Get, essa função ainda pode ser chamada pelo IDE para recuperar arquivos. O sinalizador simplesmente significa que o IDE não exibe um item de menu Get e que o plug-in não é esperado para fornecer qualquer interface do usuário.  
  
## <a name="renaming-and-sccget"></a>Renomear e SccGet  
 Situação: um usuário faz check-out de um arquivo, por exemplo,. txt e modifica a ele. Antes que o. txt pode ser verificado, um segundo usuário renomeia. txt para b. txt no banco de dados de controle do código-fonte, faz check-out de b. txt, faz algumas modificações no arquivo e verifica o arquivo. O primeiro usuário que deseja que as alterações feitas pelo segundo usuário para que o primeiro usuário renomeia a sua versão local do arquivo. txt para b. txt e faz um get no arquivo. No entanto, o cache local que mantém o controle de números de versão ainda considerará a primeira versão do. txt será armazenada localmente e então o controle de origem não é possível resolver as diferenças.  
  
 Há duas maneiras de resolver essa situação em que o cache local de versões de controle do código-fonte se torna fora de sincronia com o banco de dados de controle do código-fonte:  
  
1.  Não permita renomear um arquivo em que o banco de dados de controle de origem que está sendo verificado.  
  
2.  Fazer o equivalente de "exclusão antigo" seguido de "Adicionar novo". O seguinte algoritmo é uma forma de fazer isso.  
  
    1.  Chame o [SccQueryChanges](../extensibility/sccquerychanges-function.md) função para saber mais sobre a renomeação de. txt para b. txt no banco de dados de controle do código-fonte.  
  
    2.  Renomeie a. txt local para b. txt.  
  
    3.  Chamar o `SccGet` função para. txt e b. txt.  
  
    4.  Como. txt não existe no banco de dados de controle do código-fonte, o cache local de versão é limpos das informações de versão. txt ausente.  
  
    5.  O arquivo b. txt que está sendo extraído é mesclado com o conteúdo do arquivo local b. txt.  
  
    6.  O arquivo b. txt atualizada agora pode fazer check-in.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)

