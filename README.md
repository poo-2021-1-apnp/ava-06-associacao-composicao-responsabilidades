# Avaliação 06 Associação, Composição e Responsabilidades.

Link do Classroom: <https://classroom.github.com/a/rvkCD7Om>

[O treinamento cruel de Pai Mei](https://youtu.be/JOCe0isg_1E)


## Implementar e testar segundo as especificações

- Esta atividade é avaliada com esforço estimado entre 6 e 12h.
- Os Casos de Teste podem ser corrigidos se estiverem mal escritos, mas **a especificação dos objetos não pode ser alterada**.
- E, por fim, assegure-se de **assistir as videoaulas antes de começar**, pois lá estão explicados todos os conceitos e práticas presentes nesta atividade.


### Implementar Sistema Eventos/Atividades

Implementar conforme os Casos de Teste a seguir:

```java
// Eventos tem um nome, cidade, tipo e ano
// tipo é um enum públic declarado dentro da classe Evento
Evento ev1 = new Evento("Semana Acadêmica IFRS", "Rio Grande", Evento.Tipo.Semana, 2020);

// atividades tem vagas e carga horária opcionais
// tipo é um enum público declarado dentro da classe Atividade
Atividade atv1 = ev1.novaAtividade("Seminário TCCs TADS", 40, Atividade.Tipo.Seminario);
Atividade atv2 = ev1.novaAtividade("Minicurso ECMA6", 20, 8, Atividade.Tipo.Minicurso);

// dados do evento
System.out.println(ev1.getNome().equals("Semana Acadêmica IFRS"));
System.out.println(ev1.getTipo().equals(Evento.Tipo.Semana));
System.out.println(ev1.getCidade().equals("Rio Grande"));
System.out.println(ev1.getAno() == 2020);

// evento tem atividades
ArrayList<Atividade> atvs = ev1.getAtividades();
System.out.println(atvs.size() == 2);
System.out.println(atvs.get(0).equals(atv1));
System.out.println(atvs.get(1).equals(atv2));

// método para obter atividades pela ordem de inserção
System.out.println(atvs.getAtividade(1).equals(atv1));
System.out.println(atvs.getAtividade(2).equals(atv2));

// dados das atividades
System.out.println(atv1.getDescricao().equals("Seminário TCCs TADS"));
System.out.println(atv1.getVagas() == 40);
System.out.println(atv1.getTipo().equals(Atividade.Tipo.Seminario));
System.out.println(atv1.getAno() == 2020); // mesmo do evento

// o minicurso tem carga horária
System.out.println(atv2.getDescricao().equals("Minicurso ECMA6"));
System.out.println(atv2.getVagas() == 20);
System.out.println(atv2.getHoras() == 8);
System.out.println(atv2.getTipo().equals(Atividade.Tipo.Minicurso));

// atividades pertencem a um evento
System.out.println(atv1.getEvento().equals(ev1));
System.out.println(atv2.getEvento().equals(ev1));

// outros tipo de eventos e atividades
Evento ev2 = new Evento("Escola Regional de Banco de Dados", "Bagé", Evento.Tipo.Escola, 2021);
Atividade atv3 = ev2.novaAtividade("BigData com Apache Hadoop", "Paulo Silva", 20, 4, Atividade.Tipo.Oficina);
Atividade atv4 = ev2.novaAtividade("Data Science: uma introdução", "Maria Santos", Atividade.Tipo.Palestra);

// dados da atividade:
System.out.println(atv3.getDescricao().equals("BigData com Apache Hadoop"));
System.out.println(atv3.getMinistrante().equals("Paulo Silva"));
System.out.println(atv3.getVagas() == 20);
System.out.println(atv3.getHoras() == 4);
System.out.println(atv3.getTipo().equals(Atividade.Tipo.Oficina));
System.out.println(atv3.getAno() == 2021);

// um evento que abriga (tem) outros eventos:
Evento ev3 = new Evento("3º Salão de Pesquisa, Extensão e Ensino do IFRS", "Bento Gonçalves", Evento.Tipo.Salao, 2022);
EventoSatelite sat1 = ev3.novoEventoSatelite("7º Seminário de Iniciação Científica e Tecnológica (SICT)", Evento.Tipo.Seminario);
EventoSatelite sat2 = ev3.novoEventoSatelite("5º Seminário de Educação Profissional e Tecnológica (SEMEPT)", Evento.Tipo.Seminario);
EventoSatelite sat3 = ev3.novoEventoSatelite("Mostra de Arte e Cultura", Evento.Tipo.Mostra);

// eventos satélite são da mesma cidade do evento central
System.out.println(ev3.getCidade().equals("Bento Gonçalves"));
System.out.println(sat1.getCidade().equals(ev3.getCidade()));
System.out.println(sat1.getCidade().equals("Bento Gonçalves"));

// eventos satélites pertencem a um evento central
System.out.println(sat1.getEventoCentral().equals(ev3));

// satelites
System.out.println(ev3.getEventosSatelites().size() == 3);
System.out.println(ev3.getEventoSatelite(1).equals(sat1));
System.out.println(ev3.getEventoSatelite(2).equals(sat2));
System.out.println(ev3.getEventoSatelite(3).equals(sat3));

// inscrição nas atividades:
System.out.println(atv1.getVagas() == 40);
System.out.println(atv1.getVagasRemanescentes() == 40);

Inscrito insc1 = atv1.inscrever("Jean-Luc Picard");
Inscrito insc2 = atv1.inscrever("Worf");

// inscritos tem nome
System.out.println(insc1.getNome().equals("Jean-Luc Picard"));
System.out.println(insc2.toString().equals("Worf"));

// as vagas decrescem
System.out.println(atv1.getVagasRemanescentes() == 38);

// a inscrição tem uma chave no formato AAAAAAAAAAAAAAAA até ZZZZZZZZZZZZZZZZ
// aleatória, como: AGGASCFFEERERRER
Chave insc1chave = insc1.getChave();
System.out.println(insc1.getChave().toString().length() == 16);

// verificando se a chave está segundo as regras:
for (int i = 0; i < insc1chave.toString().length(); i++) {
  char c = insc1.getChave().toString().charAt(i);
  System.out.println(c >= 65 && c <= 90); // A~Z
}

// as chaves não podem ser as mesmas, cada inscrito deve ter uma chave única
System.out.println(insc1.getChave().equals(insc2.getChave()) == false);

// por padrão cada inscrito não concluiu a atividade
System.out.println(insc1.isConcluido() == false); // foi ao evento/atividade?

// a atvidade tem inscritos
ArrayList<Inscrito> inscritos = atv1.getInscritos();
System.out.println(inscritos.get(0).equals(insc1));
System.out.println(inscritos.get(1).equals(insc2));
System.out.println(atv1.getInscrito(2).isConcluido() == false);

// que confirmam presença (chamada)
insc1.confirmarPresenca(); // marcar como concluído
System.out.println(insc1.isConcluido() == true);
System.out.println(atv1.getInscrito(1).isConcluido() == true);
System.out.println(atv1.getInscrito(2).isConcluido() == false);
atv1.getInscrito(2).confirmarPresenca();
System.out.println(atv1.getInscrito(2).isConcluido() == true);

// inscrevendo 38 klingons
for (int i = 0; i < 38; i++) atv1.inscrever("Klingon #" + i);

// atividade sem vagas abertas
System.out.println(atv1.getVagasRemanescentes() == 0);

// não é possível inscrever-se
try {
  atv1.inscrever("Data");
  System.out.println(false); // esta linha não deve ser executada
} catch (NaoHaVagaException e) { // criar esta classe NaoHaVagaException extends RuntimeException
  System.err.println(true + " " + e); // Não há mais vagas!
}

// eventos satélite permitem inscrição
sat1.inscrever("Geordi Laforge");

// eles não tem limite de inscritos
// e tem todas as propriedades que um inscrito em atividade
System.out.println(sat1.getInscrito(1).getNome().equals("Geordi Laforge"));
Inscrito insc3 = sat1.getInscrito(1);
Chave chave3 = insc3.getChave();
System.out.println(insc3 != null);
System.out.println(chave3 != null);
System.out.println(sat1.getQuantidadeInscritos() == 1);
// esta atividade não tem limite de vagas nem carga horária
System.out.println(atv4.getVagas() == 0);
System.out.println(atv4.getHoras() == 0);
System.out.println(atv4.getVagasRemanescentes() == 0);
System.out.println(atv4.getTipo().equals(Atividade.Tipo.Palestra));
// então não há limite de inscrições
atv4.inscrever("Beverly Crusher");
atv4.inscrever("Deanna Troi");
System.out.println(atv4.getInscritos().size() == 2);
System.out.println(atv4.getQuantidadeInscritos() == 2);
```

### Desenhar o Diagrama de Classes do Sistema Eventos/Atividades

Com base nas classes anteriores efetua a engenharia reversa e desenhe o diagrama de classes, com atributos e associações, esclarecendo quais seriam as agregações e composições.

### Sistema Torneio/Campeonato de &lt;sua escolha&gt;

Imagine um sistema de torneio ou campeonato. Pode ser de esportes, e-sports ou outro. Modele o domínio, descobrindo as classes conceituais. Numa cópia adicione as associações e atributos. Na última cópia adicione os comportamentos/métodos. **Não é obrigatório implementar**. Mas _considere_.

- - -

> A good programmer looks both ways before crossing a one-way street.
>
> -- Unknown
