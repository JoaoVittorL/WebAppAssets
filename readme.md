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

Agora será listado os items que são mais usados para manipulação dentro do webApp.
Como inserir elementos de forma dinâmica em um select no HTML ?

```javascript
function getFornecedores() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var setorSheet = ss.getSheetByName("DADOS");
  let data = setorSheet
    .getRange("F2:F")
    .getValues()
    .filter((item) => {
      if (item[0] !== "") {
        return item;
      }
    });

  let newArr = data.map((item) => item[0]);
  let unique = [];
  newArr.map((r) => {
    if (unique.indexOf(r) === -1) {
      unique.push(r);
    }
  });

  let sortedUnique = unique.sort((a, b) => a.localeCompare(b));
  return sortedUnique;
}
let fornecedores = getFornecedores()
  .map((item) => "<option value='" + item + "'> " + item + "</option>")
  .join("");
```

Para fazer essa inclusão devemos buscar na planilha os dados que queremos e inserir como option.
Após isso insira no HTML dessa forma:

```html
<label>Fornecedor</label>
<select>
  <option value="Escolha" selected>Escolha</option>
  <?!= fornecedores ?>
</select>
```

Para realizar autocomplete de forma simples no WebApp.
Bibliotecas necessárias para implantação.

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.6.1/css/bootstrap.min.css"
/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.js"></script>
```

```javascript
function getPlate() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var statesSheet = ss.getSheetByName("DADOS");
  let values = statesSheet
    .getRange("J2:J")
    .getValues()
    .filter((item) => item[0] != "");
  return values;
}
```

Dentro do "script" insira essa função que busca os dados do "servidor".

```javascript
$(document).ready(function () {
  getPlate();
});

function getPlate() {
  google.script.run
    .withSuccessHandler(function (ar) {
      statesArray = [];
      ar.forEach(function (item, index) {
        statesArray.push(item[0]);
      });
      $(".autocompletePlate").autocomplete({
        source: statesArray,
        minLength: 2,
      });
    })
    .getPlate();
}
```

Para enviar, buscar ou validar os dados uso essa função como padrão.
Basicamente no lado do "servidor" vou ter uma função enviarValidarBuscar(item) que vai receber o item e manipular de alguma forma...

```javascript
google.script.run
  .withSuccessHandler(function (resposta) {
    //Aqui a resposta da função é recebida console.log(resposta)
    //Depende é claro do return da função
  })
  .enviarValidarBuscar(item);
```
