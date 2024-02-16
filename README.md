# calc
function calculator(userInput) {
  userInput = userInput.trim();

  let parts = userInput.split(' ');
  if (parts.length !== 3) {
      throw new Error("Введите корректное выражение!");
  }

  let num1 = parts[0];
  let math = parts[1];
  let num2 = parts[2];

  let operand1;
  let operand2;
  let result;

  const arabNum = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10"];
  const romeNum = ["I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X", "XL", "L", "C"];

  const convertRomanToArab = {
      I: 1, II: 2, III: 3, IV: 4, V: 5, VI: 6, VII: 7, VIII: 8, IX: 9, X: 10, XL: 40, L: 50, C: 100,
  };

  const convertArabToRoman = {
      1: "I", 2: "II", 3: "III", 4: "IV", 5: "V", 6: "VI", 7: "VII", 8: "VIII", 9: "IX", 10: "X", 40: "XL", 50: "L", 100: "C",
  };

  // Функция для проверки является ли строка римским числом
  function isRomanNum(input) {
      return romeNum.includes(input);
  }

  // Функция для преобразования римских чисел в арабские
  function romanToArabic(input) {
      return convertRomanToArab[input];
  }

  // Функция для преобразования арабских чисел в римские
  function arabicToRoman(input) {
      let result = "";

      for (let i = romeNum.length - 1; i >= 0; i--) {
          while (input >= convertRomanToArab[romeNum[i]]) {
              result += romeNum[i];
              input -= convertRomanToArab[romeNum[i]];
          }
      }

      return result;
  }

  // Преобразование чисел в числовой формат
  if (isRomanNum(num1) && isRomanNum(num2)) {
      operand1 = romanToArabic(num1);
      operand2 = romanToArabic(num2);
  } else if (arabNum.includes(num1) && arabNum.includes(num2)) {
      operand1 = Number(num1);
      operand2 = Number(num2);
  } else {
      throw new Error("Введите корректные числа одного типа!");
  }

  // Выполнение математической операции
  switch (math) {
      case "+":
          result = operand1 + operand2;
          break;
      case "-":
          result = operand1 - operand2;
          break;
      case "*":
          result = operand1 * operand2;
          break;
      case "/":
          result = Math.floor(operand1 / operand2); // Округление результата вниз при делении
          break;
      default:
          throw new Error("Введите корректный знак операции (+, -, *, /)!");
  }

  // Если операнды изначально римские числа, конвертируем результат в римское число
  if (isRomanNum(num1) && isRomanNum(num2)) {
      if (result <= 0) {
          return "";
      } else {
          result = arabicToRoman(result);
      }
  }

  // Отображение результата
  return String(result);
}
