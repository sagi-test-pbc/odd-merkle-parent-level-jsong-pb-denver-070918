
# Odd Merkle Parent Level


```python
# Odd Merkle Parent Level Example

from helper import double_sha256, merkle_parent
hex_hashes = [
    'c117ea8ec828342f4dfb0ad6bd140e03a50720ece40169ee38bdc15d9eb64cf5',
    'c131474164b412e3406696da1ee20ab0fc9bf41c8f05fa8ceea7a08d672d7cc5',
    'f391da6ecfeed1814efae39e7fcb3838ae0b02c02ae7d0a5848a66947c0727b0',
    '3d238a92a94532b946c90e19c49351c763696cff3db400485b813aecb8a13181',
    '10092f2633be5f3ce349bf9ddbde36caa3dd10dfa0ec8106bce23acbff637dae',
]
hashes = [bytes.fromhex(x) for x in hex_hashes]
if len(hashes) % 2 == 1:
    hashes.append(hashes[-1])
parent_level = []
for i in range(0, len(hex_hashes), 2):
    parent = merkle_parent(hashes[i], hashes[i+1])
    print(parent.hex())
    parent_level.append(parent)
```

### Try it

#### Calculate the next Merkle Parent Level given these hashes
```
8b30c5ba100f6f2e5ad1e2a742e5020491240f8eb514fe97c713c31718ad7ecd
7f4e6f9e224e20fda0ae4c44114237f97cd35aca38d83081c9bfd41feb907800
ade48f2bbb57318cc79f3a8678febaa827599c509dce5940602e54c7733332e7
68b3e2ab8182dfd646f13fdf01c335cf32476482d963f5cd94e934e6b3401069
43e7274e77fbe8e5a42a8fb58f7decdb04d521f319f332d88e6b06f8e6c09e27
```


```python
from helper import merkle_parent

hex_hashes = [
    '8b30c5ba100f6f2e5ad1e2a742e5020491240f8eb514fe97c713c31718ad7ecd',
    '7f4e6f9e224e20fda0ae4c44114237f97cd35aca38d83081c9bfd41feb907800',
    'ade48f2bbb57318cc79f3a8678febaa827599c509dce5940602e54c7733332e7',
    '68b3e2ab8182dfd646f13fdf01c335cf32476482d963f5cd94e934e6b3401069',
    '43e7274e77fbe8e5a42a8fb58f7decdb04d521f319f332d88e6b06f8e6c09e27',
]

# bytes.fromhex to get all the hashes in binary
# if the number of hashes is odd, duplicate the last one
# initialize parent level
# skip by two: use range(0, len(hashes), 2)
    # calculate merkle_parent of i and i+1 hashes
    # print the hash's hex
    # add parent to parent level
```

### Test Driven Example

Add the odd number of element case to the `merkle_parent_level` methods.


```python
def merkle_parent_level(hashes):
    '''Takes a list of binary hashes and returns a list that's half
    the length'''
    # if the list has exactly 1 element raise an error
    if len(hashes) == 1:
        raise RuntimeError('Cannot take a parent level with only 1 item')
    # FOR ODD CASE: if the list has an odd number of elements, duplicate the last one
    #               and put it at the end so it has an even number of elements
    if len(hashes) % 2 == 1:
        hashes.append(hashes[-1])
    # initialize next level
    parent_level = []
    # loop over every pair (use: for i in range(0, len(hashes), 2))
    for i in range(0, len(hashes), 2):
        # get the merkle parent of i and i+1 hashes
        parent = merkle_parent(hashes[i], hashes[i+1])
        # append parent to parent level
        parent_level.append(parent)
    # return parent level
    return parent_level
```
