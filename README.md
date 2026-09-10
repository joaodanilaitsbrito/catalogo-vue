# Catálogo de Livros

Aplicação web interativa para catalogação e gerenciamento de acervo bibliográfico pessoal ou institucional, desenvolvida com foco em reatividade, componentização modular e experiência do usuário limpa e responsiva.

---

## 📖 Sobre o Projeto

O **Catálogo de Livros** é um sistema desenvolvido para facilitar o controle de títulos literários e técnicos. A ferramenta permite organizar livros por gênero, registrar autores e monitorar a disponibilidade física ou de empréstimo de cada exemplar por meio de indicadores visuais de status.

O projeto foi construído utilizando a **Composition API** do Vue.js 3 com a sintaxe `<script setup>`, garantindo legibilidade de código, separação clara de responsabilidades e alto desempenho impulsionado pelo ecossistema do Vite.

---

## 🛠️ Tecnologias Utilizadas

- **Vue.js 3:** Framework progressivo para construção da interface reativa.
- **Vite:** Ferramenta de build e servidor de desenvolvimento ultrarrápido.
- **JavaScript (ES6+):** Lógica de manipulação de dados e estados reativos.
- **Composition API (`<script setup>`):** Paradigma moderno de estruturação de componentes no Vue.
- **CSS3 Moderno:** Estilização componentizada com suporte a Flexbox, CSS Grid e design responsivo.

---

## ✨ Funcionalidades

- **Cadastro de Livros:** Inclusão simplificada de novos títulos com preenchimento obrigatório de título, categoria, autor e definição inicial de status.
- **Busca em Tempo Real:** Filtragem dinâmica e instantânea do acervo com base no título da obra ou no nome do autor.
- **Edição em Linha:** Alteração direta dos dados e atualização do status de empréstimo sem necessidade de recarregar a página.
- **Exclusão de Registros:** Remoção segura de itens do acervo com diálogo de confirmação.
- **Indicadores Visuais de Status:** Identificação rápida por meio de tags cromáticas para os estados:
  - `Disponível` (verde)
  - `Emprestado` (vermelho)
  - `Reservado` (amarelo)

---

## 📋 Pré-requisitos

Antes de iniciar a instalação, certifique-se de ter instalado em seu ambiente:

- **Node.js:** Versão 18.x ou superior recomendada.
- **npm:** Gerenciador de pacotes integrado ao Node.js.

Para validar a instalação das dependências globais, execute:
```bash
node -v
npm -v