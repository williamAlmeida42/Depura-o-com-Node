# ✅ 1. Ferramenta de depuração utilizada
Utilizei:

Logs (console.log) para rastrear o fluxo de execução.

Validação de JSON para verificar formatação incorreta no users.js.

❌ 2. Bugs encontrados
Bug 1: Arquivo incorreto sendo lido
O app.js tenta ler o arquivo usuarios.json, mas o nome do arquivo enviado é users.js.

Local do erro:

js
Copiar
Editar
fs.readFile('usuarios.json', 'utf8', (err, dados) => {
Bug 2: Formatação inválida do JSON
O conteúdo de users.js não é um JSON válido. Problemas encontrados:

Falta de vírgulas entre objetos.

Strings sem aspas.

Chaves sem aspas.

Conteúdo atual de users.js:

json
Copiar
Editar
{ "nome": "Ana", idade: 22 }
{ "nome": Carlos, "idade": 17 }
{ nome: "Beatriz", "idade": 30 }
🛠️ 3. Correções realizadas
✅ Renomear o arquivo correto para leitura:
Renomeie users.js para usuarios.json ou altere a linha do readFile:

js
Copiar
Editar
fs.readFile('users.js', 'utf8', (err, dados) => {
✅ Corrigir a estrutura JSON:
Atualize o conteúdo para um JSON válido, como:

json
Copiar
Editar
[
  { "nome": "Ana", "idade": 22 },
  { "nome": "Carlos", "idade": 17 },
  { "nome": "Beatriz", "idade": 30 }
]
Salve como usuarios.json.

✅ Corrigir a variável indefinida mensagem:
No app.js, a função exibirMensagem() usa uma variável mensagem que não foi definida.

Correção:

js
Copiar
Editar
function exibirMensagem() {
  const mensagem = "Execução concluída!";
  console.log(mensagem);
}
✅ 4. Código corrigido (app.js)
js
Copiar
Editar
const fs = require('fs');

function carregarUsuarios() {
  fs.readFile('usuarios.json', 'utf8', (err, dados) => {
    if (err) {
      console.log('Erro ao ler o arquivo:', err.message);
    } else {
      const usuarios = JSON.parse(dados);
      filtrarUsuarios(usuarios);
    }
  });
}

function filtrarUsuarios(lista) {
  const resultado = lista.filter((usuario) => usuario.idade > 18);
  console.log('Usuários maiores de idade:');
  resultado.forEach((u) => {
    console.log(`- ${u.nome} (${u.idade} anos)`);
  });
}

function exibirMensagem() {
  const mensagem = "Execução concluída!";
  console.log(mensagem);
}

function main() {
  carregarUsuarios();
  exibirMensagem();
}

main();Depura-o-com-Node
