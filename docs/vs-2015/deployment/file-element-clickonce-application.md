---
title: '&lt;arquivo&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#file
- http://www.w3.org/2000/09/xmldsig#DigestValue
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <file> element [ClickOnce application manifest]
- manifests [ClickOnce], file element
ms.assetid: 56e3490c-eed5-4841-b1bf-eefe778b6ac9
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 16c301d55738519f3e097138f08b6b2c2fe2b4c7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49270725"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;arquivo&gt; elemento (aplicativo ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Identifica todos os arquivos de nonassembly baixado e usado pelo aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<file  
    name  
    size  
    group  
    optional  
    writeableType  
>  
    <typelib  
        tlbid  
        version  
        helpdir  
        resourceid  
        flags  
    />  
    <comClass  
        clsid  
        description  
        threadingModel  
        tlbid  
        progid  
        miscStatus  
        miscStatusIcon  
        miscStatusContent  
        miscStatusDocPrint  
        miscStatusThumbnail  
    />  
    <comInterfaceExternalProxyStub  
        iid  
        baseInterface  
        numMethods  
        name  
        tlbid  
        proxyStubClass32  
    />  
    <comInterfaceProxyStub  
        iid  
        baseInterface  
        numMethods  
        name  
        tlbid  
        proxyStubClass32  
    />  
    <windowClass  
        versioned  
    />  
</file>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O elemento `file` é opcional. O elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`name`|Necessário. Identifica o nome do arquivo.|  
|`size`|Necessário. Especifica o tamanho, em bytes, do arquivo.|  
|`group`|Opcional, se o `optional` atributo não for especificado ou definido como `false`; obrigatório se `optional` é `true`. O nome do grupo ao qual este arquivo pertence. O nome pode ser qualquer valor de cadeia de caracteres Unicode escolhido pelo desenvolvedor e é usado para download de arquivos sob demanda com o <xref:System.Deployment.Application.ApplicationDeployment> classe.|  
|`optional`|Opcional. Especifica se esse arquivo deve executar quando o aplicativo é o primeiro de download, ou se o arquivo deve residir apenas no servidor até que o aplicativo solicitá-lo sob demanda. Se `false` ou indefinido, o arquivo é baixado quando o aplicativo pela primeira vez é executado ou instalado. Se `true`, um `group` deve ser especificado para o manifesto do aplicativo seja válido. `optional` não pode ser true se `writeableType` for especificado com o valor `applicationData`.|  
|`writeableType`|Opcional. Especifica que esse arquivo é um arquivo de dados. Atualmente, o único valor válido é `applicationData`.|  
  
## <a name="typelib"></a>TypeLib  
 O `typelib` elemento é um filho opcional do elemento de arquivo. O elemento descreve a biblioteca de tipos que pertence ao componente COM. O elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`tlbid`|Necessário. O GUID atribuído à biblioteca de tipos.|  
|`version`|Necessário. O número de versão da biblioteca de tipos.|  
|`helpdir`|Necessário. O diretório que contém os arquivos de ajuda para o componente. Pode ter comprimento zero.|  
|`resourceid`|Opcional. A representação de cadeia de caracteres hexadecimal do identificador de localidade (LCID). É um a quatro dígitos hexadecimais sem um prefixo 0x e sem zeros à esquerda. O LCID pode ter um identificador de subidioma neutro.|  
|`flags`|Opcional. A representação de cadeia de caracteres dos sinalizadores de biblioteca de tipo para esta biblioteca de tipos. Especificamente, ele deve ser um dos "RESTRICTED", "Controle", "HIDDEN" e "HASDISKIMAGE".|  
  
## <a name="comclass"></a>comClass  
 O `comClass` elemento é um filho opcional do `file` elemento, mas é necessário se o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo contém um componente COM que pretende implantar usando com sem registro. O elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`clsid`|Necessário. A ID de classe do componente COM, expressada como um GUID.|  
