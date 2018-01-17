---
ID: 307
post_title: Python. Dynamic Module Import
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  http://sunsingerus.com/python-dynamic-module-import/
published: true
post_date: 2018-01-17 19:51:53
---
<h5>Task</h5> Object instance from dynamically specified class

<h5>Input:</h5>
<ul>
<li>path to Python file</li>
<li>class name</li>
</ul>
<h5>Output</h5>
<ul>
<li>object of the specified class</li>
</ul>

<h5>Solution</h5>

Fetch class
<pre>
def class_from_file(file_name, class_name):
    spec = importlib.util.spec_from_file_location("file_module", file_name)
    module = importlib.util.module_from_spec(spec)
    spec.loader.exec_module(module)
    _class = getattr(module, class_name)
    return _class
</pre>

Create object
<pre>
_class = class_from_file(file_name, class_name)
instance = _class()
</pre>

You may encounter the following error on the way:
<pre>
SystemError: Parent module '' not loaded, cannot perform relative import
</pre>
Most likely your dynamic module tries to import other module (possibly from the project), but relative or absolute path fails. The most straightforward way is to include target folders into <strong>sys.path</strong>
<pre>
# append 'converter' folder into sys.path
# this helps to load custom modules
converter_folder = os.path.dirname(os.path.realpath(__file__)) + '/converter'
if converter_folder not in sys.path:
    sys.path.insert(0, converter_folder)
</pre>