# My-smallest-code-interpreter-aka-Brainf-k-

           function balancedBrackets(str) {
            var brackets = str.split('').filter(x => (x === '[') || (x === ']')).join('');
            if (brackets == '') return true;
            var stack = [];
            for (var i = 0; i < brackets.length; i++) {
              if ((brackets[i] === ']') && (stack == '')) return false;
              if (brackets[i] === '[') stack.push('[')
              else if (brackets[i] === ']') stack.pop(']');
            }
            if (stack == '') return true;	
            return false
          }

          function brainLuck(code, input){
            if (balancedBrackets(code) === false) return "Brackets are unbalanced"
            var output = "";
            var byte_array = [0];
            var ba_ind = 0;
            var inp_ind = 0;
            var k = 0;
            for (var i = 0; i < code.length; i++) {
              switch(code[i]) {

                case '>' :
                  ba_ind++
                  if (byte_array[ba_ind] === undefined) byte_array[ba_ind] = 0;

                  break;

                case '<' :
                  ba_ind--
                  if (byte_array[ba_ind] === undefined) {
                    byte_array.unshift(0);
                    ba_ind++					
                  }

                  break;

                case '+' :
                  byte_array[ba_ind]++;
                  byte_array[ba_ind] %= 256;

                  break;

                case '-' :
                  byte_array[ba_ind]--
                  if (byte_array[ba_ind] == -1) byte_array[ba_ind] = 255;

                  break;

                case '.' :
                  output += String.fromCharCode(byte_array[ba_ind])
                  break;

                case ',' :
                  byte_array[ba_ind] = input.charCodeAt(inp_ind);
                  inp_ind++
                  break;

                case '[' :
                  if (byte_array[ba_ind] == 0) {
                    k = 0;
                    while (true) {
                      i++;
                      if ((code[i] === ']') && (k == 0)) break;
                      if (code[i] === '[') k++
                      else if (code[i] === ']') k--;
                    }
                  }
                  break;

                case ']' :
                  if (byte_array[ba_ind] !== 0) {
                    k = 0;
                    while (true) {
                      i--;
                      if ((code[i] === '[') && (k == 0)) break;
                      if (code[i] === ']') k++
                      else if (code[i] === '[') k--;
                    }
                  }

                  break;
              }
            }


            return output
          }
