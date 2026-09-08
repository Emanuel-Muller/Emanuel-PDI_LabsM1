# Mini relatorio — Laboratorio M1

## Identificacao

- Estudante: Emanuel Müller Bueno
- Matricula: 8113408
- Laboratorio: M1-1,2 e 3
- Linguagem: Python
## 1. Objetivo

Acredito que o objetivo do laboratorio seja ajudar o aluno a aprender como transferir os conceitos abordados em aula para a programacao, e tambem consolidar esses conhecimentos.

## 2. Operacoes implementadas
inspect: obtém largura, altura, número de canais, tipo da imagem, quantidade de pixels e estatísticas de intensidade. Para imagens coloridas, as estatísticas são calculadas separadamente por canal.

copy: cria uma nova imagem e copia cada pixel individualmente
.
channel_b / channel_g / channel_r: realiza a separação manual dos canais azul, verde e vermelho, mantendo o canal selecionado e zerando os outros.

grayscale_average: converte uma imagem colorida para tons de cinza utilizando a média simples:
G = (R + G + B) / 3.
grayscale_weighted: utiliza a média ponderada:
G = 0.299R + 0.587G + 0.114B.

quantize: reduz a quantidade de níveis de intensidade de uma imagem em tons de cinza.

brightness: altera o brilho adicionando um deslocamento aos valores dos pixels.

contrast: altera o contraste utilizando um fator multiplicativo em relação ao valor central de intensidade.

negative: gera o negativo da imagem utilizando 255 - pixel.

threshold: transforma a imagem em uma imagem binária de acordo com um valor de limiar.

histogram: calcula a quantidade de ocorrências de cada nível de intensidade da imagem.

convolution: percorre a imagem e aplica manualmente um kernel quadrado de dimensão ímpar sobre a vizinhança de cada pixel.

mean_filter: utiliza um kernel no qual todos os coeficientes possuem o mesmo peso, realizando uma média da vizinhança.

weighted_mean: utiliza um kernel 3×3 com pesos maiores no centro, produzindo uma suavização ponderada.

laplacian: utiliza um kernel Laplaciano para destacar variações bruscas de intensidade, sendo útil principalmente para detecção de 
bordas e detalhes.

sobel: utiliza os operadores Sobel horizontal e vertical para calcular a magnitude do gradiente da imagem.

## 3. Testes realizados

Registre os casos utilizados para conferir a implementacao. Inclua as imagens fornecidas e, quando pertinente, pelo menos um caso pequeno ou sintetico cujo resultado possa ser previsto manualmente.

| Teste | Entrada | Operacao | Parametros | Resultado esperado ou criterio de verificacao |
|---|---|---|---|---|
|copia |m1_gray_5x5.png |copy |- |imagem deve ser identica a de entrada(exceto nome)|
|separacao do azul      |m1_color_2x2.png|channel_b |-|somente o canal azul permanece na imagem|
|separacao do verde     |m1_color_2x2.png|channel_g |-|somente o canal verde permanece na imagem|
|tons de cinza simples  |m1_color_2x2.png|greyscale_average |-|cada pixel corresponde a media dos tres canais|
|tons de cinza ponderado|m1_color_2x2.png|greyscale_weighted |-|Cada pixel segue a formula 0.299R + 0.587G + 0.114B|
|quantizacao|m1_gray_5x5.png|quantize |2,4,8,16 niveis|output possui no maximo 2,4,8,16 niveis de intensidade|
|brilho  |m1_gray_5x5.png |brightness |valor positivo ou negativo|intensidade dos pixeis aumenta ou diminui de acordo com o valor inserido|
|contraste |m1_gray_5x5.png|contrast |Fator definido no teste|regioes claras e escuras devem se afastar ou aproximar do valor central conforme o fator utilizado|
|negativo |m1_gray_5x5.png|negative |-|cada intensidade e transformada em 255 - valor original|
|limarizacao |m1_gray_5x5.png|threshold |Limiar definido no teste|pixeis de um lado do limiar devem assumir uma intensidade e os demais outra(binario)|
|histograma |m1_gray_5x5.png|histogram |-|A soma das ocorrências do histograma deve corresponder à quantidade de pixels da imagem|
|convolucao |m1_gray_5x5.png|convolution|kernel 3x3|valores da saida correspondem a aplicacao manual dos coeficientes do kernel sobre cada vizinhanca|
|media |m1_gray_5x5.png|mean_filter |3x3|a saída apresenta suavização|
|media ponderada |m1_gray_5x5.png|weighted_mean |3x3|suavização, dando maior influência ao pixel central|
|laplaciano |m1_gray_5x5.png|laplacian |3x3|bordas e regioes com grandes variacoes de intensidade sao destacadas|
|sobel |m1_gray_5x5.png|sobel |3x3|bordas sao destacadas através da magnitude do gradiente horizontal e vertical|

