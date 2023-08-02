# my_arcan
Testa a versão 2.9.6 do Arcan2

## Para baixar a versao 2.9.6 

```shell
wget -O arcan2.zip "https://drive.google.com/uc?id=1KoQaPgfx0VbBFVcYLvTcyVZjeDHraggy&confirm=t&uuid=1a2b43c7-a451-44f6-a90f-11ba3f73643e"
```

## Step-by-step analysis examples

Let’s start by cloning ANTLR 4, our example project:

```shell
$ cd /tmp # Optional command
$ git clone https://github.com/antlr/antlr4.git
```

To simplify your command line, we recommend that you define the following alias:

```shell
$ alias arcan="path/to/arcan.sh" # On Linux
```

Obs: lembre-se da permissão de execução

```shell
$ chmod +x path/to/arcan.sh
```

## Simple analysis

```shell
$ arcan analyse -i antlr4 -p antlr -o /tmp --all -l JAVA
```

this will analyse antlr and save the output CSV files to /tmp/arcanOutput/antlr

### Let's break down each argument:

-i tells Arcan what is the input directory of the project.

-p tells Arcan what is the name of the project. This name is going to be used to create the output directory where output files are going to be saved. Output files will also have a column with the name of the project.

-o this is the directory where to create the arcanOutput directory.

--all tells Arcan to detect all smells currently supported. Note that if you do not provide this, no smells will be detected.

-l JAVA tells Arcan that it has to look for Java files.

### The output directory will contain the following files

```shell
$ ls arcanOutput/antlr
component-metrics.csv  smell-affects.csv  smell-characteristics.csv
```

which are:

component-metrics.csv: the list of components (again, classes and packages) and the metrics calculated for each one of them.

smell-characteristics.csv: the list of smells and the characteristics (i.e. metrics for smells) calculated for each instance detected.

smell-affects.csv: the list of what components are affected by which smells using the IDs from the component-metrics.csv and 
smell-characteristics.csv files, respectively.

If you are only interested in the smells detected, you should be good to go by looking only at the smell- characteristics.csv file.

### In case you also desire Arcan to print the dependency graph as a GraphML file

```shell
$ arcan analyse -i antlr4 -p antlr -o /tmp --all -l JAVA output.writeDependencyGraph=true
```

Mais detalhes em arcan-cli-manual.pdf