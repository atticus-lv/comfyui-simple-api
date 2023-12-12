This is a simple python api to connect with comfyui server
It need some external libraries to work:

+ `websocket-client` to connect with the server
+ `requests` to easy http requests
+ `pillow` to receive images
+ `blinker` to use the `signal` module for easy callbacks 

## How to use

use the `ComfyUiThread` in `server.py` to connect with the server

```python
from api.server import ComfyUiThread,Task,TestTask
comfyui_dir = 'your/path/to/comfyui/dir'
t = ComfyUiThread(comfyui_dir=comfyui_dir)
t.start()

# use callback signal, see in `message.py`
manager = t.server.manager
manager.signal_executing_node.connect(print) # send node id

# queue prompt
id = t.server.client_id
address = t.server.server_address
TestTask.test_prompt_text2img(id, address)

# to stop the connect and local server(if has)
t.stop()
```

## Known Issue

haven't been test yet, It is part of my addon