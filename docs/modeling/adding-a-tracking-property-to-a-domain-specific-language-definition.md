---
title: Adicionando uma propriedade de acompanhamento a uma definição de linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.openlocfilehash: 21899be482e47152e8ca60d78535f49613f52ede
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53946036"
---
# <a name="add-a-tracking-property-to-a-domain-specific-language-definition"></a>Adicionar uma propriedade de controle a uma definição de Linguagem Específica de Domínio

Este passo a passo mostra como adicionar uma propriedade de controle a um modelo de domínio.

Um *acompanhamento domínio* é uma propriedade que pode ser atualizada pelo usuário, mas que tem um valor padrão que é calculado usando os valores de outras propriedades de domínio ou elementos.

Por exemplo, nas ferramentas de linguagem específica do domínio (ferramentas DSL), o nome de exibição, a propriedade de uma classe de domínio tem um valor padrão que é calculado usando o nome da classe de domínio, mas um usuário pode alterar o valor em tempo de design ou redefini-lo para o valor calculado.

Este passo a passo, você criará uma linguagem específica de domínio (DSL) que tem uma propriedade que tem um valor padrão com base na propriedade de Namespace padrão do modelo de controle de Namespace. Para obter mais informações sobre propriedades de acompanhamento, consulte [definindo propriedades de controle](https://msdn.microsoft.com/0538b0e4-6221-4e7d-911a-b92cd622f0be).

- O suporte de ferramentas DSL descritores de propriedade de controle. No entanto, o designer DSL não pode ser usado para adicionar uma propriedade de acompanhamento para um idioma. Portanto, você deve adicionar código personalizado para definir e implementar a propriedade de controle.

  Uma propriedade de controle tem dois estados: acompanhar e atualizada pelo usuário. Propriedades de controle têm os seguintes recursos:

- Quando estiver no estado de controle, o valor da propriedade de acompanhamento é calculado e o valor é atualizado como outras propriedades na alteração do modelo.

- Quando estiver sendo atualizado pelo estado do usuário, o valor da propriedade de acompanhamento retém o valor para o qual o usuário definido pela última vez a propriedade.

- No **propriedades** janela, o **redefinir** de comando para a propriedade de controle é habilitada apenas quando a propriedade está no atualizada pelo estado do usuário. O **redefinir** comando define a propriedade de controle de estado do controle.

- No **propriedades** janela, quando a propriedade de controle está no estado de controle, seu valor é exibida em uma fonte normal.

- No **propriedades** janela, quando a propriedade de controle está no atualizada por estado de usuário, seu valor é exibido em uma fonte em negrito.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este passo a passo, você deve primeiro instalar esses componentes:


| | |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkID=185579](http://go.microsoft.com/fwlink/?LinkID=185579) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185580](http://go.microsoft.com/fwlink/?LinkID=185580) |
| [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185581](http://go.microsoft.com/fwlink/?LinkID=185581) |

## <a name="create-the-project"></a>Criar o projeto

1.  Crie um projeto do Designer de linguagem específica do domínio. Nomeie-o como `TrackingPropertyDSL`.

2.  No **Assistente de Designer de linguagem específica do domínio**, defina as seguintes opções:

    1.  Selecione o **MinimalLanguage** modelo.

    2.  Use o nome padrão para a linguagem específica de domínio, `TrackingPropertyDSL`.

    3.  Definir a extensão para arquivos de modelo a `trackingPropertyDsl`.

    4.  Use o ícone de modelo padrão para os arquivos de modelo.

    5.  Defina o nome do produto para `Product Name`.

    6.  Defina o nome da empresa para `Company Name`.

    7.  Use o valor padrão para o namespace raiz para projetos na solução, `CompanyName.ProductName.TrackingPropertyDSL`.

    8.  Permitir que o assistente criar um arquivo de chave de nome forte dos assemblies.

    9. Examine os detalhes da solução e, em seguida, clique em **concluir** para criar o projeto de definição de DSL.

## <a name="customize-the-default-dsl-definition"></a>Personalizar a definição de DSL padrão
 Nesta seção, você deve personalizar a definição de DSL para conter os seguintes itens:

-   Um Namespace de propriedade para cada elemento do modelo de controle.

-   Uma propriedade Boolean IsNamespaceTracking para cada elemento do modelo. Essa propriedade indicará se a propriedade de controle está no estado de controle ou em atualizada pelo estado do usuário.

-   Uma propriedade de Namespace padrão para o modelo. Essa propriedade será usada para calcular o valor padrão da propriedade de controle de Namespace.

-   Uma propriedade CustomElements calculado para o modelo. Essa propriedade indicará a proporção de elementos que têm um namespace personalizado.

### <a name="to-add-the-domain-properties"></a>Para adicionar as propriedades do domínio

1.  No designer de DSL, clique com botão direito do **ExampleModel** classe de domínio, aponte para **Add**e, em seguida, clique em **DomainProperty**.

    1.  Nomeie a nova propriedade `DefaultNamespace`.

    2.  No **propriedades** janela para a nova propriedade, defina **valor padrão** para `DefaultNamespace`e defina **tipo** para **cadeia de caracteres**.

2.  Para o **ExampleModel** domínio, adicione uma propriedade de domínio chamada `CustomElements`.

     No **propriedades** janela para a nova propriedade, defina **tipo** para **Calculated**.

3.  Para o **ExampleElement** domínio, adicione uma propriedade de domínio chamada `Namespace`.

     No **propriedades** janela para a nova propriedade, defina **é navegável** para **falso**e defina **tipo** para **CustomStorage** .

4.  Para o **ExampleElement** domínio, adicione uma propriedade de domínio chamada `IsNamespaceTracking`.

     No **propriedades** janela para a nova propriedade, defina **é navegável** para **falso**, defina **valor padrão** para `true`e defina **Tipo** à **booliano**.

### <a name="to-update-the-diagram-elements-and-dsl-details"></a>Para atualizar os elementos de diagrama e os detalhes de DSL

1.  No designer de DSL, clique com botão direito do **ExampleShape** forma geométrica, aponte para **Add**e, em seguida, clique em **decorador de texto**.

    1.  Nomeie o novo decorador de texto `NamespaceDecorator`.

    2.  No **propriedades** janela para o decorador de texto, defina **posição** para **InnerBottomLeft**.

2.  No designer de DSL, selecione a linha que conecta-se a **ExampleElement** de classe para o **ExampleShape** forma.

    1.  No **detalhes de DSL** janela, selecione a **mapas do decorador** guia.

    2.  No **decoradores** lista, selecione **NamespaceDecorator**, marque a caixa de seleção e, em seguida, no **Exibir propriedade** lista, selecione **Namespace**.

3.  Na **Gerenciador de DSL**, expanda o **Classes de domínio** pasta, clique com botão direito a **ExampleElement** nó e, em seguida, clique **adicionar novo domínio descritor de tipo**.

    1.  Expanda o **ExampleElement** nó e selecione o **descritor de tipo personalizado (descritor de tipo de domínio)** nó.

    2.  No **propriedades** janela para o descritor de tipo de domínio, defina **personalizado codificado** para **verdadeiro**.

4.  Na **Gerenciador de DSL**, selecione o **comportamento da serialização Xml** nó.

    1.  No **propriedades** janela, defina **personalizado pós-carregamento** para **verdadeiro**.

## <a name="transform-templates"></a>Transformar modelos

Agora que você definiu as propriedades e classes de domínio para sua DSL, você pode verificar a definição de DSL pode ser transformada corretamente para gerar novamente o código para seu projeto.

1.  Sobre o **Gerenciador de soluções** barra de ferramentas, clique em **transformar todos os modelos**.

2.  O sistema gera novamente o código para a solução e salva Dsldefinition. Para obter informações sobre o formato XML de arquivos de definição, consulte [o arquivo Dsldefinition DSL](../modeling/the-dsldefinition-dsl-file.md).

## <a name="create-files-for-custom-code"></a>Criar arquivos de código personalizado

Quando você transformar todos os modelos, o sistema gera o código-fonte que define sua linguagem específica do domínio nos projetos Dsl e DslPackage. Para que você pode evitar interferência com o texto gerado, escreva seu código personalizado em arquivos que são distintos de arquivos de código gerados.

Você deve fornecer o código para manter o valor e o estado de sua propriedade de acompanhamento. Para ajudar você a diferenciar o seu código personalizado do código gerado e para evitar conflitos de nomenclatura de arquivo, coloque seus arquivos de código personalizado em uma subpasta separada.

1.  Na **Gerenciador de soluções**, com o botão direito do **DSL** do projeto, aponte para **Add**e, em seguida, clique em **nova pasta**. Nomeie a nova pasta `CustomCode`.

2.  Clique com botão direito a nova **CustomCode** pasta, aponte para **Add**e, em seguida, clique em **Novo Item**.

3.  Selecione o **arquivo de código** modelo, defina as **nome** para `NamespaceTrackingProperty.cs`e, em seguida, clique em **Okey**.

     O arquivo NamespaceTrackingProperty.cs é criado e aberto para edição.

4.  Na pasta, crie os arquivos de código a seguir: `ExampleModel.cs,``HelperClasses.cs`, `Serialization.cs`, e `TypeDescriptor.cs`.

5.  No **DslPackage** do projeto, crie também um `CustomCode` pasta e adicionar a ele um `Package.cs` arquivo de código.

## <a name="add-helper-classes-to-support-tracking-properties"></a>Adicionar Classes auxiliares para dar suporte a propriedades de acompanhamento

Para o arquivo HelperClasses.cs, adicione a `TrackingHelper` e `CriticalException` classes da seguinte maneira. Você fará referência a essas classes mais tarde neste passo a passo.

1.  Adicione o seguinte código ao arquivo HelperClasses.cs.

    ```csharp
    using System;
    using System.Collections;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        internal static class TrackingHelper
        {
            /// <summary>Notify each model element in a collection that a tracked
            /// property has changed.</summary>
            /// <param name="store">The store for the model.</param>
            /// <param name="collection">The collection of model elements that
            /// contain the tracking property.</param>
            /// <param name="propertyId">The ID of the tracking property.</param>
            /// <param name="trackingPropertyId">The ID of the property that
            /// indicates whether the tracking property is tracking.</param>
            internal static void UpdateTrackingCollectionProperty(
                Store store,
                IEnumerable collection,
                Guid propertyId,
                Guid trackingPropertyId)
            {
                DomainPropertyInfo propInfo =
                    store.DomainDataDirectory.GetDomainProperty(propertyId);

                DomainPropertyInfo trackingPropInfo =
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);

                Debug.Assert(propInfo != null);
                Debug.Assert(trackingPropInfo != null);
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),
                    "Tracking property not specified as a boolean");

                foreach (ModelElement element in collection)
                {
                    // If the tracking property is currently tracking, then notify
                    // it that the tracked property has changed.
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);
                    if (isTracking)
                    {
                        propInfo.NotifyValueChange(element);
                    }
                }
            }
        }

        /// <summary>Helper class to flag critical exceptions from ones that are
        /// safe to ignore.</summary>
        internal static class CriticalException
        {
            /// <summary>Gets whether an exception is critical and can not be
            /// ignored.</summary>
            /// <param name="ex">The exception to check.</param>
            /// <returns>True if the exception is critical.</returns>
            internal static bool IsCriticalException(Exception ex)
            {
                if (ex is NullReferenceException
                    || ex is StackOverflowException
                    || ex is OutOfMemoryException
                    || ex is System.Threading.ThreadAbortException)
                    return true;

                if (ex.InnerException != null)
                    return IsCriticalException(ex.InnerException);

                return false;
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-custom-type-descriptor"></a>Adicionar código personalizado para o descritor de tipo personalizado

Implemente a `GetCustomProperties` método para o descritor de tipo para o `ExampleModel` classe de domínio.

> [!NOTE]
> O código que as ferramentas DSL gerar para o descritor de tipo personalizado `ExampleModel` chamadas `GetCustomProperties`; no entanto, as ferramentas DSL não geram código que implementa o método.

Definir esse método cria o acompanhamento de descritor de propriedade para a propriedade de controle de Namespace. Além disso, fornecer atributos para a propriedade de controle permite que o **propriedades** janela para exibir a propriedade corretamente.

### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>Para modificar o descritor de tipo para a classe de domínio ExampleModel

1.  Adicione o seguinte código ao arquivo TypeDescriptor.cs.

    ```csharp
    using System;
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the custom type descriptor for the ExampleElement domain class, add
        // the GetCustomProperties method.
        public partial class ExampleElementTypeDescriptor
        {
            /// <summary>Returns the property descriptors for the described
            /// ExampleElement domain class.</summary>
            /// <remarks>This method adds the tracking property descriptor.
            /// </remarks>
            private PropertyDescriptorCollection GetCustomProperties(
                Attribute[] attributes)
            {
                // Get the default property descriptors from the base class
                PropertyDescriptorCollection propertyDescriptors =
                    base.GetProperties(attributes);

                // Get a reference to the model element that is being described.
                ExampleElement source = this.ModelElement as ExampleElement;

                //Add the descriptor for the tracking property.
                if (source != null)
                {
                    DomainPropertyInfo domainProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.NamespaceDomainPropertyId);

                    DomainPropertyInfo trackingProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);

                    // Define attributes for the tracking property so that the
                    // Properties window displays the property correctly.
                    Attribute[] attr = new Attribute[] {
                        new DisplayNameAttribute("Element Namespace"),
                        new DescriptionAttribute("The namespace of the element."),
                        new CategoryAttribute("Tracking Properties"),
                    };

                    propertyDescriptors.Add(new TrackingPropertyDescriptor(
                        source, domainProperty, trackingProperty, attr));
                }

                // Return the property descriptors for this element
                return propertyDescriptors;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-package"></a>Adição de código personalizado para o pacote

O código gerado define um provedor de descrição de tipo para a classe de domínio ExampleElement; No entanto, você deve adicionar código para instruir a DSL para usar esse provedor de descrição de tipo.

1.  Adicione o seguinte código ao arquivo Package.cs.

    ```csharp
    using System.ComponentModel;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // Override the default Initialize method.
        internal sealed partial class TrackingPropertyDSLPackage
        {
            protected override void Initialize()
            {
                // Add the custom type descriptor for the ExampleElement type.
                TypeDescriptor.AddProvider(
                    new ExampleElementTypeDescriptionProvider(),
                    typeof(ExampleElement));

                base.Initialize();
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-model"></a>Adicionar código personalizado para o modelo

Implemente a `GetCustomElementsValue` método para o `ExampleModel` classe de domínio.

> [!NOTE]
> O código que as ferramentas DSL gerar para `ExampleModel` chamadas `GetCustomElementsValue`; no entanto, as ferramentas DSL não geram código que implementa o método.

Definindo o `GetCustomElementsValue` método fornece a lógica para a propriedade CustomElements calculado do `ExampleModel`. Esse método conta o número de `ExampleElement` classes de domínio que têm uma propriedade que tem um valor de usuário atualizado e retorna uma cadeia de caracteres que representa essa contagem como uma proporção do total elementos no modelo de controle de Namespace.

Além disso, adicione uma `OnDefaultNamespaceChanged` método a ser `ExampleModel`e substituir o `OnValueChanged` método da `DefaultNamespacePropertyHandler` aninhados de classe de `ExampleModel` chamar `OnDefaultNamespaceChanged`.

Porque a propriedade DefaultNamespace é usada para calcular o Namespace de propriedade, de controle `ExampleModel` deve notificar todos `ExampleElement` classes de domínio que o valor de DefaultNamespace foi alterado.

### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>Para modificar o manipulador de propriedades para a propriedade de acompanhamento

1.  Adicione o seguinte código ao arquivo ExampleModel.cs.

    ```csharp
    using System.Linq;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        public partial class ExampleModel
        {
            public string GetCustomElementsValue()
            {
                if (this.Elements.Count == 0) return "0/0";

                int number = this.Elements.Count(e => !e.IsNamespaceTracking);
                return string.Format("{0}/{1}", number, this.Elements.Count);
            }

            #region Value changed handler for the tracked property

            // When a tracked property changes, it needs to notify all of the properties
            // that track it.

            /// <summary>Called by the DefaultNamespace property value handler when the
            /// DefaultNamespace property changes.</summary>
            /// <param name="oldValue">The previous value of the property.</param>
            /// <param name="newValue">The new value of the property.</param>
            protected virtual void OnDefaultNamespaceChanged(
                string oldValue, string newValue)
            {
                // Use the helper class to notify all of the elements in the model
                // that the default namespace has changed.
                TrackingHelper.UpdateTrackingCollectionProperty(
                    this.Store,
                    this.Elements,
                    ExampleElement.NamespaceDomainPropertyId,
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);
            }

            // Update the change handler for the DefaultNamespace property.
            internal sealed partial class DefaultNamespacePropertyHandler
            {
                /// <summary>Called when the DefaultNamespace property changes.</summary>
                /// <param name="element">The model element that has the property that
                /// changed.</param>
                /// <param name="oldValue">The previous value of the property.</param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleModel element, string oldValue, string newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);

                    if (!element.Store.InUndoRedoOrRollback)
                    {
                        element.OnDefaultNamespaceChanged(oldValue, newValue);
                    }
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-for-the-tracking-property"></a>Adicionar código personalizado para a propriedade de controle

Adicionar um `CalculateNamespace` método para o `ExampleElement` classe de domínio.

Definir esse método fornece a lógica para a propriedade CustomElements calculado do `ExampleModel`. Esse método conta o número de `ExampleElement` classes de domínio que têm um Namespace de acompanhamento de propriedade que está no atualizada pelo estado do usuário e retorna uma cadeia de caracteres que representa essa contagem como uma proporção do total elementos no modelo.

Além disso, adicione métodos para obter e definir a propriedade de armazenamento personalizado de Namespace do e armazenamento para o `ExampleElement` classe de domínio.

> [!NOTE]
> O código que as ferramentas DSL gerar para `ExampleModel` chamadas get e defina métodos; no entanto, as ferramentas DSL não geram código que implementa os métodos.

### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>Para adicionar o método para o descritor de tipo personalizado

1.  Adicione o seguinte código ao arquivo NamespaceTrackingProperty.cs.

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the domain class that has the tracking property, add the caluclation
        // for when the property is tracking.
        public partial class ExampleElement
        {
            /// <summary>Calculates the actual value of the property when it is
            /// tracking.</summary>
            /// <returns>The value of the tracking property when it is
            /// tracking.</returns>
            /// <remarks>Making this method virtual allows child classes to modify
            /// the calculation. This method does not need to perform validation, as
            /// its caller handles validation prior to calling this method.
            /// <para>In this case, the tracking value depends on the default namespace
            /// property of the parent model.</para></remarks>
            protected virtual string CalculateNamespace()
            {
                return this.ExampleModel.DefaultNamespace;
            }

            #region Tracking property implementation

            // Implement the Namespace domain property of the ExampleElement domain class,
            // and update the IsNamespaceTracking domain property value handler.

            /// <summary>Storage for the Namespace property.</summary>
            private string namespaceStorage;

            /// <summary>Gets the value of the Namespace property.</summary>
            /// <returns>The value of the Namespace property.</returns>
            private string GetNamespaceValue()
            {
                // Only retrieve the tracked value if the store is not in the
                // middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!loading && this.IsNamespaceTracking)
                {
                    try
                    {
                        return this.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                        return default(string);
                    }
                    catch (Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                        else
                        {
                            return default(string);
                        }
                    }
                }

                return namespaceStorage;
            }

            /// <summary>Sets the value of the Namespace property.</summary>
            /// <param name="value">The new value for the property.</param>
            private void SetNamespaceValue(string value)
            {
                namespaceStorage = value;

                // Only update the state of the tracking property if the store is
                // not in the middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!this.Store.InUndoRedoOrRollback && !loading)
                {
                    this.IsNamespaceTracking = false;
                }
            }

            // Update the default behavior of the ExampleElement.IsNamespaceTracking
            // domain property value handler.
            internal sealed partial class IsNamespaceTrackingPropertyHandler
            {
                /// <summary>Called after the IsNamespaceTracking property changes.
                /// </summary>
                /// <param name="element">The model element that has the property
                /// that changed.</param>
                /// <param name="oldValue">The previous value of the property.
                /// </param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleElement element, Boolean oldValue, Boolean newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);
                    if (!element.Store.InUndoRedoOrRollback && newValue)
                    {
                        DomainPropertyInfo propInfo =
                            element.Store.DomainDataDirectory.GetDomainProperty(
                                ExampleElement.NamespaceDomainPropertyId);
                        propInfo.NotifyValueChange(element);
                    }
                }

                /// <summary>Performs the reset operation for the IsNamespaceTracking
                /// property for a model element.</summary>
                /// <param name="element">The model element that has the property
                /// to reset.</param>
                internal void ResetValue(ExampleElement element)
                {
                    object calculatedValue = null;

                    try
                    {
                        calculatedValue = element.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                    }
                    catch (System.Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                    }

                    if ((calculatedValue != null
                        && object.Equals(element.Namespace, calculatedValue)))
                    {
                        element.isNamespaceTrackingPropertyStorage = true;
                    }
                }

                /// <summary>Method to set IsNamespaceTracking to false so that this
                /// instance of this tracking property is not storage-based.
                /// </summary>
                /// <param name="element">The element on which to reset the property
                /// value.</param>
                internal void PreResetValue(ExampleElement element)
                {
                    // Force the IsNamespaceTracking property to false so that the value
                    // of the Namespace property is retrieved from storage.
                    element.isNamespaceTrackingPropertyStorage = false;
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-to-support-serialization"></a>Adicionar código personalizado para oferecer suporte à serialização

Adicione código para dar suporte o comportamento de pós-carga personalizado para serialização de XML.

> [!NOTE]
> O código que as ferramentas DSL gerar chamadas a `OnPostLoadModel` e `OnPostLoadModelAndDiagram` métodos; no entanto, as ferramentas DSL não geram código que implementa esses métodos.

### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>Para adicionar código para dar suporte o comportamento de pós-carregamento de personalizado

1.  Adicione o seguinte código ao arquivo Serialization.cs.

    ```csharp
    using System;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        #region Helper classes for maintaining state while the store is serializing.

        public abstract partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Reset the tracking state properties to their natural values
            /// based on comparing storage with calculation.</summary>
            /// <param name="store">The store that contains this model.</param>
            internal static void ResetTrackingProperties(Store store)
            {
                // Two passes required - one to set all elements to storage-based
                // then another to set some back to being tracking.
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.PreResetIsTrackingProperties();
                        continue;
                    }
                }
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.ResetIsTrackingProperties();
                        continue;
                    }
                }
            }
        }

        // Add the pre-reset and reset methods for the model element.
        public partial class ExampleElement
        {
            /// <summary>Calls the pre-reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void PreResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);
            }

            /// <summary>Calls the reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void ResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);
            }
        }

        #endregion

        #region Custom serialization code

        // To the serialization helper for the TrackingPropertyDSL class, add post
        // load handlers to bind the tracking property to the serialization process.
        // These handlers manage the tracking states and property values when the
        // model is serialized and deserialized.
        public partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Customize model loading.</summary>
            /// <param name="serializationResult">The serialization result from the
            /// load operation.</param>
            /// <param name="partition">The partition in which the new
            /// instance was created.</param>
            /// <param name="fileName">The name of the file from which the
            /// instance was deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.
            /// </param>
            private void OnPostLoadModel(
                SerializationResult serializationResult,
                Partition partition,
                string fileName,
                ExampleModel modelRoot)
            {
            }

            /// <summary>Customize model and diagram loading.</summary>
            /// <param name="serializationResult">Stores serialization result from
            /// the load operation.</param>
            /// <param name="modelPartition">Partition in which the new
            /// instance will be created.</param>
            /// <param name="modelFileName">Name of the file from which the
            /// instance will be deserialized.</param>
            /// <param name="diagramPartition">Partition in which the new
            /// diagram instance will be created.</param>
            /// <param name="diagramFileName">Name of the file from which the
            /// diagram instance will be deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.</param>
            /// <param name="diagram">The diagram matching the modelRoot.</param>
            private void OnPostLoadModelAndDiagram(
                SerializationResult serializationResult,
                Partition modelPartition,
                string modelFileName,
                Partition diagramPartition,
                string diagramFileName,
                ExampleModel modelRoot,
                TrackingPropertyDSLDiagram diagram)
            {
                Debug.Assert(modelPartition != null);
                Debug.Assert(modelPartition.Store != null);

                // Tracking properties need to be set up according to whether the
                // serialization matches the calculated values.
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(
                    modelPartition.Store);
            }
        }

        #endregion
    }
    ```

## <a name="test-the-language"></a>O idioma de teste

A próxima etapa é criar e executar o designer DSL em uma nova instância de [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] para que você possa verificar se a propriedade de controle está funcionando corretamente.

1. No menu **Compilar**, clique em **Recompilar Solução**.

2. No menu **Depuração**, clique em **Iniciar Depuração**.

    O build experimental do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] abre o **depuração** solução, que contém um arquivo de teste vazio.

3. Na **Gerenciador de soluções**, duas vezes no arquivo Test.trackingPropertyDsl para abri-lo no designer e, em seguida, clique na superfície de design.

    Observe que, nos **propriedades** janela para o diagrama, o **Namespace padrão** é de propriedade **DefaultNamespace**e o **elementos personalizados** é de propriedade **0/0**.

4. Arraste uma **ExampleElement** elemento o **caixa de ferramentas** à superfície do diagrama.

5. No **propriedades** janela para o elemento, selecione a **Namespace do elemento** propriedade e altere o valor de **DefaultNamespace** para  **OtherNamespace**.

    Observe que o valor de **Namespace do elemento** agora é mostrado em negrito.

6. No **propriedades** janela, clique com botão direito **Namespace do elemento**e, em seguida, clique em **redefinir**.

    O valor da propriedade é alterado para **DefaultNamespace**, e o valor é mostrado em uma fonte normal.

    Clique com botão direito **Namespace do elemento** novamente. O **redefinir** comando agora está desabilitado porque a propriedade está atualmente em seu estado de acompanhamento.

7. Arraste outro **ExampleElement** da **caixa de ferramentas** para a superfície do diagrama e altere seu **Namespace do elemento** para **OtherNamespace**.

8. Clique na superfície de design.

    No **propriedades** janela para o diagrama, o valor de **elementos personalizados** agora está **1/2**.

9. Alteração **Namespace padrão** para o diagrama de **DefaultNamespace** para **NewNamespace**.

     O **Namespace** faixas primeiro elemento a **Namespace padrão** propriedade, enquanto o **Namespace** do segundo elemento retém seu valor usuário atualizou  **OtherNamespace**.

10. Salve a solução e, em seguida, feche o build experimental.

## <a name="next-steps"></a>Próximas etapas

Se você planeja usar o acompanhamento mais de uma propriedade, ou implementar propriedades de controle em mais de uma DSL, você pode criar um modelo de texto para gerar o código comum para dar suporte a cada propriedade de controle. Para obter mais informações sobre modelos de texto, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor>
- <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>
- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Como: Criar uma solução de linguagem específica do domínio](../modeling/how-to-create-a-domain-specific-language-solution.md)
