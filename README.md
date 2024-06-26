<!DOCTYPE html>
<!--
Nome: Beatriz Macedo da Silva         Turma: 3°B
Nome: Daniel Lozano Borges Pires                                              
Nome: Kaua Henrique Viera                                       
Nome: Isabelle Carvalho Salun                                  
Nome: Vinícius Arnaut Mariano                                      -->
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Verificar Números Primos</title>
    <script>
        // Array para armazenar os números primos encontrados
        var primosEncontrados = [];
        
        // Função para receber o número digitado e mostrar os números primos no canvas
        function recebeNumero() {
            // Obter o elemento canvas
            var canvas = document.getElementById('meuCanvas');
            if (canvas.getContext) {
                // Obter o contexto de desenho 2D do canvas
                var cntxt = canvas.getContext('2d');
                // Largura máxima para os números no canvas
                var maxWidth = 1250;
                // Altura da linha de texto
                var lineHeight = 35;
                // Posição inicial x para desenhar os números
                var x = (canvas.width - maxWidth) / 2;
                // Posição inicial y para desenhar os números
                var y = 40;
                // Gradiente para estilo de preenchimento
                var grad = cntxt.createLinearGradient(0, 0, canvas.width, 0);
                grad.addColorStop(0, "rgb(255, 0, 0)");
                grad.addColorStop(0.5, "rgb(255, 255, 255)");
                grad.addColorStop(1, "rgb(0, 0, 0)");
                // Estilo da fonte para os números
                cntxt.font = "30px Arial";

                // Obter o número digitado pelo usuário
                var N = parseInt(document.getElementById("Numero1").value, 10);
                // Limpar o canvas
                cntxt.fillStyle = "rgb(255, 255, 255)";
                cntxt.fillRect(0, 0, canvas.width, canvas.height);
                cntxt.fillStyle = grad;
                // Chamar função para mostrar os números primos
                mostraPrimos(cntxt, N, x, y, maxWidth);
            }
        }

        // Função para calcular e mostrar os números primos no canvas
        function mostraPrimos(cntxt, N, x, y, maxWidth) {
            let num = 2; // Começar com o primeiro número primo
            let line = ''; // String para armazenar os números a serem desenhados na linha atual
            while (primosEncontrados.length < N) {
                let primo = true;
                // Verificar se o número é primo
                for (let i = 2; i < num; i++) {
                    if (num % i === 0) {
                        primo = false;
                        break;
                    }
                }
                if (primo) {
                    // Se for primo, adicionar ao array de números primos encontrados
                    primosEncontrados.push(num);
                    let textoPrimo = num.toString();
                    let width = cntxt.measureText(line + textoPrimo).width;
                    // Verificar se a largura excede o limite máximo
                    if (width > maxWidth) {
                        // Se sim, desenhar a linha atual e passar para a próxima linha
                        cntxt.fillText(line, x, y);
                        cntxt.strokeText(line, x, y);
                        y += 35; // Passar para a próxima linha
                        line = ''; // Limpar a linha atual
                    }
                    // Adicionar o número à linha atual
                    line += textoPrimo + ', ';
                }
                num++; // Passar para o próximo número
            }
            // Desenhar a última linha, se houver números restantes
            if (line !== '') {
                cntxt.fillText(line, x, y);
                cntxt.strokeText(line, x, y);
            }
            // Limpar a entrada de texto
            document.getElementById("Numero1").value = "";
            // Colocar o foco de volta no campo de entrada
            document.getElementById("Numero1").focus();
            
         }
    </script>
</head>
<body>
<div>
    <!-- Título -->
    <h1>Números Primos</h1>
    <!-- Campo de entrada para o usuário digitar a quantidade de números primos -->
    <label style="font-size: 20px;">Digite a Quantidade de Números Primos</label>
    <input type="text" id="Numero1" autofocus><br>
    <!-- Botão para acionar a função que mostra os números primos -->
    <button onclick="recebeNumero()">Mostrar Números Primos</button><br><br>
    <!-- Canvas para desenhar os números primos -->
    <canvas id="meuCanvas" width="1350" height="465" style="border:1px solid #000000; background-color: white;"></canvas>
</div>
</body>
</html>