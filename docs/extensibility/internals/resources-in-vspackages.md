---
title: Recursos em VSPackages | Microsoft Docs
description: Saiba quais tipos de recursos localizados podem ser inseridos no VSPackages. Você também pode inserir recursos em DLLs nativas de interface do usuário satélite ou em DLLs satélite gerenciadas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c4863fb40bc6f70556d8f00305d882e6edd93a0e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074386"
---
# <a name="resources-in-vspackages"></a>Recursos em VSPackages
Você pode inserir recursos localizados em DLLs de interface do usuário satélite nativas, DLLs satélite gerenciadas ou em um VSPackage gerenciado.

 Alguns recursos não podem ser inseridos em VSPackages. Os seguintes tipos gerenciados podem ser inseridos:

- Cadeias de caracteres

- Chaves de carregamento de pacote (que também são cadeias de caracteres)

- Ícones da janela de ferramentas

- Arquivos de saída de tabela de comando compilado (CTO)

- Bitmaps do CTO

- Ajuda da linha de comando

- Sobre os dados da caixa de diálogo

  Os recursos em um pacote gerenciado são selecionados pela ID do recurso. Uma exceção é o arquivo CTO, que deve ser nomeado CTMENU. O arquivo CTO deve aparecer na tabela de recursos como um `byte[]` . Todos os outros itens de recurso são identificados por tipo.

  Você pode usar o <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> atributo para indicar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] que os recursos gerenciados estão disponíveis.

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>A configuração dessa maneira indica que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] deve ignorar DLLs satélite não gerenciadas ao procurar por recursos, por exemplo, usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> . Se o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] encontrar dois ou mais recursos que tenham a mesma ID de recurso, ele usará o primeiro recurso que encontrar.

## <a name="example"></a>Exemplo
 O exemplo a seguir é uma representação gerenciada de um ícone de janela de ferramenta.

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 O exemplo a seguir demonstra como inserir a matriz de bytes CTO, que deve ser nomeada CTMENU.

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>Notas da implementação
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] atrasa o carregamento de VSPackages sempre que possível. Uma conseqüência de inserir um arquivo CTO em um VSPackage é que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o deve carregar todos esses VSPackages na memória durante a instalação, que é quando ele cria uma tabela de comando mesclada. Os recursos podem ser extraídos de um VSPackage examinando os metadados sem executar código no VSPackage. O VSPackage não é inicializado no momento, portanto, a perda de desempenho é mínima.

 Quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o solicita um recurso de um VSPackage após a instalação, esse pacote provavelmente já estará carregado e inicializado, portanto, a perda de desempenho será mínima.

## <a name="see-also"></a>Confira também
- [Gerenciar VSPackages](../../extensibility/managing-vspackages.md)
- [Recursos localizados em aplicativos do MFC: DLLs satélite](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
