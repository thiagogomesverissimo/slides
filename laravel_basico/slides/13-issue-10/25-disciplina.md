Mostrar as turmas, no show da disciplina:

    @foreach ($disciplina->turmas as $turma)
        {{ $turma->ministrante }}
        {{ $turma->inicio }}
    @endforeach

<div style="color:red;">!!! teste e commit !!!</div>
