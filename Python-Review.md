Welcome to the COMPPHYS wiki!
We made this function.

```python
def lucky_7(test_number):
  """check if the input number is equal to 7 (and between 1 and 10)"""
  
  if test_number>10:
    print("the value is too high, choose a number between 1 and 10")
    return 99
  elif test_number<1:
    print("the value is too low, choose a number between 1 and 10")
    return -99
  elif test_number==7:
    print("lucky guess, you are correct")
    return 1
  else:
    print("not correct - better luck next time!")
    return 0