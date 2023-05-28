Este código é referente à validação de CPF, mas pode ser usado para outras validações seguindo os mesmos padrões.

```javascript
function validationCpfForSearch() {
  const regex = /[.,:\/]/;
  const letraNull = /^\d+$/;
  let CPF = document.getElementById("CPF").value;

  if (CPF == "") {
    alert("Input vazio.");
  } else if (!letraNull.test(CPF) || regex.test(CPF)) {
    alert("Permito somente números.");
  } else if (CPF.length != 11) {
    alert("Valor menor que os dígitos especificados.");
  } else {
    alert("Verificações foram validadas...");
  }
}
```

Para tratar erros, os modais são utilizados e serão integrados por meio de funções.

A função "ShowModal" aplicará a classe "Show" e removerá a classe "Hide" de cada item, enquanto a função "hide" fará o contrário.

Para que o efeito do modal esteja completo, incluo no modal um botão "Voltar" com uma função específica para cada modal, como por exemplo "hiddenModalInputCpfNull()".

```javascript
let modal_input_cpf_null = document.getElementById('modal-input-cpf-null')

<div id="modal-input-cpf-null" class="default-div-modal-alert hide">
  <p class="default-p-modal-alert"> Para prosseguir, por favor, preencha o campo CPF.</p>
  <button class="default-button-modal-alert" onclick="hiddenModalInputCpfNull()">voltar</button>
</div>;

if (CPF == "") {
  showModal(modal_input_cpf_null);
  hideModal(container);
}

function showModal(modal) {
  modal.classList.remove("hide");
  modal.classList.add("show");
}

function hideModal(modal) {
  modal.classList.remove("show");
  modal.classList.add("hide");
}

function hiddenModalInputCpfNull(){
   hideModal(modal_input_cpf_null)
   showModal(container)
}
```
