# NASM CHEATSHEET

## Index
1. [Comandos de compilação/compilação e debug](#comandos)

## Comandos de compilação/compilação e debug <a name="comandos"/>
### Arquivo ./asm.sh
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

### Arquivo ./asmd.sh
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

## Cheatsheet do DDD
 * Para se colocar um break point em uma linha utiliza-se o comando `break` (ex: `break 36`) ou em um label (ex: `break _start`).
 * Para monitorar uma variável é possível mantê-la no graph display com `graph display [/option] [(size)] nome_da_variavel` (ex: `graph display (int) contador` mostra a variável em blocos de 32 bits no display)
   * As /options possíveis são:
		* /x - Mostra o número em hexa
		* /d - Mostra o número em decimal
	* as (size) possíveis são:
		* (char) - 8 bits
		* (short) - 16 bits
		* (int) - 32 bits
		* (long) - 64 bits
		* (float) - 32 bits ponto flutuante
		* (double) - 64 bits ponto flutuante
 
* Para monitorar um array no graph display pode-se usar `graph display [/option] [(size[num_elementos])] nome_do_array` (ex: `graph display /x (char[5]) array_de_bytes`).


