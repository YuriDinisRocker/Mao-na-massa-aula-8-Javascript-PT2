# Mao-na-massa-aula-8-Javascript-PT2

Vamos agora fazer a busca pelo o que o usuário digitou no campoFiltro. Se bater com o nome de algum paciente, vamos exibí-lo, caso contrário vamos continuar deixando-o escondido:

1- O primeiro passo é conseguir extrair o nome de cada paciente para comparar o valor do campoFiltro (this.value). Vamos buscar o nome de dentro da <tr> como já fizemos diversas vezes anteriormente:


          var campoFiltro = document.querySelector("#filtrar-tabela");

          campoFiltro.addEventListener("input", function() {
              var pacientes = document.querySelectorAll(".paciente");

              if (this.value.length > 0) {
                  for (var i = 0; i < pacientes.length; i++) {
                      var paciente = pacientes[i];
                      //Adição aqui
                      var tdNome = paciente.querySelector(".info-nome");
                      var nome = tdNome.textContent;


                      paciente.classList.add("invisivel");    
                  }
              } else {
                  for (var i = 0; i < pacientes.length; i++) {
                      var paciente = pacientes[i];
                      paciente.classList.remove("invisivel");
                  }
              }
          });
      
      
2- Agora precisamos comparar o que o usuário digitou com o nome de cada um dos pacientes. Vimos uma ferramenta muito poderosa para comparar textos que é Expressão Regular, que nos permite comparar até mesmo parte de textos, com por exemplo achar a palavra "Pedro", buscando apenas por "Ped".

Como queremos que a nossa Expressão Regular busque pelo o que o usuário digitou , vamos criar um nova expressão com este parâmetro:

      var campoFiltro = document.querySelector("#filtrar-tabela");

      campoFiltro.addEventListener("input", function() {
          var pacientes = document.querySelectorAll(".paciente");

          if (this.value.length > 0) {
              for (var i = 0; i < pacientes.length; i++) {
                  var paciente = pacientes[i];
                  var tdNome = paciente.querySelector(".info-nome");
                  var nome = tdNome.textContent;

                  //Adição aqui
                  var expressao = new RegExp(this.value, "i");

                  paciente.classList.add("invisivel");    
              }
          } else {
              for (var i = 0; i < pacientes.length; i++) {
                  var paciente = pacientes[i];
                  paciente.classList.remove("invisivel");
              }
          }
      });
      
      
O modificador "i" é para indicar que estamos buscando por case-insensitive, ou seja tanto "Pa" quanto "pa" achariam a palavra "Paulo", ele não liga para a diferença entre maísuculas e minúsculas.

3- Com a expressão regular em mãos, só precisamos pedir para ela testar se o nome do usuário bate com o que foi digitado. Para isto, vamos utilizar sua função .test, que em caso positivo deve exibir o paciente removendo a sua classe invisivel, e em caso negativo deve esconder o paciente adicionando a classe invisivel :

    var campoFiltro = document.querySelector("#filtrar-tabela");

    campoFiltro.addEventListener("input", function() {
        var pacientes = document.querySelectorAll(".paciente");

        if (this.value.length > 0) {
            for (var i = 0; i < pacientes.length; i++) {
                var paciente = pacientes[i];
                var tdNome = paciente.querySelector(".info-nome");
                var nome = tdNome.textContent;
                var expressao = new RegExp(this.value, "i");

                // Adição aqui
                if (expressao.test(nome)) {
                    paciente.classList.remove("invisivel");
                } else {
                    paciente.classList.add("invisivel");
                }
            }
        } else {
            for (var i = 0; i < pacientes.length; i++) {
                var paciente = pacientes[i];
                paciente.classList.remove("invisivel");
            }
        }
    });
