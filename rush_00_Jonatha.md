# Projeto Rush

## Descrição

Este projeto é uma função em C que desenha um retângulo no terminal usando caracteres específicos. A função principal, chamada `rush`, desenha o retângulo baseado na largura (x) e na altura (y) fornecidas pelo usuário.

## Estrutura do Código

O código é dividido em várias funções menores para facilitar o entendimento e a organização. Vamos ver o que cada uma dessas funções faz:

### Função `ft_putchar`

Esta função serve para imprimir um único caractere na tela. Aqui está como ela pode ser implementada:

```c
#include <unistd.h>

void	ft_putchar(char c)
{
	write(1, &c, 1);
}
```

### Função `ft_first_line`

Desenha a primeira linha do retângulo.

```c
void	ft_first_line(int x)
{
	int	x_contador;

	x_contador = 0;
	ft_putchar('o');  // Desenha o canto superior esquerdo
	while (x_contador < x - 2)  // Desenha os traços do topo
	{
		ft_putchar('-');
		x_contador++;
	}
	if (x > 1)
	{
		ft_putchar('o');  // Desenha o canto superior direito
	}
	ft_putchar('\n');  // Pula para a próxima linha
}
```

**Por que usamos `x - 2`?**

Quando desenhamos a primeira linha do retângulo, queremos que ela tenha a seguinte estrutura:
- Um caractere `o` no início (canto superior esquerdo).
- Vários caracteres `-` no meio.
- Um caractere `o` no final (canto superior direito), mas apenas se a largura for maior que 1.

Se `x = 5`, a linha deve ter:
- 1 caractere `o` no início.
- 3 caracteres `-` no meio (5 - 2 = 3).
- 1 caractere `o` no final.

Os caracteres do meio são `x - 2` porque subtraímos:
- 1 para o caractere `o` no início.
- 1 para o caractere `o` no final.

### Função `ft_second_line`

Desenha as linhas do meio do retângulo.

```c
void	ft_second_line(int x, int y)
{
	int	k;
	int	i;

	i = 0;
	while (i < y - 2)  // Repete para cada linha do meio
	{
		ft_putchar('|');  // Desenha a borda esquerda
		k = 0;
		while (k < x - 2)  // Desenha os espaços do meio
		{
			ft_putchar(' ');
			k++;
		}
		if (x > 1)
		{
			ft_putchar('|');  // Desenha a borda direita
		}
		i++;
		ft_putchar('\n');  // Pula para a próxima linha
	}
}
```

**Por que usamos `x - 2` e `y - 2`?**

Para desenhar as linhas do meio:
- Começamos com um caractere `|` no início.
- Desenhamos `x - 2` espaços no meio, porque subtraímos os dois caracteres das bordas (`|`).
- Terminamos com um caractere `|` no final, se a largura (`x`) for maior que 1.
- Repetimos o processo para `y - 2` linhas, pois a primeira e a última linhas são desenhadas separadamente.

### Função `ft_last_line`

Desenha a última linha do retângulo.

```c
void	ft_last_line(int x, int y)
{
	int	x_contador;

	x_contador = 0;
	if (y > 1)
	{	
		ft_putchar('o');  // Desenha o canto inferior esquerdo
		while (x_contador < x - 2)  // Desenha os traços do fundo
		{
			ft_putchar('-');
			x_contador++;
		}
		if (x > 1)
		{
			ft_putchar('o');  // Desenha o canto inferior direito
		}
		ft_putchar('\n');  // Pula para a próxima linha
	}
}
```

### Função `rush`

Esta é a função principal que chama as outras funções para desenhar o retângulo completo.

```c
void	rush(int x, int y)
{
	ft_first_line(x);  // Desenha a primeira linha
	ft_second_line(x, y);  // Desenha as linhas do meio
	ft_last_line(x, y);  // Desenha a última linha
}
```

## Como Funciona

Vamos ver como cada parte do retângulo é desenhada:

- **A primeira linha (`ft_first_line`):**
  - Começa com o caractere `o`.
  - Desenha traços (`-`) no meio, dependendo da largura (`x`) fornecida.
  - Termina com o caractere `o` se a largura (`x`) for maior que 1.
  - Pula para a próxima linha.

- **As linhas do meio (`ft_second_line`):**
  - Cada linha começa com o caractere `|`.
  - Desenha espaços no meio, dependendo da largura (`x`) fornecida.
  - Termina com o caractere `|` se a largura (`x`) for maior que 1.
  - Pula para a próxima linha.
  - Repete o processo para a altura (`y`) fornecida.

- **A última linha (`ft_last_line`):**
  - Funciona de forma semelhante à primeira linha, desenhando `o` e `-` nos lugares apropriados.
  - Desenha a última linha somente se a altura (`y`) for maior que 1.

## Exemplo de Uso

Para desenhar um retângulo de largura 5 e altura 3, você pode chamar a função `rush` assim:

```c
rush(5, 3);
```

A saída será:

```
o---o
|   |
o---o
```

## Como Compilar

1. Salve o código em um arquivo chamado `rush.c`.
2. Compile o código usando o comando `gcc`:

```bash
gcc -o rush rush.c
```

3. Execute o programa compilado:

```bash
./rush
```

## Conclusão

Este projeto mostra como você pode dividir um problema em partes menores e resolver cada uma delas de maneira organizada. Dessa forma, o código se torna mais fácil de entender, modificar e manter.