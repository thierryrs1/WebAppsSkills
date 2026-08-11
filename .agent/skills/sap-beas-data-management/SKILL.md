---
name: SAP BEAS Data and State Management
description: Detailed guidelines for managing data fetching, API error handling, loading states (progress indicators), and lightweight routing in BEAS/SAP WebApps.
---

## API Integration, State, and Routing

When dealing with SAP B1 or BEAS Manufacturing REST/OData APIs within the WebApp portal, you must strictly follow these rules to ensure stability, especially on factory floor devices.

### 1. Tratamento de Erros e Feedback de Loading (Obrigatório)
- **Prevenção de Congelamento:** Nunca permita que a interface congele sem dar feedback ao usuário durante chamadas de API.
- **Múltiplas Requisições (Progresso):** Sempre que a aplicação precisar disparar múltiplas requisições em lote (ex: salvar dezenas de amostras e medições ao mesmo tempo), é OBRIGATÓRIO implementar uma tela de carregamento (Loading Screen) que exiba a **porcentagem (%)** do processo concluído. Isso é vital para que o operador saiba que o sistema não travou.
- **Requisições Simples:** Para consultas únicas rápidas, utilize o componente `BusyIndicator` do padrão SAP Fiori.
- **Tratamento de Exceções:** Caso a API do ERP retorne um erro (Timeout, Erro 500, etc.), trate-o imediatamente exibindo um `MessageBox` amigável para o usuário. Falhas silenciosas (apenas no console) são proibidas.

### 2. Gerenciamento de Navegação Leve (Routing)
- **Navegação Baseada em Estado:** Como não podemos utilizar bibliotecas de roteamento modernas dependentes de bundlers (como `react-router-dom`), toda a navegação de telas deve ser controlada através de Estados (State Management) no componente raiz (`app.js`).
- **Implementação:** Utilize estados simples (ex: `const [currentScreen, setCurrentScreen] = useState('LIST')` ou o mapeamento da entidade selecionada `const [selectedOrder, setSelectedOrder] = useState(null)`) para alternar quais componentes devem ser renderizados.
- **Gestão de Memória:** Certifique-se de que o componente anterior seja corretamente desmontado ao alternar a tela, para evitar vazamento de memória nos tablets de fábrica.
