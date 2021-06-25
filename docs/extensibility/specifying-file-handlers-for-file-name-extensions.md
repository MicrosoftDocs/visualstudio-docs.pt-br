---
title: Especificando manipuladores de arquivos para extensões de nome de arquivo | Microsoft Docs
description: Saiba como determinar qual aplicativo lida com uma extensão de arquivo no SDK Visual Studio usando OpenWithList e OpenWithProgids.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ab370b4be8c12ad0df0c4822bcc7b487fb4aa21
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899440"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>Especificando identificadores de arquivo para extensões de nome de arquivo
Há várias maneiras de determinar o aplicativo que trata um arquivo que tem uma extensão de arquivo específica. Os verbos OpenWithList e OpenWithProgids são duas maneiras de especificar manipuladores de arquivos na entrada do Registro para a extensão de arquivo.

## <a name="openwithlist-verb"></a>Verbo OpenWithList
 Ao clicar com o botão direito do mouse em um arquivo Windows Explorer, você verá o **comando** Abrir. Se mais de um produto estiver associado a uma extensão, você verá um submenu **Abrir com.**

 Você pode registrar diferentes aplicativos para abrir uma extensão definindo a chave OpenWithList para a extensão de arquivo HKEY_CLASSES_ROOT. Os aplicativos listados sob essa chave para uma extensão de arquivo aparecem sob o título **Programas Recomendados** na caixa de diálogo Abrir **com.** O exemplo a seguir mostra os aplicativos registrados para abrir a extensão de arquivo .vcproj.

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> As chaves que especificam aplicativos estão na lista em HKEY_CLASSES_ROOT\Applications.

 Ao adicionar uma chave OpenWithList, você declara que seu aplicativo dá suporte a uma extensão de arquivo mesmo se outro aplicativo assume a propriedade da extensão. Essa pode ser uma versão futura do seu aplicativo ou de outro aplicativo.

## <a name="openwithprogids"></a>OpenWithProgIDs
 ProgIDs (identificadores programáticos) são versões amigáveis de ClassIDs que identificam uma versão de um aplicativo ou objeto COM. Cada objeto co-criavel deve ter seu próprio ProgID. Por exemplo, VisualStudio.DTE.7.1 inicia Visual Studio .NET 2003 enquanto VisualStudio.DTE.10.0 inicia [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Como o proprietário de um tipo de projeto ou tipo de item de projeto, você deve criar um ProgID específico da versão para sua extensão de arquivo. Esses ProgIDs podem ser redundantes, já que mais de um ProgID pode iniciar o mesmo aplicativo. Para obter mais informações, consulte [Registrando verbos para extensões de nome de arquivo](../extensibility/registering-verbs-for-file-name-extensions.md).

 Use a seguinte convenção de nomen por progIDs de arquivo com controle de versão para evitar a duplicação com o registro de outros fornecedores:

|Extensão de arquivo|ProgID com versão|
|--------------------|----------------------|
|.extension|Productname. extension.versionMajor.versionMinor|

 Você pode registrar diferentes aplicativos que podem abrir uma extensão de arquivo específica adicionando ProgIDs com versão como valores à chave HKEY_CLASSES_ROOT \\ *\<extension>* \OpenWithProgids. Essa chave do Registro contém uma lista de ProgIDs alternativos associados à extensão de arquivo. Os aplicativos associados aos ProgIDs listados aparecem no submenu **Abrir com**_nome do_ produto. Se o mesmo aplicativo for especificado nas chaves e , o sistema `OpenWithList` `OpenWithProgids` operacional mescla as duplicatas.

> [!NOTE]
> A `OpenWithProgids` chave só tem suporte no Windows XP. Como outros sistemas operacionais ignoram essa chave, não a use como o único registro para manipuladores de arquivos. Use essa chave para fornecer uma melhor experiência do usuário no Windows XP.

 Adicione os ProgIDs desejados como valores do tipo REG_NONE. O código a seguir fornece um exemplo de registro de ProgIDs para uma extensão de arquivo (.*ext*).

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 O ProgID especificado como o valor padrão para a extensão de arquivo é o manipulador de arquivos padrão. Se você modificar o ProgID para uma extensão de arquivo que é enviada com uma versão anterior do ou que pode ser assumida por outros aplicativos, você deve registrar a chave para sua extensão de arquivo e especificar o novo ProgID na lista juntamente com os [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ProgIDs antigos aos quais você dá `OpenWithProgids` suporte. Por exemplo:

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 Se o ProgID antigo tiver verbos associados a ele, esses verbos também aparecerão em **Abrir**  com Nome do Produto no menu de atalho.

## <a name="see-also"></a>Confira também
- [Sobre as extensões de nome de arquivo](../extensibility/about-file-name-extensions.md)
- [Registrar verbos para extensões de nome de arquivo](../extensibility/registering-verbs-for-file-name-extensions.md)
