import re

def num_to_words(n):
    d = {'0':'ноль','1':'один','2':'два','3':'три','4':'четыре','5':'пять','6':'шесть','7':'семь','8':'восемь','9':'девять'}
    return '-'.join([d[x] for x in str(n)])

# Просто: читаем файл, используем regex для поиска всех подходящих лексем
with open('D:/input.txt') as f:
    text = f.read()

# Находим все слова из 4+ шестнадцатеричных символов подряд
tokens = re.findall(r'\b[0-9a-fA-F]{4,}\b', text)

numbers = []
for t in tokens:
    n = int(t, 16)
    if n % 2 == 1 and n <= 409510:
        numbers.append(n)

if numbers:
    numbers.sort()
    print('Подходящие числа:', numbers)
    print('Количество чисел:', len(numbers))
    print('Минимальное число прописью:', num_to_words(numbers[0]))
else:
    print('Подходящих чисел не найдено.')
