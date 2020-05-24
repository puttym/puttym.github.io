---
layout: post
title: awk command examples
date: 2019-07-20
category: programming
---
Create the file `addresses` with the following content.
```
Ramesh Shetty, 34, 4th Cross, Kuvempu Nagar, Mysore KA
Sureshi Bendre, 56, 3rd Main, T Nagar, Chennai TN
John Simon, 24, 5th Main, Jaya Nagar, Bangalore KA
G H Shinde, 56, 6th Main, Bandra, Mumbai MH
S Manjrekar, 39, 8th Main, Chanakya Puri ND
P K Reddy, 67, 9th Main, Charminar, Hyderabad AP
```

#### Syntax for `awk` command
`awk 'instructions' files `

* Instructions must be enclosed in single quotes
* Instructions always contain curly brackets and dollar signs
* Each line of the file is considered a record
* Each word is considered a field
* $1, $2, $3 .... represent first, second, and third words in a line
* $0 represents the full line


#### To print the first word in each line

```shell
awk '{ print $1}' addresses
```
Here, space(s) is considered the separator. For `awk`, spaces and/or tabs are
the default separators. However, this can be changes as shown below.

#### Print the first word only if it meets a condition
```shell
awk '/KA/ { print $1 }' addresses
```
This prints the first word of the lines which contain the phrase KA.

#### To print the name in each address
To do this, we need to print till the first comma. That means, we should
instruct `awk` to consider comma as the separator. Remember that the default
separator is space and/or tab.

```shell
awk -F, '{ print $1 }' addresses
```

```shell
awk -F, '/MA/ { print $1 }' addresses
```

Here `-F,` changes the separator from space to comma.

#### Rearranging the data using `awk`
```shell
awk -F, '{ print $1; print $2; print $3; print $4; print $5 }' addresses
```
