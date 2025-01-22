# Informe de Laboratorio 01 - Sumador 
## Alejandro Jimémez Zabala

### Sumador con bloques primitive

```verilog

module sum1bcc_primitive (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;***
  output Cout;
  output S;
```
Se inicia definiendo las entradas (```input```) y salidas (```output```) con sus respectvas denominaciones para identificarlas en procesos posteriores.

```verilog
  wire a_ab;
  wire x_ab;
  wire cout_t;
```
En esta parte anterior del código se definen los "cables" (```wire```) que realizarán las conexiones en el sistema.

```verilog
  and(a_ab,A,B);
  xor(x_ab,A,B);

  xor(S,x_ab,Ci);
  and(cout_t,x_ab,Ci);

  or (Cout,cout_t,a_ab);

endmodule
```
Por último se codifican las compuertas existentes en el sistema, iniciando con el tipo de compuerta que se busca ejecutar (```and```, ```or```, ```xor```), seguido por su salida, y sus 2 entradas respectivamente, que para las compuertas pueden ser outputs, wires, o inputs, cuidando que haya coherencia en el sistema. 

### Sumador con despcripción de suma

```verilog
module sum1bcc (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;
```
Se inicia el código de la misma manera que con bloques primitivos, definiendo inputs, y outputs del sistema.

```verilog
  reg [1:0] st;

  assign S = st[0];
  assign Cout = st[1];
```
Usamos un nuevo elemento ```reg```, en el que se almacena 2 bits, y se asigna un bit a cada ```output``` del sistema.

```verilog
  always @ ( * ) begin
    st  <=   A+B+Ci;
  end
  
endmodule
```
Por ultimo se crea un bloque ```always```, donde se realica la operación ```or``` (+) para las entradas del sistema, y se evaluan con respecto a ```st```.
Entonces, el sumador con descripción de suma tiene una codificación centrada en el procedimiento de la operación, mientras que el sumador con bloques primitivos, toma una codificación que se puede interpretar más facilmente de una forma física.
