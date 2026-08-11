# WebAppsSkills (SAP B1 & BEAS Manufacturing)

Este repositório contém as **Skills de Inteligência Artificial** personalizadas para orientar o desenvolvimento e padronização de aplicações web (WebApps) voltadas para o ecossistema do **SAP Business One** e do **BEAS Manufacturing**.

## 🧠 Skills Disponíveis

Ao integrar este repositório ao seu assistente (Agent), ele aprenderá automaticamente as seguintes regras de negócios e arquitetura:

### 1. App Design System (`app-design-system`)
Garante que todas as interfaces gráficas criadas mantenham um rigoroso padrão corporativo SAP.
- **Ecossistema:** Uso exclusivo do React com a biblioteca `@ui5/webcomponents-react`.
- **Tema:** Exigência do tema SAP Horizon em Light Mode (bloqueio total de dark mode).
- **Usabilidade de Fábrica:** Componentes adaptados para telas touch e chão de fábrica.
- **Gotchas Fiori:** Correções e direcionamentos sobre componentes ausentes (ex: uso do `DynamicPageHeader` ao invés de `ObjectPageHeader`).

### 2. SAP & BEAS Functional (`sap-beas-functional`)
Dita as regras rígidas de arquitetura necessárias para que a aplicação rode nativamente e sem falhas dentro dos portais web do BEAS.
- **Sem HTML:** Arquitetura *headless* onde tudo inicia por um único arquivo `app.js`.
- **Vanilla/Nativo (Sem Build):** O ambiente BEAS roda módulos ES6 nativos, não devendo usar compiladores modernos como Vite, nem sintaxe JSX. Todo o código React deve ser escrito através do `React.createElement`.
- **Carregamento Dinâmico:** Proíbe importações diretas de CSS (`import './styles.css'`), orientando a injeção via manipulação dinâmica do DOM.
- **Testes Locais:** Instruções avançadas sobre como testar as aplicações puras localmente emulando o ambiente via `importmap` de CDNs.

## 🚀 Como Utilizar
Basta colocar o diretório `.agent/skills/` deste repositório na raiz do seu projeto de desenvolvimento. O seu assistente irá automaticamente rastrear e aplicar essas restrições contextuais sempre que você pedir a construção de novos componentes e lógicas pro BEAS.
