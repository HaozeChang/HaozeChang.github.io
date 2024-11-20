# This is a file illustrating how to use pdflatex

## Step 1: Install texlive

## Step 2: Write Tex file 

## Step 3: command pdflatex yourfile.tex

## Step 4: Bibtex yourfile **No .tex**

## Step 5: run pdflatex yourfile.tex twice to generate final version

A easy code file;

```python
import argparse
import os

parser = argparse.ArgumentParser(description='Compile tex file.')
parser.add_argument('--name', type=str, help='Name for tex file')  # 添加参数
args = parser.parse_args()

texfilename = args.name + '.tex'
bibfilename = args.name

# 使用字符串格式化插入变量
os.system(f'pdflatex {texfilename}')
os.system(f'bibtex {bibfilename}')
os.system(f'pdflatex {texfilename}')
os.system(f'pdflatex {texfilename}')
```