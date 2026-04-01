<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz - Parasitologia M1</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800&family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #FFF8F0;
  --card: #FFFFFF;
  --primary: #6C63FF;
  --primary-light: #E8E6FF;
  --correct: #2ECC71;
  --correct-bg: #E8F8F0;
  --wrong: #E74C3C;
  --wrong-bg: #FDECEB;
  --text: #2D3436;
  --text-light: #636E72;
  --hint-bg: #FFF3CD;
  --hint-border: #FFD93D;
  --border: #E9ECEF;
  --shadow: 0 4px 24px rgba(108,99,255,0.08);
  --radius: 16px;
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  font-family: 'Nunito', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-bar-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 6px;
  background: var(--border);
  z-index: 100;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, #6C63FF, #A78BFA, #F472B6);
  transition: width 0.5s cubic-bezier(0.4,0,0.2,1);
  border-radius: 0 3px 3px 0;
}

.header {
  text-align: center;
  padding: 40px 20px 10px;
  max-width: 700px;
  width: 100%;
}

.header h1 {
  font-family: 'Quicksand', sans-serif;
  font-weight: 700;
  font-size: 1.4rem;
  color: var(--primary);
  letter-spacing: -0.02em;
}

.header .subtitle {
  font-size: 0.85rem;
  color: var(--text-light);
  margin-top: 4px;
}

.quiz-container {
  max-width: 700px;
  width: 100%;
  padding: 10px 20px 40px;
  flex: 1;
}

.question-card {
  display: none;
  background: var(--card);
  border-radius: var(--radius);
  padding: 32px 28px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  animation: fadeIn 0.4s ease;
}

.question-card.active {
  display: block;
}

@keyframes fadeIn {
  from { opacity:0; transform:translateY(12px); }
  to { opacity:1; transform:translateY(0); }
}

.q-number {
  display: inline-block;
  background: var(--primary-light);
  color: var(--primary);
  font-weight: 800;
  font-size: 0.8rem;
  padding: 4px 12px;
  border-radius: 20px;
  margin-bottom: 16px;
  letter-spacing: 0.03em;
}

.q-text {
  font-size: 1.05rem;
  line-height: 1.65;
  color: var(--text);
  margin-bottom: 24px;
  font-weight: 600;
}

