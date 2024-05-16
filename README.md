# Projeto de Reconhecimento de Voz e Adivinhação de Números

Este projeto utiliza a API do Google para fazer a transcrição de voz e implementar um jogo de adivinhação de números. O usuário fala um número, e o sistema valida se o número falado é o número secreto previamente sorteado.

## Funcionalidades

1. **Reconhecimento de Voz**: Utiliza a API do Google para reconhecer a voz do usuário e transcrever o que foi dito.
2. **Sorteio de Número**: Gera um número aleatório dentro de um intervalo definido.
3. **Validação**: Verifica se o número falado pelo usuário é válido e se corresponde ao número secreto.

## Tecnologias Utilizadas

- HTML
- CSS
- JavaScript
- Google Speech Recognition API

## Como Executar o Projeto

### Pré-requisitos

Certifique-se de ter um navegador que suporte a API de reconhecimento de voz do Google (como Google Chrome).

Acesse a documentação da API se necessário para ver o suporte dos navegador:
https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition

### Passos

1. Clone o repositório:

   `git clone https://github.com/kisuke121253/acerte-o-numero-10-a-1000.git`

2. Navegue até o diretório do projeto:

   `cd seu-repositorio`

3. Abra o arquivo `index.html` no seu navegador.

   - No Windows: Você pode fazer isso clicando duas vezes no arquivo `index.html`.
   - No Mac/Linux: Você pode abrir o arquivo com o comando `open index.html` no terminal.

## Estrutura do Código

### Reconhecimento de Voz

O código abaixo faz o reconhecimento de voz e exibe a transcrição na tela:

```javascript
const elementoChute = document.getElementById("chute");

window.SpeechRecognition =
  window.SpeechRecognition || window.webkitSpeechRecognition;

const recognition = new SpeechRecognition();
recognition.lang = "pt-Br";
recognition.start();

recognition.addEventListener("result", onSpeak);

function onSpeak(e) {
  chute = e.results[0][0].transcript;
  exibeChuteNaTela(chute);
  verificaSeOChutePossuiUmValorValido(chute);
}

function exibeChuteNaTela(chute) {
  elementoChute.innerHTML = ` <div> Você disse</div>
    <span class="box"> ${chute}</span>`;
}

recognition.addEventListener("end", () => recognition.start());
```
### Sorteio de Número

O código abaixo sorteia um número aleatório entre 10 e 1000:

```javascript
const menorValor = 10;
const maiorValor = 1000;
const numeroSecreto = gerarNumeroAleatorio();

function gerarNumeroAleatorio() {
  return parseInt(Math.random() * maiorValor + 1);
}

console.log("Número Secreto:", numeroSecreto);

const elementoMenorValor = document.getElementById("menor-valor");
elementoMenorValor.innerHTML = menorValor;

const elementoMaiorValor = document.getElementById("maior-valor");
elementoMaiorValor.innerHTML = maiorValor;
```
### Validação

O código abaixo valida se o número falado é o número secreto:

```javascript
function verificaSeOChutePossuiUmValorValido(chute) {
  const numero = +chute;
  const gameOver = "game over";

  if (chuteForInvalido(numero)) {
    elementoChute.innerHTML += "<div>Valor inválido</div>";
  }

  if (numeroForMaiorOuMenorQueOValorPermitido(numero)) {
    elementoChute.innerHTML += `<div>Valor inválido: Fale um número entre ${menorValor} e ${maiorValor}</div>`;
  }

  if (numero === numeroSecreto) {
    document.body.innerHTML = `<h2>Você acertou!</h2>
    <h3>O número secreto era ${numeroSecreto}</h3>
    
    <button id="jogar-novamente" class="btn-jogar">Jogar novamente</button>`;
  }
  if (chute === gameOver) {
    document.body.innerHTML = `<h2>Game Over!</h2>
    <h3>O número secreto era ${numeroSecreto}</h3>
    <button id="jogar-novamente" class="btn-jogar">Jogar novamente</button>`;
  } else if (numero > numeroSecreto) {
    elementoChute.innerHTML += `<div>O número secreto é menor <i class="fa-solid fa-down-long"></i></div>`;
  } else {
    elementoChute.innerHTML += `<div>O número secreto é maior <i class="fa-solid fa-up-long"></i></div>`;
  }
}

function chuteForInvalido(numero) {
  return Number.isNaN(numero);
}

function numeroForMaiorOuMenorQueOValorPermitido(numero) {
  return numero > maiorValor || numero < menorValor;
}

document.body.addEventListener("click", (e) => {
  if (e.target.id == "jogar-novamente") {
    window.location.reload();
  }
});
```
## Contato

**Nome:** João Pedro Lacerda Sousa  
**Email:** [jpedro121256@gmail.com](mailto:jpedro121256@gmail.com)  
**LinkedIn:** [João Pedro Lacerda Sousa](https://www.linkedin.com/in/joão-pedro-lacerda-sousa-0ab308244/)
