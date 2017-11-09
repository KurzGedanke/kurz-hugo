---
title: "Problems with Flask and PyCharm"
date: 2017-09-06T13:35:44+02:00
draft: false
tags: ["python", "Flask", "pyCharm", "tutorial"]
---

I started a new Flask project and coded it in VisualCode and a Terminal. Therefore, I set up my virtual environment, installed Flask and started to code after the [Flask Quistart](http://flask.pocoo.org/docs/0.12/quickstart/). 

<!--more-->

The code looks like this:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```
 
Then I ran the app with:

```bash
$ export FLASK_APP=hello.py
$ flask run
 * Running on http://127.0.0.1:5000/
```

Because of the great support for Web Apps I decided to switch to PyCharm. I imported the project into PyCharm, set the Interpreter to the virtualenv, but when it hit run nothing happend....

If you have the same problem: Feel welcome, I've got the solution!

Create a New Project, choose the Flask Template and select your existing flask project folder. Say `yes`to the pop-up which asks you to create a project from existing source. 
 
![PyCharm Project Creation](/img/flaskPyCharm/newProject.png)
 
Your project should open now and you can change your intepreter in the settings to your virtualenv or whatever you desire. 

If you try to run the app now you should see something like this:

![PyCharm Console with nothing in it](/img/flaskPyCharm/nothing.png)

I tried everything but the solution is damn simple... add this at the end of your code:

```python
if __name__ == '__main__':
    app.run()
```

and your console should output `* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)`.

If you want to know more about the `if __name__ == '__main__':` line I can recommend [this Video from Corey Schafer](https://www.youtube.com/watch?v=sugvnHA7ElY&feature=youtu.be).

Thank you for reading! 