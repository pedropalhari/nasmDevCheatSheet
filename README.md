# NASM CHEATSHEET

## Comandos de compilação/compilação e debug

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
 * * As /options possíveis são:
 * * * /x
 * * * /d
 
* Para monitorar um array no graph display pode-se usar `graph display [/option] [(size[num_elementos])] nome_do_array` (ex: `graph display /x (char[5]) array_de_bytes`).


