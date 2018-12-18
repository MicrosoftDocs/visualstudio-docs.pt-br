---
title: Função SccGetProjPath | Microsoft Docs
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
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 978316cd9c953217a3e59a7ecd1b047cab12734b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752588"
---
# <a name="sccgetprojpath-function"></a>Função SccGetProjPath
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função solicita ao usuário para um caminho de projeto, que é uma cadeia de caracteres que é significativa apenas para o plug-in de controle do código-fonte. Ele é chamado quando o usuário é:  
  
-   Criar um novo projeto  
  
-   Adicionar um projeto existente ao controle de versão  
  
-   Tentativa de encontrar um projeto existente de controle de versão  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccGetProjPath (  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPSTR  lpUser,  
   LPSTR  lpProjName,  
   LPSTR  lpLocalPath,  
   LPSTR  lpAuxProjPath,  
   BOOL   bAllowChangePath,  
   LPBOOL pbNew  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpUser  
 [no, out] O nome de usuário (não deve exceder SCC_USER_SIZE, incluindo o terminador NULL)  
  
 lpProjName  
 [no, out] O nome do projeto IDE, espaço de trabalho do projeto ou makefile (não deve exceder SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
 lpLocalPath  
 [no, out] Caminho de trabalho do projeto. Se `bAllowChangePath` é `TRUE`, o plug-in de controle do código-fonte pode modificar essa cadeia de caracteres (não deve exceder MAX_PATH, incluindo o terminador null).  
  
 lpAuxProjPath  
 [no, out] Um buffer para o caminho retornado do projeto (não deve exceder SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
 bAllowChangePath  
 [in] Quando se trata `TRUE`, o plug-in de controle do código-fonte pode solicitar e modificar o `lpLocalPath` cadeia de caracteres.  
  
 pbNew  
 [no, out] Valor entrando indica se é necessário criar um novo projeto. Valor retornado indica o êxito da criação de um projeto:  
  
|Entrada|Interpretação|  
|--------------|--------------------|  
|TRUE|O usuário pode criar um novo projeto.|  
|FALSE|O usuário não pode criar um novo projeto.|  
  
|Saída|Interpretação|  
|--------------|--------------------|  
|TRUE|Um novo projeto foi criado.|  
|FALSE|Um projeto existente foi selecionado.|  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|O projeto com êxito foi criado ou recuperado.|  
|SCC_I_OPERATIONCANCELED|A operação foi cancelada.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|  
|SCC_E_CONNECTIONFAILURE|Houve um problema ao tentar se conectar ao sistema de controle de origem.|  
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado.|  
  
## <a name="remarks"></a>Comentários  
 A finalidade dessa função é para o IDE adquirir os parâmetros `lpProjName` e `lpAuxProjPath`. Depois que o plug-in de controle do código-fonte solicitará ao usuário essas informações, ele passa essas duas cadeias de caracteres para o IDE. O IDE persiste essas cadeias de caracteres em seu arquivo de solução e os passa para o [SccOpenProject](../extensibility/sccopenproject-function.md) sempre que o usuário abre este projeto. Essas cadeias de caracteres de habilitar o plug-in acompanhar informações associadas a um projeto.  
  
 Quando a função é chamada pela primeira vez, `lpAuxProjPath` é definido como uma cadeia de caracteres vazia. `lProjName` também pode estar vazia, ou pode conter o nome de projeto do IDE, que o plug-in de controle de origem pode usar ou ignorar. Quando a função retorna com êxito, o plug-in retorna duas cadeias de caracteres correspondentes. O IDE não faz nenhuma suposição sobre essas cadeias de caracteres, não irá usá-los e não permitirá que o usuário para modificá-los. Se o usuário deseja alterar as configurações, o IDE irá chamar `SccGetProjPath` novamente, passar os mesmos valores que tinha recebido da execução anterior. Assim, o plug-in controle total sobre essas duas cadeias de caracteres.  
  
 Para `lpUser`, o IDE pode passar um nome de usuário ou pode simplesmente passar um ponteiro para uma cadeia de caracteres vazia. Se houver um nome de usuário, o plug-in de controle do código-fonte deve usá-lo como padrão. No entanto, se nenhum nome foi passado ou se o logon falhou com o nome fornecido, o plug-in deve solicitar ao usuário para um logon e passe o nome de volta no `lpUser` quando ele recebe um logon válido. Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre alocará um buffer de tamanho (`SCC_USER_LEN`+ 1).  
  
> [!NOTE]
>  A primeira ação que executa o IDE pode ser uma chamada para o `SccOpenProject` função ou o `SccGetProjPath` função. Portanto, ambos têm um idênticos `lpUser` parâmetro, que permite que o controle do código-fonte plug-in para conectar o usuário em qualquer momento. Mesmo se o retorno da função indica uma falha, o plug-in deve preencher essa cadeia de caracteres com um nome de logon válido.  
  
 `lpLocalPath` é o diretório em que o usuário mantém o projeto. Pode ser uma cadeia de caracteres vazia. Se não houver nenhum diretório atualmente definido (como no caso de um usuário de tentar baixar um projeto do sistema de controle de origem) e se `bAllowChangePath` é `TRUE`, o plug-in de controle do código-fonte pode solicitar a entrada do usuário ou usar algum outro método para colocar seu possui a cadeia de caracteres em `lpLocalPath`. Se `bAllowChangePath` é `FALSE`, o plug-in não deve alterar a cadeia de caracteres, porque o usuário já estiver trabalhando no diretório especificado.  
  
 Se o usuário cria um novo projeto a ser colocada sob controle do código-fonte, o plug-in de controle do código-fonte pode não realmente criá-lo no sistema de controle de origem no momento `SccGetProjPath` é chamado. Em vez disso, ele passa de volta a cadeia de caracteres junto com um valor diferente de zero para `pbNew`, indicando que o projeto será criado no sistema de controle de origem.  
  
 Por exemplo, se um usuário a **novo projeto** assistente no Visual Studio adiciona o seu projeto ao controle de origem, o Visual Studio chama esta função e o plug-in determina se é okey criar um novo projeto no sistema de controle de origem para contém o projeto do Visual Studio. Se o usuário clica **Cancelar** antes de concluir o assistente, o projeto nunca é criado. Se o usuário clica **Okey**, o Visual Studio chama `SccOpenProject`, passando `SCC_OPT_CREATEIFNEW`, e o projeto de origem controlada é criado nesse momento.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)

