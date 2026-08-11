# WebAppsSkills (SAP B1 & BEAS Manufacturing)

Este repositório contém as **Skills de Inteligência Artificial** personalizadas para orientar o desenvolvimento e padronização de aplicações web (WebApps) voltadas para o ecossistema do **SAP Business One** e do **BEAS Manufacturing**.

## 🧠 Skills Disponíveis

Ao integrar este repositório ao seu assistente (Agent), ele aprenderá automaticamente as seguintes regras de negócios e arquitetura:

### 1. App Design System (`app-design-system`)
Garante que todas as interfaces gráficas criadas mantenham um rigoroso padrão corporativo SAP (estilo Fiori Object Page) perfeitamente integrado ao visual nativo do BEAS.
- **Ecossistema:** Uso exclusivo do **SAPUI5 Clássico** (OpenUI5) através do namespace global `sap`. Sem React.
- **Tema:** Exigência do tema SAP Horizon ou Belize em Light Mode (bloqueio total de dark mode).
- **Layout Fiori (Object Page):** Obrigatoriedade do uso de `sap.ui.layout.form.SimpleForm` para cabeçalhos e formulários e `sap.m.IconTabBar` para navegação em seções. 
- **Integração com BEAS (Sem Navbar):** Proibido criar barras superiores de navegação (`ShellBar` ou `ToolHeader`), pois o Portal BEAS já fornece o menu. As páginas devem ter `showHeader: false`.
- **Densidade:** Utilização da classe `sapUiSizeCompact` para exibição densa de dados, assim como é nativamente no portal.

### 2. SAP & BEAS Functional (`sap-beas-functional`)
Dita as regras rígidas de arquitetura necessárias para que a aplicação rode nativamente e sem falhas dentro dos portais web do BEAS.
- **Estrutura Obrigatória:** SEMPRE criar o arquivo `index.html` injetando o script de bootstrap do SAPUI5 e chamando o `<script type="module" src="app.js"></script>`.
- **Vanilla/Nativo (Sem Build):** O ambiente BEAS roda a aplicação de forma nativa sem compiladores modernos (Vite/Webpack). Tudo é orquestrado através do `app.js`.
- **Ciclo de Vida:** O `app.js` deve aguardar a inicialização do `sap.ui.getCore().attachInit(...)` antes de montar as telas no DOM.

### 3. SAP BEAS Data and State Management (`sap-beas-data-management`)
Garante a resiliência das chamadas de API, a excelência da experiência do usuário (UX Flow) e a segurança de dados.
- **Data Binding (JSONModel):** Utilização estrita dos *Models* nativos (`sap.ui.model.json.JSONModel`).
- **Navegação Inteligente (UX):** Buscas acionadas diretamente pelo evento `submit` dos inputs. Após o carregamento, a aplicação deve trocar de aba automaticamente (`setSelectedKey`) para poupar cliques.
- **Tratamento de Erros e Loading:** Exibição de `BusyIndicator` durante requisições e `sap.m.MessageBox` obrigatório para tratamento de falhas (Proibido falha silenciosa).
- **Segurança (Mocks Genéricos):** É PROIBIDO o uso de dados reais de clientes na construção de Mock Datas. Os dados devem ser obrigatoriamente fictícios (ex: "Produto Genérico", "OP-9999").

## 🚀 Como Utilizar
Basta colocar o diretório `.agent/skills/` deste repositório na raiz do seu projeto de desenvolvimento. O seu assistente irá automaticamente rastrear e aplicar essas restrições contextuais sempre que você pedir a construção de novos componentes e lógicas pro BEAS.
