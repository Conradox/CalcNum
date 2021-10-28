Relatório segundo trabalho
===

Neste relatório vamos apresentar as atividades realizadas neste segundo trabalho da disciplina de calculo numérico. Este trabalho consiste na criação de dois métodos utilizados para a busca de raízes em uma função e a utilização deste métodos para encontrar as raízes de determinadas função.

**Métodos:**
* Método da Bisseção
* Método da Tangente

**Função:**
* f(x) = 3x − ex


## Método da Bisseção

```octave
function rtrn = bisec_solver(l_l, r_l, e, func)
  iterations = 1;
  r1 = func(l_l);
  r2 = func(r_l);
  
  if(r1 * r2 < 0)
    disp("There is a zero beetween these numbers!");
  endif 
  m_l =  (l_l + r_l) / 2;
  
  disp("Answer using m_l:");
  r3 = func(m_l);
  
  disp(num2str(abs(r3)))
  disp(num2str(abs(e)))
  
  
  while(abs(r3) > e)
    iterations+=1;
    
    if(r1 * r3 < 0)
      r_l = m_l;
    endif
    
    if(r2 * r3 < 0)
      l_l = m_l;
    endif
    
    disp(strcat("[",num2str(l_l),";" , num2str(r_l), "]"))
    disp(num2str(r1 * r3))
    
    
    m_l =  (l_l + r_l) / 2;
    r3 = func(m_l);
  endwhile
  
  disp("Quantidade de iterações: ", num2str(iterations))
  disp(strcat("Entrada: ", num2str(m_l)))
  disp(strcat("Resultado: ", num2str(r3)))
  
endfunction
```
