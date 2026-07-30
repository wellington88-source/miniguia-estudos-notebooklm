# miniguia-estudos-notebooklm
Para alimentar o NotebookLM e garantir respostas precisas, foram selecionadas as seguintes fontes abertas:
# Linguagem de Programação Rust

> Repositório criado para o desafio de projeto da **DIO (Digital Innovation One)**: *Explorando a IA para Aprendizagem Ativa com NotebookLM*.

---

## 🎯 Contexto e Objetivos

### Contexto
O avanço da Inteligência Artificial Generativa mudou a forma como consumimos e sintetizamos informações. O **NotebookLM** (desenvolvido pelo Google) atua como um assistente de pesquisa fundamentado nas fontes enviadas pelo usuário, reduzindo alucinações e focando na precisão técnica. Neste projeto, a ferramenta foi utilizada para estruturar o aprendizado da **Linguagem de Programação Rust**, conhecida por seu foco em segurança de memória e alto desempenho.

### Objetivos de Estudo
1. **Compreensão Conceitual:** Dominar os fundamentos do sistema de *Ownership*, *Borrowing* e concorrência segura em Rust.
2. **Curadoria Crítica:** Selecionar documentações oficiais e artigos de referência sobre a linguagem.
3. **Engenharia de Prompts:** Testar e iterar prompts no NotebookLM para extrair explicações didáticas, tabelas comparativas e resumos estruturados.
4. **Portfólio Prático:** Documentar o processo de aprendizado e disponibilizar um miniguia pronto para uso no GitHub.

---

## 📑 Curadoria de Fontes

Para alimentar o NotebookLM e garantir respostas precisas sobre Rust, foram selecionadas as seguintes fontes abertas:

1. **The Rust Programming Language (The Book)**  
   * **Tipo:** Livro/Documentação Oficial (Web)  
   * **Fonte:** https://doc.rust-lang.org/book/  
   * **Descrição:** Guia oficial mantido pela comunidade Rust, cobrindo desde a instalação até conceitos avançados como *Ownership*, *Lifetimes* e *Smart Pointers*.

2. **Rust by Example**  
   * **Tipo:** Guia Prático Interativo (Web)  
   * **Fonte:** https://doc.rust-lang.org/rust-by-example/  
   * **Descrição:** Coleção de exemplos de código explicados detalhadamente, cobrindo estruturas de dados, controle de fluxo e manipulação de erros com `Result` e `Option`.

3. **Rust Language Cheat Sheet**  
   * **Tipo:** Referência Técnica (Web/PDF)  
   * **Fonte:** https://cheats.rs/  
   * **Descrição:** Resumo técnico abrangente contendo sintaxe, palavras-chave, gerenciamento de memória e tipos de dados comuns na linguagem.

---

## 🛠️ Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Nesta seção estão documentados os testes de prompts, as iterações e os desafios encontrados durante a interação com o NotebookLM ao estudar Rust.

### 🔄 Teste 1: Síntese do Conceito de Ownership
* **Prompt Inicial:** *"Me fale sobre Ownership em Rust."*  
* **Resultado:** Resposta muito genérica e focada na teoria acadêmica de alocação em Stack e Heap, sem mostrar impacto prático no código.
* **Ajuste (Refinamento):** *"Com base nas fontes enviadas, explique o conceito de Ownership em Rust em 3 regras simples. Adicione um exemplo de código legível e uma metáfora do cotidiano para que um iniciante entenda facilmente."*
* **Aprendizado/Cicatriz:** Pedir restrições numéricas (ex: "3 regras") e exigir uma metáfora visual força a IA a simplificar a explicação sem perder a precisão científica.

### 🔄 Teste 2: Diferença entre Mutabilidade e Borrowing
* **Prompt Inicial:** *"Qual a diferença de & e &mut?"*  
* **Resultado:** Exclusivamente textual, tornando a comparação confusa para quem está aprendendo a linguagem.
* **Ajuste (Refinamento):** *"Monte uma tabela comparativa no formato Markdown diferenciando Referências Imutáveis (`&T`) e Referências Mutáveis (`&mut T`). Inclua as colunas: Conceito, Permite Leitura?, Permite Escrita? e Quantidade Máxima Permitida por Escopo."*
* **Aprendizado/Cicatriz:** Exigir a formatação em tabela obriga a IA a sintetizar e organizar a informação em colunas de fácil assimilação visual.

---

## 📖 Miniguia de Estudo (Entrega Final)

### 1. Resumo Estruturado do Assunto

#### 📍 Definição Simples
Rust é uma linguagem de programação focada em **desempenho, concorrência segura e garantia de memória**. Ela elimina erros comuns de vazamento de memória sem a necessidade de um *Garbage Collector* (coletor de lixo), utilizando um conjunto de regras de posse de variáveis verificadas diretamente na compilação.

#### 📝 Explicação Detalhada em Etapas
1. **Regra de Ownership (Posse):** Cada valor em Rust possui uma variável chamada "dono". Só pode existir um dono por vez. Se o dono sai de escopo, a memória do valor é liberada automaticamente.
2. **Borrowing (Empréstimo):** Em vez de transferir a posse, uma função pode "tomar emprestado" o acesso a um valor por meio de referências imutáveis (`&`) ou mutáveis (`&mut`).
3. **Verificação pelo Compilador (*Borrow Checker*):** O compilador analisa todo o código antes da execução. Se houver risco de acesso inválido ou condição de corrida em memória (*data race*), a compilação é interrompida imediatamente.

#### 💡 Exemplo Prático
* **Cenário:** Imprimir e alterar o nome de um usuário em um sistema sem duplicar a memória alocada.
* **Aplicação:**
  ```rust
  fn main() {
      let mut usuario = String::from("Carlos");
      
      // Empréstimo imutável (apenas leitura)
      exibir_nome(&usuario); 
      
      // Empréstimo mutável (permite alteração)
      alterar_nome(&mut usuario); 
  }

  fn exibir_nome(nome: &String) {
      println!("Nome atual: {}", nome);
  }

  fn alterar_nome(nome: &mut String) {
      nome.push_str(" Silva");
  }
