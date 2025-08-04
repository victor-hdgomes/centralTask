# 🏗️ Arquitetura do Projeto Vue - CentralTask

Este documento descreve a arquitetura do projeto **CentralTask**, desenvolvido com Vue.js, Vite, Vue Router e Pinia.

---

## 📁 Estrutura Principal

centralTask/
├── public/
├── src/
│ ├── assets/
│ ├── components/ # Componentes reutilizáveis
│ ├── views/ # Páginas principais (roteadas)
│ ├── stores/ # Gerenciamento de estado com Pinia
│ ├── services/ # Chamadas à API (Axios)
│ ├── router/ # Definição de rotas com Vue Router
│ ├── App.vue # Componente raiz
│ └── main.js # Ponto de entrada da aplicação
├── .env # Variáveis de ambiente
├── package.json
├── vite.config.js
└── README.md


---

## 🔄 Fluxo de Funcionamento

1. `main.js` inicia o app, configurando Vue Router e Pinia.
2. `App.vue` serve como ponto de montagem visual.
3. `router/` define as rotas e associa as `views/`.
4. `views/` renderizam páginas conforme a navegação.
5. `components/` são usados dentro das views para funcionalidades específicas.
6. `stores/` armazenam e controlam o estado global (ex: lista de tarefas).
7. `services/` fazem chamadas HTTP usando Axios e fornecem dados para as stores.

---

## ✅ Boas Práticas Aplicadas

- **Separação de responsabilidades**: UI, lógica de estado e chamadas HTTP estão em camadas distintas.
- **Componentização**: Reutilização de componentes pequenos e específicos.
- **Gerenciamento de estado com Pinia**: Simples, escalável e reativo.
- **Serviços centralizados**: Evita duplicação de lógica de requisição HTTP.
- **Estrutura pronta para escalar**: Diretórios organizados e separados por contexto.

---

## 📋 Resumo em Tabela

| Camada        | Papel principal                                   | Localização         |
|---------------|----------------------------------------------------|---------------------|
| UI / Views    | Renderização das páginas via rotas                 | `src/views/`        |
| UI / Components| Elementos reutilizáveis dentro das views           | `src/components/`   |
| Rotas         | Define caminhos e quais views carregar             | `src/router/`       |
| Store         | Estado global e lógica de negócio                  | `src/stores/`       |
| Serviços      | Chamadas HTTP à API, abstração e tratamento        | `src/services/`     |
| Config/Env    | Variáveis e build (Vite config, chaves, endpoints) | `.env`, `vite.config.js` |

---

## 🛠️ Tecnologias Utilizadas

- **Vue 3**
- **Vite**
- **Vue Router**
- **Pinia**
- **Axios**

---

Se desejar aprofundar em algum ponto específico (stores, API, performance, etc.), abra uma _issue_ ou me chame!
