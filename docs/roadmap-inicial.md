# Roadmap: definição inicial

## Objetivo
Implementar uma biblioteca e uma aplicação **CLI** em **C (padrão C99)** para executar operações de álgebra linear com matrizes, oferecendo:
- Precisão configurável (`float32` ou `float64`),
- Relatórios de desempenho (tempo de execução, uso de memória, análise de eficiência/Big-O),
- Código organizado e testado com boas práticas de engenharia (testes automatizados, documentação, CI/CD).

---

## Escopo do MVP – v0.1.0
Funcionalidades mínimas para a primeira versão:

* **I/O**  
  - Ler matrizes de arquivos texto no formato:
    ```
    <rows> <cols>
    a11 a12 ... a1c
    ...
    ar1 ar2 ... arc
    ```
  - Gravar matriz resultante em arquivo texto.

* **Operações suportadas**  
  - Soma, subtração, multiplicação,
  - Transposta,
  - Traço (trace),
  - Determinante (2×2 e 3×3),
  - Inversa (Gauss–Jordan).

* **Interface de linha de comando**  
matrix  
–precision <float32|float64> 
[–report ] 
[–metrics time,mem,efficiency] 
–in  [–in2 ] 
–out 

- `<operation>`: `add` | `sub` | `mul` | `transpose` | `trace` | `det` | `inv`
- `--precision`: define 32 ou 64 bits para os elementos.
- `--report`: caminho de JSON/CSV com o relatório.
- `--metrics`: quais métricas incluir (tempo, memória, eficiência).
- `--in`, `--in2`: matrizes de entrada (quando necessário).
- `--out`: destino da matriz resultante.

---

## Abordagem Técnica (resumo)
- **C99** (tipos fixos, `inline`, declaração de variáveis no meio do bloco).
- **Estrutura principal**:
```c
typedef struct {
    size_t rows, cols;
    double *data; // ou float*, conforme precisão selecionada
} matrix_t;

## Ordem sugerida de desenvolvimento (marcos)

- [ ] **Infraestrutura de projeto**
  - [ ] Estrutura de diretórios (`include/`, `src/lib/`, `src/cli/`, etc.)
  - [ ] Makefile inicial (compilação básica + clean)
  - [ ] Configuração de `.gitignore`, templates de issues e PR

- [ ] **Base da biblioteca**
  - [ ] Definir `matrix_t` em `matrix.h`
  - [ ] Implementar criação e destruição de matrizes
  - [ ] Funções de I/O: ler e gravar arquivos texto

- [ ] **Operações fundamentais**
  - [ ] Soma e subtração
  - [ ] Multiplicação
  - [ ] Transposta e traço

- [ ] **Operações avançadas do MVP**
  - [ ] Determinante (2×2, 3×3)
  - [ ] Inversa (Gauss–Jordan)

- [ ] **Interface de Linha de Comando**
  - [ ] Parser de argumentos (`getopt_long`)
  - [ ] Seleção de precisão (`float32` ou `float64`)
  - [ ] Geração de relatório (`--report` e `--metrics`)

- [ ] **Qualidade e testes**
  - [ ] Testes unitários (Unity ou CMocka)
  - [ ] Integração com Valgrind (memória)
  - [ ] Configuração de CI (GitHub Actions)

- [ ] **Documentação**
  - [ ] Doxygen a partir de `include/`
  - [ ] Atualização contínua do `CHANGELOG.md`

- [ ] **Benchmarks e métricas**
  - [ ] Scripts em `bench/` para tempo/memória
  - [ ] Tabelas e gráficos para avaliação de Big-O

- [ ] **Release v0.1.0**
  - [ ] Tag `v0.1.0` e criação de binários