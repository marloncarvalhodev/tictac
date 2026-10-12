# TicTac

> Relógio digital em tempo real desenvolvido com foco em precisão temporal, hierarquia visual e estética minimalista/industrial.

 **Demonstração:** [marloncarvalhodev.github.io/tictac](https://marloncarvalhodev.github.io/tictac/)

---

## Sobre o Projeto

O **TicTac** foi concebido para entregar uma experiência limpa e funcional de leitura de tempo, eliminando elementos decorativos desnecessários em favor de uma interface utilitária refinada.

O projeto utiliza a API nativa `Intl.DateTimeFormat` para manter o horário sincronizado e formatado rigorosamente de acordo com o Horário Oficial de Brasília (`America/Sao_Paulo`), com tratamento de ciclo de vida para evitar fugas de memória.

---

## Funcionalidades

- **Sincronização em Tempo Real:** Atualização contínua de horas, minutos e segundos.
- **Hierarquia Visual nos Segundos:** Destaque para horas e minutos, com exibição secundária e mais suave dos segundos.
- **Zero Jitter Tipográfico:** Aplicação de `tabular-nums` para estabilidade métrica dos dígitos.
- **Microinteração Funcional:** Barra sutil de progresso do minuto (0 a 59s) integrada ao card.
- **Formatação Editorial:** Dia da semana e data formatados por extenso de forma natural em português (`pt-BR`).
- **Layout Responsivo:** Adaptado para diferentes resoluções sem quebras ou barras de rolagem desnecessárias.

---

## 🛠️ Tecnologias Utilizadas

- [Vue 3](https://vuejs.org/) — Composition API (`<script setup>`, `ref`, `computed`, `onMounted`, `onUnmounted`)
- [Tailwind CSS](https://tailwindcss.com/) — Estilização utilitária e design system neutro
- [Vite](https://vitejs.dev/) — Ferramenta de build e servidor de desenvolvimento
- [Intl.DateTimeFormat](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat) — Formatação nativa de datas e fusos

---

## Como Executar Localmente

Clone o repositório e acerte as dependências:

```bash
# Clonar o repositório
git clone [https://github.com/marloncarvalhodev/tictac.git](https://github.com/marloncarvalhodev/tictac.git)

# Acessar a pasta do projeto
cd tictac

# Instalar as dependências
npm install

# Iniciar o servidor de desenvolvimento
npm run dev
