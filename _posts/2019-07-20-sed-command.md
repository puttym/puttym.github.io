---
layout: post
title: sed command examples
date: 2019-07-20
category: programming
---
Create the file `addresses` with the following content.

```
Ramesh Shetty, 34, 4th Cross, Kuvempu Nagar, Mysore KA
Suresh Bendre, 56, 3rd Main, T Nagar, Chennai TN
John Simon, 24, 5th Main, Jaya Nagar, Bangalore KA
G H Shinde, 56, 6th Main, Bandra, Mumbai MH
S Manjrekar, 39, 8th Main, Chanakya Puri ND
P K Reddy, 67, 9th Main, Charminar, Hyderabad AP
```

### Replace KA with Karnataka
`sed 's/ KA/, Karnataka/' addresses`

### Replace KA and TN with Karnataka and Tamil Nadu respectively
`sed -e 's/ KA/Karnata/' -e 's/ TN/Tamil Nadu/' addresses`

### A script to replace abbreviations with state names
Syntax: `sed -f scriptfile input_file`

Write the following commands in the file `states` 
```shell
s/ KA/, Karnataka/
s/ TN/, Tamil Nadu/
s/ MH/, Maharashtra/
s/ ND/, New Delhi/
s/ AP/, Andhra Pradesh/
```

Then run the following command
```shell
sed -f states addresses
```

### To suppress the automatic output
Syntax: `sed -n [instructions] [input_file]`
```shell
sed -n -f states addresses
```

### Saving the changes
None of the above commands do not save the changes to the file. The changes are just printed and not saved. Changes can be saved in two ways:

Write the output to a new file:
```shell
sed -f states addresses > newaddresses
```
Here `>` is the redirection operator.

Save the changes to the same file:
```shell
sed -i -f states addresses
```
