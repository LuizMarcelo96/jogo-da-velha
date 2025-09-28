const rs = require('readline-sync');

let tabuleiro = [' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ']; // 0 a 8
let jogador = 'X';

function mostrar() {
  console.clear();
  console.log(`
   ${tabuleiro[0]} | ${tabuleiro[1]} | ${tabuleiro[2]}
  ---+---+---
   ${tabuleiro[3]} | ${tabuleiro[4]} | ${tabuleiro[5]}
  ---+---+---
   ${tabuleiro[6]} | ${tabuleiro[7]} | ${tabuleiro[8]}
  `);
}

function venceu() {
  const linhas = [
    [0,1,2],[3,4,5],[6,7,8],
    [0,3,6],[1,4,7],[2,5,8],
    [0,4,8],[2,4,6]
  ];
  return linhas.some(([a,b,c]) =>
    tabuleiro[a] !== ' ' &&
    tabuleiro[a] === tabuleiro[b] &&
    tabuleiro[a] === tabuleiro[c]
  );
}

while (true) {
  mostrar();
  let pos = rs.questionInt(`Jogador ${jogador}, escolha posicao (0-8): `);

  if (pos < 0 || pos > 8 || tabuleiro[pos] !== ' ') {
    console.log('Posicao invalida! Aperte ENTER e tente de novo.');
    rs.question();
    continue;
  }

  tabuleiro[pos] = jogador;

  if (venceu()) {
    mostrar();
    console.log(`🎉 Jogador ${jogador} venceu!`);
    break;
  }

  if (!tabuleiro.includes(' ')) {
    mostrar();
    console.log('Empate!');
    break;
  }

  jogador = jogador === 'X' ? 'O' : 'X';
}