## 4. Resultados

os arquivos de saída estão todos na pasta output, com suas operacoes respectivas no nome, foram utilizados os comandos listados na seção de testes realizados e os resultados estao de acordo com o resultado esperado eu acredito.

## 5. Analise tecnica

M1-1:
Resolução espacial: mede o nível de detalhe do menor elemento no espaço. Resolução radiométrica: mede a sensibilidade em distinguir variações na intensidade da luz.

Média ponderada: dá pesos diferentes para cada pixel ou canal, ajustando a importância de cada um na média final.

Redução de níveis: gera o efeito de falso contorno (posterização), dividindo tons suaves em faixas visíveis.

Perda de informação: fica mais evidente em regiões de gradiente suave, como sombras e céus.

Canais da imagem: definem quantas dimensões de dados existem por pixel (1 para cinza, 3 para RGB), alterando como a matriz de memória é acessada.

M1-2:
Brilho vs. Contraste: o brilho soma ou subtrai valores deixando tudo mais claro/escuro; o contraste multiplica valores aumentando a diferença entre claros e escuros.

Saturação: ocorre ao ultrapassar os limites de valor (ex.: >255), travando os pixels em preto ou branco e apagando detalhes.

Deslocamento do brilho: move todo o histograma para a direita (mais claro) ou esquerda (mais escuro).

Distribuição do contraste: espalha as barras do histograma pelas pontas (mais contraste) ou esmaga todas no meio (menos contraste).

Limiarização: descarta todas as variações de cinza e textura, transformando a imagem em apenas preto e branco puro.

M1-3:
Operação pontual: calcula o novo pixel usando apenas o próprio pixel. Operação de vizinhança: calcula o novo pixel usando também os pixels vizinhos.

Kernels ímpares: garantem a existência de um pixel central exato para alinhar o resultado.

Aumentar o kernel: aumenta a remoção de ruído, mas deixa a imagem mais borrada.

Tratamento de bordas: evita a criação de linhas ou artefatos falsos nas extremidades da imagem durante a filtragem.

Valores negativos no Laplaciano: surgem porque ele calcula a segunda derivada, indicando a mudança de direção nas rampas de brilho.

Gx​ vs. Gy​: o Gx​ detecta bordas verticais; o Gy​ detecta bordas horizontais.

Soma dos módulos vs. Raiz: a soma é um cálculo simples e rápido; a raiz entrega a magnitude exata e independente da direção da borda.
## 6. Limitacoes
Algumas operações possuem requisitos específicos quanto ao número de canais; por exemplo, a separação de canais necessita de uma imagem colorida e o operador Sobel foi aplicado sobre imagens em tons de cinza.

As operações de convolução utilizam kernels quadrados de dimensão ímpar, conforme a estrutura fornecida pelo projeto. Kernels de dimensão par ou inválidos são rejeitados pela infraestrutura.

## 7. Referencias

Documentação oficial do NumPy — https://numpy.org/doc/
Documentação oficial do OpenCV — https://docs.opencv.org/
