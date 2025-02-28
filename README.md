ng new angular-buzzfeed-quizz-clone
cd angular-buzzfeed-quizz-clone
ng serve
ng g c components/quiz
ng g s services/quiz
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class QuizService {
  private perguntas = [
    {
      pergunta: 'Qual sua cor favorita?',
      respostas: [
        { opcao: 'Vermelho', valor: 10 },
        { opcao: 'Azul', valor: 20 },
        { opcao: 'Verde', valor: 30 },
      ],
    },
    {
      pergunta: 'Escolha um animal:',
      respostas: [
        { opcao: 'Cachorro', valor: 10 },
        { opcao: 'Gato', valor: 20 },
        { opcao: 'Pássaro', valor: 30 },
      ],
    },
  ];

  getPerguntas() {
    return this.perguntas;
  }

  calcularResultado(pontos: number) {
    if (pontos <= 20) return 'Você é uma pessoa aventureira!';
    if (pontos <= 40) return 'Você é uma pessoa criativa!';
    return 'Você é uma pessoa tranquila!';
  }
}
import { Component, OnInit } from '@angular/core';
import { QuizService } from 'src/app/services/quiz.service';

@Component({
  selector: 'app-quiz',
  templateUrl: './quiz.component.html',
  styleUrls: ['./quiz.component.css']
})
export class QuizComponent implements OnInit {
  perguntas: any[] = [];
  perguntaAtual = 0;
  pontuacao = 0;
  resultado: string | null = null;

  constructor(private quizService: QuizService) {}

  ngOnInit() {
    this.perguntas = this.quizService.getPerguntas();
  }

  responder(valor: number) {
    this.pontuacao += valor;
    this.perguntaAtual++;

    if (this.perguntaAtual >= this.perguntas.length) {
      this.resultado = this.quizService.calcularResultado(this.pontuacao);
    }
  }
}
import { Component, OnInit } from '@angular/core';
import { QuizService } from 'src/app/services/quiz.service';

@Component({
  selector: 'app-quiz',
  templateUrl: './quiz.component.html',
  styleUrls: ['./quiz.component.css']
})
export class QuizComponent implements OnInit {
  perguntas: any[] = [];
  perguntaAtual = 0;
  pontuacao = 0;
  resultado: string | null = null;

  constructor(private quizService: QuizService) {}

  ngOnInit() {
    this.perguntas = this.quizService.getPerguntas();
  }

  responder(valor: number) {
    this.pontuacao += valor;
    this.perguntaAtual++;

    if (this.perguntaAtual >= this.perguntas.length) {
      this.resultado = this.quizService.calcularResultado(this.pontuacao);
    }
  }
}
<div *ngIf="!resultado">
  <h2>{{ perguntas[perguntaAtual]?.pergunta }}</h2>

  <button *ngFor="let resposta of perguntas[perguntaAtual]?.respostas"
          (click)="responder(resposta.valor)">
    {{ resposta.opcao }}
  </button>
</div>

<div *ngIf="resultado">
  <h2>Resultado:</h2>
  <p>{{ resultado }}</p>
</div>
h2 {
  color: #ff4081;
  text-align: center;
}

button {
  display: block;
  margin: 10px auto;
  padding: 10px;
  font-size: 16px;
  background-color: #6200ea;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #3700b3;
}
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { QuizComponent } from './components/quiz/quiz.component';

@NgModule({
  declarations: [
    AppComponent,
    QuizComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
<h1>Quiz Estilo BuzzFeed</h1>
<app-quiz></app-quiz>
ng serve
