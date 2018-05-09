# NASM CHEATSHEET

## Index
* [Comandos de compilação/compilação e debug](#comandos)
	* [Arquivo ./asm.sh](#aasm)
	* [Arquivo ./asmd.sh](#aasmd)
* [Cheatsheet do DDD](#dddcheat)
	* [break](#break)
	* [graph display](#graphdisplay)
	* [Opções](#slashoptions)
	* [Tipos](#types)

## Comandos de compilação/compilação e debug <a name="comandos"/>
### Arquivo ./asm.sh <a name="aasm"/>
```
function compile() {
	yasm -g dwarf2 -f elf64 $1.asm -l $1.lst && ld -g -o $1 $1.o;
}
compile $1
exit
```

Descrição:
Comando que compila o arquivo .asm em um arquivo executável x64.

Como usar:
`$ ./asm.sh arquivo.asm`

A saída é um arquivo executável de nome *arquivo*. 

### Arquivo ./asmd.sh <a name="aasmd"/>
```
function compile() {
	yasm -g dwarf2 -f elf64 $1.asm -l $1.lst && ld -g -o $1 $1.o;
	ddd $1;
}
compile $1
exit
```

Descrição:
Comando que compila o arquivo .asm em um arquivo executável x64.

Como usar:
`$ ./asmd.sh arquivo.asm`

A saída é um arquivo executável de nome *arquivo*. Abre automaticamente o debugger DDD.

## Cheatsheet do DDD <a name="dddcheat"/>
### break <a name="break" />

Comando:
`break LINHA/LABEL`

Exemplo:
`break 36`
`break _start`

Descrição:
Coloca um break na linha de número LINHA ou na linha do label LABEL.

### graph display <a name="graphdisplay" />

Comando:
 `graph display [/opção]  [(tipo)] VARIAVEL`
 `graph display [/opção] [(tipo[NUM_ELEMENTOS])] ARRAY`

Exemplo:
`graph display contador`
`graph display (long) timestamp`
`graph display /x (char[5]) array_de_bytes`

Descrição:
Para acompanhar a variável. Coloca no display do DDD a variável VARIAVEL ou o array ARRAY com o numero de elementos NUM_ELEMENTOS. Veja [opções](#slashoptions) e [tipos](#types).

### Opções <a name="slashoptions" />
* `/x` - Mostra o número (ou conjunto de) em hexadecimal.
* `/d` - Mostra o número (ou conjunto de) em decimal.
* `/s` - Tenta mostrar o Array em formato de String ASCII. 

### Tipos <a name="types" />
Blocos de:
* `(char)` - 8 bits.
* `(short)` - 16 bits.
* `(int)` - 32 bits.
* `(long)` - 64 bits.
* `(float)` - 32 bits ponto flutuante.
* `(double)` - 64 bits ponto flutuante.

Os tipos aceitam variações de signed/unsigned (ex: `(unsigned char)`).



