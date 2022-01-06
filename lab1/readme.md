
# Visão Geral

Nesta atividade, você vai ganhar familiaridade com a estrutura do programa MPI e com a comunicação ponto a ponto trabalhando com programas como "Hello, World", cálculo de \pi, o jogo da vida.

### Objetivos

Familiarize-se com a estrutura do programa MPI e a comunicação ponto a ponto escrevendo alguns programas MPI simples.

# Códigos-Fontes

- Hello, World: Serial C ([hello.c](hello.c))
- Envie dados para todos os processos 
- Calculo do &pi: Serial C  ([pi_serial.c](pi_serial.c))
- Produto Interno: Serial C
- Game of Life: Serial C  ([game_of_life-serial.c](game_of_life-serial.c) 
.
# Exercício 1: Rode "Hello, World"

Compile  e execute o programa "Hello, World". Certifique-se de compreender como cada processo imprime seu rank, bem como o número total de processos no comunicador MPI_COMM_WORLD.

# Exercício 2: Envie dados para todos os processos

Escreva um programa que pegue dados do processo zero e os envie para todos os outros processos. Ou seja, o processo i deve receber os dados e enviá-los para o processo i + 1, até que o último processo seja alcançado.

Suponha que os dados consistam em um único inteiro. Para simplificar, defina o valor para o primeiro processo diretamente no código. Você pode querer usar MPI_Send e MPI_Recv em sua solução.


# Exercicio 3: Encontre &pi using P2P (Mestre/Escravo)

O programa fornecido calcula o &pi; usando uma aproximação de integral. Pegue a versão serial do programa e modifique-a para funcionar em paralelo.

Primeiro, familiarize-se com a maneira como o programa serial funciona. Como ele calcula o &pi;?

Dica: veja os comentários do programa. Como a precisão do cálculo depende de DARTS e ROUNDS, o número de etapas de aproximação?


Dica: edite DARTS para ter vários valores de entrada de 10 a 10000. 
O que você acha que acontecerá com a precisão com a qual calculamos o &pi; quando dividimos o trabalho entre os nós?

Agora paralelize o programa serial. Use apenas as seis chamadas MPI básicas.

Dica: Como o número de DARTS e ROUNDS é codificado, todos os escravos já sabem disso, mas cada trabalhador deve calcular quantos estão em sua parte nos DARDOS para que ele faça sua parte no trabalho. Ao terminar, cada processo escavo envia sua soma parcial de volta ao processo mestre, que a recebe e calcula a soma final. 


# Exercise 5: Use P2P no "Jogo da Vida"

Neste exercicio 
In this exercise, you continue learning about point-to-point message-passing routines in MPI.
After completing this exercise, you should be able to write the real parallel MPI code to solve the Game of Life.

[Here is some background on the "Game of Life"](Game_of_life.md), in case you're new to the problem.

To start this exercise, add the initialization and finalization routines to the serial "Game of Life" code. This will effectly duplicate the exact same calculation on each processor. In order to show that the code is performing as expected, add statements to print overall size, and the rank of the local process. Don't forget to add the MPI header file.

Para iniciar este exercício, adicione as rotinas de inicialização e finalização ao código serial "Game of Life". Isso duplicará com eficácia o mesmo cálculo exato em cada processador. Para mostrar que o código está funcionando conforme o esperado, adicione instruções para imprimir o tamanho geral e a classificação do processo local. Não se esqueça de adicionar o arquivo de cabeçalho MPI.


**Domain Decomposition**

In order to truly run the "Game of Life" program in parallel, we must set up our domain decomposition, i.e., divide the domain into chunks and send one chunk to each processor. In the current exercise, we will limit ourselves to two processors. If you are writing your code in C, divide the domain with a horizontal line, so the upper half will be processed on one processor and the lower half on a different processor. If you are using Fortran, divide the domain with a vertical line, so the left half goes to one processor and the right half to another.

Hint: Although this can be done with different kinds of sends and receives, use blocking sends and receives for the current problem. We have chosen the configuration described above because in C arrays, rows are contiguous, and in Fortran columns are contiguous. This approach allows the specification of the initial array location and the number of words in the send and receive routines.

One issue that you need to consider is that of internal domain boundaries. Figure 1 shows the "left-right" domain decomposition described above. Each cell needs information from all adjacent cells to determine its new state. With domain decomposition, some of the required cells no longer are available on the local processor. A common way to tackle this problem is through the use of ghost cells. In the current example, a column of ghost cells is added to the right side of the left domain, and a column is also added to the left side of the right domain (shown in Figure 2). After each time step, the ghost cells are filled by passing the appropriate data from the other processor. You may want to refer to the figure in the 
[background on the "Game of Life"](Game_of_life.md) to see how to fill the other ghost cells.

Figure 1. Left-right domain decomposition.

<img src="lr_decomp.jpg" alt="Figure 1" width="400px"/>

Figure 2. Ghost cells.

<img src="ghost.jpg" alt="Figure 2" width="400px"/>


**Your Challenge**

Implement the domain decomposition described above, and add message passing to the ghost cells. Don't forget to divide the domain using a horizontal line for C and a vertical line for Fortran. In a subsequent lesson we will examine domain decomposition in the opposite direction.


# Solutions

The solutions will be made available at the end of the lab.

# Acknowledgment

The examples in this lab are provided for educational purposes by 
[National Center for Supercomputing Applications](http://www.ncsa.illinois.edu/), 
(in particular their [Cyberinfrastructure Tutor](http://www.citutor.org/)), 
[Lawrence Livermore National Laboratory](https://computing.llnl.gov/) and 
[Argonne National Laboratory](http://www.mcs.anl.gov/). Much of the LLNL MPI materials comes from the 
[Cornell Theory Center](http://www.cac.cornell.edu/). 
We would like to thank them for allowing us to develop the material for machines at PDC. 
You might find other useful educational materials at these sites.
