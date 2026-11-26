# MACSLang — versão Java didática

## Requisitos
JDK 21, Windows (também funciona em Linux com os comandos manuais). Não é necessário MSYS2 nem G++ para o modo Java. Verifique `java -version` e `javac -version` no terminal. Se não estiverem disponíveis, instale um JDK 21 autorizado (por exemplo, Eclipse Temurin) e configure o PATH.

## Execução
Extraia o ZIP e clique duas vezes em `executar.bat`. Escolha 1 para fatorial. Depois de cada execução, o menu reaparece. Escolha 0 para sair. Quando o programa pedir um número, digite 5. A saída esperada é 120.

No terminal aberto na pasta do projeto:

```
javac -encoding UTF-8 Main.java Lexico.java Sintatico.java Semantico.java Gerador.java
java Main exemplos/fatorial.macs
java Programa
```

## Arquitetura
Main chama Lexico, Sintatico, Semantico e Gerador. O gerador escreve Programa.java e usa javac (via ToolProvider) para gerar Programa.class. A JVM executa o bytecode. Cada etapa está em um arquivo próprio. O código contém comentários em português nas instruções e blocos relevantes.

## Limitações importantes
O enunciado A3 permite Java para implementar o compilador, mas especifica destino Windows x86. Esta versão gera bytecode JVM, não um executável nativo x86 de 32 bits. Confirme com o professor se aceita esse destino; caso contrário, será necessário adaptar o backend para código nativo. Não há otimizações próprias. A execução foi testada em Linux com JDK 21, não no Windows. O script .bat não foi executado aqui.

Decisões didáticas onde a especificação não define detalhes: float é representado por double; variáveis sem valor recebem um padrão; input de string lê uma palavra; funções não acessam variáveis do programa principal; não há funções aninhadas nem sombreamento de variáveis. O parser implementa a sintaxe descrita, sem extensões como arrays ou chamadas isoladas como instrução. Literais usam escapes compatíveis com Java. A análise de retorno é conservadora; o javac pode identificar restrições adicionais (por exemplo, código inalcançável ou limites de literais).

## Testes
Cinco exemplos válidos e quatro inválidos estão em exemplos/. TESTES.txt registra a execução.

## Revisão de conformidade
As quatro fases estão separadas em classes e arquivos. O exemplo da página 4 do enunciado foi executado com entrada 5 e saída 120. Foram validados 12 casos: cinco programas válidos e sete inválidos (incluindo condição, argumento e retorno incompatíveis). A arquitetura nativa x86 continua pendente de aprovação; a JVM não substitui esse requisito automaticamente.

## Testar um arquivo próprio
Crie um arquivo `meu_programa.macs` e execute `java Main meu_programa.macs`, seguido de `java Programa` somente se a compilação for bem-sucedida. O menu permite repetir os exemplos, mas a calculadora inclusa demonstra uma soma fixa de 10 e 20.

## Publicação
O arquivo `.gitignore` exclui bytecode, código gerado e configurações locais. O relatório em `docs/` descreve as fases e limitações. Não é necessário enviar o JDK ou arquivos compilados.
