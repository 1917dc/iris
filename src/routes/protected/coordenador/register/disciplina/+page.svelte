<script lang="ts">

</script>

<svelte:head>
    <title>Cadastro - Disciplina</title>
</svelte:head>
<div class="justify-center">
    <div class="prose m-auto select-none">
        <h1 class="text-center text-primary mt-20">Cadastro de Disciplina</h1>
        <form method="post" action="?/register" class="form-control">
            <div class="m-3">
                <label class="label-text" for="subjectName">Nome da Disciplina</label>
                <label class="input input-bordered flex items-center gap-2">
                    <input
                            name="subjectName"
                            type="text"
                            class="grow"
                            placeholder="Matemática, Física, Português"
                            spellcheck="false"
                            autocomplete="off"
                    />
                </label>
            </div>

            <div class="m-3">
                <label class="label-text" for="professor">Professor</label>
                <label class="input input-bordered flex items-center gap-2">
                    <input
                            name="professor"
                            type="text"
                            class="grow"
                            placeholder="João Alcântara"
                            spellcheck="false"
                            autocomplete="off"
                    />
                </label>
            </div>

            <div class="m-3">
                <label class="label-text" for="classNumber">Séria/Turma</label>
                <label class="input input-bordered flex items-center gap-2">
                    <input
                            name="classNumber"
                            type="text"
                            class="grow"
                            placeholder="3º ano"
                            spellcheck="false"
                            autocomplete="off"
                    />
                </label>
            </div>

            <div class="m-3">
                <label class="label-text" for="credits">Horas por semana</label>
                <label class="input input-bordered flex items-center gap-2">
                    <input
                            name="credits"
                            type="number"
                            min="1"
                            max="10"
                            class="grow"
                            placeholder="2 horas por semana"
                            spellcheck="false"
                    />
                </label>
            </div>

            <div class="m-3">
                <label class="label-text" for="semester">Ano letivo</label>
                <label class="input input-bordered flex items-center gap-2">
                    <input
                            name="semester"
                            type="text"
                            class="grow"
                            placeholder="2025"
                            spellcheck="false"
                            autocomplete="off"
                    />
                </label>
            </div>

            <button class="btn btn-primary m-10" type="submit">
                Registrar Disciplina
            </button>
        </form>

        <dialog id="modal_confirm" class="modal">
            <div class="modal-box prose">
                <h1 class="text-lg font-black">Aviso:</h1>
                <p class="font">
                    Ao confirmar esse diálogo, as alterações serão enviadas, verifique se
                    os dados estão realmente corretos.
                </p>
                <div class="modal-action">
                    <form method="dialog">
                        <button class="btn btn-success">
                            Confirmar
                        </button>
                        <button class="btn btn-error">
                            Cancelar
                        </button>
                    </form>
                </div>
            </div>
        </dialog>
    </div>
</div>
