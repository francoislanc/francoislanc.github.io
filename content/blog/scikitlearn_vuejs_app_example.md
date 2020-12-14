+++
title = "Scikit-learn in a Vue.js app :snake:"
description = ""
tags = [
    "pyodide",
    "webassembly",
    "python",
    "javascript",
    "vuejs",
    "web"
]
date = "2020-08-19"
+++

A Vue.js example app which runs "[train_test_split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)" from scikit-learn with only the browser and no python server. It uses [Pyodide](https://github.com/iodide-project/pyodide), which is an experimental project to create a full Python data science stack that runs entirely in the browser. For more information on Pyodide, checkout this [mozilla blog post](https://hacks.mozilla.org/2019/04/pyodide-bringing-the-scientific-python-stack-to-the-browser/).

[![App Screenshot](/scikitlearn_vuejs_app_example/pyodide-vuejs-app-example.gif)](/scikitlearn_vuejs_app_example/pyodide-vuejs-app-example.gif)

Developed with [pyodide](https://github.com/iodide-project/pyodide), [scikit-learn](http://scikit-learn.org/), and [Vue.js](https://vuejs.org/).  
The source code is available on [Github](https://github.com/francoislanc/pyodide-vuejs-app-example).
