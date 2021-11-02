Relatório segundo trabalho
===

Neste relatório, vamos apresentar as atividades realizadas para o segundo trabalho da disciplina de cálculo numérico. Este trabalho consiste na criação de dois métodos utilizados para a busca de raízes em uma função e a utilização destes métodos para encontrar as raízes de uma determinada função.

**Métodos:**
* Método da Bisseção
* Método da Tangente

**Função:**
* f(x) = 3x − e^x
## Implementações
### Função auxiliar
Nós criamos uma função auxiliar para permitir a passagem de funções matemáticas como parâmetro a partir de uma string. Isso cria um ambiente mais dinâmico em que as funções podem ser passadas como parâmetro pelo terminal e os nossos métodos não dependem da definição ou a implementação das funções a serem utilizadas de forma programática.


```octave
function rtrn = func_exec(str_func, x)
  rtrn = eval(str_func);
endfunction
```
### Método da Bisseção

```octave
function rtrn = bisec(func, l_l, r_l, e)
  iterations = 1;
  
  r1 = func_exec(func, l_l);
  r2 = func_exec(func, r_l);
  
  if(r1 * r2 > 0)
    disp("Intervalo invalido!");
    return;
  endif

  m_l =  (l_l + r_l) / 2;
  
  r3 = func_exec(func, m_l);
  
  while(abs(r3) > e)
    r1 = func_exec(func, l_l);
    r2 = func_exec(func, r_l);
    
    iterations+=1;
    
    if(r1 * r3 < 0)
      r_l = m_l;
    endif
    
    if(r2 * r3 < 0)
      l_l = m_l;
    endif
    
    m_l =  (l_l + r_l) / 2;
    
    r3 = func_exec(func, m_l);
   
  endwhile
  
  disp(strcat("Quantidade de iterações: ", num2str(iterations)))
  disp(strcat("Entrada: ", num2str(m_l)))
  disp(strcat("Resultado: ", num2str(r3)))
  
endfunction
```
### Método da tangente

```
function rtrn = func_exec(str_func, x)
  rtrn = eval(str_func);
endfunction

function result = secante(f, x_k, x_k_1, erro)
 x = (x_k_1 * func_exec(f, x_k) - x_k * func_exec(f, x_k_1)) / (func_exec(f, x_k) - func_exec(f, x_k_1));
 k=0;
  
 while( abs (x_k - x_k_1) >= erro && abs(func_exec(f, x)) >= erro)
   x = (x_k_1 * func_exec(f, x_k) - x_k * func_exec(f, x_k_1)) / (func_exec(f, x_k) - func_exec(f, x_k_1));
   x_k_1 = x_k;
   x_k = x;
   k = k+1;

 end
 result = x;
 disp(strcat("Quantidade de iterações: ", num2str(k)))
 disp(strcat("Entrada: ", num2str(x)))
 disp(strcat("Resultado: ", num2str(func_exec(f, x))))
endfunction

```
### Exemplos
```octave
secante("3 * x - e ^ x", 0, 1, 0.00005);
%PRINT
%Quantidade de iterações:5
%Entrada:0.61906
%Resultado:3.7642e-06  %

bisec("3 * x - e ^ x", 1, 2, 0.00005);
%PRINT
%Quantidade de iterações:14
%Entrada:1.5121
%Resultado:-1.7584e-05
```

## Resultados
### Busca pelos intervalos
Antes de realizar a descoberta das raízes, precisamos fazer uma simples análise para buscar os intervalos que irão ser passados como parâmetro para os nossos métodos, uma das maneiras de se fazer isso é a partir de uma análise gráfica. Neste caso, usamos o próprio octave para plotar o gráfico da função.
<br>
<img src="func_graph.png" width="500">
<br>
A partir do gráfico conseguimos facilmente visualizar que as raízes estão entre os intervalos [0,1] e [1,2].

### Tabela de resultados

Intervalo|Método | Função |Erro Admitido | QTD Iterações| Resultado X | Resultado Y|
|-------|-------|------|--------|--------|-------|---------|
| [0,1] | Tangente | 3 * x - e ^ x | 0.00005 | 5 | 0.61906 | 3.7642e-06 |
| [1,2] | Tangente | 3 * x - e ^ x | 0.00005 | 10| 1.5121  | -1.7584e-05 |
| [0,1] | Bisseção| 3 * x - e ^ x | 0.00005 | 13 | 0.61902 | -4.8837e-05 |
| [1,2] | Bisseção| 3 * x - e ^ x | 0.00005 | 14 | 1.5121  | -1.7584e-05 |