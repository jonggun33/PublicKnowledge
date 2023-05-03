# Python
jonggun Gim <jonggun.gim@gmail.com>
:description: This document is for amassing my know-how's about the python language to be transferred to others.
:author: Jonggun Gim
:sectnums:
:toc: left
:doctype: manpage
:source-highlighter: highlight.js

## About this document
{description}


## Grammar
[Python Cheatsheet](https://perso.limsi.fr/pointal/_media/python:cours:mementopython3-english.pdf)

### Basics
[Learn Python Tutorial - javatpoint](https://www.javatpoint.com/python-tutorial)
``` shell
pip install pytest --proxy http://12.26.226.2:8080 --trusted-host pypi.org --trusted-host files.pythonhosted.org
pip install pycurl --proxy http://12.127.21.100:8080 --trusted-host pypi.org --trusted-host files.pythonhosted.org
virtualenv --system-site-packages --no-download venv
```

### Closure
``` python
def makeMultiply(mag):
	def multiply(a):
		return mag*a
	return multiply
twoTimes = makeMultiply(2)
twoTimes(4) //8
```

### Decorator
``` python
def capitalize(f):
	def upper()://no argument
		print(datetime.datetime.now())
		f()
	return uppper
@capitalize
def hi():
	return 'hi'
```

## GUI
### tkinter
[tkinter 공부하기 좋은 블로그](https://comdoc.tistory.com/entry/tkinter-%EA%B3%B5%EB%B6%80%ED%95%98%EA%B8%B0-%EC%A2%8B%EC%9D%80-%EB%B8%94%EB%A1%9C%EA%B7%B8)
``` python
from tkinter import *
root = Tk()
root.title('Sample'); root.geometry('900x100+300+300');
combo = Combobox(root, width=100)
Button(root, text = 'Delete Item', command = delItem).grid(row=0, column = 2)
root.mainloop()
```

### Qt5
``` python
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *
import sys
import time
app = QApplication(sys.argv)
try:
    due = QTime.currentTime()
    message = 'alert'
    if len(sys.argv) < 2:
        raise ValueError
    hours, mins = sys.argv[1].split(':')
    due = QTime(int(hours), int(mins))
    if not due.isValid():
        raise ValueError
    if len(sys.argv) >2:
        message = ' '.join(sys.argv[2:])
except ValueError:
    message = 'wrong format'
while QTime.currentTime() <due:
    time.sleep(20)
label = QLabel('<font color=red size=72><b>' + message + '</b></font>')
label.setWindowFlags(Qt.SplashScreen)
label.show()
QTimer.singleShot(6000, app.quit)
app.exec_()
```

## Scraping
* [Web Scraping Tutorial with Python: Tips and Tricks](https://hackernoon.com/web-scraping-tutorial-with-python-tips-and-tricks-db070e70e071)
* [Requests: HTTP for Humans™ - Requests 2.23.0 documentation](https://requests.readthedocs.io/en/master/)

``` python
import requests
from bs4 import BeautifulSoup
res = requests.get(BASE_URL + '/pages/page3.html')
soup = BeautifulSoup(res.text, 'lxml')
table_tag = soup.find(id='giftList')
```

## Web Server
[개발환경 구축 - Flask로 만드는 블로그](https://opentutorials.org/module/3669/22002)
``` python
from flask import Flask, jsonify, request,render_template,redirect, url_for
app = Flask(__name__)
@app.route('/hello', methods=['GET', 'POST'])
def hello():
    data = request.get_json()
    return jsonify(
            message='Hello and Hi Flask',
            count = 10,
            a=str(request.args.get('a')),
            b = data
            )
@app.route('/')
def home():
    return render_template('home.html')
@app.route('/login', methods = ['POST', 'GET'])
def login():
    if request.method ## 'POST':
        user = request.form['nm']
        return redirect(url_for('user', usr=user))
    else:
        return render_template('login.html')
@app.route('/<usr>')
def user(usr):
    return f'<h1>{usr}</h1>'
if(__name__## '__main__'):
    app.run(debug=True)
```

## Functional Programming
[What is FP](https://towardsdatascience.com/why-developers-are-falling-in-love-with-functional-programming-13514df4048e)

### Should Eliminate
#### Variable Mutation (Side Effects)
``` python
global_list = []
def append_to_list(x):
    global_list.append(x)
global_list = []
def append_to_list(x):
    global_list.append(x)
```
    
#### Loop
``` python
from functools import reduce
integers = [1,2,3,4,5,6]
odd_ints = filter(lambda n: n % 2 ## 1, integers)
squared_odds = map(lambda n: n * n, odd_ints)
total = reduce(lambda acc, n: acc + n, squared_odds)
```


## For ML/AL/DL
* [Jupyter Notebook on Azure](https://notebooks.azure.com/anon-hkagba/projects/gims)
* [Simple statistics with SciPy](https://oneau.wordpress.com/2011/02/28/simple-statistics-with-scipy/)
* [Visualization with Seaborn](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html)
* [How to rewrite your SQL queries in Pandas, and more](https://medium.com/jbennetcodes/how-to-rewrite-your-sql-queries-in-pandas-and-more-149d341fc53e)

### Change Detection

* [Contextual Changepoint Detection with Python and R using RPy2](https://medium.com/bigdatarepublic/contextual-changepoint-detection-with-python-and-r-using-rpy2-fa7d86259ba9)
* [A Brief Introduction to Change Point Detection using Python - Tech Rando](https://techrando.com/2019/08/14/a-brief-introduction-to-change-point-detection-using-python/)


## Code Snippets
[Popular Python recipes](http://code.activestate.com/recipes/langs/python/)
