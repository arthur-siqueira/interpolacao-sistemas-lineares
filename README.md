# Projeto de Métodos Numéricos: Interpolação como Aplicação de Sistemas Lineares

Este projeto implementa funções em Python (utilizando `numpy`) para calcular a **interpolação polinomial** e a **interpolação por spline cúbica natural**.

O foco do notebook é demonstrar como esses métodos de interpolação podem ser resolvidos através da formulação e solução de sistemas de equações lineares. As funções geram as matrizes e vetores necessários automaticamente a partir dos pontos de entrada $(x, y)$.

## 🛠️ Funcionalidades

O notebook está dividido em duas partes principais, cada uma com sua função de interpolação e uma função auxiliar para avaliação:

### 1. Interpolação Polinomial

Encontra um **único** polinômio de grau $n-1$ que passa por todos os $n$ pontos.

* **`interpolacao_polinomial(x_pontos, y_pontos)`**:
    * Constrói a **Matriz de Vandermonde** $A$ (tamanho $n \times n$), onde $A[i, j] = x_i^j$.
    * Resolve o sistema linear $Ac = y$ para encontrar o vetor de coeficientes $c$.
* **`avaliar_polinomio(coefs, x_valores)`**:
    * Função auxiliar que usa os coeficientes `coefs` para calcular $y$ para qualquer `x`.

### 2. Interpolação por Spline Cúbica Natural

Cria um conjunto de polinômios cúbicos, um para cada intervalo entre os pontos, garantindo uma curva suave.

* **`spline_cubica_natural(x_pontos, y_pontos)`**:
    * Calcula os intervalos `h` entre os pontos.
    * Constrói o sistema linear tridiagonal $AM = B$ (tamanho $(n-2) \times (n-2)$) para encontrar as segundas derivadas $M$ nos pontos internos.
    * Resolve o sistema para $M$ e aplica a condição "natural" (adicionando zeros nos extremos `M[0]` e `M[n-1]`).
    * Calcula os coeficientes finais $[a_i, b_i, c_i, d_i]$ para cada segmento da spline.
* **`avaliar_spline(x_pontos, coefs, x_valores)`**:
    * Função auxiliar que localiza o intervalo correto para um `x` (usando `np.searchsorted`) e avalia o polinômio cúbico daquele segmento.

## 🚀 Como Executar

O notebook `interpolacao_sistemas_lineares.ipynb` contém todo o código e os testes.

1.  **Dependências:** Certifique-se de ter as bibliotecas `numpy` e `matplotlib` instaladas:
    ```bash
    pip install numpy matplotlib
    ```
2.  **Execução:** Abra o notebook em um ambiente como Jupyter ou Google Colab.
3.  **Resultados:** A última célula do notebook define um conjunto de pontos de teste e executa ambas as funções de interpolação. Ela imprime os coeficientes calculados no console e gera dois gráficos que comparam visualmente os resultados dos métodos.

### Gráficos de Saída

* **Gráfico 1: Interpolação Polinomial**
    * Mostra o único polinômio de grau 4 que passa por todos os 5 pontos. Note as oscilações (fenômeno de Runge) necessárias para ajustar todos os pontos.

* **Gráfico 2: Interpolação por Spline Cúbica**
    * Mostra as splines cúbicas conectadas. A curva é visivelmente mais suave e "natural" do que a interpolação polinomial, embora também passe por todos os pontos.

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