|`description`|Opcional. O nome de classe.|  
|`threadingModel`|Opcional. O modelo de threading usado pelas classes de COM em processo. Se essa propriedade for nula, nenhum modelo de threading é usado. O componente é criado no thread principal do cliente e chamadas de outros threads são empacotadas para este thread. A lista a seguir mostra os valores válidos:<br /><br /> `Apartment`, `Free`, `Both` e `Neutral`.|  
|`tlbid`|Opcional. GUID da biblioteca de tipos para esse componente COM.|  
|`progid`|Opcional. Identificador programático dependente de versão associado com o componente COM. O formato de um `ProgID` é `<vendor>.<component>.<version>`.|  
|`miscStatus`|Opcional. As informações fornecidas pelo duplicatas no assembly do manifesto a `MiscStatus` chave do registro. Se os valores para o `miscStatusIcon`, `miscStatusContent`, `miscStatusDocprint`, ou `miscStatusThumbnail` atributos não forem encontrados, o valor padrão correspondente listado na `miscStatus` é usado para os atributos ausentes. O valor pode ser uma lista delimitada por vírgulas dos valores de atributo da tabela a seguir. Você pode usar esse atributo, se o COM é uma classe OCX requer `MiscStatus` valores de chave do registro.|  
|`miscStatusIcon`|Opcional. As informações fornecidas pelo DVASPECT_ICON do manifesto de duplicatas no assembly. Ele pode fornecer um ícone de um objeto. O valor pode ser uma lista delimitada por vírgulas dos valores de atributo da tabela a seguir. Você pode usar esse atributo, se o COM é uma classe OCX requer `Miscstatus` valores de chave do registro.|  
|`miscStatusContent`|Opcional. As informações fornecidas pelo DVASPECT_CONTENT do manifesto de duplicatas no assembly. Ele pode fornecer um documento composto que pode ser exibido para uma tela ou impressora. O valor pode ser uma lista delimitada por vírgulas dos valores de atributo da tabela a seguir. Você pode usar esse atributo, se o COM é uma classe OCX requer `MiscStatus` valores de chave do registro.|  
|`miscStatusDocPrint`|Opcional. As informações fornecidas pelo DVASPECT_DOCPRINT do manifesto de duplicatas no assembly. Ele pode fornecer uma representação de objeto que pode ser exibida na tela como se impresso em uma impressora. O valor pode ser uma lista delimitada por vírgulas dos valores de atributo da tabela a seguir. Você pode usar esse atributo, se o COM é uma classe OCX requer `MiscStatus` valores de chave do registro.|  
|`miscStatusThumbnail`|Opcional. As informações fornecidas pelo DVASPECT_THUMBNAIL do manifesto de duplicatas em um assembly. Ele pode fornecer uma miniatura de um objeto que pode ser exibido em uma ferramenta de procura. O valor pode ser uma lista delimitada por vírgulas dos valores de atributo da tabela a seguir. Você pode usar esse atributo, se o COM é uma classe OCX requer `MiscStatus` valores de chave do registro.|  
  
## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub  
 O `comInterfaceExternalProxyStub` elemento é um filho opcional do `file` elemento, mas pode ser necessário se o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo contém um componente COM que pretende implantar usando com sem registro. O elemento contém os atributos a seguir.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`iid`|Necessário. A interface IID (ID) que é atendido por esse proxy. O IID deve ter as chaves em torno dele.|  
|`baseInterface`|Opcional. O IID da interface da qual a interface referenciada por `iid` é derivado.|  
|`numMethods`|Opcional. O número de métodos implementados pela interface.|  
|`name`|Opcional. O nome da interface como ele será exibido no código.|  
|`tlbid`|Opcional. A biblioteca de tipos que contém a descrição da interface especificada pelo `iid` atributo.|  
|`proxyStubClass32`|Opcional. Mapeia uma IID para um CLSID em DLLs do proxy de 32 bits.|  
  
## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub  
 O `comInterfaceProxyStub` elemento é um filho opcional do `file` elemento, mas pode ser necessário se o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo contém um componente COM que pretende implantar usando com sem registro. O elemento contém os atributos a seguir.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`iid`|Necessário. A interface IID (ID) que é atendido por esse proxy. O IID deve ter as chaves em torno dele.|  
