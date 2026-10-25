# 🐧 Desafio de Orientação e Navegação Linux (Shell Basics)

Este repositório documenta um laboratório prático que resolvi para treinar fundamentos essenciais de Linux, movimentação via terminal puro, manipulação de permissões e decodificação de dados.

## 🎯 O Cenário do Desafio
Você acaba de receber acesso a uma máquina Linux e nada além disso. Sem interface gráfica, sem documentação, sem alguém para perguntar. Só um shell, um prompt e a sua capacidade de se orientar.

Antes de explorar qualquer vulnerabilidade, um profissional precisa se mover com naturalidade dentro de um sistema que não é dele: listar o que existe, encontrar o que está escondido por convenção, entender permissões e reconhecer quando um conteúdo está codificado em vez de cifrado.

---

## 🛠️ Passo a Passo da Resolução

### 🚩 Flag 1: Arquivos Ocultos e Nomes com Hifens
* **O desafio:** A primeira flag estava na pasta pessoal, escondida entre diretórios com nomes complexos.
* **O problema:** Algumas pastas tinham nomes iniciados por hífens (ex: `--pasta_secreta`), o que fazia o shell confundi-las com comandos.
* **A solução:** 
  1. Usei `ls -la` para listar todas as pastas e arquivos ocultos.
  2. Para acessar e ler o arquivo dentro de uma pasta iniciada por hífen sem que o terminal desse erro, utilizei o separador `--`:
     ```bash
     cat -- --pasta_secreta/--flag/recibo.txt
     ```

---

### 🚩 Flag 2: Busca Avançada com o comando `find`
* **O desafio:** Encontrar um arquivo específico na máquina seguindo critérios rígidos definidos pelo usuário (`flagkeeper`), tamanho exato e permissões.
* **A solução:**
  1. Utilizei o comando `find` filtrando pelo usuário dono, tamanho em bytes e permissões octais, redirecionando os erros de permissão para o limbo (`2>/dev/null`):
     ```bash
     find / -user flagkeeper -size 1337c -perm 640 2>/dev/null
     ```
  2. O comando localizou o arquivo `/opt/gamma/notes4242.dat`.
  3. Li o conteúdo do arquivo com o comando `cat`:
     ```bash
     cat /opt/gamma/notes4242.dat
     ```

---

### 🚩 Flag 3: Desfarce e Decodificação (Base64)
* **O desafio:** O último arquivo estava em `/opt/data/payload.txt` com o conteúdo totalmente ilegível.
* **A solução:**
  1. Identifiquei que não era uma criptografia complexa, mas sim uma codificação padrão **Base64**.
  2. Decodifiquei e visualizei o conteúdo direto na tela com o comando:
     ```bash
     base64 -d /opt/data/payload.txt
     ```
  3. (Opcional) Também é possível decodificar e salvar o resultado em um novo arquivo de forma simultânea:
     ```bash
     base64 -d /opt/data/payload.txt > Resultado.txt
     ```

---

## 💡 Aprendizados Principais
* Manipulação segura de arquivos com caracteres especiais e hífens no shell.
* Domínio de filtros avançados do comando `find` (`-user`, `-size`, `-perm`).
* Diferenciação rápida entre dados codificados (como Base64) e cifrados.
