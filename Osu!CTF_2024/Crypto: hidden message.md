My friend really likes sending me hidden messages, something about a public key with 
n = 5912718291679762008847883587848216166109 and e = 876603837240112836821145245971528442417. 
What is the name of player with the user ID of the private key exponent? (Wrap with osu{})

First we need to calculate factors p and q form N.
Then we can caluclate D

This is the calculated vlaue from the below code 

osu{124493}

Profile name = chocomint

flag = osu{chocomint}
```python3
from sympy import mod_inverse
from sympy import factorint

# Given values
n = 5912718291679762008847883587848216166109
e = 876603837240112836821145245971528442417
d = None  # Replace None with the actual private key exponent if you have it

# factors = factorint(n)
# print("Factors of", n, "are", factors)

# Calculate d if it's not given
if d is None:
    print("Private key exponent 'd' is not provided. Calculating 'd' using Euler's totient function.")
    # Factors of n
    p = 59644326261100157131
    q = 99132954671935298039
    phi_n = (p - 1) * (q - 1)
    d = mod_inverse(e, phi_n)

# Assuming you have the user ID related to the private key exponent
user_id = d  # Replace this with the actual user ID if it's provided

print("User ID associated with the private key exponent (wrapped with osu{{}}): osu{{{}}}".format(user_id))
```
