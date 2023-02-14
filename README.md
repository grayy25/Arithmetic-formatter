# Arithmetic-formatter
def arithmetic_arranger(problems, *args):
  #["32 + 698", "3801 - 2", "45 + 43", "123 + 49"]
  arranged_problems = []

  if (len(problems) > 5):
    return "Error: Too many problems."

  for i in problems:
    op = i.split()

    if (op[1] not in "+-"):
      return "Error: Operator must be '+' or '-'."

    if (op[0].isdigit() == False or op[2].isdigit() == False):
      return "Error: Numbers must only contain digits."

    if (len(op[0]) > 4 or len(op[2]) > 4):
      return "Error: Numbers cannot be more than four digits."

    longestVal = max(len(op[0]), len(op[2]))
    width = longestVal + 2

    line1 = f"{op[0]:>{width}}"
    line2 = op[1] + f"{op[2]:>{width-1}}"
    l = '-' * width

    try:
      arranged_problems[0] += (' ' * 4) + line1
    except IndexError:
      arranged_problems.append(line1)

    try:
      arranged_problems[1] += (' ' * 4) + line2
    except IndexError:
      arranged_problems.append(line2)

    try:
      arranged_problems[2] += (' ' * 4) + l
    except IndexError:
      arranged_problems.append(l)
      
    res = " "
    
    if (args):
      ans = " "
      if (op[1] == '-'):
        ans = str(int(op[0]) - int(op[2]))
      else:
        ans = str(int(op[0]) + int(op[2]))

      a = f"{ans:>{width}}"
      try:
        arranged_problems[3] += (' ' * 4) + a
      except IndexError:
        arranged_problems.append(a)
        
      res = f"{arranged_problems[0]}\n{arranged_problems[1]}\n{arranged_problems[2]}\n{arranged_problems[3]}"
      continue;
    
    res = f"{arranged_problems[0]}\n{arranged_problems[1]}\n{arranged_problems[2]}"
  
  return res


print(arithmetic_arranger(['3801 - 2', '123 + 49']))
print('  3801      123\n'
        '-    2    +  49\n'
        '------    -----')

# print(arithmetic_arranger(['32 - 698', '1 - 3801', '45 + 43', '123 + 49', '988 + 40'], True))
# print('   32         1      45      123      988\n'
#          '- 698    - 3801    + 43    +  49    +  40\n'
#         '-----    ------    ----    -----    -----\n'
#         ' -666     -3800      88      172     1028')