.options {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

.option-btn {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  background: #F8F9FA;
  border: 2px solid var(--border);
  border-radius: 12px;
  padding: 14px 18px;
  cursor: pointer;
  transition: all 0.2s ease;
  text-align: left;
  font-family: 'Nunito', sans-serif;
  font-size: 0.95rem;
  line-height: 1.5;
  color: var(--text);
  font-weight: 600;
  width: 100%;
}

.option-btn:hover:not(.disabled) {
  border-color: var(--primary);
  background: var(--primary-light);
  transform: translateX(4px);
}

.option-btn .letter {
  flex-shrink: 0;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 800;
  font-size: 0.8rem;
  color: var(--text-light);
  transition: all 0.2s ease;
}

.option-btn:hover:not(.disabled) .letter {
  background: var(--primary);
  color: #fff;
}

.option-btn.correct {
  border-color: var(--correct);
  background: var(--correct-bg);
}
.option-btn.correct .letter {
  background: var(--correct);
  color: #fff;
}

.option-btn.wrong {
  border-color: var(--wrong);
  background: var(--wrong-bg);
}
.option-btn.wrong .letter {
  background: var(--wrong);
  color: #fff;
}

.option-btn.disabled {
  cursor: default;
  opacity: 0.7;
}
.option-btn.correct.disabled,
.option-btn.wrong.disabled {
  opacity: 1;
}

.explanation {
  display: none;
  background: #F0F4FF;
  border-left: 4px solid var(--primary);
  border-radius: 0 12px 12px 0;
  padding: 16px 20px;
  margin-bottom: 20px;
  font-size: 0.9rem;
  line-height: 1.6;
  color: var(--text);
  animation: fadeIn 0.3s ease;
}
.explanation.show { display: block; }

.explanation .exp-title {
  font-weight: 800;
  color: var(--primary);
  margin-bottom: 6px;
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.hint-btn {
  background: none;
  border: 2px dashed var(--hint-border);
  border-radius: 10px;
  padding: 10px 18px;
  cursor: pointer;
  font-family: 'Nunito', sans-serif;
  font-size: 0.85rem;
  font-weight: 700;
  color: #B8860B;
  transition: all 0.2s ease;
  margin-bottom: 12px;
  display: inline-block;
}
.hint-btn:hover {
  background: var(--hint-bg);
}

.hint-box {
  display: none;
  background: var(--hint-bg);
  border: 1px solid var(--hint-border);
  border-radius: 10px;
  padding: 12px 18px;
  margin-bottom: 20px;
  font-size: 0.88rem;
  color: #856404;
  line-height: 1.5;
  animation: fadeIn 0.3s ease;
}
.hint-box.show { display: block; }

.nav-buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 16px;
  gap: 12px;
}

.nav-btn {
  font-family: 'Nunito', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 12px 28px;
  border-radius: 12px;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
}

.nav-btn.prev {
  background: #F0F0F0;
  color: var(--text-light);
}
.nav-btn.prev:hover { background: #E0E0E0; }

.nav-btn.next {
  background: var(--primary);
  color: #fff;
  margin-left: auto;
}
.nav-btn.next:hover { background: #5A52E0; transform:translateY(-1px); }

.nav-btn:disabled {
  opacity: 0.4;
  cursor: default;
  transform: none !important;
}

.counter {
  text-align: center;
  font-size: 0.8rem;
  color: var(--text-light);
  font-weight: 600;
}

/* Results */
.results-card {
  display: none;
  text-align: center;
  background: var(--card);
  border-radius: var(--radius);
  padding: 48px 32px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  animation: fadeIn 0.5s ease;
}
.results-card.active { display: block; }

.results-emoji {
  font-size: 4rem;
  margin-bottom: 16px;
}

.results-title {
  font-family: 'Quicksand', sans-serif;
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 8px;
}

.results-score {
  font-size: 3.5rem;
  font-weight: 800;
  color: var(--primary);
  margin: 16px 0;
}

.results-detail {
  font-size: 1rem;
  color: var(--text-light);
  margin-bottom: 8px;
}

.results-message {
  font-size: 1.1rem;
  font-weight: 700;
  margin: 20px 0;
  padding: 16px 24px;
  border-radius: 12px;
  display: inline-block;
}

.results-message.great {
  background: var(--correct-bg);
  color: #1B8C4E;
}
.results-message.ok {
  background: #FFF3CD;
  color: #856404;
}
.results-message.low {
  background: var(--wrong-bg);
  color: #C0392B;
}

.restart-btn {
  font-family: 'Nunito', sans-serif;
  font-weight: 700;
  font-size: 1rem;
  padding: 14px 36px;
  border-radius: 12px;
  border: none;
  background: var(--primary);
  color: #fff;
  cursor: pointer;
  margin-top: 20px;
  transition: all 0.2s ease;
}
.restart-btn:hover { background: #5A52E0; transform:translateY(-2px); }

@media (max-width: 600px) {
  .question-card, .results-card { padding: 24px 18px; }
  .q-text { font-size: 0.95rem; }
  .option-btn { font-size: 0.88rem; padding: 12px 14px; }
  .nav-btn { padding: 10px 20px; font-size: 0.85rem; }
  .results-score { font-size: 2.8rem; }
}
</style>
</head>
<body>

<div class="progress-bar-container">
  <div class="progress-bar" id="progressBar"></div>
</div>

<div class="header">
  <h1>🔬 Parasitologia — Casos Clínicos M1</h1>
  <p class="subtitle">27 questões · Responda e avance no seu ritmo</p>
</div>

<div class="quiz-container" id="quizContainer"></div>

<script>
const questions = [
  {
    text: "Um paciente de 6 anos apresenta tosse seca, febre baixa e infiltrados pulmonares migratórios ao raio-X. Semanas depois, a mãe relata a eliminação de um verme cilíndrico de aproximadamente 20 cm nas fezes. Qual é o diagnóstico e o mecanismo inicial da fase pulmonar?",
    options: [
      "Ascaridíase; Ciclo de Looss.",
      "Tricuríase; Ação traumática.",
      "Enterobíase; Migração errática.",
      "Estrongiloidíase; Penetração cutânea."
    ],
    correct: 0,
    hint: "Considere o tamanho do verme adulto e a presença de sintomas respiratórios seguidos de gastrointestinais.",
    explanation: "O Ascaris lumbricoides é o maior nematódeo intestinal (até 40 cm) e realiza o Ciclo de Looss: as larvas eclodem no intestino, penetram a parede intestinal, migram pela circulação até os pulmões (causando a Síndrome de Loeffler), sobem pela árvore brônquica e são deglutidas, retornando ao intestino para se tornarem adultos."
  },
  {
    text: "Um escolar apresenta prurido anal intenso, predominantemente noturno, e irritabilidade. A mãe relata que outras crianças na mesma creche apresentam sintomas semelhantes. Qual o método diagnóstico padrão-ouro para esta suspeita clínica?",
    options: [
      "Exame parasitológico de fezes (EPF) convencional.",
      "Hemograma para pesquisa de eosinofilia.",
      "Cultura de fezes para pesquisa de larvas.",
      "Método de Graham (fita adesiva)."
    ],
    correct: 3,
    hint: "Pense no local onde a fêmea do parasito deposita seus ovos durante a noite.",
    explanation: "O Enterobius vermicularis (oxiúro) deposita seus ovos na região perianal durante a noite. O método de Graham (fita adesiva ou swab anal) é o padrão-ouro porque coleta diretamente os ovos depositados nessa região, algo que o EPF convencional frequentemente não detecta."
  },
  {
    text: "Um paciente de 5 anos, residente em área rural com saneamento precário, apresenta diarreia crônica, tenesmo e prolapso retal. O exame de fezes revela ovos elípticos com poros polares em formato de barril. Qual o agente etiológico?",
    options: [
      "Ancylostoma duodenale.",
      "Trichuris trichiura.",
      "Enterobius vermicularis.",
      "Ascaris lumbricoides."
    ],
    correct: 1,
    hint: "O formato do ovo e o sintoma de prolapso retal são pistas fundamentais.",
    explanation: "Trichuris trichiura apresenta ovos característicos em formato de barril com poros polares (tampões mucóides nas extremidades). Em infecções maciças em crianças, o verme fixa-se profundamente na mucosa do ceco e cólon, podendo causar prolapso retal pelo edema e inflamação intensos."
  },
  {
    text: "Um paciente agricultor que trabalha descalço apresenta palidez cutânea intensa, cansaço aos esforços e exames laboratoriais revelando anemia microcítica e hipocrômica. Qual o mecanismo de espoliação deste parasito?",
    options: [
      "Obstrução de canais biliares e pancreáticos.",
      "Absorção direta de vitamina B12.",
      "Hematofagismo por fixação na mucosa através de dentes ou lâminas.",
      "Ingestão de quimo e nutrientes pré-digeridos."
    ],
    correct: 2,
    hint: "Este parasito é conhecido como o agente da 'doença do amarelão' devido à perda crônica de sangue.",
    explanation: "Os Ancilostomídeos (Ancylostoma duodenale e Necator americanus) são hematófagos obrigatórios. Fixam-se na mucosa do intestino delgado usando dentes (Ancylostoma) ou lâminas cortantes (Necator), dilacerando capilares e ingerindo sangue. A perda crônica leva à anemia ferropriva (microcítica e hipocrômica)."
  },
  {
    text: "Após passar férias em uma praia onde circulam cães e gatos, um paciente desenvolve uma lesão cutânea linear, serpiginosa e intensamente pruriginosa no pé. Qual a conduta terapêutica e o agente provável?",
    options: [
      "Tiabendazol tópico; Ancylostoma braziliense.",
      "Praziquantel; Taenia solium.",
      "Dietilcarbamazina; Wuchereria bancrofti.",
      "Albendazol oral; Toxocara canis."
    ],
    correct: 0,
    hint: "O parasito em questão é um ancilostomídeo de animais que não consegue completar o ciclo no homem.",
    explanation: "A Larva Migrans Cutânea (bicho geográfico) é causada principalmente por Ancylostoma braziliense, um ancilostomídeo de cães e gatos. A larva penetra a pele humana mas não consegue atingir a circulação, ficando 'presa' na epiderme e criando trajetos serpiginosos. O tratamento padrão é Tiabendazol tópico ou Albendazol/Ivermectina oral."
  },
  {
    text: "Uma criança de 3 anos apresenta febre, hepatomegalia e eosinofilia persistente extrema (>30%). Os pais relatam que ela costuma brincar em uma caixa de areia frequentada por filhotes de cachorro. Qual a forma infectante ingerida pelo paciente?",
    options: [
      "Larva L3 filarióide.",
      "Cisto com quatro núcleos.",
      "Ovo operculado não embrionado.",
      "Ovo contendo larva L3."
    ],
    correct: 3,
    hint: "O ser humano atua como hospedeiro acidental ao ingerir ovos do ambiente contaminado por animais.",
    explanation: "Na Toxocaríase (Larva Migrans Visceral), o ser humano ingere ovos de Toxocara canis embrionados contendo a larva L3. No intestino, a larva eclode e migra pelos tecidos (fígado, pulmões, olhos, SNC), mas não completa seu ciclo no homem, gerando intensa reação eosinofílica tecidual."
  },
  {
    text: "Um paciente com diagnóstico de DPOC em uso prolongado de altas doses de corticosteroides desenvolve um quadro de sepse por gram-negativos e insuficiência respiratória. O exame de fezes revela larvas rabditóides. Qual o risco biológico específico deste parasito?",
    options: [
      "Obstrução intestinal por 'bolo' de vermes.",
      "Desenvolvimento de anemia megaloblástica.",
      "Formação de cistos hidáticos pulmonares.",
      "Autoinfecção interna e hiperinfecção."
    ],
    correct: 3,
    hint: "Corticosteroides podem induzir a transformação de larvas no intestino, perpetuando o ciclo no próprio hospedeiro.",
    explanation: "O Strongyloides stercoralis possui a capacidade única de autoinfecção: larvas rabditóides transformam-se em filarióides no próprio intestino e penetram a mucosa, reiniciando o ciclo. Em imunossuprimidos (uso de corticoides), esse processo se acelera descontroladamente (hiperinfecção), levando à disseminação maciça de larvas e sepse bacteriana por translocação."
  },
  {
    text: "Qual a principal diferença morfológica entre a larva rabditóide de Strongyloides stercoralis e a de um Ancilostomídeo encontrada no exame de fezes fresco?",
    options: [
      "O Strongyloides possui esôfago filarióide.",
      "O Strongyloides apresenta primórdio genital evidente e cavidade bucal curta.",
      "Apenas os ancilostomídeos são encontrados como larva nas fezes.",
      "Os ancilostomídeos possuem cauda bifurcada."
    ],
    correct: 1,
    hint: "Foque nas estruturas da extremidade anterior e na presença de órgãos genitais rudimentares.",
    explanation: "A larva rabditóide de Strongyloides stercoralis distingue-se pela cavidade bucal curta (vestíbulo bucal curto) e pela presença de um primórdio genital evidente (esboço genital visível). Já a larva rabditóide dos ancilostomídeos tem cavidade bucal longa e primórdio genital pouco visível."
  },
  {
    text: "Um paciente que consome peixe cru (sashimi) regularmente apresenta dor abdominal, flatulência e fadiga. O hemograma mostra anemia com VCM elevado (macrocitose). Qual a causa fisiopatológica da anemia?",
    options: [
      "Deficiência de ferro por sangramento oculto.",
      "Inibição da síntese de eritropoetina nos rins.",
      "Destruição de hemácias no baço (hemólise).",
      "Competição pelo consumo de vitamina B12 pelo parasito."
    ],
    correct: 3,
    hint: "Este verme é o maior parasito humano e tem 'afinidade extrema' por um nutriente essencial para a síntese de DNA.",
    explanation: "O Diphyllobothrium latum é o maior cestódeo humano (até 12 metros) e absorve grandes quantidades de vitamina B12 do lúmen intestinal. A deficiência de B12 leva à anemia megaloblástica (macrocítica), pois essa vitamina é essencial para a síntese de DNA nas células precursoras eritrocitárias."
  },
  {
    text: "Um paciente ingere acidentalmente água contaminada com ovos de Taenia solium. Qual a patologia que este paciente corre o risco de desenvolver?",
    options: [
      "Hidatidose hepática.",
      "Teníase intestinal.",
      "Cisticercose (humano como hospedeiro intermediário).",
      "Anemia botriocefálica."
    ],
    correct: 2,
    hint: "Considere a diferença entre ingerir a larva na carne versus ingerir o ovo liberado por um portador do verme adulto.",
    explanation: "Quando o ser humano ingere ovos de T. solium (via água ou alimentos contaminados), ele assume o papel de hospedeiro intermediário. Os embriões (oncosferas) eclodem no intestino, penetram a parede e se distribuem pelos tecidos formando cisticercos — é a cisticercose, que pode afetar cérebro, olhos e músculos."
  },
  {
    text: "O Hymenolepis nana é um cestódeo peculiar por possuir a capacidade de completar seu ciclo sem a necessidade de um hospedeiro intermediário. Como é classificado esse tipo de ciclo?",
    options: [
      "Ciclo heteroxênico obrigatório.",
      "Reprodução partenogenética.",
      "Ciclo de Looss.",
      "Ciclo monoxênico."
    ],
    correct: 3,
    hint: "Pense no termo utilizado para parasitos que possuem apenas um hospedeiro em seu ciclo biológico.",
    explanation: "Ciclo monoxênico é aquele em que o parasito necessita de apenas um hospedeiro para completar todo o seu desenvolvimento. O Hymenolepis nana pode completar seu ciclo inteiramente no ser humano: o ovo é ingerido, a larva cisticercóide se desenvolve nas vilosidades intestinais e o verme adulto se estabelece no lúmen."
  },
  {
    text: "Qual a característica morfológica que permite diferenciar, macroscopicamente, uma proglote grávida de Taenia solium de uma de Taenia saginata?",
    options: [
      "O número de ramificações uterinas (menos de 12 vs mais de 15).",
      "O tamanho total do verme adulto.",
      "A cor da proglote (branca vs rosada).",
      "A presença de ventosas no escólex."
    ],
    correct: 0,
    hint: "A diferenciação é feita através da técnica de tamisação e contagem das estruturas internas de útero.",
    explanation: "A diferenciação entre as duas espécies de Taenia é feita pela contagem das ramificações uterinas na proglote grávida: T. solium possui menos de 12 ramificações uterinas de cada lado, enquanto T. saginata possui mais de 15. Essa análise é feita após tamisação das fezes e clarificação da proglote."
  },
  {
    text: "Um morador de zona rural que trabalha com ovelhas e possui cães de pastoreio apresenta dor no hipocôndrio direito. O ultrassom revela uma massa cística volumosa no fígado com 'vesículas filhas' em seu interior. Qual o diagnóstico mais provável?",
    options: [
      "Abscesso amebiano.",
      "Cisticercose hepática.",
      "Hidatidose (Cisto Hidático).",
      "Ascaridíase errática."
    ],
    correct: 2,
    hint: "Relacione o contexto epidemiológico de ovelhas e cães com a formação de cistos complexos.",
    explanation: "A Hidatidose é causada pelo Echinococcus granulosus, cujo ciclo envolve cães (hospedeiro definitivo) e herbívoros como ovelhas (hospedeiro intermediário). O ser humano é hospedeiro intermediário acidental ao ingerir ovos. O cisto hidático no fígado é característico com suas vesículas filhas (endógenas e exógenas)."
  },
  {
    text: "Um paciente apresenta diarreia explosiva, esteatorreia (fezes gordurosas e fétidas) e perda de peso após retornar de um acampamento. O exame de fezes revela estruturas ovais com 2 a 4 núcleos e um conjunto de fibras internas (axonemas). Qual a forma biológica encontrada?",
    options: [
      "Ovo de Hymenolepis nana.",
      "Trofozoíto de Giardia lamblia.",
      "Cisto de Giardia lamblia.",
      "Larva filarióide de Strongyloides."
    ],
    correct: 2,
    hint: "Esta é a forma de resistência que permite a sobrevivência do parasito no ambiente por até 60 dias.",
    explanation: "O cisto de Giardia lamblia é oval, possui 2 a 4 núcleos e apresenta axonemas (restos dos flagelos) no seu interior. É a forma de resistência e transmissão do parasito, encontrada mais comumente no exame de fezes formadas. A esteatorreia ocorre porque os trofozoítos recobrem a mucosa do duodeno, impedindo a absorção de gorduras."
  },
  {
    text: "A Síndrome de Loeffler é uma manifestação clínica comum a diversos parasitos que realizam migração pulmonar. Quais dos seguintes agentes estão classicamente associados a esta síndrome?",
    options: [
      "Enterobius, Trichuris e Taenia.",
      "Ascaris, Strongyloides e Ancilostomídeos.",
      "Giardia, Hymenolepis e Schistosoma.",
      "Toxocara, Enterobius e Ascaris."
    ],
    correct: 1,
    hint: "Pense no grupo de nematódeos que 'precisa passar pelo pulmão' para sofrer mudas larvares.",
    explanation: "A Síndrome de Loeffler (eosinofilia pulmonar transitória) é causada pela passagem de larvas pelos pulmões durante o Ciclo de Looss. Os três agentes clássicos são: Ascaris lumbricoides, Strongyloides stercoralis e os Ancilostomídeos (Ancylostoma e Necator). Todos realizam migração pulmonar obrigatória em seu ciclo."
  },
  {
    text: "Um paciente apresenta linfedema progressivo em membros inferiores, evoluindo para um aspecto de 'casca de árvore' e aumento bizarro do volume (elefantíase). Qual o vetor responsável pela transmissão desta parasitose?",
    options: [
      "Mosca de estábulo.",
      "Caramujos do gênero Biomphalaria.",
      "Percevejo conhecido como 'barbeiro'.",
      "Mosquito do gênero Culex."
    ],
    correct: 3,
    hint: "O transmissor é um inseto hematófago de hábito predominantemente noturno.",
    explanation: "A Filariose Linfática (Wuchereria bancrofti) é transmitida pelo mosquito Culex quinquefasciatus, de hábito noturno. As microfilárias apresentam periodicidade noturna no sangue periférico, coincidindo com o horário de repasto do vetor. A obstrução crônica dos vasos linfáticos leva à elefantíase."
  },
  {
    text: "Em um exame de fezes realizado pela técnica de Kato-Katz, o analista identifica ovos com uma 'tampinha' em uma das extremidades. Qual o provável parasito e qual o termo técnico para essa estrutura?",
    options: [
      "Diphyllobothrium latum; Opérculo.",
      "Enterobius vermicularis; Membrana dupla.",
      "Trichuris trichiura; Poro polar.",
      "Ascaris lumbricoides; Membrana mamilonada."
    ],
    correct: 0,
    hint: "Essa estrutura é típica de ovos que liberam larvas ciliadas em meio aquático.",
    explanation: "O ovo de Diphyllobothrium latum é operculado — possui uma 'tampinha' (opérculo) em uma das extremidades pela qual o coracídio (larva ciliada) é liberado na água. Essa é uma característica importante para diferenciá-lo de outros ovos de helmintos no exame parasitológico."
  },
  {
    text: "Um paciente de 40 anos apresenta quilúria (presença de linfa na urina, aspecto leitoso). Esta condição é uma complicação de qual fase da filariose linfática?",
    options: [
      "Fase pulmonar (EPT).",
      "Fase crônica.",
      "Fase aguda (Linfangite).",
      "Período de incubação."
    ],
    correct: 1,
    hint: "Sinais de obstrução linfática severa surgem após anos de infecção persistente.",
    explanation: "A quilúria é uma manifestação da fase crônica da filariose linfática. Após anos de infecção e reação inflamatória persistente contra os vermes adultos nos vasos linfáticos, ocorre obstrução e dilatação linfática (varizes linfáticas). Quando os vasos linfáticos renais rompem na pelve renal, a linfa é eliminada na urina."
  },
  {
    text: "No tratamento da Himenolepíase por Hymenolepis nana, por que é recomendada a repetição da dose de Praziquantel após 10 dias?",
    options: [
      "Porque o Praziquantel tem baixa absorção intestinal.",
      "Para evitar a resistência medicamentosa do parasito.",
      "Para eliminar vermes que estavam na fase larval interna durante a primeira dose.",
      "Para tratar a reinfecção por ovos presentes no peridomicílio."
    ],
    correct: 2,
    hint: "Considere que este parasito possui uma fase de desenvolvimento dentro das vilosidades do intestino delgado.",
    explanation: "O Hymenolepis nana possui uma fase larval cisticercóide dentro das vilosidades intestinais, onde o Praziquantel não alcança efetivamente. A primeira dose elimina os vermes adultos no lúmen, mas as larvas que estão se desenvolvendo nas vilosidades podem emergir depois. A segunda dose, após 10 dias, elimina esses novos vermes adultos."
  },
  {
    text: "Um paciente apresenta anemia megaloblástica e o médico prescreve reposição de Vitamina B12. Qual parasito deve ser investigado obrigatoriamente neste contexto clínico?",
    options: [
      "Schistosoma mansoni.",
      "Ancylostoma duodenale.",
      "Diphyllobothrium latum.",
      "Giardia lamblia."
    ],
    correct: 2,
    hint: "Trata-se de um helminto cestódeo associado ao consumo de peixes crus ou defumados.",
    explanation: "O Diphyllobothrium latum é o parasito classicamente associado à anemia megaloblástica por competição com o hospedeiro pela absorção de vitamina B12. É adquirido pelo consumo de peixes crus, defumados ou mal cozidos contendo a larva plerocercóide."
  },
  {
    text: "Qual a principal ação patogênica do Strongyloides stercoralis no intestino delgado durante uma infecção grave?",
    options: [
      "Obstrução mecânica do lúmen intestinal.",
      "Ação espoliativa exclusiva de ferro.",
      "Ação destrutiva com enterite catarral ou edematosa e úlceras na submucosa.",
      "Ação tóxica por liberação de neurotoxinas."
    ],
    correct: 2,
    hint: "Considere o habitat das fêmeas partenogenéticas e a reação inflamatória que geram na parede intestinal.",
    explanation: "As fêmeas partenogenéticas de S. stercoralis penetram a mucosa do intestino delgado (duodeno e jejuno), causando ação mecânica e destrutiva. Provocam enterite catarral, edematosa ou ulcerativa, com formação de úlceras na submucosa que podem levar a íleo paralítico e má absorção em infecções graves."
  },
  {
    text: "Sobre o diagnóstico da Teníase, qual técnica permite diferenciar as espécies T. solium e T. saginata com base nas proglotes?",
    options: [
      "Método de Hoffman.",
      "Kato-Katz.",
      "Reação de Casoni.",
      "Tamisação de fezes."
    ],
    correct: 3,
    hint: "Pense no processo de 'peneirar' as fezes para encontrar segmentos do corpo do verme.",
    explanation: "A tamisação consiste em peneirar as fezes para recuperar proglotes grávidas inteiras. Após clarificação, é possível contar as ramificações uterinas e diferenciar T. solium (<12 ramificações) de T. saginata (>15 ramificações). Os métodos de Hoffman e Kato-Katz são para pesquisa de ovos, que são indistinguíveis entre as espécies."
  },
  {
    text: "Um paciente imunossuprimido apresenta quadros recorrentes de pneumonia e sepse bacteriana. O médico suspeita de estrongiloidíase disseminada. Qual o mecanismo de autoinfecção interna que explica a cronicidade e gravidade neste caso?",
    options: [
      "Ingestão de ovos presentes na região perianal.",
      "Permanência de vermes adultos no fígado por anos.",
      "Transformação de larvas rabditóides em filarióides ainda no lúmen intestinal.",
      "Eclosão de ovos de Taenia no estômago devido ao vômito."
    ],
    correct: 2,
    hint: "O processo envolve a aceleração do desenvolvimento larvário antes da eliminação nas fezes.",
    explanation: "Na autoinfecção interna do Strongyloides, as larvas rabditóides (L1/L2) transformam-se em larvas filarióides infectantes (L3) ainda dentro do lúmen intestinal, antes de serem eliminadas nas fezes. Essas larvas L3 penetram a mucosa intestinal e reiniciam o ciclo, perpetuando a infecção indefinidamente, especialmente em imunossuprimidos."
  },
  {
    text: "A presença de eosinofilia intensa é um achado laboratorial comum em diversas helmintoses. Em qual das seguintes situações a eosinofilia é MAIS marcante de acordo com o material?",
    options: [
      "Fase crônica da Enterobíase.",
      "Giardíase assintomática.",
      "Teníase intestinal por T. saginata.",
      "Larva Migrans Visceral (Toxocaríase)."
    ],
    correct: 3,
    hint: "Pense em parasitos que permanecem em estágio larvário migrando ativamente pelos tecidos humanos.",
    explanation: "A Larva Migrans Visceral (Toxocaríase) produz a eosinofilia mais intensa (frequentemente >30-50%) porque as larvas de Toxocara migram ativamente pelos tecidos (fígado, pulmões, SNC, olhos) sem completar seu ciclo, mantendo uma resposta imune Th2 exacerbada e prolongada com produção contínua de eosinófilos."
  },
  {
    text: "Qual a medicação de escolha para o tratamento da Larva Migrans Ocular causada por Toxocara canis para reduzir a inflamação e prevenir perda visual?",
    options: [
      "Prednisona (Corticosteroides).",
      "Praziquantel 25 mg/kg.",
      "Dietilcarbamazina (DEC).",
      "Ivermectina em dose única."
    ],
    correct: 0,
    hint: "Além do anti-helmíntico, é necessário suprimir a resposta imunitária do hospedeiro no olho.",
    explanation: "Na Larva Migrans Ocular, a principal preocupação é o dano inflamatório ao olho causado pela reação imune contra a larva. Os corticosteroides (Prednisona) são a base do tratamento para suprimir a inflamação intraocular e prevenir perda visual permanente. Anti-helmínticos são usados com cautela, pois a morte da larva pode agravar a inflamação."
  },
  {
    text: "Ovos de ancilostomídeos são frequentemente descritos como elípticos e de casca fina. Qual a razão biológica para a casca ser fina?",
    options: [
      "Para resistir ao suco gástrico durante a ingestão.",
      "Porque eles eclodem rapidamente liberando larvas L1 no solo.",
      "É uma adaptação para a flutuação em água doce.",
      "Para facilitar a penetração cutânea direta do ovo."
    ],
    correct: 1,
    hint: "Considere o estágio do ciclo biológico que ocorre imediatamente após a eliminação dos ovos nas fezes.",
    explanation: "Os ovos de ancilostomídeos possuem casca fina porque precisam eclodir rapidamente no solo, liberando a larva L1 (rabditóide) que se alimentará e se desenvolverá no ambiente até se tornar larva L3 (filarióide infectante). A casca fina facilita a eclosão rápida em condições adequadas de umidade e temperatura."
  },
  {
    text: "Um paciente com diagnóstico de cisticercose calcificada no cérebro apresenta crises epiléticas. Qual o fármaco que atua no aumento da permeabilidade da membrana do parasito ao cálcio, sendo usado em formas viáveis?",
    options: [
      "Praziquantel.",
      "Tiabendazol.",
      "Albendazol.",
      "Levamisol."
    ],
    correct: 0,
    hint: "Este medicamento é amplamente utilizado tanto para cestódeos (tênias) quanto para trematódeos (esquistossomo).",
    explanation: "O Praziquantel atua aumentando a permeabilidade da membrana tegumentar do parasito aos íons cálcio (Ca²⁺), causando contração espástica da musculatura, vacuolização e desintegração do tegumento. É usado em cisticercose com cistos viáveis, teníase e esquistossomose. Em cistos calcificados, o tratamento foca no controle das crises com anticonvulsivantes."
  }
];

const state = {
  current: 0,
  answers: new Array(questions.length).fill(null),
  hintsShown: new Array(questions.length).fill(false)
};

function render() {
  const container = document.getElementById('quizContainer');
  let html = '';

  questions.forEach((q, i) => {
    const isActive = i === state.current;
    html += `<div class="question-card${isActive ? ' active' : ''}" id="q${i}">
      <span class="q-number">Questão ${i + 1} de ${questions.length}</span>
      <p class="q-text">${q.text}</p>
      <div class="options">
        ${q.options.map((opt, j) => {
          const letters = ['A','B','C','D'];
          let cls = 'option-btn';
          if (state.answers[i] !== null) {
            cls += ' disabled';
            if (j === q.correct) cls += ' correct';
            else if (j === state.answers[i] && j !== q.correct) cls += ' wrong';
          }
          return `<button class="${cls}" onclick="answer(${i},${j})" ${state.answers[i] !== null ? 'disabled' : ''}>
            <span class="letter">${letters[j]}</span>
            <span>${opt}</span>
          </button>`;
        }).join('')}
      </div>
      <button class="hint-btn" onclick="toggleHint(${i})" ${state.answers[i] !== null ? 'style="display:none"' : ''}>💡 Mostrar dica</button>
      <div class="hint-box${state.hintsShown[i] ? ' show' : ''}" id="hint${i}">💡 ${q.hint}</div>
      <div class="explanation${state.answers[i] !== null ? ' show' : ''}" id="exp${i}">
        <div class="exp-title">${state.answers[i] === q.correct ? '✅ Correto!' : state.answers[i] !== null ? '❌ Incorreto' : ''} Explicação</div>
        ${q.explanation}
      </div>
      <div class="nav-buttons">
        ${i > 0 ? `<button class="nav-btn prev" onclick="go(${i - 1})">← Anterior</button>` : '<div></div>'}
        <span class="counter">${i + 1} / ${questions.length}</span>
        ${i < questions.length - 1
          ? `<button class="nav-btn next" onclick="go(${i + 1})">Próxima →</button>`
          : `<button class="nav-btn next" onclick="showResults()">Ver Resultado 🎯</button>`
        }
      </div>
    </div>`;
  });

  // Results card
  const answered = state.answers.filter(a => a !== null).length;
  const correct = state.answers.filter((a, i) => a === questions[i].correct).length;
  const pct = answered > 0 ? Math.round((correct / questions.length) * 100) : 0;
  let emoji, msg, msgClass;
  if (pct >= 90) { emoji = '🏆🎉'; msg = 'Incrível! Você arrasou! Domina parasitologia!'; msgClass = 'great'; }
  else if (pct >= 80) { emoji = '🌟😄'; msg = 'Muito bem! Você foi excelente!'; msgClass = 'great'; }
  else if (pct >= 60) { emoji = '💪📚'; msg = 'Bom trabalho! Revise alguns tópicos e ficará perfeito!'; msgClass = 'ok'; }
  else if (pct >= 40) { emoji = '📖🧐'; msg = 'Não desanime! Revise o conteúdo e tente novamente!'; msgClass = 'low'; }
  else { emoji = '🤗💕'; msg = 'Que pena, mas não tem problema! Estude mais e volte mais forte!'; msgClass = 'low'; }

  html += `<div class="results-card" id="results">
    <div class="results-emoji">${emoji}</div>
    <div class="results-title">Resultado Final</div>
    <div class="results-score">${pct}%</div>
    <div class="results-detail">Você acertou <strong>${correct}</strong> de <strong>${questions.length}</strong> questões</div>
    <div class="results-message ${msgClass}">${msg}</div>
    <br>
    <button class="restart-btn" onclick="restart()">🔄 Refazer Quiz</button>
    <br><br>
    <button class="nav-btn prev" onclick="reviewAnswers()" style="margin:0 auto">📋 Revisar Respostas</button>
  </div>`;

  container.innerHTML = html;
  updateProgress();
}

function answer(qi, oi) {
  if (state.answers[qi] !== null) return;
  state.answers[qi] = oi;
  render();
  // scroll to explanation
  const exp = document.getElementById(`exp${qi}`);
  if (exp) setTimeout(() => exp.scrollIntoView({ behavior: 'smooth', block: 'nearest' }), 100);
}

function toggleHint(qi) {
  state.hintsShown[qi] = !state.hintsShown[qi];
  const box = document.getElementById(`hint${qi}`);
  if (box) box.classList.toggle('show');
}

function go(idx) {
  state.current = idx;
  render();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function showResults() {
  // hide all questions, show results
  document.querySelectorAll('.question-card').forEach(c => c.classList.remove('active'));
  const r = document.getElementById('results');
  if (r) { r.classList.add('active'); r.style.display = 'block'; }
  state.current = -1;
  updateProgress();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function reviewAnswers() {
  state.current = 0;
  render();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function restart() {
  state.current = 0;
  state.answers.fill(null);
  state.hintsShown.fill(false);
  render();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function updateProgress() {
  const answered = state.answers.filter(a => a !== null).length;
  const pct = (answered / questions.length) * 100;
  document.getElementById('progressBar').style.width = pct + '%';
}

render();
</script>
</body>
</html>