|`baseInterface`|Opcional. O IID da interface da qual a interface referenciada por `iid` é derivado.|  
|`numMethods`|Opcional. O número de métodos implementados pela interface.|  
|`Name`|Opcional. O nome da interface como ele será exibido no código.|  
|`Tlbid`|Opcional. A biblioteca de tipos que contém a descrição da interface especificada pelo `iid` atributo.|  
|`proxyStubClass32`|Opcional. Mapeia uma IID para um CLSID em DLLs do proxy de 32 bits.|  
|`threadingModel`|Opcional. Opcional. O modelo de threading usado pelas classes de COM em processo. Se essa propriedade for nula, nenhum modelo de threading é usado. O componente é criado no thread principal do cliente e chamadas de outros threads são empacotadas para este thread. A lista a seguir mostra os valores válidos:<br /><br /> `Apartment`, `Free`, `Both` e `Neutral`.|  
  
## <a name="windowclass"></a>windowClass  
 O `windowClass` elemento é um filho opcional do `file` elemento, mas pode ser necessário se o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo contém um componente COM que pretende implantar usando com sem registro. O elemento se refere a uma classe de janela definida pelo componente COM que deve ter uma versão aplicada a ele. O elemento contém os atributos a seguir.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`versioned`|Opcional. Controla se a janela interna usado no registro de nome da classe contém a versão do assembly que contém a classe de janela. O valor desse atributo pode ser `yes` ou `no`. O padrão é `yes`. O valor `no` só deve ser usado se a mesma classe de janela é definida por um componente lado a lado e um componente não-side-by-side equivalente e deseja tratá-los como a mesma classe de janela. Observe que se aplicam as regras comuns sobre o registro de classe de janela — somente o primeiro componente que registra a classe de janela será possível registrá-lo, porque ele não tem uma versão aplicada a ele.|  
  
## <a name="hash"></a>hash  
 O `hash` elemento é um filho opcional de `file` elemento. O `hash` elemento não tem atributos.  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] usa um algoritmo hash de todos os arquivos em um aplicativo como uma verificação de segurança, para garantir que nenhum dos arquivos foram alterados após a implantação. Se o `hash` elemento não for incluído, essa verificação não será executada. Portanto, omitindo o `hash` elemento não é recomendado.  
  
 Se um manifesto contém um arquivo que não será transformada em hash, esse manifesto não pode ser digitalmente assinados, pois os usuários não é possível verificar o conteúdo de um arquivo sem hash.  
  
## <a name="dsigtransforms"></a>DSIG:Transforms  
 O `dsig:Transforms` elemento é um filho necessário do `hash` elemento. O `dsig:Transforms` elemento não tem atributos.  
  
## <a name="dsigtransform"></a>DSIG:Transform  
 O `dsig:Transform` elemento é um filho necessário do `dsig:Transforms` elemento. O `dsig:Transform` elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Algorithm`|O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] é `urn:schemas-microsoft-com:HashTransforms.Identity`.|  
  
## <a name="dsigdigestmethod"></a>DSIG:DigestMethod  
 O `dsig:DigestMethod` elemento é um filho necessário do `hash` elemento. O `dsig:DigestMethod` elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Algorithm`|O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] é `http://www.w3.org/2000/09/xmldsig#sha1`.|  
  
## <a name="dsigdigestvalue"></a>DSIG:DigestValue  
 O `dsig:DigestValue` elemento é um filho necessário do `hash` elemento. O `dsig:DigestValue` elemento não tem atributos. Seu valor de texto é o hash calculado para o arquivo especificado.  
  
## <a name="remarks"></a>Comentários  
 Este elemento identifica todos os arquivos de nonassembly que compõem o aplicativo e, em particular, os valores de hash para o arquivo de verificação. Esse elemento também pode incluir dados de isolamento (COM Component Object Model) associados ao arquivo. Se um arquivo for alterado, o arquivo de manifesto do aplicativo também deve ser atualizado para refletir a alteração.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra `file` elementos em um aplicativo de manifesto para um aplicativo implantado usando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
```  
<file name="Icon.ico" size="9216">  
  <hash>  
    <dsig:Transforms>  
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
    </dsig:Transforms>  
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
    <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>  
  </hash>  
</file>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)



