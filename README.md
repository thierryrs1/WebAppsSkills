# WebAppsSkills (SAP B1 & BEAS Manufacturing)

Este repositório contém as **Skills de Inteligência Artificial** personalizadas para orientar o desenvolvimento e padronização de aplicações web (WebApps) voltadas para o ecossistema do **SAP Business One** e do **BEAS Manufacturing**.

## 🧠 Skills Disponíveis

Ao integrar este repositório ao seu assistente (Agent), ele aprenderá automaticamente as seguintes regras de negócios e arquitetura:

### 1. App Design System (`app-design-system`)
Garante que todas as interfaces gráficas criadas mantenham um rigoroso padrão corporativo SAP.
- **Ecossistema:** Uso exclusivo do **SAPUI5 Clássico** (OpenUI5) através do namespace global `sap`.
- **Tema:** Exigência do tema SAP Belize ou Horizon em Light Mode (bloqueio total de dark mode).
- **Usabilidade de Fábrica:** Componentes adaptados para telas touch (`sap.m`) e chão de fábrica.
- **Componentes:** Instanciação programática via JS de componentes como `sap.m.Button`, `sap.m.Table`, `sap.m.Page`.

### 2. SAP & BEAS Functional (`sap-beas-functional`)
Dita as regras rígidas de arquitetura necessárias para que a aplicação rode nativamente e sem falhas dentro dos portais web do BEAS.
- **Estrutura Obrigatória:** SEMPRE criar o arquivo `index.html` injetando o script de bootstrap do SAPUI5 e chamando o `<script type="module" src="app.js"></script>`.
- **Vanilla/Nativo (Sem Build):** O ambiente BEAS roda a aplicação de forma nativa sem compiladores modernos (Vite/Webpack) ou React. Tudo é orquestrado através do `app.js` utilizando a API global do SAPUI5.
- **Ciclo de Vida:** O `app.js` deve aguardar a inicialização do `sap.ui.getCore().attachInit(...)` antes de montar as telas no DOM.

### 3. SAP BEAS Data and State Management (`sap-beas-data-management`)
Garante a resiliência e estabilidade das chamadas de API e navegação nos dispositivos do chão de fábrica.
- **Data Binding (JSONModel):** Utilização estrita dos *Models* nativos do SAPUI5 (`sap.ui.model.json.JSONModel`) para gerenciar o estado da tela ao invés de variáveis JS comuns.
- **Tratamento de Loading:** Exibição de `BusyIndicator` ou telas de carregamento para evitar que o usuário ache que o app travou.
- **Prevenção de Falha Silenciosa:** Todo erro retornado pelo ERP deve acionar um `sap.m.MessageBox` de aviso.
- **Routing Nativo:** Navegação gerida por containers como `sap.m.App`, alternando as páginas de forma controlada pelo framework ao invés de limpar o HTML na mão.

## 🚀 Como Utilizar
Basta colocar o diretório `.agent/skills/` deste repositório na raiz do seu projeto de desenvolvimento. O seu assistente irá automaticamente rastrear e aplicar essas restrições contextuais sempre que você pedir a construção de novos componentes e lógicas pro BEAS.
