<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Aplicação Escolar</title>
  <style>
    * {
      margin: 0; padding: 0; box-sizing: border-box;
      font-family: 'Segoe UI', sans-serif;
    }
    body {
      background-color: #f2f2f2;
      padding: 20px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    nav {
      background-color: #0051a3;
      padding: 15px 30px;
      display: flex;
      justify-content: center;
      gap: 20px;
      border-radius: 8px;
      width: 100%;
      max-width: 900px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    nav button {
      background-color: #fff;
      color: #0051a3;
      border: none;
      padding: 12px 25px;
      cursor: pointer;
      font-weight: 700;
      border-radius: 6px;
      font-size: 1rem;
      transition: background-color 0.3s ease;
      box-shadow: 0 2px 5px rgba(0,81,163,0.3);
      user-select: none;
    }
    nav button:hover, nav button:focus {
      background-color: #e3e3e3;
      outline: none;
    }
    section {
      margin-top: 30px;
      background-color: #fff;
      padding: 25px 30px 40px 30px;
      border-radius: 12px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 900px;
    }
    h2, h3 {
      color: #333;
      margin-bottom: 20px;
    }
    label {
      font-weight: 600;
      margin-bottom: 6px;
      display: block;
      color: #444;
    }
    input, select, textarea, button {
      margin-bottom: 15px;
      padding: 12px 15px;
      border-radius: 7px;
      border: 1.8px solid #ccc;
      width: 100%;
      font-size: 1rem;
      transition: border-color 0.3s ease;
    }
    input:focus, select:focus, textarea:focus {
      border-color: #0051a3;
      outline: none;
      box-shadow: 0 0 6px #0051a3aa;
    }
    textarea {
      resize: vertical;
      min-height: 70px;
    }
    button {
      background-color: #0051a3;
      color: white;
      border: none;
      font-weight: 700;
      cursor: pointer;
      box-shadow: 0 4px 8px #003f82cc;
      transition: background-color 0.3s ease;
      user-select: none;
    }
    button:hover, button:focus {
      background-color: #003f82;
      outline: none;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      font-size: 0.95rem;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 12px 10px;
      text-align: left;
      vertical-align: middle;
    }
    th {
      background-color: #0051a3;
      color: white;
      font-weight: 700;
    }
    td button {
      margin-right: 7px;
      padding: 6px 12px;
      font-size: 0.9rem;
      border-radius: 5px;
      user-select: none;
      box-shadow: none;
    }
    td button.edit-btn {
      background-color: #28a745;
      box-shadow: 0 3px 6px #1e7e34cc;
    }
    td button.edit-btn:hover {
      background-color: #1e7e34;
    }
    td button.delete-btn {
      background-color: #dc3545;
      box-shadow: 0 3px 6px #a71d2ccc;
    }
    td button.delete-btn:hover {
      background-color: #a71d2c;
    }
    #dadosAluno {
      background-color: #e7f1ff;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      font-size: 1.05rem;
      color: #003f82;
      box-shadow: inset 0 0 6px #0051a3aa;
      min-height: 110px;
    }
    .msg {
      padding: 12px 15px;
      border-radius: 6px;
      margin-bottom: 15px;
      font-weight: 600;
    }
    .msg.error {
      background-color: #f8d7da;
      color: #842029;
      border: 1.5px solid #f5c2c7;
    }
    .msg.success {
      background-color: #d1e7dd;
      color: #0f5132;
      border: 1.5px solid #badbcc;
    }
    @media (max-width: 600px) {
      nav {
        flex-direction: column;
        gap: 15px;
      }
      section {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <nav>
    <button onclick="mostrarSecao('perfil')">Ver meu Perfil</button>
    <button onclick="mostrarSecao('admin')">Administração</button>
  </nav>

  <!-- Seção do Perfil do Aluno -->
  <section id="perfil" style="display: none">
    <h2>Perfil do Aluno</h2>
    <label for="cpfBusca">Digite seu CPF:</label>
    <input type="text" id="cpfBusca" placeholder="000.000.000-00" />
    <button onclick="buscarAlunoPorCPF()">Buscar</button>
    <div id="dadosAluno"></div>
  </section>

  <!-- Seção da Administração -->
  <section id="admin" style="display: none">
    <h2>Administração</h2>

    <!-- Cursos -->
    <div>
      <h3>Cursos</h3>
      <input type="hidden" id="idCursoEditando" />
      <label for="nomeCurso">Nome do curso</label>
      <input type="text" id="nomeCurso" placeholder="Ex: Informática" />
      <label for="descCurso">Descrição do curso</label>
      <textarea id="descCurso" placeholder="Descrição detalhada do curso"></textarea>
      <label for="cargaCurso">Carga Horária</label>
      <input type="text" id="cargaCurso" placeholder="Ex: 80h" />
      <button onclick="salvarCurso()">Salvar Curso</button>

      <table id="listaCursos" aria-label="Tabela de Cursos">
        <thead>
          <tr>
            <th>Nome</th>
            <th>Descrição</th>
            <th>Carga Horária</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>

    <!-- Alunos -->
    <div style="margin-top: 40px">
      <h3>Alunos</h3>
      <input type="hidden" id="idAlunoEditando" />
      <label for="nomeAluno">Nome do aluno</label>
      <input type="text" id="nomeAluno" placeholder="Nome completo" />
      <label for="cpfAluno">CPF do aluno</label>
      <input type="text" id="cpfAluno" placeholder="000.000.000-00" />
      <label for="nascimentoAluno">Data de Nascimento</label>
      <input type="date" id="nascimentoAluno" title="Data de nascimento do aluno" />
      <label for="cursoAluno">Curso</label>
      <select id="cursoAluno" aria-label="Selecione o curso">
        <option value="">Selecione um curso</option>
      </select>
      <button onclick="salvarAluno()">Salvar Aluno</button>

      <table id="listaAlunos" aria-label="Tabela de Alunos">
        <thead>
          <tr>
            <th>Nome</th>
            <th>CPF</th>
            <th>Data de Nascimento</th>
            <th>Curso</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </section>

  <script>
    let cursos = JSON.parse(localStorage.getItem("cursos") || "[]");
    let alunos = JSON.parse(localStorage.getItem("alunos") || "[]");

    function mostrarSecao(id) {
      document.getElementById("perfil").style.display = "none";
      document.getElementById("admin").style.display = "none";
      document.getElementById(id).style.display = "block";
      if (id === "admin") {
        listarCursos();
        listarAlunos();
      }
      clearMensagens();
      clearPerfil();
    }

    function salvarLocal() {
      localStorage.setItem("cursos", JSON.stringify(cursos));
      localStorage.setItem("alunos", JSON.stringify(alunos));
    }

    function mostrarMensagem(container, texto, tipo = "success") {
      container.innerHTML = `<div class="msg ${tipo}">${texto}</div>`;
      setTimeout(() => { container.innerHTML = ""; }, 3500);
    }

    // Validação simples para CPF (ex: 000.000.000-00 ou só números)
    function validarCPF(cpf) {
      const regex = /^\d{3}\.?\d{3}\.?\d{3}\-?\d{2}$/;
      return regex.test(cpf);
    }

    // Valida campos básicos no cadastro do curso
    function validarCurso(nome, carga) {
      if (!nome.trim()) return "O nome do curso é obrigatório.";
      if (!carga.trim()) return "A carga horária é obrigatória.";
      return null;
    }

    // Valida campos básicos no cadastro do aluno
    function validarAluno(nome, cpf, nascimento, curso) {
      if (!nome.trim()) return "O nome do aluno é obrigatório.";
      if (!cpf.trim()) return "O CPF do aluno é obrigatório.";
      if (!validarCPF(cpf)) return "CPF inválido. Use formato: 000.000.000-00";
      if (!nascimento.trim()) return "A data de nascimento é obrigatória.";
      if (!curso.trim()) return "Selecione um curso.";
      return null;
    }

    // CURSOS
    function salvarCurso() {
      clearMensagens();
      const id = document.getElementById("idCursoEditando").value;
      const nome = document.getElementById("nomeCurso").value;
      const desc = document.getElementById("descCurso").value;
      const carga = document.getElementById("cargaCurso").value;

      const erro = validarCurso(nome, carga);
      if (erro) {
        mostrarMensagem(document.getElementById("admin"), erro, "error");
        return;
      }

      if (id) {
        const i = cursos.findIndex(c => c.id == id);
        cursos[i] = { id: Number(id), nome, desc, carga };
      } else {
        cursos.push({ id: Date.now(), nome, desc, carga });
      }

      salvarLocal();
      limparCurso();
      listarCursos();
      mostrarMensagem(document.getElementById("admin"), "Curso salvo com sucesso!", "success");
    }

    function listarCursos() {
      const tbody = document.querySelector("#listaCursos tbody");
      const select = document.getElementById("cursoAluno");
      tbody.innerHTML = "";
      select.innerHTML = '<option value="">Selecione um curso</option>';
      cursos.forEach(curso => {
        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td>${curso.nome}</td>
          <td>${curso.desc}</td>
          <td>${curso.carga}</td>
          <td>
            <button class="edit-btn" onclick="editarCurso(${curso.id})" aria-label="Editar curso ${curso.nome}">Editar</button>
            <button class="delete-btn" onclick="removerCurso(${curso.id})" aria-label="Excluir curso ${curso.nome}">Excluir</button>
          </td>
        `;
        tbody.appendChild(tr);
        const opt = document.createElement("option");
        opt.value = curso.nome;
        opt.textContent = curso.nome;
        select.appendChild(opt);
      });
    }

    function editarCurso(id) {
      clearMensagens();
      const curso = cursos.find(c => c.id === id);
      if (!curso) return;
      document.getElementById("idCursoEditando").value = curso.id;
      document.getElementById("nomeCurso").value = curso.nome;
      document.getElementById("descCurso").value = curso.desc;
      document.getElementById("cargaCurso").value = curso.carga;
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function removerCurso(id) {
      clearMensagens();
      if (!confirm("Tem certeza que deseja excluir este curso?")) return;
      cursos = cursos.filter(c => c.id !== id);
      salvarLocal();
      listarCursos();
      mostrarMensagem(document.getElementById("admin"), "Curso excluído com sucesso!", "success");
    }

    function limparCurso() {
      document.getElementById("idCursoEditando").value = "";
      document.getElementById("nomeCurso").value = "";
      document.getElementById("descCurso").value = "";
      document.getElementById("cargaCurso").value = "";
    }

    // ALUNOS
    function salvarAluno() {
      clearMensagens();
      const id = document.getElementById("idAlunoEditando").value;
      const nome = document.getElementById("nomeAluno").value;
      const cpf = document.getElementById("cpfAluno").value;
      const nascimento = document.getElementById("nascimentoAluno").value;
      const curso = document.getElementById("cursoAluno").value;

      const erro = validarAluno(nome, cpf, nascimento, curso);
      if (erro) {
        mostrarMensagem(document.getElementById("admin"), erro, "error");
        return;
      }

      if (id) {
        const i = alunos.findIndex(a => a.id == id);
        alunos[i] = { id: Number(id), nome, cpf, nascimento, curso };
      } else {
        alunos.push({ id: Date.now(), nome, cpf, nascimento, curso });
      }

      salvarLocal();
      limparAluno();
      listarAlunos();
      mostrarMensagem(document.getElementById("admin"), "Aluno salvo com sucesso!", "success");
    }

    function listarAlunos() {
      const tbody = document.querySelector("#listaAlunos tbody");
      tbody.innerHTML = "";
      alunos.forEach(aluno => {
        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td>${aluno.nome}</td>
          <td>${aluno.cpf}</td>
          <td>${aluno.nascimento}</td>
          <td>${aluno.curso}</td>
          <td>
            <button class="edit-btn" onclick="editarAluno(${aluno.id})" aria-label="Editar aluno ${aluno.nome}">Editar</button>
            <button class="delete-btn" onclick="removerAluno(${aluno.id})" aria-label="Excluir aluno ${aluno.nome}">Excluir</button>
          </td>
        `;
        tbody.appendChild(tr);
      });
    }

    function editarAluno(id) {
      clearMensagens();
      const aluno = alunos.find(a => a.id === id);
      if (!aluno) return;
      document.getElementById("idAlunoEditando").value = aluno.id;
      document.getElementById("nomeAluno").value = aluno.nome;
      document.getElementById("cpfAluno").value = aluno.cpf;
      document.getElementById("nascimentoAluno").value = aluno.nascimento;
      document.getElementById("cursoAluno").value = aluno.curso;
      window.scrollTo({ top: document.getElementById("admin").offsetTop, behavior: "smooth" });
    }

    function removerAluno(id) {
      clearMensagens();
      if (!confirm("Tem certeza que deseja excluir este aluno?")) return;
      alunos = alunos.filter(a => a.id !== id);
      salvarLocal();
      listarAlunos();
      mostrarMensagem(document.getElementById("admin"), "Aluno excluído com sucesso!", "success");
    }

    function limparAluno() {
      document.getElementById("idAlunoEditando").value = "";
      document.getElementById("nomeAluno").value = "";
      document.getElementById("cpfAluno").value = "";
      document.getElementById("nascimentoAluno").value = "";
      document.getElementById("cursoAluno").value = "";
    }

    // PERFIL ALUNO
    function buscarAlunoPorCPF() {
      clearPerfil();
      const cpf = document.getElementById("cpfBusca").value.trim();
      const div = document.getElementById("dadosAluno");
      if (!cpf) {
        mostrarMensagem(div, "Por favor, digite o CPF.", "error");
        return;
      }
      const aluno = alunos.find(a => a.cpf === cpf);
      if (aluno) {
        div.innerHTML = `
          <p><strong>Nome:</strong> ${aluno.nome}</p>
          <p><strong>CPF:</strong> ${aluno.cpf}</p>
          <p><strong>Data de Nascimento:</strong> ${aluno.nascimento}</p>
          <p><strong>Curso:</strong> ${aluno.curso}</p>
        `;
      } else {
        mostrarMensagem(div, "Aluno não encontrado.", "error");
      }
    }

    function clearPerfil() {
      document.getElementById("dadosAluno").innerHTML = "";
    }

    function clearMensagens() {
      const adminSection = document.getElementById("admin");
      const perfilSection = document.getElementById("dadosAluno");
      if (adminSection) adminSection.querySelectorAll(".msg").forEach(el => el.remove());
      if (perfilSection) perfilSection.innerHTML = "";
    }

    // Inicializa mostrando perfil
    mostrarSecao("perfil");
  </script>
</body>
</html>
