---
title: Visão geral das soluções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 97070a3c47f5e102ce974e0d7eeeea0380beff57
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921230"
---
# <a name="solutions-overview"></a>Visão geral das soluções
Uma solução é um agrupamento de um ou mais projetos que trabalham juntos para criar um aplicativo. As projeto e informações de status que pertencem à solução são armazenados em dois arquivos de solução diferente. O arquivo de solução (. sln) é baseado em texto e pode ser colocado sob controle do código-fonte e compartilhado entre usuários. O arquivo de opção (. suo) de usuário da solução é binário. Como resultado, o arquivo. suo não pode ser colocado sob controle do código-fonte e contém informações específicas do usuário.  
  
 Qualquer VSPackage pode gravar em um dos tipos de arquivo de solução. Devido à natureza dos arquivos, há duas interfaces diferentes implementados para gravar a eles. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> interface grava informações de texto para o arquivo e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> interface grava fluxos binários no arquivo. suo.  
  
> [!NOTE]
>  Um projeto não precisa gravar explicitamente uma entrada para si mesmo no arquivo de solução; o ambiente cuida disso para o projeto. Portanto, a menos que você deseja adicionar o conteúdo adicional especificamente para o arquivo de solução, não é necessário registrar o VSPackage dessa maneira.  
  
 Cada VSPackage que dão suporte a persistência de solução usa três interfaces, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> interface, que é implementada pelo ambiente e chamado pelo VSPackage, e `IVsPersistSolutionProps` e `IVsPersistSolutionOpts`, que são implementados pelo VSPackage. O `IVsPersistSolutionOpts` interface só precisa ser implementado se informações particulares deve ser gravada pelo VSPackage para o arquivo. suo.  
  
 Quando uma solução é aberta, o seguinte processo ocorre.  
  
1. O ambiente lê a solução.  
  
2. Se o ambiente de encontrar um `CLSID`, ele carrega o VSPackage correspondente.  
  
3. Se um VSPackage é carregado, as chamadas de ambiente `QueryInterface` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> interface para a interface que requer o VSPackage.  
  
   1.  Ao ler de um arquivo. sln, o ambiente chama `QueryInterface` para `IVsPersistSolutionProps`.  
  
   2.  Ao ler de um arquivo. suo, o ambiente chama `QueryInterface` para `IVsPersistSolutionOpts`.  
  
   Informações específicas relacionadas ao uso desses arquivos podem ser encontradas no [solução (. Arquivo DPD)](../../extensibility/internals/solution-dot-sln-file.md) e [opções de usuário da solução (. Arquivo suo)](../../extensibility/internals/solution-user-options-dot-suo-file.md).  
  
> [!NOTE]
>  Se você quiser criar uma nova configuração de solução consiste em configurações de dois projetos e exclusão de um terço da compilação, você precisa usar a automação ou páginas de propriedade de interface do usuário. Você não pode alterar as configurações de Gerenciador de build da solução e suas propriedades diretamente, mas você pode manipular o Gerenciador de build da solução usando o `SolutionBuild` classe do DTE no modelo de automação. Para obter mais informações sobre a configuração de soluções, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>